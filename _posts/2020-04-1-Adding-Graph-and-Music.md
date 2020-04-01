---
layout: post
author: Blake
title: Adding a Graph and some Music
excerpt_separator: <!--more-->
---

This week I implemented a graph that tracks the player's progress, implemented background music, and tweeked some existing UI.

<!--more-->

### [**WEBBUILD LINK**](/4-1-WebBuild/index.html)

## Last Meeting's Feedback Reflection (15 Min)

I knew Project Saturn was missing a lot of "juice" in my last playable demo. I also knew that the back half of the game beyond the theoretical age of 30 felt very bland. Professor Yarger agreed with these points. Here's the feedback I got:

- Empty space in top right of scene
- Scoring metrics other than just money/more than 1 objective
- Give the player more feedback
- Make the player feel consequences
- Background Music and Sound Effects
- In-game age not currently shown

Professor Yarger gave me the idea to fill the empty space in my game with a graph of the user's checking account and retirement fund. I think this would be a great idea as it would give the player something to look at while no events are happening and provide more feedback to the player as to how they're doing (could be racing against another "your savings at this time should be X" graph line). Professor Yarger also suggested that I come up with some fun blurbs to give the player more feedback on their decisions or events they encounter. 

#### Plan for this week

I'm really interested in filling the empty space with a live graph of the scoring metrics so I'm going to look into that first. After that I need to finish my Billing script that will automatically deduct money from the player's bank account for reoccuring payments. After that I'm going to look into getting some simple background music and SFX for the game. If I have time I'm going to come up with more events in the back half of the game. Also I'll create a quick script to show the player's age in game.

## Bank Account Graph (4 Hours 30 Min)

Code Monkey, a Unity tutorial channel, has a playlist on how to create a graph in Unity [here](https://youtu.be/ck72XNhxeS0). I watched the first video and then watched the summary video. It is a very detailed series that ends up creating a nice looking graph class for Unity, but I'm not sure it was exactly what I was looking for. Here's the graph from the video:

![code_monkey_graph](/images/code_monkey_graph.PNG)

My initial thoughts for a graph in Project Saturn looked more like this:

![stock_graph](/images/stock_graph.png)

You can't tell from the still images here, but in the 2nd "stock market" graph the entire graph would keep moving to the left as the player played the game and the arrow would stay somewhere around the middle of the graph. The highlighted green line in this photo from google images would be the retirement goal or something along those lines. 

Continuing my research on how to implement this, I found a [thread](https://answers.unity.com/questions/594921/moving-graph-using-vectrosity.html) on Unity's website of someone who was also trying to create a moving graph. The answerer used a queue system to maintain what plot points. This was closer to what I wanted to achieve, but a graph that moved in real time throughout the game would be more pleasing to look at in my opinion. 

I decided that having a graph that incrementally updates is better than having no graph at all. Also I have a limited amount of time remaining in the semester. So I began working on implementing a queue-based plot point system and modifying the class that the Code Monkey channel created. I tried importing the package he provided in his last video, but there were a lot of errors in the script. So I removed the package because it seems like he had a custom utilties package that had a bug in it that I didn't feel like finding and fixing. 

So I had to create new script files for the bit of his code that I wanted to use (also in his video description he says it's fine to use his graph code in viewer games). Instead of just copying and pasting lines in his scripts, I retyped the code so I could process and understand what each line was doing in case I needed to make tweaks later. So I followed the tutorial videos and implemented things about Code Monkey's graph class that I wanted in my graph and skipped over things I didn't want to implement. It was a wonderful tutorial, but the creator types REALLY fast and sort of fast forwards through things after he quickly explains what he's doing. I had to stop and pause often to actually see the code that he was writing. After I finished implementing the parts that I wanted, my graph looked like this: 

![graph_after_tutorial](/images/graph_after_tutorial.PNG)

Now it was time to implement the components to make my graph look more like my original vision of a moving stock graph. I only wanted the graph to run to about 2/3 of the graph width. When it reaches this amount of points, I wanted the oldest value to be removed from the graph when graphing a new "furthest" x-value. I was able to get a moving graph. It has a few bugs such as the axis separators leaking off the graph and the X-axis ages being 6 years ahead of where they should be, but I had already spent way more time working on the graph this week than I thought I was going to. I wanted to try to get a few more things done this week. I think the graph will be more exciting when the Billing Script is implemented. Here's a gif of the graph demo:

![graph-demo](/images/graph-demo.gif)

## Background Music (30 Min)

I am not a composer by any means of the word, so I went to [gamesounds.xyz](https://gamesounds.xyz/) to look for some royalty free music. Project Saturn is not an intense game and doesn't require a lot of action, so I looked to music to reflect that. Specifically I was looking for something that resembled elevator music. The selection was pretty limited, but I think I found something that fits the atmosphere quite well.

## Add Age Counter (15 Min)

The game now tracks the player's age in the profile UI.

## Conclusion

The graph took way longer to implement than I originally planned. When making my plans for this week, I expected to only spend half the amount of time I spent on it. This meant that my Billing Script didn't get implemented (which would have made the graph more interesting to look it...) and my back half of the game is still pretty empty with events. I was able to implement background music, but I didn't have time to implement any SFX.

