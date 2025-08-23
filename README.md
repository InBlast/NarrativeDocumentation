# NarrativeDocumentation
Documentation for the Narrative Pro Plugin.  
Please use the table of content to navigate between the different sections.  

I highly advise to not directly use any class provided by Narrative. Subclass it first in BP (your BP_MasterClassName), then subclass this created master class to create the multiple versions of what you will use in your game.  
## Video Tutorials :
[Video tutorials by Primal](https://www.youtube.com/@wonderscapecreations/playlists)
[Official Video tutorial](https://www.youtube.com/@narrativetools/playlists) 

# Tales
## Quests
## Dialogues

# Inventory
## Items

# Navigation
## POI
**_Narrative Base class :_ APOIActor** 

I suggest to subclass APOIActor into your own BP, and then use this newly created BP to place POI.

| Variable Name | Description |
| ---- |----------|
|POITag|A unique Tag for the POI. Create one for every POI you want in your world|
|Create Map Marker|Should this POI have a world map marker visible ? (on minimap, worldmap, and compass) |
|Supports Fast Travel|Can this POI be used to fast travel to ?|
|POI Display Name|The display name in game|
|POIIcon|The displayed icon (on minimap, worldmap, and compass) |
|Linked POIs|Unknown|

**Usage :**  
Place your BP_POI in the world :  

<img src="https://github.com/user-attachments/assets/44427a11-697d-483c-b20d-9db40405b912" width="500">  

You can adjust the radius of the sphere and the position of the Fast Travel Capsule

The player will discover the POI when he enters the Sphere.  
The player will be placed at the FastTravelCapsule location when fast travelling to the POI.  

Set up the POI variables :  

<img src="https://github.com/user-attachments/assets/6318551b-3a6d-4bd6-8c87-b615526dc34d" width="500">  

For the POI to work correctly, you will need to run the [Navigator Utility Widget](#navigator-utility-widget)


## Minimap
TESTESTEST

TESTESTEST

TESTESTEST

TESTESTEST

TESTESTEST

TESTESTEST

TESTESTEST

TESTESTEST

TESTESTEST

TESTESTEST

TESTESTEST

TESTESTEST

TESTESTEST

TESTESTEST

TESTESTEST

TESTESTEST

TESTESTEST
### Navigator Utility Widget
TESTESTEST

TESTESTEST

TESTESTEST

TESTESTEST

TESTESTEST

TESTESTEST

TESTESTEST

TESTESTEST

TESTESTEST

TESTESTEST

TESTESTEST

TESTESTEST

TESTESTEST

TESTESTEST

TESTESTEST

TESTESTEST

TESTESTEST

TESTESTEST

# NPC
## NPC Definition
## AI

# Player

# Interaction
## Interactable Component
## Interactible Component

# Combat
## GAS



