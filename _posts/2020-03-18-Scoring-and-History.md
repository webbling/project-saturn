---
layout: post
author: Blake
title: Event History and more UI
excerpt_separator: <!--more-->
---
This week I spend time finishing some game setup features and spent the majority of my time implementing an Event History feature.

<!--more-->

The WebBuild link is at the bottom of the page.

## Adding to Profile Selector (1 Hour)

I added more options for the player's profile. While adding more components I also went back into scripts that store user data and added more variables and functions to handle the profile creation process.

I'm still struggling to determine how much information about their choices I should be giving away in this part of the game. For example, I tell the playing that having a spouse will boost their income, but I don't tell them that owning a house will come with many more costs than an apartment. I feel like not providing information here will create more learning-centric lessons later in the game.

I don't really enjoy how I have my UI organized. Unity UI Canvas wants to put items lower in the hierarchy to the front. Right now I have the UI windows that I want to show first at the top of my heirarchy (because that makes sense to me, top = first). Instead of just disabling each window with the OnClick() button event, I have to disable the current UI window and enable the next one in the hierarchy. Ideally, I would have 1 UI window that I could edit the text of, but some of the UI windows have more/less Text components and different button locations. This isn't a huge issue, it's just tricky to make sure I handle everything currently with the various OnClick() events on the buttons. It's a solution that works for now, but it gets too confusing in the future I'll have to adjust it.

- Features I want to add in the future
	- I want the player to be able to pick more specific options for Houses and Cars
	- I want to be able to gray-out/invalidate options based on previous choices. E.g. You can't select a sports car if you have a spouse + children
	
## Profile UI (45 min)

Created UI so that the player can see (most of) their choices that they made in the profile creation. On this feature I got a little held up on when to change the Text components in the UI. I was trying to update them with a separate function I created that would have to caleld X times for X number of things in the profile UI, but then I realized I could just update them in the Start() function in my FetchCharacteristic script. Unity Events handle updating the values in the UserProfile script.  

![profile-unpopulated](/images/profile-unpopulated.png)

<!--more-->

![profile-populated](/images/profile-populated.png)

## Event History (3.5 Hours)

I think having a component that shows the player all of the different monetary transactions is crucial for the learning experience of the game. It's important for the player to see how they money is being spent as they simulate their virtual life. That way if things start going south, they can see exactly how their money was used and pin point locations where they can improve.

I spent about half an hour researching the best way to do this in Unity. I saw a few different solutions make use of a component called a Scroll View. When looking up what that was, I found [this](https://www.youtube.com/watch?v=oDBVRcHhc0M) wonderfully helpful 1 minute tutorial video. This video actually used the Scroll Rect component with a Mask component instead of a Scroll View. This was exactly what I wanted my Event History to look like.

#### Scroll Rect Prototype

![scroll-rect-prototype](/images/scroll-rect-prototype.gif)

At first my image of Saturn wasn't being confined. I could scroll way down and way up and essentially lose the image in the scroll rect. After rewatching the above tutorial video a few times I realized I was attaching the wrong Rect Transform component to the Scroll Rect component. Once I had the correct component attached, it behaved exactly like the tutorial example. The user and scroll using the mouse scroll wheel or they can click and drag.

#### Adding Events to Scroll Rect

My next issue was adding events to the history. In the YouTube video I linked, the creator had constant sized image in his Scroll View, much like my prototype. The history will expand as the game progresses and I want most recent events at the top of the History UI.

I thought I was going to have an issue with the Rect Transform Height of the Event Container (attached to Scroll Rect) because every time I add an event the size of the Rect Transform is going to have to increase (unless it eventually hits a max size that I have yet to determine). This ended up being a non-issue when I realized I can anchor the Event Container and everything inside of it to the top of the game object that has the Scroll Rect component.

Using a Vertical Layout Group on my Event Container works as long as I increase the Rect Transform Height every time I add an event to the Event History. The problem I ran into when writing a AddEvent script prototype was that eventContainer.rect.height cannot be changed because apparently "rect" is not a modifible variable. 

After looking into this, I found that the Rect Transform component has a sizeDelta property that can be modified. This just required setting it to a new Vector2() value that used the existing width and the new height. I was then able to create a working prototype of adding entries to my Event History.

![before-adding](/images/add-event-prototype1.png) ![after-adding](/images/add-event-prototype2.png)

I disabled the mask and took a before and after screenshot of the Unity editor to show that this prototype worked. As of right now the new events show up at the bottom of the history. I will change this in the future if it's too unnatural, but I didn't want to spend time making it look perfect before it functioned correctly.

At this point I was a little stumped on how to instantiate new entries into the Event History. I couldn't reuse my method for creating the larger Event UI that happens in the top left of the screen because that UI reuses 1 window over and over. It just updates the texts, gets set active, and then inactive when the player clicks one of the Accept or Ignore buttons. I thought where the best place would be to instantiate my EventRecap (what my entry prefab is called). My script EventPicker handles updating the larger Event UI so it has all the information that I would want to go into my EventRecap entry. 

I was halfway through updating my AddEventToHistory prototype script to have a EventPicker variable that it could access, when I realized down the road I'm going to have more things in my Event History than just my Random Events. Instead of wasting too much time thinking about that, I just continued with my current implementatino method in order to get something working. Here is a gif demo of the Event History in action

![history-gif](/images/event-history-demo.gif)

## Prepping Build (15 min)

As I was working on different components I was moving around and disabling a lot of UI. After I finished Event History I spent some time making sure everything was working correctly before making a Web Build.

## Bugfixes (30 min)

- Child Selector
	- Last week I mentioned a dollar sign would show up. I fixed this bug by adding bool variables in my script letting me know which value I'm currently rolling for. Then I fixed the problem of having a float child value by changing my minRoll and maxRoll variables to ints instead of floats. Lastly, I realized Random.Range() is [inclusive, exclusive] so I fixed the child selector only choosing 1 or 2.
	
- Setting Income and NumChildren in the Player Profile
	- Setting bool values with OnClick() events is easy because there are only two values it can be. This was a little tricker with the int values for my Income and NumChildren variables. I solved this by making a function that grabs the current rolled value from my RollAmount scripted when called. Then in my PlayerProfile script I have two functions that set Income and NumChildren, if the current rolled value is 0 then they can be manually set (from my Test Profile button).
	
- Income == Children
	- The solution to my last bug fix caused another bug to occur. NumChildren was now equal to Income.
	
	![too-many-children](/images/too-many-children.png)
	
	This happened becuase I forgot that I had two different instances of my RollAmount script. I tried to make my functions that set Income and NumChildren to take in a paramter of RollAmount, but then the function wasn't recognized by the OnClick() event. So I implemented a "hacky" solution of making two RollAmount variables in my PlayerProfile script that grab the right values for Income and NumChildren.
	
## Lifestyle Adjustments

Obviously it goes without saying that this has been a crazy week in terms of COVID-19 impacting everything. Usually I will go somewhere on North Campus to get work done because it's easier for me to associate my apartment with leisure time and campus with work time. Setting up my laptop at my kitchen counter helped me stay focus more than when it was setup at my desk (which also has my Desktop PC that I use for video games). I also attempted the Pomodoro workstyle technique that Professor Yarger mentioned in the email to WSoft MDP students. That helped alot. I would use the short break times to update this blog post with what I worked on that past half an hour. I think both of these techniques will help me stay focused the rest of the semester. 
	
## WebBuild

[Link](/3-18-WebBuild/index.html)