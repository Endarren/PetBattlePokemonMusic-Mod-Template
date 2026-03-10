The addon Pet Battle Pokemon Mod has received many requests for specific sounds and music tracks. However, I do not have the time to make all of those sound files and put them into the addon. Also, some of these requests are from games that I have not played, so it is hard for me to make tracks and sounds for Pet Battle Pokemon Mod. So for that, and to satisfy the requests to make it so others can share their sounds and tracks with other, I created this addon. Actually, it is not really an addon, more like a formatted data pack template. This template will give anyone who does not have any programming knowledge a basis for making their own mods for Pet Battle Pokemon Mod and share it with others. All that you have to do, besides getting sound files, is just change some of the file names, change some values in those files, put in the information for your sounds, tracks, and ability sound effects, and then post it up as an addon on Curse. I will include a complete set of instructions to how you do that once the template is published.

Note: You will want to manually download this because you need to access it and placing it in the addon directory in WoW will not really help. This addon is not a library.
Instructions

Before you start, manually download the addon, and extract it into a folder using "Extract Here". Also copy the sound files you want to use into that folder.
Step 1: Naming

In order for your mod to be distinguished from other mods, you will need to give it a name.

First you need to rename the folder. Make sure you do not use any spaces in the new name of the folder. Do not start the folder name with a number and do not use ! @ # $ % ^ & * - + = in it.

Next, open the folder and find two files named “PBPMTemplate.toc” and “PBPMTemplate.lua”. Both files are simply text files and can be opened with Notepad or any simple text editor. You will need to rename both of them to be the same as the folder. So if you named the folder “MyPBPMMod”, then you have to name the files “MyPBPMMod.toc” and “MyPBPMMod.lua” respectively.
Step 2: Modifying the TOC file

This next step is to change some parts of the *.toc file

Once you open the TOC file, it should look like this:
## Author: Endar_ren
## Interface: 50001
## Title: PBPMTemplate
## Version: 1.0
## Dependencies: PetBattlePokemonMusic
embeds.xml
PBPMTemplate.lua

First, you will need to change the value on the

 “## Title: “ 

line to what you want it to be shown as in the game. For this example, you can change it to

“## Title: My PBPM Mod”

Next, change the author name to your user name.

The last thing you need to change is the last line “PBPMTemplate.lua” to the name of the other file you changed. For this example, it would be changed to “MyPBPMMod.lua”. After this last change, save the TOC file and close it.
Step 3: Modify the Lua file

Now you open up the other file, the *.lua file. This file will require you to replace some words to make it into a different addon. The first line of the *.lua file should be this:

PBPMTemplate = LibStub("AceAddon-3.0"):NewAddon("PBPMTemplate", "AceConsole-3.0", "AceEvent-3.0" );

Using the Replace tool of the text editor, replace all usages of “PBPMTemplate” with whatever you named the file, without the .lua. For this example, you would replace all “PBPMTemplate” with “ MyPBPMMod”.
Step 4: Adding Sounds

Now it is time to start putting in your information.

The table modSoundFiles is where you will put the information needed by Pet Battle Pokemon Mod for each sound file that your mod will use. You will have to put in each and every sound file that you mod uses, that is not included in Pet Battle Pokemon Mod, in this table. Each entry in the table will look like this:

modSoundFiles["zap"] =	{Length = 1, 
				  FileName ="Interface\\AddOns\\Protomod\\zap.ogg"}

The value inside the [ ] is the name of the sound file you want to use in game. This name does not have to be the same as the actual file name. It does have to be unique. No two sound files in modSoundFiles can have the exact same name.

Next are the two values inside the curly brackets ({ }): Length and FileName. Length is simply the length of the sound in seconds. FileName is the address of the sound file. It is not the absolute file path, a file path that starts all the way at C drive. It just needs to start from your World of Warcraft directory. For example:

“Interface\\AddOns\\PetBattlePokemonMusic\\Music\\RSE\\RSE Trainer Start.ogg” 

is the FileName for one of the sound files in Pet Battle Pokemon Mod. It starts in the WoW directory, which is not seen in the file name, and goes down to Interface, then addons, and then to the Pet Battle Pokemon Mod addon.

The second table is called Tracks. This table is used to store the custom music tracks that your mod will come with.

self.db.global.CustomTracks["Music Track Name"] =
{StartSoundKey = "Ruby, Saphire, & Emerald Wild Pokemon Battle Start",
MusicKey = "Ruby, Saphire, & Emerald Wild Pokemon Battle",
VictoryKey = "Ruby, Saphire, & Emerald Wild Pokemon Battle Victory"}

Like the modSoundFiles table, the string or word in the brackets ([ ]) is the name of the track. Again, each has to be unique in the Tracks table. The three values in the curly brackets ({ }) are the names of the sounds to use at those points. StartSoundKey is the beginning sound, MusicKey is the music that plays during the battle, and VictoryKey is the sound played when you win. The value for any of them is the same as the sound name you used in modSoundFiles, in the [ ].

The final table is the effectSounds table. This one holds all of the sound settings for battle pet abilities and can do different sounds depending on what happened.

effectSounds[421] = {	Damage = {File = "Boom", On = true},
				Healing ={File = "zap", On = true},
				Applied ={File = "zap", On = true},
				Dodged = {File = "zap", On = true},
				Missed = {File = "Battleship Miss", On = true},
				Faded = {File = "zap", On = true},
				Blocked ={File = "zap", On = true}}

This time, instead of a word or string in the brackets ([ ]), it is a number. That number is the ID number of a battle pet ability, in this case, 421 is Arcane Blast for battle pets. Finding the ID of an ability is pretty simple. Just go to Wowhead.com, go to the database and look under battle pet abilities. Once you find the ability you want you can find the ID at the end of its URL.

As for the information inside the curly brackets ({ }), there are seven, I suppose you could call catagories: Damage, Healing, Applied, Dodged, Missed, Faded, and Blocked. The name of the category indicates when the sound will be used for that ability. Using the example above, when the battle pet ability Arcane Blast is used and it does damage, the Boom sound file will be played. If the attack missed, the Battleship Miss sound file would be played. This means that each category can have a different sound file, if you want it to. You might also notice that Healing is there for Arcane Blast. Although Arcane Blast does not restore health, it still has a healing category for two reasons. The first and primary reason was that it was easier for me to code it that way. The second reason is that there could come at some point a way that Arcane Blast could do healing (how I have no idea, but it could happen). So having it in already allows for it to be used if it can happen.

Now for each category, there are two pieces of information. The first is called File. That name is not really accurate. It is actually the name of the sound as it is in the addon. The second piece of information is whether this category is used or not. It is either true or false.

Once you fill in all of the tables with the information they need, then your mod will be ready to go.
Step 5: Sharing

To share your mod with others, you will have to upload it to Curse. To do that, you just have to create an account and use CurseForge to create the project in World of Warcraft and upload it. Make sure that you do not use "All Rights Reserved", since you did not make the template. Make sure the project description has enough details to explain what you mod is and that it is a mod to another addon. Also please do not ask for donations for your mod unless you made all of the sound from scratch. After you create the project, you just have to wait for it to be approved. Once it gets approved, you can contact me and I will add a link to your mod on the page for Pet Battle Pokemon Mod.
