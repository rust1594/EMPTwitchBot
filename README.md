# EMP Radio Twitch Bot

## Summary 
Node.js implemetation of a chatbot for twitch, intended for multiple channels and for helping host raid trains. 
Also has specific commands that are listed down below.

## Features 

### Permission Levels
The bot has three levels of permissions built in. Certain bot commands require a different permission levels.

- 1st permission level - all chat users
The very base level permission, has access to all common chat commands. But cannot use higher level commands.

- 2nd permission level - moderator
This permission level is granted to users that are moderator in the channel that the user and bot are currently in. 

- 3rd permission level - admin
This is a special permission level intended for bot behavior across the twitch platform. Determined through the code itself, to be a list file in the future.


### Current Commands
All commands start with an exclamation point. Brackets represent user input; do not actually include the brackets

#### Commands open to all users
##### Basic Commands
These "basic" commands just have a simple text response. They are not being listed here because they can be added, edited, and removed by admins. How that is done will be listed below. To show the current commands of the bot, use the command:
!list_basic


##### Help
`!help` or `!h`  
Lists all the available commands as a chat response.

##### Donate link
`!Donate`  
If set up for the particular channel, the bot will respond with a link or information on how to donate to the channel. If not set up, then it will respond that there is no available donation link set up.

##### Answers Question
`! [question]?`
or
`! [Option 1] or [Option 1]?`  
Must have a space a first character. If you ask a question, the bot will respond with a yes or no. If the command lists two options, will reply with one or the two options. 

#### Commands only for Moderators

##### Shout out
`!empso [@channel]`  
Responds with a hyperlink to the channel included in the message. 

#### Commands only for Admins

##### Host Channel on the EMP_Radio channel
`!emphost [@channel]`  
Set the EMP_Radio's channel to host the channel included in the message.

##### Join Channel
`!empjoin [@channel]`  
Have the bot join the channel included in the message. This must be used in a channel that the bot is already in.

##### Leave Channel
`!emppart [@channel`  
Have the bot leave the channel included in the message. This must be used in a channel that the bot is already in.

##### Add basic command
`!empadd [newcommand], [message response]`  
Adds a command that the bot can respond to. The user input needs to include two parts;
[Newcommand] - this is the command typed in by users that the bot will repond to. Do not include the exclamation point in front.
[message response] - what the bot will respond with.
The new command and the message response needs to be separated with a comma.

##### Edit Basic command
`!empedit [command], [new response]`  
Allows the response to a basic command to be replaced. Requires two inputs
[command] - the basic command that is to be edited. Must match a command that already exists.
[new response] - the new message text for the command.
The command and the message response needs to be separated with a comma.

##### Remove basic command
`!empremove [command]`  
Removes a basic command from the bots repitoire. Requires the command to be in the message.
[command] - the command to be removed. Must exist within the bots list.

### Autohosting a show
The bot allows for a "show" to be created; that is, to create a list of twitch channels that will be raided one after another.
The bot will do two things; Host the current channel in the show on the EMP_Radio channel, and will join that channels chat so that it's commands can be accessed as the show goes on.
LIMITATIONS: currently, there can only be one show saved by the bot at a time. So please, be careful about creating shows and if possible do it day of, or do it after upcoming show has happened. (having multiple shows is a planned update).

To create a show, the command `!addshow` on the emp_radio channel. The bot will then start to ask a series of questions:

- 1st Question -  "What date will it be? (MM/DD/YYYY)"
The date the show will start on. Please keep to this format.

- 2nd Question - "Ok. Now the full set list. Assumes PST/PDT. Comma to separate time and user, semicolon for new line"
  This is where the show information is inputted. It is recommended that you prepare this list in an outside text editor (such as notepad) and then copy it in.
  The format for each spot in the show is [time], [channel]. To separate the time and channel, a comma must be used. To separate each listing, a semicolon must be used.
  Here is an example input:

  `11:00 am, channel1;
  12:00 pm, channel2;
  1:00 pm, channel3;
  2:15 pm, channel4`

  Please notice that there is NOT a semicolon at the end of the input. Including one could break it.

- 3rd Question - "Almost Done. Here is what I received:" - "Does this look correct?"
This is to review the data the bot has received and how it processed it. Please double check what it thinks the show is.

When done, please type a `y` for yes and a `n` for no.
`y` will finalize the data, and create the schedule for the show.
`n` will abort the process, and you will need to start over.

## Installation of Bot
If you wish to run this bot in a separate instance, then this is the discussion for that. This bot runs entrirely in node.js, so the machine you run this on will require that, along with a few modules. 

### Required Modules
Requires tmi.js, schedule.

Install these modules with npm, with the following commands:
npm install tmi.js
npm install node-schedule

### Initialization files
there are several files that need to be populated with data in order for the bot to run. There are stored in the settings folder

oauth.txt - for the channel that the bot is operating out of, you will need an oauth token for that channel. One can be created for your channel here: https://twitchapps.com/tmi/
This whole token needs to be in a file name oauth.txt. There is an example file included.

twitch_bot_channel.txt - the name of the channel that the bot will run from. There is an example file included.

### Operation files
These are files that, while not necessary, help out with the functionality of the bot. These file are in the "data" folder.

admins.json - list of the channels that have admin rights to the bot.

channels.txt - Channels that the bot will join on startup. Basically where the bot will permanently reside.

commands.json - the list of basic commands that the bot has. These are the ones that can be added and removed by the admins.

donations.txt the list of channels and their donation links, associated with the "!donate" command

set_list.json - The show information that will be auto hosted by the bot.


