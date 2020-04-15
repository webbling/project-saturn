---
layout: post
author: Blake
title: Road to Retirement
excerpt_separator: <!--more-->
---

Preparing a demo for stakeholder interviews.

<!--more-->

### [**WEBBUILD LINK**](/4-15-WebBuild/index.html)

## Last Meeting's Feedback Review

Here's the feedback from last week's meeting:

- Don't collect any taxes on the part time job, it falls in the lowest tax bracket

- Separate income and retirement values (or combine them???)

- Compounding interest on retirement savings

	- Typically somewhere around %7
	
- 401k and the Stock Market

	- Value goes up and down constantly, but grows over time
	
- Look at an online retirement calculator to see some of these values above 

- End of game loop is broken

- Game Title

During our meeting I discussed how it's been difficult creating this simulation game. I've feels like every time I implement something and test the results it feels unrealistic. I think it's becasue I'm focusing on trying to make too many things feel realistic in a short amount of time versus a few. For this last deliverable, I'm going to attempt to make the retirement fund over time feel realistic.

Right now the graph, and the game in general, is only keeping track of the player's checking account. There are certain things that everyone MUST spend money on in order to survive, but in reality I have no way of knowing how someone would like to spend their money. So instead of coming up with artifical ways to keep the checking account small, I can pivot this value shown on the graph to be the retirement fund instead. 

If I offer the player a way to determine how much of their income they would like to contribute to their retirement account, then I can track their retirement fund account on the graph with a certain percentage interest and determine if they saved enough by age 65 to retire. There are many other aspects of handling a personal budget, but creating a product that teaches 1 helpful lesson (saving enough for retirement) is better than teaching 0 lessons (the current iteration of Project Saturn).

I'm also highly considering overhauling my Timeline script and turning the game into a turn-based game instead of a constantly running game. Every turn an event will happen. Most of the time they will be very minor, but occasionally they might be significant. The issue with this is I don't have anymore room in my scene for new UI. Something will have to be replaced. I think since I don't have any of my other systems working with the Event History window I will replace that and move the profile UI to that location. I will then have room at the bottom of my screen for an Event UI window. 

## Housekeeping Items

#### Music License

Professor Yargar asked me to double check the music license of the BGM in Project Saturn. This is what I found when going back to the website I found it on.

"This work has been identified as being free of known restrictions under copyright law, including all related and neighboring rights.
You can copy, modify, distribute and perform the work, even for commercial purposes, all without asking permission."

#### Game Title

Right now I'm thinking "Road to Retirement" would be the most fitting title for Project Saturn based on my goal discussed above of focusing on saving enough money for retirement

#### Contacting Stakeholders

I contacted Don Rawitsch, Barry Fishman, and Melissa Gordon by email. So far I've heard back from Mr. Rawitsch and Professor Fishman. My interview with Professor Fishman is Friday April 17th @ 11:30am. My interview with Mr. Rawitsch is on Monday April 20th @ 3:00pm. I have no heard back from Ms. Gordon yet. 

## Timeline Script Overhaul + Billing Readjustment

Currently I keep track of time by incrementing a counter every frame. In a 60 fps game, 60 frames is 1 second. So when this counter got to 60 it would add 1 seconds to secondsElapsed and get set to 0. Over time this design felt increasingly unsatisfactory, leading to my decision to overhaul it. The new system uses a turn based time system. Every turn is 1 year in the game and every year will be accompanied by a funny/witty/tragic event (haven't been written yet, they should be later on in this blog). I plan on having these events oftentimes be minor. In this new turn based system, starting at 15 currently makes the game take too long. It would take writing 50 events to get from 15 to 65, and ideally I would want more than 50 events for some "replayability". I went back to the lifestyle creation process I had before where many decisions are made at the beginning of the game. I will however have staged events in the game every 5-7 years or so that will allow the player to alter these choices as well as be offered different income opportunities. 

I reduced the amount of bills the player has to make it less confusing. Currently there is just the housing and transportation bills. I guess another form of billing will be the yearly events that could potentially impact the player's accounts. There are currently just 2 methods of housing and transportation. I would like to add more options, but with a final deliverable due date on the horizon this is not something that can be added at this time. The graph now tracks the retirement fund instead of the checking account. Currently the process is hard coded for 20% of the player's yearly income to be put in their retirement fund. I'm looking to implement a small amount of UI to make this amount adjustable from year to year. For example the player could recieve a promotion and want to add more money to their retirement every year.

![new-timeline-demo](/images/new-timeline-demo.gif)

I still need to handle the end of the game and potentially add a debt mechanic if I have time.

## Percentage of Paycheck to Retirement Allocation

I created some UI that allows the player to determine how much of their paycheck they want to put towards their retirement account. They are only limited from going below 0% and above 100%. The choice is theirs! However I think the default value with be 5%. Here's a demo.

![allocation-demo](/images/allocation-demo.gif)

## End Game Event

When the counter reaches "0 years until retirement" a Unity Event triggers an endGame event. The game combines your checking account and retirement account into a netWorth variable. This netWorth variable is divided by (currentYearlyIncome \* 0.8). This calculation is the number of years the player can retire and spend 80% of their currentIncome. The numbers are a little unbalanced right now as you can see in the demo below.

![endgame-demo](/images/endgame-demo.gif)

## Conclusion

I started to implement the yearly events, but I ran out of time this week and only wrote about 6 or 7. I also need to connect the events with the players accounts before I would fully call them implemented. The only other thing I would maybe implement before my interview with Professor Fishman on Friday is additional costs because right now the game is too easy to "win". I might create another Lifestyle Choice at the beginning of the game to allow the player to choose how much they spend on hobbies, food, etc. I might also add a debt mechanic if the checking account ever falls negative or if the player goes to college (because as it stands there's no penalty for going to college). The game is working in a (to my knowledge) bug free state right now so I'm hesitent to add anything majorly new at this point and running the risk of having a buggy final executable. I guess I will have this current webbuild to fall back on if I need to. 