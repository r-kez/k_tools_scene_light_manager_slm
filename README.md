# K-Tools: Scene Light Manager - Feature Guide

Welcome to the Scene Light Manager (SLM)! This addon is a complete toolkit designed to streamline your entire lighting workflow, from initial organization to final render-pass setup. It provides a "Set-Based" or "Group-Based" workflow that makes managing complex scenes simple and visual.

## [Get on Gumroad](https://kezives.gumroad.com/l/xiqpc)
#### Consider supporting if the add-on is useful for you :)

Here is a breakdown of the features you have built so far.

---

## 🚀 Core Workflow: The 5 Management Tabs

Your workflow is organized into five distinct modes:

* **Collections:** Your main workspace. This is where you organize your lights and assets into logical groups (like "Key_Lights", "Fill_Lights", "Assets_Bouncers"). It manages scene hierarchy and properties.
* **Light Groups (LG):** Control your render passes. This tab is a powerful UI for Blender's native `Light Group` system. You can create groups, assign custom icons, and add/remove lights and mesh emitters to control your passes in the compositor.
* **Light Linking (LL):** Take control of which objects receive light. This tab manages Blender's `Light Linking` (`receiver_collection`). You can create "Sets" (e.g., "Characters_Only") and define which lights should only affect the objects in that set.
* **Shadow Linking (SL):** Control which objects cast shadows. This tab manages Blender's `Shadow Linking` (`blocker_collection`). You can define "Sets" of objects (e.g., "Windows_Blockers") and assign lights to use them as shadow blockers.
* **Quick Actions:** Your speed-dial. This tab provides a central hub to access all "Quick Assign" menus (for Collections, LG, LL, and SL), allowing you to manage any selected object without leaving the tab.

---

## ✨ Key Features & Systems

### 1. Collection Management

* **Smart Organization:** Create (`+`) and **Delete (`-`)** addon-managed collections (e.g., `LIGHTS.001`). **Warning: This deletes the collection and its contents.**
* **Pin User Collections:** **Pin (`📌`)** any existing collection from your scene (e.g., "My_Imported_Assets") to the SLM interface. Removing a pinned collection (`-`) only **removes it from the UI**, it *does not delete* your original collection.
* **Dynamic UI:**
    * **Live Count:** Instantly see the number of SLM-managed items `(n)` inside each collection.
    * **Outliner Sync:** The list item icon automatically syncs with the collection's **Outliner Color Tag**.
    * **Sorting:** `Move Up` (`🔼`) and `Move Down` (`🔽`) operators to re-order your lists.
* **Discovery:** An optional setting in the *Preferences* (`Discover Collections on Refresh`) allows the `Refresh` button to scan your entire scene for collections matching search terms (e.g., "luz", "licht"), not just the ones inside your main "LIGHTS" collection.

### 2. Light & Asset Management (In-Depth)

* **Unified List:** View all your lights, mesh lights, targets, bouncers, and blockers in a single hierarchical list.
* **Targeting System:**
    * **Group Target:** Assign one "Target" (Empty) to an entire collection. All lights set to "Auto" mode will automatically follow it.
    * **Individual Target:** Create a dedicated target for any single light, which overrides the Group Target.
    * **Auto-Hierarchy:** The UI automatically indents lights to show you exactly what is tracking what (`Group Target` > `Light`, `Individual Target` > `Light`).
* **Asset Spawning:**
    * A single `Add` (`+`) menu allows you to add standard lights (Point, Sun, etc.) or pre-built assets.
    * **Add Bouncer/Blocker:** Spawns a Plane with the correct material and a pre-assigned "Individual Target" for easy aiming.
    * **Add Mesh Light:** Spawns a "Softbox" plane with a pre-built emissive material and a pre-assigned target.
