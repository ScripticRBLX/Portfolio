# Sprint Script

This script is designed for Roblox games to handle player sprinting functionality. The script listens for a `SprintEvent` and adjusts the player's walking speed accordingly.

### Script

**Path:** `ServerScriptService/SprintScript` (script)

```lua
local event = game.ReplicatedStorage:WaitForChild("SprintEvent")

event.OnServerEvent:Connect(function(plr, playerstate)
    if not plr.Character then return end
    
    if playerstate == "sprint" then
        plr.Character:WaitForChild("Humanoid").WalkSpeed += 5
    elseif playerstate == "walk" then
        plr.Character:WaitForChild("Humanoid").WalkSpeed -= 5
    end
end)
```

**Path:** `StarterPlayer/StarterPlayerScripts/Keybind` (local script)

```lua
local uis = game:GetService("UserInputService")
local camera = workspace.CurrentCamera 
local event = game.ReplicatedStorage:WaitForChild("SprintEvent")

uis.InputBegan:Connect(function(input)
    if input.KeyCode == Enum.KeyCode.LeftShift then
        event:FireServer("sprint")
        camera.FieldOfView = 90
    end
end)

uis.InputEnded:Connect(function(input)
    if input.KeyCode == Enum.KeyCode.LeftShift then
        event:FireServer("walk")
        camera.FieldOfView = 70
    end
end)
```
**Path:** `ReplicatedStorage/SprintEvent` (Remote Event)
