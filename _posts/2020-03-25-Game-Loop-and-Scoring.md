---
layout: post
author: Blake
title: Game Loop and Scoring
excerpt_separator: <!--more-->
---
Worked on closing the game loop, a game timeline, separating decisions, and began scoring.

<!--more-->

### [**LINK TO WEBBUILD**](/3-25-WebBuild/index.html)

*Note*: For the purposes of showing off this week's components I increased the pace of the game in this build.

I'm slowly getting used to working on everything from my apartment. Despite it being a little difficult to maintain focus in my apartment, I was able to make some good progress this week.

## Previous Week Feedback

Here's some feedback I got at our meeting last week:

- Not all decisions should be made at the beginning of the game
- Introduce events that change income
- Create events centered around having or not having a spouse
- Close the feedback loop!!!
- Implement a scoring system

These are all things I knew I had in front of me before my meeting and going into this week. I should have prioritized closing the game loop before implementing the Event History UI/Scripts, but I think there's some value in seeing what the scripts are doing (which will happen through the Event History).

## Design Brainstorming (30 Min)

Overall Project Note: I think I need to reduce my scope. Whenever I sit down and think about Project Saturn's design, my mind constantly jumps to all these different things I want to implement to create a realistic simulation. However, I can't realistically see me finishing all of them without the game being unbalanced or a buggy mess. 

I agree that too many decisions are made at the beginning of the game. I think it would be a good idea to spread them out. I think I'm still going to have the game start with the player as a teenager. Maybe they'll have a modest teenage job income instead of rolling for their income immediately. I'm going to write a script that handles the timeline of the game and forces more life impacting events to happen at set times.

I'm also going to need a script that handles the reoccuring costs such as utilities, car insurance, loan payments, etc. I don't want this events to flood the event history so I'm going to set up the script in a way that will let me toy with how often they show up in the Event History.

