# 🧭 RayUtil — Simple Raycasting Utility for Roblox Studio

A lightweight **Luau module** that simplifies raycasting operations in Roblox Studio.
It provides easy-to-use helper functions for performing world raycasts and viewport-based raycasts using the player’s camera and mouse position.

---

## 📦 Features

* 🎯 **Easy Raycasting:** Simplifies `workspace:Raycast()` calls.
* 🖱️ **Ray From View:** Instantly cast rays from the player’s screen position (mouse location).
* ⚙️ **Optional Parameters:** Supports custom `RaycastParams` for filtering or collision groups.
* 💡 **Graceful Fallback:** Returns a position even if no object is hit (useful for placing indicators or cursors).

---

## 📁 Installation

1. Copy the `RayUtil` module into your Roblox project (e.g., inside `ReplicatedStorage` or `StarterPlayerScripts`).
2. Require it in your scripts:

```lua
local RayUtil = require(game.ReplicatedStorage:WaitForChild("RayUtil"))
```

---

## ⚙️ API Reference

### `RayUtil.Raycast(origin: Vector3, direction: Vector3, max_distance: number, params: RaycastParams?)`

Casts a ray from an origin point along a direction for a maximum distance.

#### **Parameters**

| Name                  | Type            | Description                                                       |
| --------------------- | --------------- | ----------------------------------------------------------------- |
| `origin`              | `Vector3`       | Starting point of the ray.                                        |
| `direction`           | `Vector3`       | Direction vector for the ray. *(Does not need to be normalized.)* |
| `max_distance`        | `number`        | Maximum distance to cast the ray.                                 |
| `params` *(optional)* | `RaycastParams` | Optional parameters for filtering hits.                           |

#### **Returns**

* If an object is hit, returns the standard [`RaycastResult`](https://create.roblox.com/docs/reference/engine/datatypes/RaycastResult).
* If nothing is hit, returns a table with a single field:

  ```lua
  { Position = origin + direction * max_distance }
  ```

#### **Example**

```lua
local result = RayUtil.Raycast(Vector3.new(0, 10, 0), Vector3.new(0, -1, 0), 100)
print(result.Position) -- Hit position or end point
```

---

### `RayUtil.RayFromView(distance: number, params: RaycastParams?)`

Casts a ray from the **player’s camera** through the **mouse position** on the screen.

#### **Parameters**

| Name                  | Type            | Description                               |
| --------------------- | --------------- | ----------------------------------------- |
| `distance`            | `number`        | Maximum distance to cast from the camera. |
| `params` *(optional)* | `RaycastParams` | Optional filtering parameters.            |

#### **Returns**

* Same as `RayUtil.Raycast` — a `RaycastResult` or `{ Position = Vector3 }` fallback.

#### **Example**

```lua
local result = RayUtil.RayFromView(500)
print("Mouse hit position:", result.Position)
```

---

## 🧠 Implementation Details

* Uses `UserInputService:GetMouseLocation()` and `Camera:ViewportPointToRay()` to create rays from screen coordinates.
* Defaults to a new `RaycastParams` if none are provided.
* Works with **strict type checking** (`--!strict`) for cleaner and safer code.

---

## 🧩 Example Use Cases

* **Object placement** where the mouse points in 3D space.
* **Line of sight** or **target detection** in FPS or building games.
* **Ground detection** for aligning parts or character movement.

---

## 📝 License

This module is released under the [MIT License](LICENSE).
Feel free to modify and use it in your own Roblox projects.
