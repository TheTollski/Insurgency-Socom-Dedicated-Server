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
		6. I haven't done this yet, but: "move nextmap.smx to disabled folder because incompatible with insurgency build"

Add admins: https://wiki.alliedmods.net/Adding_Admins_(SourceMod)

Add SourceMod plugins:
	How to add most SourceMod plugins: Put the plugin's ".smx" file into the "addons/sourcemod/plugins" folder.
	Recommended plugins:
		LastX: Lists last X players who disconnected from the server. https://forums.alliedmods.net/showthread.php?t=58559
			Install: Put "lastx.smx" into "addons/sourcemod/plugins".
			Configure: Set "sm_lastxhistory". Not sure where to set it permanently.
			Use: Call "lastx".
		Advertisements 0.7: Recurring messages to players. https://forums.alliedmods.net/showthread.php?t=221272
			Install: Put "advertisements.smx" into "addons/sourcemod/plugins" and "advertisements.txt" into "addons/sourcemod/configs".
			Configure: Set advertisement text in "addons/sourcemod/configs/advertisements.txt". Set variables ("sm_advertisements_enabled", "sm_advertisements_file", "sm_advertisements_interval") in "cfg/sourcemod/advertisements.cfg".