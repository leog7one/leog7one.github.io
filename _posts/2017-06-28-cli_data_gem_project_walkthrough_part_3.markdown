---
layout: post
title:  "CLI Data Gem Project Walkthrough Part 3"
date:   2017-06-28 16:50:06 -0400
---



While I had the beers coming out in list as I wanted, I now needed to make info from the beers come up!

This was harder than I thought I. I actually had to go back and change the way I iterated through the beers first.

I want to send a thanks to Cernan for pointing me in the right direction.

As I left off from the last time when I type the number of the beer itself it would bring back all the info on all the beers iof I type '1' into the terminal. And if I type any other number, nothing would come up.

We looked at the way I was getting the info from Ratebeer.com

I first had it as such:

`beer_name = doc.css('tr td a')`

What this was doing was only grabbing the name and the style of beer as those were the 'a' elements.

I switched up and followed what Cernan had told me. Just use:

`beer_rows = doc.css('tr')`

This made more sense as the Ratebeer.com website separated all the beers into rows with the information in them. And the nokogiri doc came back as an array in which I can choose the item in the array! When he went over this I said to myself! OF COURSE IT'S SO SIMPLE! The basics are a power tool!!

With that I created this to get the list of beers:

```
beer_rows = doc.css("tr")
		index = 0
			beer_rows.each_with_index do |row, i|

				beer = BeerMe::Beer.new
				beer.name = row.css('td')[1].text
				#since the iteration will bring back the first row and the 2nd elemet is 'name'
				#but has the index of 0 we will skip it using 'next' and then put the rest as those are the beers.
				if i == 0 
					next
				end
				puts "#{i}. #{beer.name}"
			end
```

This then produced the list as I wanted:

<a href="https://ibb.co/k8KkNk"><img src="https://preview.ibb.co/f0fEF5/Screen_Shot_2017_06_28_at_3_22_25_PM.png" alt="Screen Shot 2017 06 28 at 3 22 25 PM" border="0" /></a>


I then figured with the rows now containg all the info I need I can now go in and get the rest of info for the 2nd part of my CLI APP
I wanted the app to produce the info of:
Beer Style: Style
Beer Score: Score
Beer Reviews: Reviews

I already had my CLI App loaded with dummy info from before as I tested that the app will run in the terminal, so I figued I will go from there.

I created 

```
def self.scrape_beer_info
		#scrapes the table and only gets the info from the rows
		doc = Nokogiri::HTML(open("https://www.ratebeer.com/Ratings/TopOfTheMonth.asp"))
		
		beer_rows = doc.css("tr")
	end
```

This was to get the info from the tables into the CLI by using:

```
def beer_info
		@@info = BeerMe::Beer.scrape_beer_info
	end
```

This seemed to work as I was getting the info to come up correctly.


<a href="https://ibb.co/n2Rzhk"><img src="https://preview.ibb.co/jT7i8Q/Screen_Shot_2017_06_28_at_3_32_59_PM.png" alt="Screen Shot 2017 06 28 at 3 32 59 PM" border="0" /></a>


Then I tested what would happen if I choose a number that wasnt listed, like 47.
I then got this error:

<a href="https://ibb.co/i9PVoQ"><img src="https://preview.ibb.co/h0yqoQ/Screen_Shot_2017_06_28_at_3_35_03_PM.png" alt="Screen Shot 2017 06 28 at 3 35 03 PM" border="0" /></a>


Now I knew the reason this was happening was becuase there was no 47 in the list and the beer_info didnt have a row that went that high, so of course is there is no method error for 'css' as it does not even exist!

I will be honest, I was doing WAY TOO MUCH overthinking as I tend to do and was looking at the situation as way more complex than it should have been. I all had to do, which is what I usually need to do is..go back to the basics.

What I first tried was this, since 45 was the highest number in the list:

```
if input.to_i > 0 && input.to_i <46
				#grabs the row based on input number and pulls the info for style, score and review number using nokogiri.
				info = beer_info[input.to_i]
				beer_style = info.css('td')[4].text
				beer_score = info.css('td')[2].text
				beer_reviews = info.css('td')[3].text

				puts "Beer Style: #{beer_style}"
				puts "Beer Score: #{beer_score}"
				puts "Beer Reviews: #{beer_reviews}"

			elsif input == "list"
				list_beers
				
				
			elsif 
				puts "Please choose a valid number."

			elsif input == "exit"

```

And it worked!

But then I thought, this list is constantly updating, It is not a functioning app if it doesnt keep up on its on from the site.
So I thought, how can the program always now how many rows are in the beer_ info array?? beer_info.length !!!

I change the code to 

`if input.to_i > 0 && input.to_i < beer_info.length`

and now it worked perfectly! It now says "Please choose a valid number", if an invalid one is chosen.

<a href="https://ibb.co/hdaEF5"><img src="https://preview.ibb.co/f50gv5/Screen_Shot_2017_06_28_at_3_43_11_PM.png" alt="Screen Shot 2017 06 28 at 3 43 11 PM" border="0" /></a>

My CLI App is now complete and working and now I am finishing up the little tidbits here and there and will be submitting for review!

Here is the link to the Github for the BeerMe CLI App! Check it out and let me know what you think!

[](https://github.com/leog7one/beerme-cli-app)



