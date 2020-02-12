---
layout: post
author: Blake
title: Design Progress
excerpt_separator: <!--more-->
---
Not much technical progress, but starting to visualize what this project is going to be.

<!--more-->

During my phone interview with Don Rawitsch he told me about an economic focused course he took in high school where every student was given an economic profile and you had to balance your finances and make it through a year. 

<!--more-->

This reminded me of a very similar activity I did in my 7th grade Enrichment class (a class taken in lieu of a musical arts class where the curriculum was decided by the teacher). In this activity, all students were given an income, family size, and a few other attributes. The students then had to construct a household budget based on their profile. A lot of people in my class, myself included, really pushed their budget to the max. We bought cars and houses outside of our means of income and didn't prepare for unexpected events to occur. We valued quality of life in the now versus quality of life in the future (when we ran out of money).

<!--more--> 

I think developing a game that emulates this activity would be a very valuable way to teach how manage personal finances. 

## Basic Design Concept

![Basic Design Concept 3](/images/Design-Concept-3.png)

The game begins with a setup scene. In this scene the player chooses most of their monthly costs such as transportation, living arrangements, and more. Decisions made during setup will greatly impact the difficulty of the game. 

![Basic Design Concept 1](/images/Design-Concept-1.png)

Right now I'm imagining the game is a single scene after setup. In this scene you have multiple components that either display the game state, the player's profile, and the player's resources.

<!--more-->

#### Scene Components

- **Player Avatar**: An avatar that will change emotion based on how the player is doing in the game

- **Resource Bars**: Happiness and bank balance of the player. Gives the player visual feedback as to how they are doing.

- **Event Log**: All the events that happen in the game that effect the player. Examples would be paying rent, buying groceries, spending money on a hobby, etc.

- **Profile**: Gives basic info about the player such as their occupation, their income, how many family members they're supporting, etc.

- **Calander**: Gives the player an idea how long they've made it and when they get paid next.

- **Event Pop Up**: This is a random event and gives the player limited choices on how to handle it. Based on how they handle it will effect their resource bars.

<!--more-->

![Basic Design Concept 2](/images/Design-Concept-2.png)

Here is an example of someone who is doing poorly in the game. Their bank resource bar is in an alright place, but their happiness level is low.

## Plans for next week

1. Create a functional script that handles Random Events
2. Create a lengthy, but not excessive list of random events to begin play testing
3. Functional player controller 
4. Explore adding very short minigames associated with some of the Random Events