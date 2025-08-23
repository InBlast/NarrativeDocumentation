# Narrative Documentation by InBlast
This is my try to provide a comprehensive documentation for Narrative, based on experience and reading sessions of the C++ code.  
It is **NOT** an official documentation ([Link to official documentation](https://docs.narrativetools.io/)).  
This documentation is not exhaustive and might contain mistakes, please be aware of that.  

Please use the table of content to navigate between the different sections :  
<img src="https://github.com/user-attachments/assets/f13273f3-c958-4c2a-b901-f41e726c6d46" width="200"> 

I highly advise to not directly use any class provided by Narrative. Subclass it first in BP (your BP_MasterClassName), then subclass this created master class to create the multiple versions of what you will use in your game.  

## Video Tutorials :
[Video tutorials by Primal](https://www.youtube.com/@wonderscapecreations/playlists)  
[Official Video tutorial](https://www.youtube.com/@narrativetools/playlists) 

# Tales
## Quests
### Conditions
Even if conditions also appear in the quest graph, note that using conditions in quest graph is currently unsupported  
**_Narrative Base class :_ UNarrativeCondition** 
## Dialogues
## Events


# Inventory
## Narrative Item
## Item Collection

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

For the POI to work correctly, you will need to run the [Navigator Utility Widget](#utility-navigator-widget) when you finished to configure all the POI.


## Minimap

### Utility Navigator Widget

Search for Utility_Navigator in the plugin files :  
<img width="185" height="206" alt="image" src="https://github.com/user-attachments/assets/49c5fce5-02e9-4f91-b65c-edb7fb929dc0" />  
Right click on it and chose "Run Editor Utility Widget" :  
<img width="282" height="148" alt="image" src="https://github.com/user-attachments/assets/0929aafd-ad2f-4fe1-b78f-859169d715b6" />  
<img src="https://github.com/user-attachments/assets/635a9368-786e-40ce-b775-05d8d7647961" width="500">  

If you add or modify POIs after clicking "Generate POIs", you can just run "Generate POIs" again. There is no "Delete POIs" step needed.

# Player and NPCs
## NPC 
### NPC Definition
## Player
### Player Character
### Player Controller
### Player State
### Player Definition
**_Narrative Base class :_ UPlayerDefinition** (Child of **UCharacterDefinition**)  

| Variable Name | Description |
| ---- |----------|
|Default Appearance| [Character Appearance](#character-appearance) The default look of your player|
|Default Currency|The default currrency your player has|
|Default Item Loadout|The default Items your player start with. Can be [Narrative Item](#narrrative-item), [Item Collection](#item-collection) and/or a roll table|
|Default Owned Tags|The display name in game|
|Default Factions|The displayed icon (on minimap, worldmap, and compass) |
|Trigger Sets|Unknown|
|Attack Priority|Unknown|
|Ability Configuration|Unknown|

## Ability Configuration
## Character Appearance


# Interaction
## Interactable Component
## Interactible Component

# Combat
## GAS