Lastly I'm going to need a script for scoring. I think the two values I'm going to make sure are always displayed in the bottom right corner of the scene are current income and retirement savings. I think the overall goal of this simulation is going to have enough money saved to retire at 65. According to [America's Debt Help Organization](https://www.debt.org/retirement/how-much-do-i-need-to-save/), the general rule of thumb is you should save enough to have 80% of your yearly salary when you worked. Meaning if you made 50k a year while you worked, you need to save enough to have 40k per year during retirement. I think this is a very simple way to determine if the player won or lost the game. The average life expectancy in the US is 78.6 years so the player should have enough to live 15 years past retirement (might be increased later on in development).

## Timeline Script, Implementation, and UI Rearrangement (2 Hours 15 Min)

This will be one of the more important scripts to determine when the game ends so I'm starting with this one.

I've set up the Update() function very similar to how I set up the RandomEvents() script. The script requires a numMinutes int variable. This will be the total minutes of gameplay (not counting pauses when the player handles decisions/events) that it will take to reach the age of retirement. There is a tracker to tell how many second have elapsed and it's accompanied by a list of variables related to major decisions/events. These events are: deciding to attend college, choosing a career (rolling your income), deciding transportation method, deciding to get married, deciding housing situation, and deciding to have children. More can be added if needed.

I wanted to set up this timeline so I only had to change numMinutes and not any of the other variables that handle major events. Regardless how many minutes of gameplay there are going to be, I want the major events to happen at the same percentage progress. E.g. it would be weird to choose if you wanted to go to college or not halfway through the timeline. After some thinking I determined the best way to do this would be to store the age I want this events to occur at and convert them to the seconds elapsed value they will occur at in Start(). When seconds elapsed is equal to the converted value the major event at that time will invoke a Unity Event to handle the UI.

After creating the Timeline script I had to reorganize all of my UI since every UI window was called by the previous with the Unity Button's OnClick() event. I handle most actions with the Unity Button OnClick() event so it took a little bit to make sure everything was changed correctly and required multiple play-throughs. I repurposed the first income roller to roll for a part time teenage job ranging from $3000 to $6000 per year after taxes (estimated with $7.25 federal minimum wage and 10-20 hours per week). I then took my full-time income roller and separated it based on if the player chose to go to college or not. [This](https://smartschoolsusa.org/blog/the-average-salary-by-education-level-2019-2020) source sais that the average salary for non-degree high school graduates is 37,000 and the average salary for bachelor degree college graduates is 60,0000. I think I'll just +- those values by 5,000 for now. The income also increases by 50% now if the player gets married.

Had to fix a bug where both income roller events (no college degree and college degree) would occur. Fixed this by creating a PlayerProfile variable in my Timeline script that has access to the player's college choice bool variable.

Lastly, I added a placeholder UI window at the end of the game. Something else will replace it next week.

## Fixing SetIncome() (30 Min)

Adding the part time teen job and variable income rollers for college broke my script. My issue was that my RollAmount script requires a public Text component that is set in the inspector. I tried creating a function that reset my roller with a new Text component and new minAmount and maxAmount values, but [I guess Unity doesn't like functions to have 2 or more arguments](https://forum.unity.com/threads/ui-doesnt-accept-functions-with-more-than-two-arguments-or-arrays.306671/). I was able to fix this problem by having multiple function reset my income roller instead of just one. This is unforuntate because it just increases the complexity of the component and makes it harder to keep things clean/organized.

## Player Profile UI Bug (30 Min)

My script that populates values in my profile UI window was designed around having all the player's lifestyle decisions made beforehand. So everything was called during the Start() function. This wasn't too hard to fix. I just had to reorganize the script into separate functions that are called during OnClick() events and take in a Text argument for the specific section being changed by the event. After changing the script I had to go and change some UI components to accomodate the new script organization. Then I tested the major events again to see that my fixes worked.

## Displaying Bank Account Script, Scoring UI, Income Script, and Bills Script (1 Hour 45 Min)

Updating the player's bank account was a very easy script to write and I had already thought about where I wanted to place this UI when I was making the Profile and Event History last week. It's just 2 functions that grab the value of the checking account or retirement fund variables from the PlayerProfile and update the Text components of the bank account UI.

Writing the income script required some more thought. I didn't want the checking account value to just go up every frame. That would be way too fast. At the same time, I didn't want the value going up once per in game year (varies depending on the value of numMinutes in the Timeline script). I have a value for secondsPerInGameYear, but I can't just update it 4 times per year because not all InGameYears will be divisible by 4. I set it up to be modifiable since I couldn't make a final decision at the time. I had an issue for a little bit where my IncomeScript wasn't able to grab the secondsPerIngameYear variable from my Timeline script. I realized that secondsPerInGameYear ws being set in the Start() function of Timeline and I was trying to use it in the Start() function of IncomeScript. I fixed this by adding a 1 second delay with a coroutine in IncomeScript's Start() fucntion. I was stuck on a bug where my Payday event in Timeline would only give me my first paycheck. After trying to research why my UnityEvent was only invoking once, I realized that I was setting the players checkingAccount = to income instead of +=...

My script for Bills/Reoccuring payments is set up similarly to my IncomeScript. As of right now I am undecided how often and in what increments they should be taken out of the checking account. I didn't make substantial progress on this script and it will be finished next week.

## Playtesting (15 Min)

I playtested the game for a bit after finishing the Income Script. For the purposes of our meeting, I didn't want it to take 5 minutes to play the whole game so I made the game length 1 minute instead. This felt VERY frontloaded and there was nothing to do in the back half of the game. I plan on getting some feedback on this in our meeting this week. Do I keep it frontloaded right now and create things to do in the back half of the game? Or do I ditch the realism of making decision at the "accurate" age in order to spread out the already implemented game evnts?

## Conclusion

The game now has a clear start and end. There is also a scoring system now so the player can see how they're doing and how they did when they hit the age of retirement. next week I plan to include an age display, make the retirement fund interactable, finsih the billing script, and write a script to handle the end of the game.





