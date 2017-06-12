---
layout: post
title:  "CLI Data Gem Project Walkthrough Part 2"
date:   2017-06-12 15:23:39 +0000
---



The list now has 1 beer on it so I can move forward with completing my CLI App!

As per the first part of this walkthrough, I was able to get the Beers to list in order and numbered.

Now I have the task of linking the number to the beer to bring back the info for the beer.

Currently when we run the App, the Title and list comes up along with the menu

￼![](https://ibb.co/jCzs3F)

Now when I type the number the links to the information come up:
￼![](https://ibb.co/e2Z3Av)

The plan is to get the ‘Style’ of the beer to come up when the number of the beer is entered.
So we want the text to display:

Style: Bitter

So I figure I need to find out how are the 2 elements returning, and how to extract the information from the:
￼![](https://ibb.co/coO8ca)

**UPDATE**

After a few days I tried again and found an issue.

There are now 3 beers in the list which is good!
![](https://ibb.co/dzNOAv)
￼

but when I enter the number 2 to bring back the info on the beer, I get nothing:
![](https://ibb.co/nmbTca)
￼

but yet, If I enter 1, I get all the results of the URL’s to the beers on the list:
![](https://ibb.co/h2eQOF)
￼

Do I need to find a different way to iterate through the beers? I will continue working and update soon!


