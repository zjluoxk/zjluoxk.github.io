---
layout: post
title:      "Folium: The Coolest Visualization Library Ever!"
date:       2021-01-07 02:45:20 +0000
permalink:  folium_the_coolest_visualization_library_ever
---

I consider myself a visual person. I like it so much that I took graduate CFD classes just to learn how to code fluid simulations and plot them:

![CFD](https://i.pinimg.com/originals/44/9d/d0/449dd01faf59a275b571ba15763b3ba6.gif)

To be honest, it may have been an subconscious influence that made me majored in Aerospace Engineering haha.

Anyways, during the task of modeling the King County house sales, I was trying to visualize the results of my multivariate linear regression. I had gotten great R^2, and I also had multiple models since I decided to model by zipcode. But the question is how can I put all of this on a single intuitive plot?

After a good hour of research I stumpled across Folium! This library is very easy to use, and one can pretty much do all your typical Google Map type of visualization with it. With this library I was able created the following plot: locating on a map every house sale data, visualize the price by color and overlap a R^2 choropleth on top as well.

![Static](https://raw.githubusercontent.com/zjluoxk/2015_King_County_Housing/main/images/Both.PNG)

One of the neat features I found is it can also put toggleable layers on the plot and as well as add popups. This is from the same plot after I toggle off the R^2 choropleth and click on one of the house data point to create a popup:

![Popup](https://raw.githubusercontent.com/zjluoxk/2015_King_County_Housing/main/images/Popup.PNG)

Doesn't that look fun? Check out Folium then!


