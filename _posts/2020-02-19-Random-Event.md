---
layout: post
author: Blake
title: Random Events
excerpt_separator: <!--more-->
---
Big picture still a little fuzzy, but I know I'll be dealing with random events.

<!--more-->

## Stakeholder Updates

I've gotten responses from a teacher who teaches a Money Management course and Prodege Game Studios. I'm waiting to hear back from both of them. My questions for the teacher were more material/curriculum oriented and my questions for Prodege were more game design oriented. Hopefully next week I'll have heard back from them and have some information to share.

## RandomEvents Script Design

Before writing this script I thought about all of the things I wanted it to do. Typically I don't do this with scripts I write, but I believe this script is going to be crucial to the game play experience so it's worth putting more thought into.

Script Goals:

- Increased chance of event occuring over time

	- The longer the game progresses between events, the more likely one will happen
	
- Be able to easily add or remove events (different script)

- When an event occurs, create/enable UI for interaction (different script), and pause the game state (this script)

- I don't want the same event to occur twice in the same game (different script)

## Writing the script

Unity's Update() function will run every second the game is launched. My idea is to have a float value increase by a certain amount every second that an event doesn't happen. So first I needed to find a method of increasing this float value outside of Update(), because Update() would increase the value X times or frames per seconds (I think). 

I found a Unity function called InvokeRepeating(string methodName, float time, float repeatTime). 

![InvokeRepeating](/images/random_event/InvokeRepeating.png)

This function can be called in the Start() function of a Unity monobehavior script. It will repeat the passed function every X second(s) based on the value passed in the repeatTime parameter. I tested this function by writing to the console log.

![RepeatTest](/images/random_event/RepeatTest.png)

During this function I will call Random.Range(0, 100) which will generate a random number. If this number is less than the current event chance, then the event will trigger. If it is larger than the event chance, then the event chance will increase by a determined amount.

![EventHappening](/images/random_event/EventHappening.png)

## Thinking ahead

I think it will be best to invoke a UnityEvent when the random number is less than the event chance. This will allow another script to choose the event and enable the UI, keeping my RandomEvent script from being overly cluttered.

Another thing I did was make my bool variable "eventHappening" a scriptable object. This will allow me to easily "pause game time" when the player encounters an event. I might still implement a event decision timer later on to force the player to think rationally in a quick manner, but that decision will be made further down the road.

## Stakeholder Update

I emailed Prodege Studios some questions as well as a high school personal finance teacher, but neither of them have responded. I'll reach out to them again and see if I can get some answers.

## Next Week

I need to start designing and implementing UI for the Unity Scene. Doing this sooner rather than later will allow for better testing. All of my testing this week was done through the Unity Console which was a little annoying to do.