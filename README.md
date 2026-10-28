# ChempSDK
SDK for Custom Maps and Custom Spawnables in Chemp Physics.
Import this into a Unity 6 project.

# Creating a map
## Step 1: Creating your scene
- Firstly, go to the !Maps folder.
- Second, duplicate the Example Map folder, and rename the duplicate as you wish.
- Then, go into your new folder, and rename the scene as you wish.
- Next, go into the scene.
- Do NOT delete or move the "hut" GameObject! This is for you to use as an anchor for your map.
- Set up your map as you wish
- If you like, you can add a LuaBehaviour script to any object in the scene, and write a script in Lua. To do this, follow the steps below.
    - Create a txt file somewhere, and drag it into your map's folder.
    - Double-click it to edit it.
    - Begin writing your lua script. A decent amount of Lua knowledge is recommended. Documentation is shown below.
    - The game will try to automatically run your LuaBehaviour script. You can have multiple of these.

## Step 2: Building your AssetBundle(s)
- Go back to the !Maps folder, select your map folder and go to ChempSDK - Bundle Builder
- Click "Build for Android + Windows"
- Output .zip file will be in !Builds. This is safe to upload directly to mod.io.

## Step 3: Uploading to mod.io (Basically, getting your map in-game)
- Go to https://mod.io/
- Go to browse games
- Search for "Chemp Physics"
- Click "Add Mod" in the top right
- Follow the steps on the mod.io site

# Creating a Custom Spawnable
## Step 1: Creating your prefab
- First, go to the !Spawnables folder and create a new folder. Name it as you wish.
- Secondly, Create a new GameObject in your scene.
- Then, set it up as you wish.
- To make it have physics, add a Rigidbody component, and colliders.
    - a Mesh Collider must have "Convex" ON to work properly with physics.
    - Rigidbody Interpolation is recommended to be set to Interpolate, and Collision Detection to Continous or Continous Dynamic.
    - A Rigidbody's Mass is it's weight.
- Add a ChempComponentMods component and set it's type to Chemp Entity.
- For every physics body / Rigidbody in your spawnable, add a ChempComponentMods component to it, set it's type to Chemp Rigidbody Entity, and assign Entity as the ChempComponentMods with it's type as Chemp Entity on the root of your spawnable.
- To make it grabbable, go to each collider you want to be able to be grabbed, and add a ChempComponentMods component.
- Change the component type to Grip, and assign Colliders To Phase with your object's colliders.
- If you like, you can add a LuaBehaviour script, and write a script in Lua. To do this, follow the steps below.
    - Create a txt file somewhere, and drag it into your spawnable's folder.
    - Double-click it to edit it.
    - Begin writing your lua script. A decent amount of Lua knowledge is recommended. Documentation is shown below.
    - The game will try to automatically run your LuaBehaviour script. You can have multiple of these.
- Afterwards, drag it into your mod folder.
- Finally, right click in the folder, hover over "Create", go down to "ChempSDK" and select ModInfo.
    - Assign Mod Name to whatever your mod's name will be
    - Click the + on the Spawnables dropdown, and assign the Prefab to the object shown in the mod folder. Make sure you don't accidentally assign the 3D model!
    - Assign UID to something completely unique. This is used to identify your spawnable.

## Step 2: Building your mod to see  it in-game
- Go back to the !Maps folder, select your map folder and go to ChempSDK - Bundle Builder
- Click "Build for Android + Windows"
- Output .zip file will be in !Builds. This is safe to upload directly to mod.io.

## Step 3: Uploading to mod.io (Basically, getting your map in-game)
- Go to https://mod.io/
- Go to browse games
- Search for "Chemp Physics"
- Click "Add Mod" in the top right
- Follow the steps on the mod.io site

# Lua Documentation
Below lies the Lua documentation.

# Non-Static Lua Types
## LuaTransform
Accessible via `transform` on any Lua script.
### Variables:

```transform.Position```
Returns the position of the transform object. Useful for knowing where an object is or moving an object.

```transform.EulerAngles```
Returns the position of the transform object. Useful for knowing where an object is or moving an object.

```transform.Forward```
Returns a normalized vector representing the blue axis of the transform in world space.

```transform.Right```
Returns a normalized vector representing the red axis of the transform in world space.

```transform.Up```
Returns a normalized vector representing the green axis of the transform in world space.

