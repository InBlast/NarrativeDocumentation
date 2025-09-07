# Narrative Pro Documentation by InBlast
This is my try to provide a comprehensive documentation for Narrative Pro, based on experience and reading sessions of the C++ code.  
It is **NOT** an official documentation ([Link to official documentation](https://docs.narrativetools.io/)).  
This documentation is not exhaustive and might contain mistakes, please be aware of that. I encourage you to analyse as much as you can the demo provided in the plugin files, and to test by yourself.  
This documentation has been written with usage in blueprint in mind, for game designers : it doesn't details how the C++ part works, only what a game designer needs to know to work in BP with Narrative Pro.  

Use the table of content to navigate between the different sections :  
<img src="https://github.com/user-attachments/assets/f13273f3-c958-4c2a-b901-f41e726c6d46" width="200"> 

I highly advise to not directly use any class provided by Narrative. Subclass it first in BP (your BP_MasterClassName), then subclass this created master class to create the multiple versions of what you will use in your game. This way you can easily update Narrative Pro. If you need to do modifications in the plugin C++ code, please keep in mind that you will need to remake them in case of Narrative update.  

I use screenshots from the Narrative Pro open world demo as much as I can, so you can also check the same files by yourself.   

If you find any mistake, or if you would like to add something, please contact me on the Reubs Discord server.

## Video Tutorials
[Video tutorials by Primal](https://www.youtube.com/@wonderscapecreations/playlists)  
[Official Video tutorial](https://www.youtube.com/@narrativetools/playlists) 

# Quests & Dialogues Generalities

It's recommended to make your own Master Dialogue and Master Quest BP. You can follow these links for that :  
[Master Dialogue](https://docs.narrativetools.io/pro/dialogue/master-dialogue)  
[Master Quest](https://docs.narrativetools.io/pro/quests/master-quest)  
This way you can make modifications to all your Dialogues/Quests by editing your master BP. 

## Conditions
**_Narrative Base class :_ UNarrativeCondition**  
Even if conditions also appear in the quest graph, note that using conditions in quest graph is currently unsupported. You can only use them in Dialogues for the moment.  

| Function Name | Description |
| ---- |----------|
|Check Condition|Check whether this condition is true or false|
|Get Graph Display Text|Define the text that will show up on a node if this condition is added to it|

## Events
**_Narrative Base class :_ UNarrativeEvent**    

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

| Variable Name |Variable Type| Description |
| ---- |---|----------|
|State Node Type|EStateNodeType|Type of the State Node. Can be **Regular** (Quest in progress), **Success** (Quest is finished and successful, Quest end node) or **Failure** (Quest is finished but failed, Quest end node) |
|ID|FName|Unique Node ID, it's the current state of the quest. Used for saving purposes, but it can also be used in condition checks|
|Description|FText|The description of the quest as it will appear in the player Quest Journal|
|On Entered Func Name|FName|The Event in the EventGraph which will be called when this state Starts and when it ends (= When the next state will start)|
|Conditions|TArray\<UNarrativeCondition\>|Please ignore, currently only works in Dialogues|
|Events|TArray\<UNarrativeEvent\>|[Events](#events) A list of events to run when the State node starts/Ends or both|


### Tasks
**_Narrative Base class :_ UNarrativeTask**  
Task are used as a condition for a quest to go to the next State.
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

| Variable Name |Variable Type| Description |
| ---- |---|----------|
|Required Quantity|Int32|The amount of time the task needs to be completed|
|Description Override|FText|Override of the description. Redondant in my opinion with the functions above|
|Optional|Bool|Is the task optional?|
|Hidden|Bool|Is the task displayed in the Quest journal ?|
|Tick Interval|Float|The interval for the tick function. (0=no tick, 0.5 = every 0.5s, etc...|
|Marker Settings|FTaskNavigationMarker|The settings for the navigation marker of the task|

Any Public variable you create in the task can be modifed in the Quest Graph under its category :
<img width="377" height="290" alt="image" src="https://github.com/user-attachments/assets/a4419daa-5100-411f-be3d-76d3a9bea61d" />
<img width="425" height="188" alt="image" src="https://github.com/user-attachments/assets/d71615ef-82e9-4cef-acfb-8a4778d48c33" />


You need to handle the task logic in the Task BP, and using the following nodes to influence the task progress :  
<img width="642" height="172" alt="image" src="https://github.com/user-attachments/assets/a3cec8e3-2cc3-4337-bbe4-72053aaf1ed8" />



# Dialogues

All Dialogues you create should inherit from your own DBP_DialogueMaster.  

## Dialogue Graph  


## Tagged Dialogue Set  
**_Narrative Base class :_ UTaggedDialogueSet** (DataAsset)  

This asset is a list of FTaggedDialogue :
| Variable Name |Variable Type| Description |
| ---- |---|----------|
|Tag|FGameplayTag|The tag that will kick off this dialogue|
|Dialogue|[TSoftClassPtr\<class UDialogue\>](#dialogues)|The Dialogue to play|
|Cooldown|float|The amount of time we should cooldown before playing this dialogue again|
|Max Distance|float|Tagged dialogue wont play unless we're within this range from it|
|Required Tags|FGameplayTagContainer|Tags that if owned by the NPC, will prevent this dialogue beginning. For example, we wouldn't want to greet a player if we were fighting someone|
|Blocked Tags|FGameplayTagContainer|Tags that if owned by the NPC, will prevent this dialogue beginning. For example, we wouldn't want to greet a player if we were fighting someone|

This is used to trigger a dialogue when a specific tag is added to the NPC. NPCs in the demo have some tags already working with that, not sure of how it works yet.
# Inventory

## Narrative Item

## Item Collection

## Loot Table Roll

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

| Variable Name |Variable Type| Description |
| ---- |---|----------|
|POITag|FGameplayTag|A unique Tag for the POI. Create one for every POI you want in your world|
|Create Map Marker|Bool|Should this POI have a world map marker visible ? (on minimap, worldmap, and compass) |
|Supports Fast Travel|Boool|Can this POI be used to fast travel to ?|
|POI Display Name|FText|The display name in game|
|POIIcon|UTexture2D|The displayed icon (on minimap, worldmap, and compass) |
|Linked POIs|TArray\<TSoftObjectPtr\<APOIActor\>\>|Unknown|

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
**_Narrative Base class :_ UNPCDefinition** (Child of **UCharacterDefinition**)  

| Variable Name |Variable Type| Description |
| ---- |---|----------|
|NPCID|FName|ID Used for Dialogues|
|NPCName|FText|The name of this NPC. Will be used for the interaction and navigation markers.|
|Min Level|int32|The NPCs level will not be lower than this value|
|Max Level|int32|The NPCs level will not be higher than this value|
|Allow Multiple Instances|Bool|Is this NPC unique, or can we spawn multiple of them?|
|Unique NPCGUID|FGuid|If this NPC is unique, we'll use this as the NPCs save system GUID|
|NPCClass Path|TSoftClassPtr\<ANarrativeNPCCharacter\>|Base class of the NPC|
|Dialogue|[TSoftClassPtr\<class UDialogue\>](#dialogues)|The dialogue that should play when we interact with this NPC|
|Tagged Dialogue Set|[TSoftObjectPtr\<class UTaggedDialogueSet\>](#tagged-dialogue-set)|The NPCs tagged dialogues - usually free movement dialopgues that can be kicked off via a tag "TaggedDialogue.Taunt, TaggedDialogue.Greet, etc.|
|Is Vendor|Bool|Whether this NPCs inventory should be a vendor inventory - that is to say they are a shop vendor|
|Trading Currency|int32|Default currency this character should have in their inventory|
|Trading Item Loadout|[TArray\<FLootTableRoll\>](#loot-table-roll)|The items we should grant the character by default.|
|Default Currency|Int32|The default currrency your NPC has|
|Default Item Loadout|[TArray\<FLootTableRoll\>](#loot-table-roll)|The default Items this NPC start with. Can be [Narrative Item](#narrrative-item), [Item Collection](#item-collection) and/or a roll table|
|Activity Configuration|[TSoftObjectPtr\<class UNPCActivityConfiguration\>](#npc-activity-configuration)|The NPCs activity config|
|Default Appearance|UCharacterAppearanceBase| [Character Appearance](#character-appearance) The default look of your NPC|
|Default Owned Tags|FGameplayTagContainer|The list of the tag the NPC starts with. |
|Default Factions|FGameplayTagContainer|The factions the NPC is a member of|
|Trigger Sets|TArray\<UTriggerSet\>|Unknown|
|Attack Priority|Float|This influence the chance for an enemy in combat to pick the NPC as its target. The higher it is, the higher is the chance|
|Ability Configuration|[Ability Configuration](#ability-configuration)|List of abilities available to the NPC|

## NPC AI

<img width="490" height="394" alt="image" src="https://github.com/user-attachments/assets/c2fefac3-b911-4cd2-a71a-b01cece341d5" />

1. Every "Rescore Interval" (NPCActivityConfiguration), the NPCAC will, for every Default NPCActivity, request a score from the NPCGoalItem (Default Score, or GetGoalScore if overwritten).  
2. The NPCActivity with the highest score meeting all tag requirements will be chosen as active activity.
3. The chosen activity will replace the BT/BB of the NPC, and run until changed  


### NPC Activity Configuration
**_Narrative Base class :_ UNPCActivityConfiguration** (DataAsset)  

The NPC configuration is the list of the activities an NPC can perform.

| Variable Name |Variable Type| Description |
| ---- |---|----------|
|Rescore interval|float|How often we want to re-score our goals, which may change our current activity|
|DefaultActivities|TArray\<TSubclassOf\<class UNPCActivity\>\>|The activities to grant the NPC|
|GoalGenerators|TArray\<TSubclassOf\<class UNPCGoalGenerator\>\>|The goal generators the NPC can use to generate goals - you can add your own goals manually via AC->AddGoal(), goals do not have to be added via generators|

### NPC Activity
**_Narrative Base class :_ UNPCActivity**  

The NPC Activity describe an activity that an NPC can do (Idling, Running away, following you, going to pickup something, etc.... It contains the logic which doesn't belong in the BT.

| Variable Name |Variable Type| Description |
| ---- |---|----------|
|Behavior Tree|TObjectPtr\<class UBehaviorTree\>|The behaviour tree the NPC needs to run when performing this activity|
|Supported Goal Type|TSubclassOf<class UNPCGoalItem>|The goal class this activity supports, if it supports one. You can leave this empty if your activity doesn't need a goal, eg Idle, etc|
|Is Interruptable|bool|Whether we're allowed to interrupt this activity or not|
|Save Activity|bool|Whether this activity should be saved to disk or not|
|Activity Name|FText|The name of the this activity|
|Owned Tags|FGameplayTagContainer|The tags we'll grant the NPC/Settlement when this ability starts |
|Block Tags|FGameplayTagContainer|We'll block the activity from running if the has any of these tags |
|Require Tags|FGameplayTagContainer|We'll require these tags to be on the owner before we run the activity |

### NPC Goal Item
**_Narrative Base class :_ UNPCGoalItem**  

The GoalItem contains all the data needed for a specific activity to run and will pass the data to this activity.

| Function Name | Description |
| ---- |----------|
|Get Debug String| Event run when the task begins|
|Get Goal Key| Returning a valid object will act as a key - you can access the goal later via this object, and we'll prevent goals with the same key from being added in future|
|Get Goal Score|Return a score for the goal - The NPC will score each potential activity and pick the one with the highest score|
|Initialize|Called when the goal is added, or loaded back in from disk|
|On Removed|Called when the goal is removed|
|Prepare For Save|Prepare the goal for a save - this might for example mean storing an actors GUID so we can find it later when we load|
|Should CleanUp|Return whether the goal has become invalid and should be removed, ie if an AttackGoals target has died|

| Variable Name |Variable Type| Description |
| ---- |---|----------|
|Remove on Succeeded|bool|If true, this goal will automatically be removed when its owning activity completes the goal|
|Default Score|float|The default score this goal will be given if its activity doesn't override the ScoreGoal function |
|Save Goal|bool|Whether we're allowed to interrupt this activity or not|
|Goal Lifetime|float|Goal Expiry time. If less than zero goal will never expire and needs to be removed either by scoring < 0 or manually removed via RemoveGoal()|
|Owned Tags|FGameplayTagContainer|The tags we'll grant the NPC when an activity acts on this goal. We'll remove when the goal ends|
|Block Tags|FGameplayTagContainer|We'll force a low score if you have these tags, meaning the goal won't be acted on|
|Require Tags|FGameplayTagContainer|We'll require these tags to be on the owner to act on this goal|

## Player
### Player Character
### Player Controller
### Player State
### Player Definition
**_Narrative Base class :_ UPlayerDefinition** (Child of **UCharacterDefinition**)  

| Variable Name |Variable Type| Description |
| ---- |---|----------|
|Default Appearance|UCharacterAppearanceBase| [Character Appearance](#character-appearance) The default look of your Character|
|Default Currency|Int32|The default currrency your player has|
|Default Item Loadout|TArray\<FLootTableRoll\>|The default Items your player start with. Can be [Narrative Item](#narrrative-item), [Item Collection](#item-collection) and/or a roll table|
|Default Owned Tags|FGameplayTagContainer|The list of the tag the player starts with. |
|Default Factions|FGameplayTagContainer|The factions the player is a member of|
|Trigger Sets|TArray\<UTriggerSet\>|Unknown|
|Attack Priority|Float|This influence the chance for an enemy in combat to pick the player as its target. The higher it is, the higher is the chance|
|Ability Configuration|UAbilityConfiguration|[Ability Configuration](#ability-configuration)|

## Ability Configuration
## Character Appearance
**_Narrative Base class :_ UCharacterAppearance** (Child of **UCharacterAppearanceBase**)  

Variables from the FCharacterCreatorAttributeSet :
| Variable Name |Variable Type| Description |
| ---- |---|----------|
|Form Tag|FGameplayTag| Unknown|
|Character Visual Class|TSubclassOf\<ANarrativeCharacterVisual\>|Unknown|
|Base Mesh|USkeletalMesh|Unknown|
|Hide Base Mesh|Bool|Unknown|
|Base Mesh Anim BP|TSubclassOf\<UAnimInstance\>|Unknown|
|Unarmed Anim Layer|TSubclassOf\<UAnimInstance\>|Unknown|
|Meshes|TMap\<FGameplayTag, FCharacterCreatorAttribute_Mesh\>|Unknown|
|Grooms|TMap\<FGameplayTag, FCharacterCreatorAttribute_Groom\>|Unknown|
|Morphs|TArray\<FCharacterCreatorAttribute_Morph\>|Unknown|
|Scalar Values|TMap\<FGameplayTag, float\>|Unknown|
|Vector Values|TMap\<FGameplayTag, FLinearColor\>|Unknown|

## Character Appearance Base
Base for Appearance class

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