* **Auto-Tagging (Smart Meshes):** When you assign any `MESH` (like a custom plane) to a Light Group or Light Link, the addon will:
    1.  Automatically add the `mesh_light` tag to its name (so the Isolate system can see it).
    2.  Automatically move it to the "Mesh_Lights" collection (if it's currently "stray" in the root of the scene).

### 3. The "Isolate" (Solo) System

* **One-Click Solo:** A dedicated `Isolate` button (using your custom `STICKY_UVS` icons) is available on **every** major list item:
    * Collections (List 1)
    * Light Groups (List 1)
    * Light Link Sets (List 1)
    * Shadow Link Sets (List 1)
    * Individual Lights/Objects (Lists 2 & 3)
* **Context-Aware:** It "solos" exactly what you clicked on: a single object, or all lights *and* objects belonging to a Set.
* **Mute World:** An optional setting (`Isolate Mutes World`) automatically disconnects your World/HDRI shader for a true "black box" lighting environment.

### 4. Custom Icon "Tag" System

* **Visual Workflow:** Assign unique, color-coded icons for every **Light Group (LG)**, **Light Link (LL)**, and **Shadow Link (SL)** set you create.
* **Custom Icon Sets:** Uses three distinct icon shapes Circles for Light Groups, Diamonds for Light Linking and Rounded Square for Shadow Linking. you can also hange the Collection Tag Color directly from UI.
* **Global Info:** The main "Collections" light list automatically checks all other systems and displays the tags for that light, giving you an at-a-glance summary:
    * `Light Name [LG Icon] [LL Icon] [SL Icon]`

### 5. Universal "Quick Popup" (The Hotkey)

This is the central hub for your entire workflow, designed to be assigned to a hotkey (like `Q`).

* **Hotkey Manager:** The addon hotkey can be set/changed directly from the *Preferences* panel.
* **Context-Aware UI:** The popup is "smart" and changes based on your selection:
    * **1 Emitter Selected:** Shows basic controls (`Energy`, `Color`) and the "Assign" menus.
    * **2+ Emitters Selected:** Hides basic controls but keeps "Batch" and "Assign" menus.
    * **1 Receiver Selected (non-emitter mesh):** Hides emitter controls and *only* shows the "Receiver" (Affected Object) menus.
* **Popup Features:**
    * **Batch Controls:**
        * **Energy (Add):** A `[+]` / `[-]` style operator to add or subtract energy from all selected items. Includes a safety check to prevent values from going to zero.
        * **Exposure (Set):** A slider to `override` (set) the `exposure` value for all selected lights in real-time.
    * **Quick Target/Parent:**
        * An **eyedropper** to assign a `Track To` target (with Keep Transform) to all selected items.
        * An **eyedropper** to assign a `Parent` (with Keep Transform) to all selected items.
        * These fields auto-populate with the active object's current target/parent, and clearing them (`X`) removes the constraint/parent.
    * **All Quick Assign Menus:**
        * **Collections:** "Move to Collection..."
        * **Light Group (LG):** "Assign to Group..." (for Emitters)
        * **Light Linking (LL):** "Assign to Set..." (for Emitters) AND "Quick Assign Object..." (for Receivers)
        * **Shadow Linking (SL):** "Assign to Set..." (for Emitters) AND "Quick Assign Object..." (for Receivers)

### 6. Linking Menus & Operators

* **Full "Set-Based" Control:** All LL and SL operators are "Set-centric", allowing you to manage groups of lights/objects instead of one light at a time.
* **Dynamic Menus:** All "Quick Assign" menus are dynamic, showing your custom icons and displaying the *current* set/group of the active object.
* **Smart Creation:** All "Quick Assign" menus include "New Group from Selected" operators to create a new Set and assign the selected items in one click.
* **Native UI Integration (List 3):** The "Receiver/Blocker" object lists use Blender's native `template_light_linking_collection`, which supports **drag-and-drop** from the Outliner and native **Include/Exclude** toggles, giving you the best of both worlds.
* **Custom Asset Scanner:** A tool in the *Preferences* to scan your Asset Browser libraries for custom node groups, allowing you to override the addon's default "Softbox" asset.

---

# K-Tools: Scene Light Manager - Add-on Preferences

This guide explains the settings available in the SLM Add-on Preferences (`Edit > Preferences > Add-ons > Scene Light Manager`).

## Naming and Search

This section controls how the addon finds and names your core lighting collections.

* **Main Collection Name:**
    * This is the name of the "Master" collection (e.g., "LIGHTS") that the addon uses as its root.
    * The `Refresh` button in the "Collections" tab will automatically find this collection and list all of its children.
* **Discover Collections on Refresh:**
    * **OFF (Default):** The addon only lists collections that are children of your "Main Collection" or collections you "Pin" manually. This is fast.
    * **ON (Slower):** When checked, the `Refresh` button will *also* scan your entire scene (`bpy.data.collections`) for any collection that matches the terms below.
* **Collection Terms:**
    * (Only appears if "Discover Collections" is ON).
    * A comma-separated list of names (e.g., "light,lights,luz,lumiere,licht,조명,ライト,灯光") to help the addon "discover" other light collections in your scene.
* **Enable Mesh Light Listing:**
    * Tells the addon to treat `MESH` objects as potential lights. This is **ON by default** and uses name-based detection, which is very fast.
* **Mesh Light Terms:**
    * (Only appears if "Enable Mesh Light Listing" is ON).
    * A comma-separated list of tags (e.g., "mesh_light,emissive,meshlight") that the addon uses to identify a mesh as a light in the Collections and other modes.
    * **Tip:** When you add a plain mesh to a Light Group or Light Link set, the addon will automatically rename it (e.g., `MyPlane` -> `MyPlane_mesh_light`) using the *first* term from this list.

---

## Performance

This section controls how "live" the addon feels.

* **Enable Auto-Refresh:**
    * **ON (Default):** The addon automatically monitors your scene. When you add, delete, or move a relevant object, the UI lists will update automatically.
    * **OFF:** The UI will not update unless you manually press the `Refresh` button in a panel.
* **Sync List to 3D View:**
    * **ON (Default):** Clicking an item in an SLM list (e.g., a light in the "Collections" tab) will also select and activate it in the 3D Viewport.
    * **OFF:** Clicking in the list only updates the UI, it does not change your 3D View selection.

---

## Light List Display

This section controls what information is shown in the various "Light Lists" (in the Collections, LG, LL, and SL tabs).

* **Show Hide Select:** Toggles the "Selectable" (mouse cursor) icon in the lists.
* **Show Hide Viewport:** Toggles the "Viewport Visibility" (monitor) icon in the lists.
* **Show Hide Render:** Toggles the "Render Visibility" (camera) icon in the lists.

---

## Keyboard Shortcuts

This section allows you to manage the hotkey for the **SLM Quick Popup Menu**.

* The addon attempts to register `Y` as the default hotkey in the 3D View.
* You can use this panel to change the key (e.g., to `Shift+Alt+L`) or remove it entirely.
* If the shortcut is removed, a button "Add Shortcut" will appear to let you restore it.

---

## Custom Softbox Node Group

This section allows you to **override** the addon's default assets (like the `SLM-SOFT_BOX` node group used by the "Assign Softbox" operator) with your own custom assets from your Asset Browser.

* **Use Custom Softbox:**
    * **OFF (Default):** The addon will import its built-in `SLM-SOFT_BOX` from its own asset file.
    * **ON:** The addon will *ignore* its built-in asset and will instead try to load the asset you specify in the fields below.
* **Current Custom Node:**
    * **File Path:** The absolute path to your `.blend` file (e.g., `C:\MyAssets\Blender\NodeGroups.blend`).
    * **Node Group Name:** The exact name of the node group *inside* that `.blend` file (e.g., "My_Awesome_Softbox").
* **Asset Library Finder:**
    * This is a helper tool to find and fill in the fields above automatically.
    * **Scan Asset Libraries:** Click this to make the addon scan all of your registered Asset Browser libraries. ***It may freeze Blender's UI while scanning depending how big is your Assets repository***.
    * **Search:** A filter to search the results of the scan.
    * **Temp List:** A list showing all the Node Groups found in your libraries. *Use the 'Filtering options' to find your Node Group asset faster (Bottom Left arrow icon)*.
    * **Set as Custom Softbox:** Click an item in the list, then click this button to "capture" its File Path and Name into the "Current Custom Node" fields.
