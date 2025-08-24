# Narrative Pro Documentation by InBlast
This is my try to provide a comprehensive documentation for Narrative, based on experience and reading sessions of the C++ code.  
It is **NOT** an official documentation ([Link to official documentation](https://docs.narrativetools.io/)).  
This documentation is not exhaustive and might contain mistakes, please be aware of that. I encourage you to analyse as much as you can the demo provided in the plugin files, and to test by yourself.
If you find any mistake, or if you would like to add something, please contact me on the Reubs Discord server.

Use the table of content to navigate between the different sections :  
<img src="https://github.com/user-attachments/assets/f13273f3-c958-4c2a-b901-f41e726c6d46" width="200"> 

I highly advise to not directly use any class provided by Narrative. Subclass it first in BP (your BP_MasterClassName), then subclass this created master class to create the multiple versions of what you will use in your game. This way you can easily update Narrative Pro. If you need to do modifications in the plugin C++ code, please keep in mind that you will need to remake them in case of Narrative update.  

I use screenshots from the Narrative Pro open world demo as much as I can, so you can also check the same files by yourself.  

## Video Tutorials :
[Video tutorials by Primal](https://www.youtube.com/@wonderscapecreations/playlists)  
[Official Video tutorial](https://www.youtube.com/@narrativetools/playlists) 

# Quests & Dialogues Generalities

It's recommended to make your own Master Dialogue and Master Quest BP. You can follow these links for that :  
[Master Dialogue](https://docs.narrativetools.io/pro/dialogue/master-dialogue)  
[Master Quest](https://docs.narrativetools.io/pro/quests/master-quest)  
This way you can make modifications to all your Dialogues/Quests by editing your master BP.  

# Quests
All Quests you create should inherit from your own QBP_QuestMaster BP.  

Quests are made of a Quest Graph and of an Event Graph :   
<img width="327" height="36" alt="image" src="https://github.com/user-attachments/assets/890f6d4e-3384-4946-a048-b2228cd4bfbb" />
## Quest Graph

The Quest Graph is a succession of Quest States and of Tasks.  
<img width="471" height="112" alt="image" src="https://github.com/user-attachments/assets/fa656702-1d50-418c-8d2a-5919d0cc630d" />

Double clicking on a State node or on a Task node will add an event binded to this node in the Event Graph. It will appear in the "On Entered Func Name" variable of the node.
To remove the binded event, Shift+click on the spark icon on the top right of the node, and delete the event in the Event Graph.  
<img width="223" height="91" alt="image" src="https://github.com/user-attachments/assets/d25d29d9-64db-438a-8eaf-be2979039af7" />

### Quest State

A quest states represents the current step of the Quest. It needs to be followed by a [Task](#tasks), which will act as a condition to start the next State Node

| Variable Name | Description |
| ---- |----------|
|State Node Type|Type of the State Node. Can be **Regular** (Quest in progress), **Success** (Quest is finished and successful, Quest end node) or **Failure** (Quest is finished but failed, Quest end node) |
|ID|Unique Node ID, it's the current state of the quest. Used for saving purposes, but it can also be used in condition checks|
|Description|The description of the quest as it will appear in the player Quest Journal|
|On Entered Func Name|The Event in the EventGraph which will be called when this state Starts and when it ends (= When the next state will start)|
|Conditions|Please ignore, currently only works in Dialogues|
|Events|[Events](#events) A list of events to run when the State node starts/Ends or both|


### Tasks
**_Narrative Base class :_ UNarrativeTask**  
You can create new Tasks in Blueprint. Please note that the newly created tasks won't be accessible directly when adding a new task to the Quest Graph : add any other task, select the task node, and change the task from there :  
<img width="724" height="218" alt="image" src="https://github.com/user-attachments/assets/91878871-c60a-485a-b2bf-4c4607ee2a84" />

| Function Name | Description |
| ---- |----------|
|Begin Task| Event run when the task begins|
|End Task|Event run when the task ends|
|Get Navigation Marker Attach Actor|This will be run when the start starts and try to attach a Navigation marker to the target actor. You can override it to place your own actor|
|Get Navigator Marker Location|This will be run when the task starts and add the quest marker at the location. Will be used if Get Navigation Marker Attach Actor doesn't return a valid actor|
|Get Task Description|Return the task text. Can be overrided to add some logic automating the task description.|
|Get Task Node Description|Return the description displayed in the Quest graph. No impact in game, it's just for more clarification when making quests.|
|Get Task Progress Text|To override the default task progress text|
|On Task Completed|Event run when the task is completed|
|Tick Task|Tick event|

| Variable Name | Description |
| ---- |----------|
|Required Quantity|The amount of time the task needs to be completed|
|Description Override|Override of the description. Redondant in my opinion with the functions above|
|Optional|Is the task optional?|
|Hidden|Is the task displayed in the Quest journal ?|
|Tick Interval|The interval for the tick function. (0=no tick, 0.5 = every 0.5s, etc...|
|Marker Settings|The settings for the navigation marker of the task|

Any Public variable you create in the task can be modifed in the Quest Graph under its category :
<img width="377" height="290" alt="image" src="https://github.com/user-attachments/assets/a4419daa-5100-411f-be3d-76d3a9bea61d" />
<img width="425" height="188" alt="image" src="https://github.com/user-attachments/assets/d71615ef-82e9-4cef-acfb-8a4778d48c33" />


You need to handle the task logic in the Task BP, and run the "Complete Task" node when the task is considered as complete :  
<img width="211" height="127" alt="image" src="https://github.com/user-attachments/assets/953568be-6356-41e6-a9dc-0b64b6e9bc6e" />


### Conditions
Even if conditions also appear in the quest graph, note that using conditions in quest graph is currently unsupported  

# Dialogues

All Dialogues you create should inherit from your own DBP_DialogueMaster.  

## Dialogue Graph


## Events


# Inventory

## Narrative Item

## Item Collection

# Navigation

## Navigation Markers Component
**_Narrative Base class :_ UNavigationMarkerComponent**   
Navigation markers are a component added on actors which will add a marker visible on your minimap, world map and compass.  
You do not need to subclass them.
The component can be manually added to an actor, au automatically added by various Narrative Pro systems, such as [Tasks](#tasks).  

> Important : Navigation markers do not support World partition. This means that if a Navigation marker is on an Actor which isn't loaded, or if you try to add one via a Task on an Actor which isn't loaded, it won't work as expected. If you need to add a Navigation Marker to an Actor in a Task, I suggest to give the task the responsability to spawn the Actor at Runtime and add the marker to it. Actors spawned at Runtime are excluded from World Partition. You can also make the actor not spatially loaded to have it always loaded.



## Point of Interest
**_Narrative Base class :_ APOIActor** 

I suggest to subclass APOIActor into your own BP, and then use this newly created BP to place POI.

A POI is a named area of your map. It could be a dungeon entrance, a city, etc... Think Skyrim and all the discoverable locations : these are POI.

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
Then, once in game, when you enter the POI Sphere, the location will be discovered :
<img width="568" height="189" alt="image" src="https://github.com/user-attachments/assets/25bc8976-ddd9-4078-9108-2f87658f8cd3" />


## Minimap

## Utility Navigator Widget

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
|Default Owned Tags|The list of the tag the player starts with. |
|Default Factions|The factions the player is a member of|
|Trigger Sets|Unknown|
|Attack Priority|This influence the chance for an enemy in combat to pick the player as its target. The higher it is, the higher is the chance|
|Ability Configuration|[Ability COnfiguration](#ability-configuration)|

## Ability Configuration
## Character Appearance
ONGOING
| Variable Name | Description |
| ---- |----------|
|Form Tag| Unknown|
|Character Visual Class|Unknown|
|Base Mesh|Unknown|
|Hide Base Mesh|Unknown|
|Base Mesh Anim BP|Unknown|
|Unarmed Anim Layer|Unknown|
|Meshes|Unknown|
|Grooms|Unknown|
|Morphs|Unknown|
|Scalar Values|Unknown|
|Vector Values|Unknown|


# Interaction
## Interactable Component
## Interactible Component

# Combat
## GAS
the Gameplay Ability System isn't a feature of Narrative : it's a Unreal Engine feature. It's a very powerful framework, multiplayer ready, but it requires C++ for its setup and to be able to use some of the functionnalities. If you do not know C++, or if you want to be able to do everything BP only, I suggest to get the cheap plugin [Gameplay Blueprint Attributes](https://www.fab.com/listings/a7de98c4-51f5-4c4a-8dbc-52aff9d14e40).  
Narrative do few additions to GAS, and you will find them detailed here.  
For Unreal GAS documentation, please check [Tranek GAS Documentation](https://github.com/tranek/GASDocumentation) instead.


# Narrative Pro Changelog
Because the changelog available on Narrative Pro official documentation only contains the changelog of the current version, I store here the history of the changelogs.

<details>
  <summary>2.0.1</summary>
  
  **Features**  
-Added conditions to dialogue node texts  
-Added FPS mode  
-Added FreeMovement, StopMovement, Speakers, NonUniqueNPCs properties to DialoguePlayParams  
-Added more activities  
-Added motion matching with GASP  
-Added new demo map  
-Added new inventory function to add item from a loot table  
-Added new NarrativeCharacterVisual to the Characters to easily get each visual aspects (meshes)  
-Added NPC Spawners demo map  
-Added setup config ini files to Resources folder  
-Added the new Gameplay Camera  
-Added weapon attachments  
-Moved GameplayHUD to variable inside PlayerController  
-Optimised NarrativePlayer meshes. It will now spawn in the extra components instead.  
-Re-organised C++ code for cleaner implementation  
-Removed Goals replaced with GoalItems  
-Removed Settlements  
-Replaced NPC Sub System with CharacterSubSystem   
-Updated combat  
-Updated Navigator utility to feature stopping, generation POI's and Deleting map tiles  

  **Bugfixes/Misc**  
-Fixed bug with build errors  
-Fixed bug with combat T posing  
-Removed build breaking data table  
-Updated PlayCutscene function to fix but with input not resetting during dialogue  
-Renamed Gameplay to GameplayHUD on player controller  
-Renamed NarrativeComponent to TalesComponent  
  
</details>



