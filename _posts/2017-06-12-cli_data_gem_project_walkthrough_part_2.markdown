---
layout: post
title:  "CLI Data Gem Project Walkthrough Part 2"
date:   2017-06-12 11:23:40 -0400
---



The list now has 1 beer on it so I can move forward with completing my CLI App!

As per the first part of this walkthrough, I was able to get the Beers to list in order and numbered.

Now I have the task of linking the number to the beer to bring back the info for the beer.

Currently when we run the App, the Title and list comes up along with the menu

![](https://image.ibb.co/eZCC3F/Screen_Shot_2017_06_06_at_8_52_13_PM.png)


Now when I type the number the links to the information come up:
￼![](https://image.ibb.co/c7qbVv/Screen_Shot_2017_06_06_at_8_53_11_PM.png)

The plan is to get the ‘Style’ of the beer to come up when the number of the beer is entered.
So we want the text to display:

Style: Bitter

So I figure I need to find out how are the 2 elements returning, and how to extract the information from the:
￼![](https://image.ibb.co/iNuEHa/Screen_Shot_2017_06_06_at_8_55_59_PM.png)

**UPDATE**

After a few days I tried again and found an issue.

There are now 3 beers in the list which is good!
![](https://preview.ibb.co/kgbTca/Screen_Shot_2017_06_11_at_2_01_37_AM.png)
￼

but when I enter the number 2 to bring back the info on the beer, I get nothing:
![](https://preview.ibb.co/jfQMxa/Screen_Shot_2017_06_11_at_2_03_03_AM.png)
￼

but yet, If I enter 1, I get all the results of the URL’s to the beers on the list:
![](https://preview.ibb.co/gWnZHa/Screen_Shot_2017_06_11_at_2_04_35_AM.png)
￼

Do I need to find a different way to iterate through the beers? I will continue working and update soon!