```transform.LocalScale```
The scale of the transform relative to the GameObjects parent.

```transform.Parent```
The parent of the transform.

```transform.GameObject```
The game object this transform is attached to.

### Methods:

```transform:TransformPoint(LuaVector3)```
Transforms position from local space to world space.

```transform:InverseTransformPoint(LuaVector3)```
Transforms position from world space to local space.

## LuaGameObject
Accessible via `gameObject` on any Lua script.
### Variables:

```gameObject.Transform```
The Transform attached to the GameObject.

```gameObject.Name```
The name of the object.

```gameObject.Tag```
The tag assigned to the GameObject.

```gameObject.Active```
The local active state of the GameObject. True if active, false if inactive.

### Methods:

```gameObject:FindChild("child name")```
Finds a child by name and returns it.

## LuaCollider
Accessible via `collider` on any Lua script. ```nil``` if none is found.
### Variables:

```collider.AttachedRigidbody```
The rigidbody the collider is attached to.

## LuaCollision
Given by `OnCollisionEnter`, `OnCollisionExit`, and `OnCollisionStay`
### Variables:

```collision.Body```
The Rigidbody of the collider that your object collides with

```collision.Collider```
The collider that your object collides with

```collision.GameObject```
The GameObject whose collider you are colliding with.

```collision.RelativeVelocity```
The relative linear velocity of the two colliding objects

```collision.Rigidbody```
The Rigidbody we hit. ```nil``` if the object we hit is a collider with no rigidbody attached.

## LuaRigidbody
Accessible via `rigidbody` on any Lua script. ```nil``` if none is found.
### Variables:

```rigidbody.LinearVelocity```
The linear velocity vector of the rigidbody. It represents the rate of change of Rigidbody position.

```rigidbody.AngularVelocity```
The angular velocity vector of the rigidbody measured in radians per second.

### Methods:

```rigidbody:AddForce(force, forceMode)```
Adds a force to the Rigidbody. forceMode is optional. Options are "Force", "Acceleration", "Impulse", and "VelocityChange". More info on those [here](https://docs.unity.com/en-us/engine/6000.6/script-reference/unityengine/forcemode).

```rigidbody:AddTorque(torque, forceMode)```
Adds a torque to the Rigidbody. forceMode is optional. Options are "Force", "Acceleration", "Impulse", and "VelocityChange". More info on those [here](https://docs.unity.com/en-us/engine/6000.6/script-reference/unityengine/forcemode).

## LuaVector3
Representation of 3D vectors and points.
Create one with ```lv3 = LuaVector3(1,1,1)```, replacing ```x```, ```y```, ```z``` with your own numbers.

### Fields:

```LuaVector3.X```
X component of the vector.

```LuaVector3.Y```
X component of the vector.

```LuaVector3.Z```
X component of the vector.

```LuaVector3.Magnitude```
Returns the length of this vector.

# Static Lua Types
## LuaPlayer
Has static methods related to the Player.

### Methods:

```LuaPlayer.GetPlayerRigidbody()```
Gets the main / body Rigidbody of the Player as a LuaRigidbody.

```LuaPlayer.GetPlayerHand(leftHand)```
Gets the rigidbody of a player hand, which hand is determined by ```leftHand```. Pass ```true``` if you want the left hand, ```false``` for the right.

# Built-In methods for Lua
These methods are not required to exist within your code, but you can use them.

```Update()```
Runs every frame.

```FixedUpdate()```
Runs every physics frame.

```OnCollisionEnter(LuaCollision)```
Runs when your object collides with another.

```OnCollisionStay(LuaCollision)```
Runs every physics frame when your object is colliding with another.

```OnCollisionExit(LuaCollision)```
Runs when your object stops colliding with another.

```OnTriggerEnter(LuaCollider)```
Runs when a Collider with the Collider.isTrigger property overlaps another Collider.

```OnTriggerStay(LuaCollider)```
Runs every physics frame when a Collider with the Collider.isTrigger property overlaps another Collider.

```OnTriggerExit(LuaCollider)```
Runs when the Collider other has stopped touching the trigger.

# Important Lua Notes
Lua uses ```nil``` instead of ```null```. You may be fooled into thinking ```null``` is valid, but Lua sees ```null``` as an empty variable, which returns ```nil```. So use ```nil```.

You are required to use a period (```.```) for variables and **static** method calls. For non-static method calls, use a colon (```:```) instead.
