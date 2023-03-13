
# Passel Public Version
This is an adapted version of the public Passel bot, made specifically to be used on the Obsolescence private server. Most of the options have been deleted, since we have no 
use for them.

**Feel free to fork this repo and create your own bot by adding more features, or using this code in another bot you may 
already have. [Click for the discord python API](https://discordpy.readthedocs.io/en/stable/api.html).**
***

# About
Passel is a discord bot that manages the number of pins in a server. Discord has a pin limit of 50 pins per channel. However, 
with passel, that limit can be bypassed. The following readme will explain how the bot works and how to add and set up the bot in a server.

## How it works
The bot works by unpinning one message and sending it to a different channel during setup. 

**Also, any channel that has 50 pins should have one message unpinned, and then repin that 1 message after the bot is setup.**

***Please keep in mind that the bot only pins messages that REACH and EXCEED the limit of 50 pins per channel in discord.***

***
# Setup
Set up consists of the 3 following sections. Please follow each section carefully. It would be easy to do this setup if 
you are the server owner or have administrator permissions. You MUST do the setup on a laptop or computer.

## 1. Create a Discord bot in the developer portal
You must first create a discord bot account in the [discord developer portal](https://discord.com/developers/applications). 

 1. log in to the portal using your discord account
 2. click on new application
 3. give the bot a name, you can name it anything you want, does not have to be passel
 4. optional: under settings > general information, add a profile photo for the bot
 5. optional: under settings > general information, add a description for the bot
 6. under settings > bot, click on add bot, click on "yes, do it!" 
 7. click on reset token, **when you see the token copy it and store in a safe place.** DO NOT EVER post this token anywhere. If you do go back to the portal and reset the token and update it the main.py file in the section below. The token should look something like this `MTAwMTg3MDk1OTUzNzU2NTc1Ng.GZ6ikH.C_NRQfjO2oB1otGsRJZz5cpTRhKrIZ6twRnI4M`, a random generation of characters.
 8. uncheck PUBLIC BOT and REQUIRES OAUTH2 CODE GRANT
 9. under Privileged Gateway Intents, check PRESENCE INTENT, SERVER MEMBERS INTENT, and MESSAGE CONTENT INTENT
 10. save your changes
 11. under BOT PERMISSIONS, check Embed Links, Read Messages, Manage Messages, Attach Files, Use External Emoji, Send Messages and Read Message History.

### Add the created bot to your server

The bot is now created, so it is time to add it to the server.

1. click on the OAuth2 arrow in the sidebar, then click on URL generator
2. under scopes select bot
3. you should see a new menu, under bot permissions, check Embed Links, Read Messages, Manage Messages, Attach Files, Use External Emoji, Send Messages and Read Message History.
4. then copy and paste the invite link into a browser and invite the bot

***
## 2. Edit the main.py file
This section, you will be editing the python code to fit your server's needs. 

**MUST DO THIS BEFORE PROCEEDING**
1. on your discord account, go to settings
2. then, on the sidebar click on advanced
3. check Developer mode so its green

Now, to configure the bot, you need to check out the repository, or download the ZIP folder directly, making sure to unzip it. 

Afterward, you can optionally change the bot command to anything else on line 14. The default is "p.", and can be changed to anything that is 1 character or multiple characters. 
Normally for discord bots, do not replace this with anything that is more than 2 characters. 

You can also set a list of black listed channels to which the bot will not have access to copy the pins from. This can be configured on line 21.
Add each channel ID as list, separated by a comma.

Adding one channel should look like: `blacklisted_channels  = [926958717696634901]`

More than one channel should look like: `blacklisted_channels  = [926958717696634901, 972685609040748584, 840372439824334888]`

You can obtain a channel's ID by right-clicking its name on Discord, and selecting "COPY ID".

## 3. Host the bot on fly.io for free

_Instructions adapted from Notorious' PDF (Notorious#1472) on the original repository._

1. Install flyctl on your computer by downloading from [here](https://fly.io/docs/hands-on/install-flyctl/).
2. Use the following command to create an account and authenticate yourself:
```shell
fylctl auth signup
```
Just create the account on your browser, and eventually you will be logged in on the terminal.

3. Checkout the repository, or download the ZIP folder directly, making sure to unzip it. 
4. Make sure that your terminal is in the project base directory and run the following commands:
```shell
flyctl launch
flyctl deploy
```

Launch will create the application in Fly.io. It will request some inputs, but just say ignore most of them. Make sure
to select "No" when asked to overwrite the Dockerfile, and when asked to create a postgres database.

The Deploy command will bring the bot online. 

5. A fly.toml file should have been created on the project directory. Open it and delete all settings that are under [[services]].
6. Run the following commands:
```shell
flyctl secrets set TOKEN=<TOKEN>
flyctl secrets set PINS_CHANNEL=<CHANNEL_ID>
```

Make sure to substitute <TOKEN> with the discord bot token that you copied above, and <CHANNEL_ID> with the ID of the
channel where the bot should copy the pins to. Try not to delete this channel in the future or, if you do so, make sure to update
the Channel ID via the above command.

7. You can now run the Deploy command again to update. Afterward, go to the fly.io dashboard and check the application logs.
If you see a "We have logged in as Pinanços", then you have been successful in deploying the bot!

### Extra commands

If you want to temporarily shut down the bot, then you can run the following command:
```shell
flyctl scale count 0
```

Re-run the command with "1" instead of "0" to restart the application.