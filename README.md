# 🧪 LAB 04 (2 Hours) — Interactable 1 (Basic): Collectables + Collector Box  
Includes script + where to attach  

---

## Goal
Students will **grab items** and **drop them into a collector box** to “submit” them.  
When an item enters the box, it will **disappear** (set inactive).

---

## Learning Outcomes
By the end of this lab, you will be able to:
- Create collectable prefabs
- Configure XR Grab Interactable correctly
- Use **Tags** to identify collectable objects
- Use a **Trigger Zone** to detect dropped objects
- Write and attach a simple C# script using `OnTriggerEnter()`

---

## Requirements
- Unity **2022.3 LTS**
- XR Interaction Toolkit installed
- OpenXR enabled
- Your **same VR project** from previous labs

Recommended folder structure:
- `Assets/_Project/Prefabs`
- `Assets/_Project/Scripts`
- `Assets/_Project/Materials` (optional)

---

## Important Setup Notes (Read This First)
To make **grab + trigger detection** work correctly:

Collectable item must have:
- **Collider** (Sphere Collider / Box Collider)
- **Rigidbody** (not kinematic for basic use)
- **XR Grab Interactable**

Collector box must have:
- **Collider set as Trigger** (`Is Trigger = true`)
- Script attached: `CollectorZone.cs`

At least ONE of the two objects in the trigger interaction must have a **Rigidbody**  
(In our case, the collectable has a Rigidbody)

---

# Step-by-Step

---

## A) Create the Tag: `Collectable`
1. Select **any object** in the Scene (anything).
2. In Inspector → Top area → **Tag** dropdown → choose **Add Tag...**
3. Click **+** and create a tag named exactly:
   - `Collectable`

Spelling must match exactly (capital C).

---

## B) Create Collectable Prefab (Gem)
### 1) Create the object
1. Hierarchy → **Right Click** → `3D Object` → `Sphere`
2. Rename it to:
   - `Collectable_Gem`
3. Set Scale to:
   - `X = 0.15, Y = 0.15, Z = 0.15`

### 2) Add Rigidbody
1. Select `Collectable_Gem`
2. Inspector → **Add Component** → `Rigidbody`
3. Keep:
   - `Use Gravity`  ON  
   - `Is Kinematic` OFF (for this basic lab)

### 3) Add XR Grab Interactable
1. Inspector → **Add Component**
2. Add:
   - `XR Grab Interactable`

This allows you to grab the gem using VR controllers.

### 4) Set the Tag
- Set Tag to:
  - `Collectable`

### 5) Make it a Prefab
1. Drag `Collectable_Gem` from **Hierarchy** into:
   - `Assets/_Project/Prefabs`
2. Unity creates a prefab (blue icon)

### 6) Remove the original from the Scene
- Delete the Sphere from the Hierarchy (scene version)
- Keep the prefab in the folder

---

## C) Spawn 10 Gems in the Scene
1. Drag the `Collectable_Gem` prefab into the Scene
2. Duplicate it until you have **10**
   - Windows: `Ctrl + D`
3. Place them around the player area (easy to test)

---

## D) Create Collector Box (Trigger Zone)
### 1) Create the box
1. Hierarchy → Right click → `3D Object` → `Cube`
2. Rename it to:
   - `CollectorBox`
3. Set Scale to:
   - `X = 0.6, Y = 0.3, Z = 0.6`

### 2) Position it
Place it in front of the player at reachable height:
- Example:
  - `Y = 0.5` (so it is above ground)

### 3) Make the collider a Trigger
1. Select `CollectorBox`
2. In Inspector → find **Box Collider**
3. Tick:
   - `Is Trigger`

This makes it a detection zone (not a solid wall).

---

## E) Script: `CollectorZone.cs`
### 1) Create Script
Go to:
- `Assets/_Project/Scripts`
Right click → `Create` → `C# Script`
Name it exactly:
- `CollectorZone`

### 2) Paste this code (replace everything)
```csharp
using UnityEngine;

public class CollectorZone : MonoBehaviour
{
    [Header("Tag that can be collected")]
    public string collectableTag = "Collectable";

    private void OnTriggerEnter(Collider other)
    {
        // Only collect objects with the correct tag
        if (!other.CompareTag(collectableTag)) return;

        // Disable the object (makes it disappear)
        other.gameObject.SetActive(false);
    }
}
```
## F) Attach Script to CollectorBox

1. Select `CollectorBox`
2. Inspector → Add Component
3. Add: `CollectorZone`

Now the box can collect objects entering it.

---

## Testing

1. Press Play
2. Grab a gem using the VR controller
3. Drop it inside `CollectorBox`
4. The gem should disappear

---

## Common Issues and Fixes

### Gem doesn’t disappear
Check:
- Is the gem Tag set to `Collectable`?
- Is `CollectorBox` collider set to `Is Trigger = true`?
- Does the gem have a `Rigidbody`?
- Does the gem have a `Collider` (Sphere Collider)?
- Is `CollectorZone` script attached to `CollectorBox`?

### Can’t grab the gem
Check:
- `XR Grab Interactable` is added to the gem
- XR Hands/Controllers are set correctly from previous labs
- The gem has a `Rigidbody` and a `Collider`

## Submission Task (Video)

Add a second item type: Key (Cube) and show both can be collected.

### Requirements

1. Create a cube object:
   - Name: `Collectable_Key`
   - Scale: `0.15, 0.15, 0.15`

2. Add components:
   - `Rigidbody` (Use Gravity = ON)
   - `XR Grab Interactable`

3. Set Tag:
   - `Collectable`

4. Make it a prefab and add a few in the scene.

5. Record a video showing:
   - collecting gems
   - collecting keys

### Filename
- `Lab04_<ITNo>.mp4`

Example:
- `Lab04_IT21012345.mp4`


## Next Lab Lab 05: counters + UI HUD + GameManager + multi-item types.














