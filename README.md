# TTS-Necromunda
Table Top Simulator Assets for the game Necromunda


## How-to create new models
- https://www.youtube.com/watch?v=zHlxPai-Knc
- https://www.dicefromhell.de/how-to-scan-a-tabletop-miniature-part-1

Notes:
- take care of taking good pictures!
- the unity part is NOT needed.
- you can use cylinder.obj as collider
- Scale your model in TTS, and save it as an object.

## How-to contribute them to this repo:

### Initialization
- create account
- install github desktop
- clone repo


### Workflow
- choose a unique, descriptive name for your file (counter-example: "Goliath_1")
- add description to README, following existing format
- optional: add raw and intermediary files in subfolder "raw/{FILE_NAME}/"
	- raw pictures in subfolder "pics"
	- Zephyr masks in subfolder "pics"
	- Zephyr project, intermediary and output files in subfolder "zephyr"
	- Blender project and output files in subfolder "blender"
	
- from TTS, save your properly scaled model in the "models" folder.
- place your final .obj and .jpg (model and texture) in the "models" folder.
- edit the .json file to fix the paths, depending on where you installed TTS.

You can commit your changes back to the repository at any stage, from github desktop.


# How to use models:
- If you have followed the steps to contribute to this repo, you may have cloned the files in the proper location for TTS to directly show in "saved objects" the contents of the repo.

- If you do not want to bother with git, simply "Download zip", then extract resulting "models" folder into your TTS saved objects folder (in Windows: "{USER}\Documents\My Games\Tabletop Simulator\Saves\Saved Objects")
