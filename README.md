JP Engine
=========
Welcome to JP Engine! This is an automation tool for automating bashing, questing, walking, and random other things in Imperian. 

Prerequisites
-------------
In order to use JP Engine you need the following things:
* Mudlet version 2.1 (untested on earlier versions)
* GMCP Data enabled (Settings -> General -> Enable GMCP (restart required))
* The mudlet mapper must be installed and updated (Settings -> Mapper -> Download)
* Wrap width must be set to 0 (CONFIG WRAPWIDTH 0) This is not strictly required, but many features will not work.

How to Install
--------------
1. Download the files to your computer
2. Unzip if downloaded the zip file
3. Locate the JP.xml file
4. Use "Package Manager" in Mudlet. Uninstall any previous versions and then use "Install" to locate JP.xml
5. JP Engine is now installed

Using the System
----------------
Virtually all of the commands to use JP Engine begin with "jp". This is primarily to keep from interfering with things already on your system. The `jp` command on its own will bring up a help menu with command line references for the multitude of commands.  You can use `jp area`, `jp set`, `jp talk`, `jp custom`, and a few others to bring up more specific help information.

To get started you will need some data. Data comes from either your friends or you. Your friends can message you data in game (more on this later) or you can insert it yourself. As data is not included with the engine itself, we will start with setting up example data. In this example, we will use the "Booming Dunes" as our first area.

Head on over to the Booming Dunes. Anywhere in the area is fine, but for each area you must be physically in the area to edit it. Each area is stored separately so you don't accidentally start bashing a mob that happens to have the same name in a different area.  There are six types of mobs in the area that you will want to bash. We want to add each one in turn. So do the following:
```
    jp bashon a huge beaded lizard
    jp bashon a sandy boa
    jp bashon a musk hog sow
    jp bashon a rattlesnake
    jp bashon a sidewinder
    jp bashon a stout musk hog
```
Now you may wonder where we got those names. Those are the names that appear when you use the `info here` command with a mob in the room.  But the names are not the end of the story. If you've bashed in the Booming Dunes before, you know that those pesky boa's are aggressive and will automatically attack you, even if you haven't attacked them. To account for that, we want to tell the system that they are aggro and to take care of them first. We can do both with the command
```
    jp bash aggro on a sandy boa
```
This tells the engine that boa's will try to attack you immediately and to give them a high priority in the bashing queue.

Now assume for a second that your afraid of taking on more than you can chew, and only want to bash in a room with one or two boas. You can set a maximum number of any mob to bash with:
```
    jp bash max 2 a sandy boa
```
With this command set, any time there are 3 or more boas in the room, we skip it.

But not all mobs are created the same. Those musk hogs are worth money, so we want to bash them before the rattlesnake or sidewinder. We can do that with the priority command. Simply do:
```
    jp bash priority 1 a stout musk hog
    jp bash priority 2 a musk hog sow
```
Things with higher priority get bashed first, so in a room with some of each, the boa will be bashed first (because it's aggro), then a musk hog sow, then a stout musk hog, then anything else. Note that everything defaults to a priority of 0, but aggro get 100 added to their priority and teaming mobs (more about those later) get 50 added to their priority. So if you set a non-aggro mob to a priority of greater than 100, it will actually be bashed before the aggro mobs. If you find this confusing, don't worry. Just keep your priority numbers at 49 or lower and you'll be fine. (And please don't try negative numbers).

Now a side note about teaming mobs. Some mobs team, that is they won't attack you first, but once you attack one, all of the mobs in the room will attack you. We can tell JP Engine about this with the "team" flag. Simply do `jp bash team on <thing>` and that thing will be flagged as a teamer. This does a two things. First teaming mobs will be prioritized by default against non-teaming mobs. Second, if you are in a room with teaming mobs JP Engine won't pause between mobs for you to heal. (It will finish the room, and then wait to heal.) There are no mobs that team in the Booming Dunes, so we will skip this for now.

Ok, so as you're bashing you'll run into Kazim the Hidesman. If you see him, you'll want to give him your hogs and lizards then put the money he gives you into your pack. To do this you need to know Kazim's number, which is 74268 (you can see this if you find Kazim and do `info here`).  We're going to set the three commands by using the command:
```
    jp questadd 74268 give 50 hog to kazim
    jp questadd 74268 give 50 lizard to kazim
    jp questadd 74268 put gold in pack
```
That's it! And don't worry if you mess up typing something in, you can do `jp questdel 74268` to remove the commands and start over.

Next there is a room in the Booming Dunes that you don't want to wander in. In this room, the sands shift and you're randomly moved to another room. The room's vnum is 11144. So let's exclude the walker from going to that room with:
```
    jp area no_walk 11144
```

Now that we have all the data set, let's try it out. We need to do two things to do so. First we turn JP Engine on with `jp set all on` and then we tell the mapper to calculate a route with `jp determine path`. And then we're off, bashing and walking away. **Important Note: Do not leave your computer unattended. Automation in Imperian is ok, but not if you're not at your computer! Penalties apply if you are caught afk.** 

Bashing is fun and all, but what if you want to share the love and send your data to a friend so they don't have to enter it in again? Simple, just msg them the data. While in the Booming Dunes do `jp msg area <name>` to send one or more messages to your friend with the data. If they have JP Engine as well, all they have to do is read the message and follow the on-screen prompts to load all the data.

But what about when things go bad? To stop things in an emergency do `jp stop` to stop the engine. If it's not an emergency you can also do `jp set all off` which turns everything off again. If you don't finish your path, or have other walking related errors, you can do `jp clear path` to clear the saved path. 
