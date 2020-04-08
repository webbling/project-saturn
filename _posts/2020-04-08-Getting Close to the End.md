---
layout: post
author: Blake
title: Getting Close to the End
excerpt_separator: <!--more-->
---

The end of the semester is quickly approaching.

<!--more-->

### [**WEBBUILD LINK**](/4-8-WebBuild/index.html)

## Last Meeting's Feedback Reflection

I got a lot of feedback about the graph and music I implemented plus a few other things.

- Lots of wasted space on the graph
	- Ceate a way for the player to appreciate/fear slope differences
	- Show the entire graph
- Graph has no axis labels (whoops)
- The y-axis becomes unreadable very quickly once numbers become 5 digits
- Add a "Play Again" Button
- The Project needs an official Game Title
- Double Check Royalties on Music and future SFX
- Variable music? (My personal note)

This meeting is a a good example of how important the implementation/feedback loop is. I thought that the player would only be interested in the last five years of the graph. However, once the player got late into the game it was very uninteresting to look at. Part of this was also because I kept 0 as a permanent minimum for the y-axis and the maximum 20% more than the checking account amount. This caused the graph to get squeezed into the top left corner of the graph.

#### Plan for this Week

- Alter the graph so that the player can see the entire progress of the game
- Create Billing script so that the slope of the graph will have variances
- Add more events to the back half of the game
- Add SFX to events 

## Altering Graph

So I was able to get the UI to show the entire graph over the course of the game, but I ran into a critical problem that can be seen in this picture.

![graph_squish](/images/graph_squish.PNG)

In the later stages of the game, the graph doesn't condense the x-axis and the amount of gray dotted axis separators. I needed to implement some logic so that the graph didn't look like such a mess at this point in the game. I tried to partition my axis separators to only have 10 of them regardless of how many plot points I had on my graph. I would then have all plot points exist in the same range so that the last x-axis label was the age of the player. This worked initially, but I think due to some rounding the graph slowly inched past my last x-axis label. I left this problem alone right now because I had to deal with implementing a variable x-axis label system. To prevent the labels from getting squished together like in the picture above, I made the max amount of x-axis points 10. I tried implementing logic to make the furthest x-axis label the current age, the closest the starting age, and everything inbetween variable amounts. However, early in the game the "step" isn't large enough and I end up showing inaccurate x-axis labels. I had already spent too much time on this issue so my solution right now is to have only the beginning age and the current age on the x-axis for now. This **WILL** change by the end of the project to include more x-axis labels. The three other changes I made to the graph were making the plot points transparent (too many points made the graph look messy), fixing the Y-axis to have nice and clean labels representing money in the player's account, and making the labels/axis separators scale correctly (this was a SetParent() issue).

![graph_april8](/images/graph_april8.PNG)

## Billing Script

I want bills to be paid throughout the year in order to make the graph more interesting to look at. This made implementing this script a littel tricky because I have a secondsElapsed variable in my Timeline script that I use to track how many seconds have passed in the game. I have it set up to only pay 1 bill at a time and it checks which bill should be paid by modding the secondsElapsed by the BillPerYear variable in my BillsScript. This is an issue if secondsPerYear is not divisible by BillsPerYear. I have not yet figured out how to cleanly implement around this. I might have to revisit my Timeline script and change things there or scrap the Bills system I have right now for something new. I have something to show this week in our meeting, but I'm not currently happy with the BillScript. Here's an image of the graph when the BillsScript is in effect.

![graph_bills](/images/graph_bills.PNG)

## Unexpected Circumstances This Week

I had a large project due in another class which took up all of my available time this past week. I would have liked to have spent more time working on Project Saturn this week, but as it stands I have to prioritize an upper level elective CS project over this one.