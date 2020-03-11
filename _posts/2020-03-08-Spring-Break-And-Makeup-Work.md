---
layout: post
author: Blake
title: Post Spring Break & Makeup Work
excerpt_separator: <!--more-->
---

Making up for lack of progress over Spring Break.

<!--more-->

Leading up to spring break I let this project fall back on my priority list. This was not ideal by any means. Despite going to California for spring break, I was able to find some time to work on Project Saturn.

## Stakeholder Updates  (30 min)

I got some email responses. After some back and forth, both Sandon Newton from Protege Studios and Melissa Gordon from Huron High School got back to me about Project Saturn.

#### Sandon Newton from Protege Studios

My questions for Mr. Newton were focused on game design. Answers are verbatim.

1. I see that many of Protege's products are centered around learning through games. What is the best way to force a learning experience to occur in a game?

	- We study user interaction with out games and the type of response it elicits. If we want to invoke a certain learning experience we will try different game design techniques until we find the right one or combination to funnel the user into the direction we want. However, you always want the user/player to think it was their choice, consequence, and most importantly you want the user to walk away with a good feeling or the time spent was worthwhile.
	
2. What are some techniques used to make a video game more learning-centric (player finding information/solutions on their own) versus making it teaching-centric (player being told information/solutions)?

	- First, a learning-centric game should define the problem, the question, or mission right away. It shouldn't be a mystery. This could be done with story cut-scenes, narration, or straight up here it is. Second, the Designer should consider all the tools in their toolbox and not leave anything out for consideration. We prefer the player to discover and struggle a bit for the information on their own, however, we also have to consider different types of learners that may need a guided-hand or additional information so we will consider teacher-centric model when its warranted. A good book to reference for game designer techniques is "The Art of Game Design" by Jesse Schell. 
	
3. What are some common pitfalls that educational video games tend to make?

	- Educational game developers sometimes lose themselves in the doing do much right away by pushing lots of quick flashy imagery, bulky-loaded interfaces that are difficult for the user to navigate and understand. Designers seem to forget that learning games are people focused (the interactive part) and ultimately to invoke a "happy experience". Its different for every project but the goal is the same, how do we make them happy. If you can make the learner happy (engaged) then we have broken across the threshold of the learner's Dojo and can start pushing new learnings that 'stick'. 
	
4. My project is intended for a grade 9-12 audience. At this level of education assessment is essential for testing knowledge gained. What is a good/satisfying way for assessment to be incorporated in a game to prove that the player learned the intended lessons?

	- If your project is a true game then your goal is to access their learning without them knowing about it, meaning, you wouldn't give a quiz or test in the middle of the game to prove their knowledge. You would have to capture and analyze data the user is creating. This can be something as simple as a the number of mouse clicks in a given time, how long did it take to get the right answer, or did inventory items get put in the right order. You could give your audience a standard quiz/test at the end to prove knowledge but as a game designer you can be creative in capturing their knowledge without them knowing, like an in game puzzle that requires bit of 'learned' or 'practiced' knowledge to solve it successfully. 
	
5. Is there anything crucial when it comes to creating educational video games that I did not mention that you think is important that I know?

	- Listening, and getting feedback as soon as possible from the intended audience of your project. This could even be at the prototype or paper idea stages. Getting feedback (data) early will help prove your designed learning system or identify areas you will need additional insight. You will find surprising answers and possibly save you time and money on things that are irrelevant and just bad. You will have to train yourself to listen and adjust the plan if warranted.
	
#### Melissa Gordon from Huron High School

My questions for Ms. Gordon were focused on personal finance and high school education. Answers are verbatim.

1. What are the most important core lessons in the Money Management course curriculum?

	- We've changed the names to personal finance 1 and 2 now, but in 1 we focus on careers, budgeting, payroll, taxes, and investing. In 2 we focus on credit, credit cards, credit scores/reports, debt/bankruptcy, and insurance (auto, home, renters and medical).
	
