---
layout: post
title:      "Scraping EDGAR from SEC"
date:       2021-05-20 00:41:29 +0000
permalink:  scraping_edgar_from_sec
---


Python EDGAR download API: https://github.com/edgarminers/python-edgar

1) From Wikipedia, download a list of stock symbols and CIK. CIK is import because that's what EDGAR recognizes, not symbols.

2) Make folders to where to store the HTM files from EDGAR. Depends on how many you download, the total files may be large! For example, S&P 500 quarterly statements for 10 years, is around 34 GB.

3) Use the following code to figure out which file and folder is not yet filled:


```
SP500_Symbols = df_sp500.Symbol.to_list()
SP500_CIK = df_sp500.CIK.to_list()
SP500_Companies = df_sp500.Security.to_list()

symbol2company = dict(zip(SP500_Symbols,SP500_CIK))

to_do_list = []
selectedreport = '10-Q'
for selectedsymbol in SP500_Symbols:
    selectedcompany = symbol2company[selectedsymbol]
    for year in years:
        for quarter in quarters:
            if not os.path.isfile(f'./data/{selectedsymbol}/{selectedsymbol}_{year}_{quarter}-{selectedreport}.htm'):
                to_do_list.append([selectedsymbol,selectedcompany,selectedreport,year,quarter])

print(len(to_do_list))
print(to_do_list)
```

4) Use following code for the to try to download HTM files from EDGAR. Some of them may fail, so it needs to be run couple times:


```
%%time
list_of_fails = []
for to_do in to_do_list[:]:
    selectedsymbol = to_do[0]
    selectedcompany = to_do[1]
    selectedreport = to_do[2]
    year = to_do[3]
    quarter = to_do[4]
    # print(to_do)

    try:
        url = "N/A"

        csv = csvs[(year,quarter)]

        csv.columns.values[0] = 'Item'

        # companyreport = csv[(csv['Item'].str.contains(f"/{selectedcompany}/")) & (csv['Item'].str.contains(selectedreport.lower()))]
        companyreport = csv[csv['Item'].map(lambda item: (f"/{selectedcompany}/" in item) and (selectedreport.lower() in item))]
        if len(companyreport) == 0:
            continue

        Filing = companyreport['Item'].str.split('|')
        # Filing = companyreport.split('|')

        Filing = Filing.to_list()

        for item in Filing[0]:
            
            if 'html' in item:
                report = item
                
        url = 'https://www.sec.gov/Archives/' + report
        url = url.strip()

        df = pd.read_html(url)

        time.sleep(.12)

        document_index = df[0]
        document_index = document_index.dropna()

        document_name = document_index[document_index['Description'].str.contains(selectedreport)]
        document_name = document_name['Document'].str.split(' ')
        document_name = document_name[0][0]

        report_formatted = report.replace('-','').replace('index.html','')
        url = 'https://www.sec.gov/Archives/' + report_formatted.strip() + '/' + document_name # That's the HTM with all the numbers and text

        urllib.request.urlretrieve(url, f'./data/{selectedsymbol}/{selectedsymbol}_{year}_{quarter}-{selectedreport}.htm')
        time.sleep(.12)
    except:
        # time.sleep(1)
        failure = [selectedsymbol,selectedcompany,selectedreport,year,quarter,url]
        list_of_fails.append(failure)
        print(failure)
# pickle.dump(list_of_fails,open('list_of_fails','wb'))
```

Tada! Now you have the raw HTM files for a specific report for a symbol of your choosing!
