# Required Server Settings
The startup command for the server must include:
	- `-workshop`
	- `+sv_pure 0`

The server's `server.cfg` must enable thirdperson:
	- `sv_thirdperson 1`
	- `sv_thirdperson_dist 100`
	- `sv_thirdperson_aimdist 1000`

# Recommended Insurgency Server Addons and Plugins

Installing Metamod and SourceMod:
	1. https://wiki.alliedmods.net/Installing_Metamod:Source
		1. Download Metamod:Source.
		2. Extract package.
		3. Put the "addons" folder inside server's "insurgency" folder.
		4. Restart server.
		5. Type "meta version" into server console to verify it worked.
	2. https://wiki.alliedmods.net/Installing_SourceMod
		1. Download SourceMod.
		2. Extract package.
		3. Put the "addons" and "cfg" folders inside the server's "insurgency" folder.
		4. Restart server.
		5. Type "sm" into server console to verify it worked.
		6. Move "nextmap.smx" to "disabled" folder because incompatible with Insurgency.

Add admins: https://wiki.alliedmods.net/Adding_Admins_(SourceMod)

Add SourceMod plugins. Recommended plugins:
	- Advertisements 0.7: Recurring messages to players. https://forums.alliedmods.net/showthread.php?t=221272
		- Install: Put "advertisements.smx" into "addons/sourcemod/plugins" and "advertisements.txt" into "addons/sourcemod/configs".
		- Configure: Set advertisement text in "addons/sourcemod/configs/advertisements.txt". Set variables in "cfg/sourcemod/advertisements.cfg" (file automatically created after server restarts with plugin installed).
	- AFK Manager: Kicks/Moves AFK players. https://forums.alliedmods.net/showthread.php?p=708265
		- Install: Put "afk_manager4.smx" into "addons/sourcemod/plugins" and "afk_manager.phrases.txt" into "addons/sourcemod/translations".
		- Configure: Set variables in "cfg/sourcemod/afk_manager.cfg" (file automatically created after server restarts with plugin installed).
	- Bot Stacker: Stacks bots against players when all players are on the same team.
		- Install: Put "botstacker.smx" into "addons/sourcemod/plugins" and "botstacker.txt" into "addons/sourcemod/configs".
		- Configure: Set bot counts in "addons/sourcemod/configs/botstacker.txt". Set variables in "cfg/sourcemod/botstacker.cfg" (file automatically created after server restarts with plugin installed).
	- LastX: Lists last X players who disconnected from the server. https://forums.alliedmods.net/showthread.php?t=58559
		- Install: Put "lastx.smx" into "addons/sourcemod/plugins".
		- Configure: Set "sm_lastxhistory". Not sure where to set it permanently.
		- Use: Call "lastx".
	- Simple Player Stats: Tracks information about connections, played time, kills, deaths, and objectives for each player.
		- Install: Put "simpleplayerstats.smx" into "addons/sourcemod/plugins".
	- Sm_Allinfo 2.1.1: Stores data of players who connect to the server. https://forums.alliedmods.net/showthread.php?t=83330?t=83330
		- Install: Put "sm_allinfo_v2.1.1.smx"  into "addons/sourcemod/plugins".
		- Use: Call "sm_allinfo <player name>".
		- Note: Data is stored in "addons/sourcemod/logs/allinfo_players.txt".

# VPS Setup

## Install Insurgency Server
Follow the instructions here: https://linuxgsm.com/servers/insserver/

This is what I ended up doing:
1. Remote into VPS as default user.
2. (Ubuntu >= 20.10) Execute: `sudo dpkg --add-architecture i386; sudo apt update; sudo apt install curl wget file tar bzip2 gzip unzip bsdmainutils python3 util-linux ca-certificates binutils bc jq tmux netcat lib32gcc-s1 lib32stdc++6 libsdl2-2.0-0:i386 steamcmd`
3. `sudo adduser insserver`
4. `su - insserver`
5. `wget -O linuxgsm.sh https://linuxgsm.sh && chmod +x linuxgsm.sh && bash linuxgsm.sh insserver`
6. `./insserver install`
7. `./insserver start`

## Setup Files
1. SFTP into VPS using `insserver` user credentials.
2. Upload Metamod and SourceMod files.
  1. Upload Metamod and SourceMod packages (the `.tar.gz` files) to /home/insserver/serverfiles/insurgency.
  2. Remote into VPS as `insserver` user.
  3. Navigate to serverfiles/insurgency (execute `cd serverfiles/insurgency/`).
  4. Extract Metamod and SourceMod packages (execute `tar -xf mmsource-1.11.0-git1148-linux.tar.gz` and `tar -xf sourcemod-1.11.0-git6911-linux.tar.gz`).
  5. You can delete the Metamod and SourceMod packages.
3. Upload additional configuration files.
4. Modify startup script by editing `/home/insserver/lgsm/config-lgsm/insserver/common.cfg`.
  1. Add: `defaultmap="desertglory firefight"`
  2. Add: `maxplayers="16"`
  3. Add: `startparameters="-game insurgency -strictportbind -ip ${ip} -port ${port} +clientport ${clientport} +tv_port ${sourcetvport} -tickrate ${tickrate} +sv_setsteamaccount ${gslt} +map ${defaultmap} -maxplayers ${maxplayers} -workshop -norestart -condebug +sv_pure 0"`

## Restart Insurgency Server
1. Remote into VPS as `insserver` user.
2. `./insserver restart`

## Add Cron Jobs
The following lines can be added to the `insserver` user's cronjob file (run `crontab -e`):
1. Every 3 minutes check the game server and restart it if it has crashed (this will not start game server it if was manually stopped):
  * `*/3 * * * * /home/insserver/insserver monitor > /dev/null 2>&1`
2. Every day at 12pm server time (probably UTC) restart the game server and install any updates:
  * `0 12 * * *  /home/insserver/insserver force-update > /dev/null 2>&1`