2. How often does the class participate in learning activities that aren't a traditional classroom lecture?

	- Frequently--we use a website called [next gen personal finance](http://ngpf.org/) as well as assignments from [Take Charge Today](https://takechargetoday.arizona.edu/search-free-lessons) in addition to other lessons/projects we've developed.
	
3. I'm not sure if this is something you can answer, but what is the approximate percentage of Huron High students that take this class?

	- No idea. I can see if I can get that information for you, but I'm not even sure if that information is available. I'm guessing we have 8 classes a year with at least 20 kids in them...
	
4. Do you think a simulation based computer game that involves making personal finance decisions could be beneficial to Huron High's Money Management course? Do you think it could be beneficial to personal finance classes in general?

	- We use personal finance simulations on the NGPF website that they have created. We also have a virtual business simulation that focuses on independent lessons in personal finance. We use these as supplemental activities. Depending on the game, it's usability, and if the kids are actually interested in it would be really important--the games on NGPF are meant to be finished within a class period to 10-15 minutes. 
	
5. Is there anything crucial about creating classroom activities that aren't traditional classroom lectures that you think I should know about?

	- I think the most important thing about this class is the experience--talking with students in class and getting them to talk to other people outside of class. They come back the next day after talking to their families and often have questions or stories they want to share. Once they buy in, you know you're good!
	
I appreciate the reponses from both Mr. Newton and Ms. Gordon. I was especially eager for Ms. Gordon's response since a target audience for Project Saturn could be the students she teaches.

## Unity Work (5 hours yotal)

#### Random Event Script Fixes (15 min)

Per Austin Yarger's advice, I abandoned InvokeRepeating(). Update() runs once per frame. If the game is running 60 frames per second, I can just have the Update() function call my EventUpdate() function on the 60th frame. If Update() is in frames 1-59 it just increases a counter variable by a number that can divide 60. This will allow me to implement a fast forward feature in the future.

#### RestartScene (5 min)

Pressing ESC will reload the game.

#### Event Library (1.5 hours)

I want to be able to add and delete events easily so I searched online for a little bit for ways that people store text/dialogue. PlayerPrefs was brought up a lot on different form posts, but I saw someone say that should really only be used for player options. It might be useful later on, but it's not what I'm looking for to store my events. I looked at creating a JSON file, but I don't really see the difference than just putting all the events in a C# dictionary. It would be a cleaner option that I might explore more when I expand the events library. Lastly, I saw some suggestions to make use of a SQLite database. I think this option is extremely unnecessary given the scope and size of my project. For now I will store my events in a dictionary of structs.

[This](https://www.youngadultmoney.com/10-examples-of-unexpected-expenses-to-plan-for/) was the website I used for initial (negative) random event ideas to test the scripts.

Here's an example of an event (I cut out the time waiting for the UI to popup):

![Event-picker-demo](/images/event-picker-demo.gif)

#### Picking an Event (1 hour)

This script will use the Event Library dictionary, select a random index from 0 to numEvents, calculate the cost of the event (somewhere between a min and max value), and fill the UI elements with the appropriate information.

The first issue I ran into was accessing my dictionary from the EventPciker script. My error message was, "Inconsistent accessibility: field type 'Dictionary<int, EventLibrary.Event>' is less accessible than field 'EventLibrary.events'". After a few minutes of googling, I found out this error was because my EventLibrary.Event class was still private, which was not allowing the Dictionary to be a public variable. Changing the class to public solved this.

#### Starting UI (2 hours)

I haven't done a done of UI design in Unity so this is an area I have little experience in. The first problem I encountered was that all my text was fuzzy even when entering play mode. I found a solution online that said to make your text very large (150pt font) and then scale it down to make it a lot sharper. I'm not sure if this is the best solution, but it works for now. 

My second issue is scaling and automatically shifting elements when screen size is variable (such as going from scene view to maximized game view in Unity). All UI that I've created in the past has suffered from this issue. Since my game is most likely going to be 2-3 UI rich scenes, I feel like it's important to figure out how to scale and place things properly early on. I learned about the Canvas Scaler component and how that can be used to create consistantly spaced UI. I also learned about the Horizontal and Vertical Layout Group components. These can be used to group UI elements and control the spacing and padding on them.

## Design Brainstorming (1.5 hours total)

#### Profile Creation (30 min)

I want the user to be in control of their game/simulation. Meaning I want them to make decisions at the beginning of the game. Such as what their living situation is (renting apt or owning a home), their method of transportation (car, bus, etc.), if they plan on having a family, what type of phone they want to buy, etc. These decisions will allow more or less random events to occur which will shape the player's success.

As of right now the only thing I'm not planning on having the player choose is their income. The reason I don't want to let the player choose their income is because I think it would make the game too easy. 

#### Play Time (45 min)

While beginning Unity implementations I thought about time flow in Project Saturn and specifically the answer Ms. Gordon gave me about non-lecture classroom activities. Educational games that supplement lectures should be completed in 1 class period. In typical high schools this ranges from 40-50 minutes taking into account the time needed to introduce the activity.

I think I want a full playthrough of Project Saturn to take 10-15 minutes. The reason for this being I envision the player making decisions on their first of second playthrough that wouldn't create a balanced budget. My reasoning for thinking this is because that is exactly what happened to me when I did a longer term simulation of this concept in 7th grade.

I'm still making the decision if the player should start the game as a young adult post college or as a teenager. Starting as a teenage would make the game more relevent to them, but a lot of random events wouldn't apply to them. I would also have to think about the ages 17-22 where they would either be in college, trade school, etc.

My first idea is to start the game as a teenage and give the player their generated salary. Then they make their budgeting decisions before a timeskip takes them to mid-late 20's. Then the game would playout with their decisions in mind. 

## Intro UI (2.75 hours total)

#### Game Start UI + IncomePicker script (30 min)

When a game starts this welcome UI will pop up and assign the player their income. I thought of a little juice mechanic to add where the income cycles through multiple randomly generation values until the player stops the roller. The value when the rolelr is stopped will be their yearly income for the rest of the game. 

I had a small issue with being unable to add the StopRoller() function to my button's OnClick() event, but I realized it was because my StopRoller() function was not public.

#### Quit Game Button (15 min)

This was a little tricky. I thought it was as simple as executeing "Application.Quit", but that doesn't close the Unity Editor (which isn't a huge deal in all honesty, it just makes testing a little more annoying). Unity stops that code from closing the application because that would close Unity. I found [this](https://answers.unity.com/questions/899037/applicationquit-not-working-1.html) solution on Unity's forums that will allow my Quit Game button to stop play mode in the Unity Editor.

#### Looking at PlayerPrefs (15 min)

Earlier in this post I said I found some results on PlayerPrefs when looking at how to store data in my game. After looking through some documentation about PlayerPrefs it appears to me this scripting component is more for user game settings that are stored between game sessions. I don't think this component will be the best thing to use when the player is setting up their profile at the beginning of the game.

#### Profile Creation Design and Implementation (1.75 hours)

Once the player knows their income they will be able to make lifestyle decisions that will effect their outcome. Here's the list I've thought of so far:

- Family 
	- Spouse 
	- Children (randomized 1-3 if chosen)
		- Child care + food
- Shelter
	- House (homeowner), multiple price options
	- Apartment (renting)
- Transportation
	- Car, multiple price options
		- Insurance
		- Gas
	- Bus, monthly pass
	- Bike, no per month fee
- Luxery Utilties
	- Cable
	- Internet
	- Phone
	- Streaming Services
- Food
	- Grocery shopping
- Retirement Saving (input percentage?)
- College?
	- Debt payments
	
I'm storing the player's chocies in a class called UserProfile. When creating this profile I learned about Auto-Implemented Properties in C#. I thought they would fix a problem I was having where I couldn't change my class variables through my button UI's OnClick() event. This didn't solve my issue though (or I implemented something incorrectly). So I just made setter functions for all my variables. I might change this later if I find a better way to do it.

I added the same bit of juice that I used for the income roller for a child amount roller. I was able to reuse the same script, but I went in and changed the variable names on that script to make it a bit less confusing in the Unity Editor.

Currently it's been taking me a little bit of time to change things around and find specific options in my Unity heirarchy. Over this next week I might spend some time thinking about how I'm organizing my UI and exploring a better way to organize it. 

Known Bugs: The child amount roller is currently rolling floats, needs to be changed to ints.

## Conclusion (15 min)

[Here](/3-11-WebBuild/index.html) is a WebBuild of the game. It does seem pretty barebones, but it feels like I accomplished a lot in terms of organizing information, organzing UI, and creating scripts that will be used throughout the game. Next week I plan to focus on how scoring will work in this the game and making the game look a bit better since it's very primitive right now. 

At first the WebBuild wasn't being attached to this post properly. I was trying to place the files in a folder that is automatically generated by jekyll. Meaning every time I launched the page the WebBuild files got erased. I realized I needed to be placing the WebBuild files outside this automaticall generated folder.