---
layout: post
title:  CLI Data Gem Project Walkthrough Part 1
date:   2017-06-02 14:53:57 -0400
---


It took a while to think of what I wanted to My CLI Data Gem Project to be on.

So after some thought, I decide to create my Data Gem based on what I like, trying new beers! Why not make it something fun?!

Here is want I to create:

1.  run ./bin/beer-me
2.  "Top New Beers Month Year" come up
3.  List of Beers Populates

```
1. Beer Name 1
2. Beer Name 2
```

4.  Menu Asks "Enter beer number to display style or type 'list' to see the beers again or type 'exit':"
5.  When you type in number it returns the style of the beer

I had a hard time on getting started so I watched the Data Gem walkthrough to get me up and running and boy did it help alot!

After going through the video, I was up and running and had my CLI Working with Dummy info. So I thought "this should be a cinch to complete!".. I was so wrong! HAHA!!

I am thinking becuase of the site I chose to scrape I could have made thing much harder for myself, but I didnt want to take the easier route and pick a whole new site, plus I wanted to make it on the topic I wanted it on, I am being stubborn and would really like to get this gem to work.

The reason I figured this would be a cinch was based on the tutorials and lessons on scraping I have already gone through and using the css selectors was pretty straight forward.


Then I went in for the scraping..... 
I am getting this info from RateBeer.com
Getting the title was simple as it was the only “h1” tag on the whole page. I wanted to get the title to pull from the page because it updates every month. (Top New Beers May 2017  , Top New Beers June 2017 )
As I went through the elements, I noticed all the info was in a table. not only that, multiple individual elements were under the same css(“td a”)

When I attempted to iterate through these results two things came back:

Beer name
Beer style

I then wanted them to be numbered which made them come back:

1. Beer Name
2. Beer Style

We would not want it like that as the only thing we would want displaying in the first list will be the beer names such as :

1. Beer Name 1
2. Beer Name 2

I noticed that since they used the same “a” element I need to find another way to separate the beer name and the beer style from there. This took me LOTS of time to figure out. Being new to this kind of thing I was making my way through with what I knew,  I had moments of ‘Oh’s!’ and “Ah’s!” and “What the hell’s?”.. haha!!

I then came to use what I used in the student scraper.  Both of these ‘a’ elements had links to them. and each link contained mostly the same path except for a different number at the end representing the beer. But each link had “beer” or StyleGuide” in it.

So I figured I would try this :

```
beer_name = doc.css("tr td a")
			beer_name.each_with_index do |beer, i|
				if beer.attr('href').include?('beer')
				puts "#{i}. " + beer.text
			else
				puts ""
			end
```

As I was typing it I was thinking , “I got you now!”.. then I ran it.. and came back with some thing that looked like this:

0.Beer name

2.Beer name

I was like "NOOOOO!!!" But then saw I was a step closer. I tried more and more different ways to try to get the list to appear as :

1.Beer name
2.Beer name

This was happening because the other ‘a’ element was the beer style
Then I went back to basic, very basic thinking. This is a moment you realize, sometimes you are over thinking an issue when it is something the basics can handle. So I thought, What is the output of the iteration?? An array.

What if I iterated through and deleted the beer styles that were returning in the array.
I had to create a way for the index to come back as 0 when the styles were done being iterated through and then only count the Beer Name in the array. So I came up with this:

```
beer_name = doc.css("tr td a")
		index = 0
			beer_name.each_with_index do |beer, i|
				if beer.attr('href').include?('StyleGuide')
					beer.delete('StyleGuide')
					index
				elsif beer.attr('href').include?('beer')
					puts "#{index+=1}. #{beer.text}" 
				end
			end			
```

This reset the index back to 0 after deleting all the items where the href included ‘StyleGuide”, which was the link to the Style of the beer and the text included the style of beer
Then I outputed  the number and beer name by returning the ‘href’ that included ‘beer’, which was in the link to the beer itself and the text included the name of the beer.

This then returned my beers correctly!

1.Beer name
2.Beer name

This CLI Data GEM is hard, but I feel its the ability to scrape the website I am doing is what is really making this difficult.
I am not done yet as I now have to do the second level and have it so where when you choose a beer number it returns the style for the beer.

Unfortunately, the site has updated to a new month and there are no beers on the list. I will have to ask a question regarding that. 

Once I am complete, I will do a full walkthrough of the methods I employed to make the gem!

Wish me luck!!



