Installing Metamod and SourceMod:
	https://wiki.alliedmods.net/Installing_Metamod:Source
		1. Download Metamod:Source.
		2. Extract package.
		3. Put the "addons" folder inside server's "insurgency" folder.
		4. Restart server.
		5. Type "meta version" into server console to verify it worked.
	https://wiki.alliedmods.net/Installing_SourceMod
		1. Download SourceMod.
		2. Extract package.
		3. Put the "addons" (and maybe "cfg") folder(s) inside the server's "insurgency" folder.
		4. Restart server.
		5. Type "sm" into server console to verify it worked.
		6. Move "nextmap.smx" to "disabled" folder because incompatible with Insurgency. 

Add admins: https://wiki.alliedmods.net/Adding_Admins_(SourceMod)

Add SourceMod plugins:
	Recommended plugins:
		AFK Manager: Kicks/Moves AFK players. https://forums.alliedmods.net/showthread.php?p=708265
			Install: Put "afk_manager4.smx" into "addons/sourcemod/plugins" and "afk_manager.phrases.txt" into "addons/sourcemod/translations".
			Configure: Set variables in "cfg/sourcemod/afk_manager.cfg" (file automatically created after server restarts with plugin installed).
		Bot Balancer: Stacks bots against player until multiple people connect to server.
		LastX: Lists last X players who disconnected from the server. https://forums.alliedmods.net/showthread.php?t=58559
			Install: Put "lastx.smx" into "addons/sourcemod/plugins".
			Configure: Set "sm_lastxhistory". Not sure where to set it permanently.
			Use: Call "lastx".
		Advertisements 0.7: Recurring messages to players. https://forums.alliedmods.net/showthread.php?t=221272
			Install: Put "advertisements.smx" into "addons/sourcemod/plugins" and "advertisements.txt" into "addons/sourcemod/configs".
			Configure: Set advertisement text in "addons/sourcemod/configs/advertisements.txt". Set variables in "cfg/sourcemod/advertisements.cfg" (file automatically created after server restarts with plugin installed).
		Sm_Allinfo 2.1.1: Stores data of players who connect to the server. https://forums.alliedmods.net/showthread.php?t=83330?t=83330
			Install: Put "sm_allinfo_v2.1.1.smx"  into "addons/sourcemod/plugins".
			Use: Call "sm_allinfo <player name>".
			Note: Data is stored in "addons/sourcemod/logs/allinfo_players.txt".