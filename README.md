local Rayfield = loadstring(game:HttpGet("https://sirius.menu/rayfield"))()

local Window = Rayfield:CreateWindow({
   Name = "Encrypted Hub | SW2 | PREMIUM",
   Icon = nil, -- No icon
   LoadingTitle = "Loading..",
   LoadingSubtitle = "by Kryptic.dev",
   Theme = { -- Pure Yellow & Black Theme
      TextColor = Color3.fromRGB(128, 0, 128), -- Bright Yellow Text

      Background = Color3.fromRGB(0, 0, 0), -- Pure Black Background
      Topbar = Color3.fromRGB(0, 0, 0), -- Black Topbar
      Shadow = Color3.fromRGB(0, 0, 0), -- Black Shadow

      NotificationBackground = Color3.fromRGB(0, 0, 0), -- Black Notification Background
      NotificationActionsBackground = Color3.fromRGB(128, 0, 128), -- Yellow Notification Actions

      TabBackground = Color3.fromRGB(0, 0, 0), -- Black Tab Background
      TabStroke = Color3.fromRGB(128, 0, 128), -- Purple Tab Border
      TabBackgroundSelected = Color3.fromRGB(128, 0, 128), -- Yellow Selected Tab
      TabTextColor = Color3.fromRGB(128, 0, 128), -- Yellow Tab Text
      SelectedTabTextColor = Color3.fromRGB(0, 0, 0), -- Black Text on Selected Tab

      ElementBackground = Color3.fromRGB(0, 0, 0), -- Black Element Background
      ElementBackgroundHover = Color3.fromRGB(0, 0, 0), -- Hover stays Black
      SecondaryElementBackground = Color3.fromRGB(0, 0, 0), -- Fully Black Secondary Elements
      ElementStroke = Color3.fromRGB(128, 0, 128), -- Yellow Element Border
      SecondaryElementStroke = Color3.fromRGB(128, 0, 128), -- Yellow Border on Secondary Element

      SliderBackground = Color3.fromRGB(128, 0, 128), -- Yellow Slider Background
      SliderProgress = Color3.fromRGB(128, 0, 128), -- Yellow Slider Progress
      SliderStroke = Color3.fromRGB(128, 0, 128), -- Yellow Slider Stroke

      ToggleBackground = Color3.fromRGB(0, 0, 0), -- Black Toggle Background
      ToggleEnabled = Color3.fromRGB(128, 0, 128), -- Yellow When Enabled
      ToggleDisabled = Color3.fromRGB(0, 0, 0), -- Black When Disabled
      ToggleEnabledStroke = Color3.fromRGB(128, 0, 128), -- Yellow Border When Enabled
      ToggleDisabledStroke = Color3.fromRGB(0, 0, 0), -- Black Border When Disabled
      ToggleEnabledOuterStroke = Color3.fromRGB(128, 0, 128), -- Yellow Outer Stroke When Enabled
      ToggleDisabledOuterStroke = Color3.fromRGB(0, 0, 0), -- Black Outer Stroke When Disabled

      DropdownSelected = Color3.fromRGB(128, 0, 128), -- Yellow Selected Dropdown
      DropdownUnselected = Color3.fromRGB(0, 0, 0), -- Black Unselected Dropdown

      InputBackground = Color3.fromRGB(0, 0, 0), -- Black Input Background
      InputStroke = Color3.fromRGB(128, 0, 128), -- Yellow Input Stroke
      PlaceholderColor = Color3.fromRGB(128, 0, 128) -- Yellow Placeholder Text
   },

   DisableRayfieldPrompts = false,
   DisableBuildWarnings = false,

   ConfigurationSaving = {
      Enabled = False,
      FolderName = "YellowBlackThemeHub",
      FileName = "BigHub"
   },

   Discord = {
      Enabled = false,
      Invite = "noinvitelink",
      RememberJoins = true
   },

KeySystem = true, -- Set this to true to use our key system
   KeySettings = {
      Title = "Untitled",
      Subtitle = "Key System",
      Note = "Ask Vip Leo", -- Use this to tell the user how to get a key
      FileName = "Key", -- It is recommended to use something unique as other scripts using Rayfield may overwrite your key file
      SaveKey = true, -- The user's key will be saved, but if you change the key, they will be unable to use your script
      GrabKeyFromSite = false, -- If this is true, set Key below to the RAW site you would like Rayfield to get the key from
      Key = {"WprHUUaLrbkBWTDDAXnDUbwKgcnJkJHk", "FvHLXZqH6GmjWTYbXZtVBGpUG3rBk5Hk", "Px34YVsqU9zV9Y5DtbdCfnQz6T3Kp83X", "Dh9YrF0q2tXw6DJ8LbsZKDmk9v0RyxU5", "K38m4dDql1X2g5czk6vTbWNuqUdzmV3Wa","7Y0P1Hcaj1mB5DSZvfiUJwSVhwJf2ibg","DVmOKOp3nCJpjdtyRZQmI4dSMCk46VA7","3n9kj0GzXqYwI8LroR6jQ5sDmaV2kFZ9","7LgFwpKzN0VjS9O4R2XyT6Dq7aIoFqH5"},
   }
})

local MainTab = Window:CreateTab("Main", 4483362458) -- Title, Image
local MainSection = MainTab:CreateSection("Card")

local Players = game:GetService("Players")
local ReplicatedStorage = game:GetService("ReplicatedStorage")
local VirtualInputManager = game:GetService("VirtualInputManager")
local player = Players.LocalPlayer

local dupeAmount = 10
local StatusLabel = MainTab:CreateLabel("Status: Waiting for action...")

-- Notification function with error handling
local function notify(message, time, type)
    local success, err = pcall(function()
        game:GetService("StarterGui"):SetCore("SendNotification", {
            Title = type or "Info",
            Text = message,
            Duration = time or 5,
        })
    end)

    if not success then
        warn("Notification failed: " .. err)
    end
end

-- Textbox for Duplication Amount
MainTab:CreateInput({
    Name = "Laptop & Card Dupe",
    PlaceholderText = "Amount",
    RemoveTextAfterFocusLost = false,
    Flag = "DupeAmount",
    Callback = function(value)
        dupeAmount = tonumber(value) or 10
        if dupeAmount <= 0 then
            dupeAmount = 10  -- Fallback value
            StatusLabel.Text = "Invalid amount, defaulting to 10."
        end
    end
})

-- Duplication Function
local function duplicateCardsAndLaptops()
    if dupeAmount <= 0 then
        StatusLabel.Text = "Invalid amount!"
        return
    end

    StatusLabel.Text = "Buying cards & laptops..."

    -- Open Dealer UI
    fireclickdetector(game.Workspace["Streetz War"].Anonymous.ClickDetector)
    wait(1) -- Wait to ensure the UI is open
    player.PlayerGui:WaitForChild("DealerGui")
    local shopGui = player.PlayerGui.DealerGui.ShopFrame
    shopGui.Visible = true
    player.PlayerGui.DealerGui.Frame.Visible = false
    game:GetService("RunService"):Set3dRenderingEnabled(false)

    -- Position player correctly
    repeat wait() until player.Character and player.Character:FindFirstChild("HumanoidRootPart")
    player.Character.HumanoidRootPart.CFrame = CFrame.new(-55, 4.5, 170)

    wait(0.5)

    -- Click buttons for purchasing
    local cardButton = shopGui["Blank Card"]
    local laptopButton = shopGui["laptop"]

    for i = 1, dupeAmount do
        task.wait()
        -- Click the card button
        if cardButton.Visible then
            local cardPos = cardButton.AbsolutePosition
            VirtualInputManager:SendMouseButtonEvent(cardPos.X + 150, cardPos.Y + 60, 0, true, game, 0)
            task.wait(0.1)
            VirtualInputManager:SendMouseButtonEvent(cardPos.X + 150, cardPos.Y + 60, 0, false, game, 0)
        end

        task.wait(0.1)

        -- Click the laptop button
        if laptopButton.Visible then
            local laptopPos = laptopButton.AbsolutePosition
            VirtualInputManager:SendMouseButtonEvent(laptopPos.X + 150, laptopPos.Y + 60, 0, true, game, 0)
            task.wait(0.1)
            VirtualInputManager:SendMouseButtonEvent(laptopPos.X + 150, laptopPos.Y + 60, 0, false, game, 0)
        end
    end

    game:GetService("RunService"):Set3dRenderingEnabled(true)

    -- Close the UI
    local exitButton = shopGui.exit
    VirtualInputManager:SendMouseButtonEvent(exitButton.AbsolutePosition.X + 300, exitButton.AbsolutePosition.Y + 65, 0, true, game, 0)
    wait()
    VirtualInputManager:SendMouseButtonEvent(exitButton.AbsolutePosition.X + 300, exitButton.AbsolutePosition.Y + 65, 0, false, game, 0)

    -- Move player to next step
    player.Character.HumanoidRootPart.CFrame = CFrame.new(954, 4.7, -61)
    wait(4)

    -- Process Laptops
    StatusLabel.Text = "Processing laptops..."
    local laptopCount = 0
    for _, v in pairs(player.Backpack:GetChildren()) do
        if v.Name == "Laptop" then
            laptopCount = laptopCount + 1
        end
    end

    for i = 1, laptopCount - 1 do
        spawn(function()
            local args = { true, "NEW123" }
            ReplicatedStorage.Assets.Other.GiverPunchmade:InvokeServer(unpack(args))
        end)
    end

    wait(4)
    player.Backpack.Laptop.Parent = player.Character
    wait(4)

    -- Process Cards
    StatusLabel.Text = "Processing cards..."
    local cardCount = 0
    for _, v in pairs(player.Backpack:GetChildren()) do
        if v.Name == "Loaded Card" then
            cardCount = cardCount + 1
        end
    end

    for i = 1, cardCount do
        spawn(function()
            local args = { false, "NEW123" }
            ReplicatedStorage.Assets.Other.GiverPunchmade:InvokeServer(unpack(args))
        end)
    end

    wait(1)
    StatusLabel.Text = "Duplication Complete!"
    player.Character.Humanoid:UnequipTools()
end

-- Button for Duplication
MainTab:CreateButton({
    Name = "Dupe Laptop & Card",
    Callback = function()
        duplicateCardsAndLaptops()
    
        end
})

MainTab:CreateButton({
    Name = "Atm 1",
    Callback = function()
        game.Players.LocalPlayer.Character.HumanoidRootPart.CFrame = CFrame.new()            
        end
})

local MainSection = MainTab:CreateSection("Gun Dupe")

local Button = MainTab:CreateButton({
   Name = "Safe Dupe",
   Callback = function()
        game.Players.LocalPlayer.Character.HumanoidRootPart.CFrame = CFrame.new(-134776, -196, 3325) 

            wait(5) 
            game.Players.LocalPlayer.Character.HumanoidRootPart.CFrame = CFrame.new(-134811, -197, 3288)        
   end,
})

MainTab:CreateButton({
    Name = "Gun Dupe",
    Callback = function()
         local player = game.Players.LocalPlayer
        local character = player.Character or player.CharacterAdded:Wait()
        local humanoidRootPart = character:WaitForChild("HumanoidRootPart")
        local safeZones = game.Workspace.SafeZones:GetChildren()
        
        local closestSafeZone = nil
        local shortestDistance = math.huge 

        for _, safeZone in ipairs(safeZones) do
            local distance = (humanoidRootPart.Position - safeZone.Position).Magnitude
            if distance < shortestDistance then
                shortestDistance = distance
                closestSafeZone = safeZone
            end
        end
        
        if closestSafeZone then
            humanoidRootPart.CFrame = closestSafeZone.CFrame
            character.Humanoid:ChangeState(Enum.HumanoidStateType.Dead) 
        else
            warn("No safe zones found.")
        end
    end
})
             
local MainSection = MainTab:CreateSection("Payloads")

local Button = MainTab:CreateButton({
    Name = "Cash Dupe (WIP)",
    Callback = function()
        
        end
    })
local VisualsTab = Window:CreateTab("Visuals", 4483362458) -- Title, Image

local lastplayername = ""
local lastplayerlvl = ""
local lastplayeremoji = ""
local espEnabled = false

-- Function to update the character GUI with text
local function updateCharacterGui(field, text)
    local character = game.Players.LocalPlayer.Character
    if character and character:FindFirstChild("Head") then
        local nameGui = character.Head:FindFirstChild("NameGui")
        if nameGui and nameGui:FindFirstChild("Main") then
            local guiElement = nameGui.Main:FindFirstChild(field)
            if guiElement then
                guiElement.Text = text
            end
        end
    end
end

VisualsTab:CreateInput({
    Name = "Custom Name",
    PlaceholderText = "Enter Name...",
    RemoveTextAfterFocusLost = false,
    Callback = function(text)
        lastplayername = text
        updateCharacterGui("Name", text)
    end
})

VisualsTab:CreateInput({
    Name = "Custom Level",
    PlaceholderText = "Enter Level...",
    RemoveTextAfterFocusLost = false,
    Callback = function(text)
        lastplayerlvl = text
        updateCharacterGui("Level", "LVL " .. text)
    end
})

VisualsTab:CreateInput({
    Name = "Custom Emoji",
    PlaceholderText = "Enter Emoji...",
    RemoveTextAfterFocusLost = false,
    Callback = function(text)
        lastplayeremoji = text
        updateCharacterGui("Extras", "[" .. text .. "]")
    end
})

VisualsTab:CreateButton({
    Name = "Apply Changes",
    Callback = function()
        updateCharacterGui("Name", lastplayername)
        updateCharacterGui("Level", "LVL " .. lastplayerlvl)
        updateCharacterGui("Extras", "[" .. lastplayeremoji .. "]")
        Rayfield:Notify({
            Title = "Updated",
            Content = "Updated By Streetzwars.com",
            Duration = 5
        })
    end
})

local AimTab = Window:CreateTab("Aim", 4483362458) -- Title, Image
local AimSection = AimTab:CreateSection("Weapon Features")

local Toggle = AimTab:CreateToggle({
    Name = "Tool Stealing",
    CurrentValue = false,
    Flag = "ToolStealing",
    Callback = function(Value)
        _G.ToolStealing = Value
        
        while _G.ToolStealing do
            game:GetService("RunService").RenderStepped:Wait()
            
            local tool = game.Workspace:FindFirstChildOfClass("Tool")
            if tool then
                game.Players.LocalPlayer.Character.Humanoid:EquipTool(tool)
            end
        end
    end
})

local Toggle = AimTab:CreateToggle({
    Name = "Infinite Ammo",
    CurrentValue = false,
    Flag = "InfiniteAmmo",
    Callback = function(state)
        _G.infiniteAmmo = state

        task.spawn(function()
            while _G.infiniteAmmo do
                local player = game.Players.LocalPlayer
                local tool = player.Character and player.Character:FindFirstChildOfClass("Tool")

                if tool and tool:FindFirstChild("Stuff") then
                    local ammoValues = tool.Stuff.Values
                    ammoValues.CurrentAmmo.MaxValue = 1000000000
                    ammoValues.StoredAmmo.MaxValue = 10000000000
                    ammoValues.CurrentAmmo.Value = 10000000000000000000000
                    ammoValues.StoredAmmo.Value = 10000000000000
                end

                task.wait(0.5) -- Prevents excessive loops
            end
        end)
    end
})

local Toggle = AimTab:CreateToggle({
    Name = "Zero Recoil",
    CurrentValue = false,
    Flag = "ZeroRecoil", 
    Callback = function(state)
        _G.zeroRecoil = state
        local player = game.Players.LocalPlayer
        local character = player.Character or player.CharacterAdded:Wait()

        local function removeRecoil()
            local tool = character:FindFirstChildOfClass("Tool")

            if tool and tool:FindFirstChild("Recoil") then
                tool.Recoil.Value = 0
            end
            if tool and tool:FindFirstChild("CameraShake") then
                tool.CameraShake.Value = 0
            end
            if tool and tool:FindFirstChild("Rotation") then
                tool.Rotation.Value = 0
            end
        end

        task.spawn(function()
            while _G.zeroRecoil do
                removeRecoil()
                wait(0.1) -- Prevent overloading the loop
            end
        end)
    end
})

local Toggle = AimTab:CreateToggle({
    Name = "Modify Weapon",
    CurrentValue = false,
    Flag = "ChangeToolColor", 
    Callback = function(state)
        _G.changeToolColor = state
        local player = game.Players.LocalPlayer
        local character = player.Character or player.CharacterAdded:Wait()

        -- Function to change the tool color to yellow
        local function changeToolColorToYellow()
            local tool = character:FindFirstChildOfClass("Tool")  -- Find the first tool

            -- Check if tool exists and has a handle
            if tool and tool:FindFirstChild("Handle") then
                -- Change the tool's handle color to yellow
                tool.Handle.BrickColor = BrickColor.new("Bright yellow")
            end
        end

        -- Toggle the color change on and off
        task.spawn(function()
            while _G.changeToolColor do
                changeToolColorToYellow()
                wait(0.1) -- Prevent overloading the loop
            end
        end)
    end
})

local AimSection = AimTab:CreateSection("Aimbot")

local Players = game:GetService("Players")
local RunService = game:GetService("RunService")
local UserInputService = game:GetService("UserInputService")

local localPlayer = Players.LocalPlayer
local mouse = localPlayer:GetMouse()
local camera = workspace.CurrentCamera

_G.aimbotSystemEnabled = false

local aimCircleRadius = 100
local aimbotEnabled = false
local circleColor = Color3.new(1, 1, 0) -- Yellow

local aimCircle = nil

local function createAimCircle()
    if not aimCircle then
        aimCircle = Drawing.new("Circle")
        aimCircle.Visible = false
        aimCircle.Color = circleColor
        aimCircle.Thickness = 2
        aimCircle.Radius = aimCircleRadius
        aimCircle.Filled = false
    end
end

local function destroyAimCircle()
    if aimCircle then
        aimCircle:Remove()
        aimCircle = nil
    end
end

local function isPlayerInAimCircle(player)
    local character = player.Character
    if character and character:FindFirstChild("HumanoidRootPart") then
        local rootPart = character.HumanoidRootPart
        local screenPos, onScreen = workspace.CurrentCamera:WorldToScreenPoint(rootPart.Position)
        if onScreen then
            local mousePos = Vector2.new(mouse.X, mouse.Y)
            local distFromMouse = (mousePos - Vector2.new(screenPos.X, screenPos.Y)).Magnitude
            return distFromMouse <= aimCircleRadius, distFromMouse
        end
    end
    return false, math.huge
end

local function getClosestPlayer()
    local closestPlayer = nil
    local closestDistance = aimCircleRadius

    for _, player in pairs(Players:GetPlayers()) do
        if player ~= localPlayer then
            local character = player.Character
            if character and character:FindFirstChild("Humanoid") and character.Humanoid.Health > 0 then
                local inCircle, distance = isPlayerInAimCircle(player)
                if inCircle and distance < closestDistance then
                    closestDistance = distance
                    closestPlayer = player
                end
            end
        end
    end

    return closestPlayer
end

local function aimAtTarget(player)
    local character = player.Character
    if character and character:FindFirstChild("HumanoidRootPart") and character:FindFirstChild("Head") then
        local head = character.Head
        camera.CFrame = CFrame.new(camera.CFrame.Position, head.Position)
    end
end

UserInputService.InputBegan:Connect(function(input)
    if input.UserInputType == Enum.UserInputType.MouseButton2 and _G.aimbotSystemEnabled then
        aimbotEnabled = true
    end
end)

UserInputService.InputEnded:Connect(function(input)
    if input.UserInputType == Enum.UserInputType.MouseButton2 then
        aimbotEnabled = false
    end
end)

RunService.RenderStepped:Connect(function()
    if not _G.aimbotSystemEnabled then
        destroyAimCircle()
        return
    end

    if not aimCircle then
        createAimCircle()
    end

    aimCircle.Position = Vector2.new(mouse.X, mouse.Y + 40)
    aimCircle.Visible = true

    if aimbotEnabled then
        local closestPlayer = getClosestPlayer()
        if closestPlayer then
            aimAtTarget(closestPlayer)
        end
    end
end)

local Toggle = AimTab:CreateToggle({
    Name = "Aimbot",
    CurrentValue = false,
    Flag = "Aimbot",
    Callback = function(Value)
        _G.aimbotSystemEnabled = Value
        if not _G.aimbotSystemEnabled then
            destroyAimCircle()
        end
    end
})

local Toggle = AimTab:CreateToggle({
   Name = "Aimlock ",
   CurrentValue = false,
   Flag = "Toggle1", -- A flag is the identifier for the configuration file, make sure every element has a different flag if you're using configuration saving to ensure no overlaps
   Callback = function(Value)
        local Area = game:GetService("Workspace")
local RunService = game:GetService("RunService")
local UIS = game:GetService("UserInputService")
local Players = game:GetService("Players")
local LocalPlayer = Players.LocalPlayer
local MyCharacter = LocalPlayer.Character
local MyRoot = MyCharacter:FindFirstChild("HumanoidRootPart")
local MyHumanoid = MyCharacter:FindFirstChild("Humanoid")
local Mouse = LocalPlayer:GetMouse()
local MyView = Area.CurrentCamera


local AutoLockActive = false
local LockDistance = 100 -- Maximum distance to lock onto players
local Epitaph = .045 -- Prediction for moving players (larger value means more prediction)


local function FindNearestPlayer()
    local dist = math.huge
    local Target = nil
    for _, v in pairs(Players:GetPlayers()) do
        if v ~= LocalPlayer and v.Character:FindFirstChild("Humanoid") and v.Character:FindFirstChild("Humanoid").Health > 0 and v.Character:FindFirstChild("HumanoidRootPart") then
            local TheirCharacter = v.Character
            local CharacterRoot, Visible = MyView:WorldToViewportPoint(TheirCharacter.HumanoidRootPart.Position)
            if Visible then
                local RealMag = (Vector2.new(Mouse.X, Mouse.Y) - Vector2.new(CharacterRoot.X, CharacterRoot.Y)).Magnitude
                if RealMag < dist and RealMag < LockDistance then
                    dist = RealMag
                    Target = TheirCharacter
                end
            end
        end
    end
    return Target
end


local function AutoLockCamera()
    if AutoLockActive then
        local Target = FindNearestPlayer()
        if Target then
            local FuturePosition = Target.HumanoidRootPart.CFrame + (Target.HumanoidRootPart.Velocity * Epitaph)
            MyView.CFrame = CFrame.lookAt(MyView.CFrame.Position, FuturePosition.Position) -- Lock camera to the target's future position
        end
    end
end


local ScreenGui = Instance.new("ScreenGui")
ScreenGui.Parent = game.Players.LocalPlayer:WaitForChild("PlayerGui")

local ToggleButton = Instance.new("TextButton")
ToggleButton.Size = UDim2.new(0, 200, 0, 50)
ToggleButton.Position = UDim2.new(0.5, -100, 0.9, -25)
ToggleButton.Text = "Enable AutoLock"
ToggleButton.Parent = ScreenGui
ToggleButton.BackgroundColor3 = Color3.fromRGB(0, 255, 0)

ToggleButton.MouseButton1Click:Connect(function()
    AutoLockActive = not AutoLockActive -- Toggle the AutoLock state
    if AutoLockActive then
        ToggleButton.Text = "Disable AutoLock"
        ToggleButton.BackgroundColor3 = Color3.fromRGB(255, 0, 0) -- Change to red when active
    else
        ToggleButton.Text = "Enable AutoLock"
        ToggleButton.BackgroundColor3 = Color3.fromRGB(0, 255, 0) -- Change to green when inactive
    end
end)


RunService.RenderStepped:Connect(function()
    AutoLockCamera()
end)


game.StarterGui:SetCore("SendNotification", {
    Title = "AutoLock Active",
    Text = "Auto AimLock script is now active.",
    Duration = 5,
})  
   end,
})

local camera = workspace.CurrentCamera
local entities = game:GetService("Players")
local localplayer = entities.LocalPlayer 
local runservice = game:GetService("RunService")

local esp_settings = {
    enabled = true,
    skel = true,
    skel_col = Color3.fromRGB(255,255,255)
}

local function draw(player, character)
    local skel_parts = {}
    local part_names = {"head", "torso", "leftarm", "rightarm", "leftleg", "rightleg"}
    
    for _, name in ipairs(part_names) do
        skel_parts[name] = Drawing.new("Line")
        skel_parts[name].Visible = false
        skel_parts[name].Thickness = 1.5
        skel_parts[name].Color = esp_settings.skel_col
    end
    
    local function update()
        local connection
        connection = runservice.RenderStepped:Connect(function()
            if character and character:FindFirstChild("HumanoidRootPart") and character:FindFirstChild("Humanoid") and character:FindFirstChild("Humanoid").Health > 0 then
                local root_2d, on_screen = camera:WorldToViewportPoint(character.HumanoidRootPart.Position)
                if on_screen and character.Humanoid.RigType == Enum.HumanoidRigType.R6 and esp_settings.enabled then
                    local head_2d = camera:WorldToViewportPoint(character.Head.Position)
                    local torso_upper_2d = camera:WorldToViewportPoint(character.Torso.Position + Vector3.new(0,1,0))
                    local torso_lower_2d = camera:WorldToViewportPoint(character.Torso.Position + Vector3.new(0,-1,0))
                    local leftarm_2d = camera:WorldToViewportPoint(character["Left Arm"].Position + Vector3.new(0,-1,0))
                    local rightarm_2d = camera:WorldToViewportPoint(character["Right Arm"].Position + Vector3.new(0,-1,0))
                    local leftleg_2d = camera:WorldToViewportPoint(character["Left Leg"].Position + Vector3.new(0,-1,0))
                    local rightleg_2d = camera:WorldToViewportPoint(character["Right Leg"].Position + Vector3.new(0,-1,0))
                    
                    skel_parts.head.From, skel_parts.head.To = Vector2.new(head_2d.X, head_2d.Y), Vector2.new(torso_upper_2d.X, torso_upper_2d.Y)
                    skel_parts.torso.From, skel_parts.torso.To = Vector2.new(torso_upper_2d.X, torso_upper_2d.Y), Vector2.new(torso_lower_2d.X, torso_lower_2d.Y)
                    skel_parts.leftarm.From, skel_parts.leftarm.To = Vector2.new(torso_upper_2d.X, torso_upper_2d.Y), Vector2.new(leftarm_2d.X, leftarm_2d.Y)
                    skel_parts.rightarm.From, skel_parts.rightarm.To = Vector2.new(torso_upper_2d.X, torso_upper_2d.Y), Vector2.new(rightarm_2d.X, rightarm_2d.Y)
                    skel_parts.leftleg.From, skel_parts.leftleg.To = Vector2.new(torso_lower_2d.X, torso_lower_2d.Y), Vector2.new(leftleg_2d.X, leftleg_2d.Y)
                    skel_parts.rightleg.From, skel_parts.rightleg.To = Vector2.new(torso_lower_2d.X, torso_lower_2d.Y), Vector2.new(rightleg_2d.X, rightleg_2d.Y)
                    
                    for _, part in pairs(skel_parts) do
                        part.Visible = esp_settings.skel
                    end
                else
                    for _, part in pairs(skel_parts) do
                        part.Visible = false
                    end
                end
            else
                connection:Disconnect()
                for _, part in pairs(skel_parts) do
                    part.Visible = false
                end
            end
        end)
    end
    coroutine.wrap(update)()
end

local function playeradded(player)
    if player.Character then
        coroutine.wrap(draw)(player, player.Character)
    end
    player.CharacterAdded:Connect(function(character)
        coroutine.wrap(draw)(player, character)
    end)
end

for _, player in ipairs(entities:GetPlayers()) do
    if player ~= localplayer then
        playeradded(player)
    end
end

entities.PlayerAdded:Connect(playeradded)


local Toggle = AimTab:CreateToggle({
    Name = "Skeleton ESP",
    CurrentValue = true,
    Flag = "ESP_Toggle",
    Callback = function(value)
        esp_settings.enabled = value
    end
})

local TeleportsTab = Window:CreateTab("Teleports", 4483362458) -- Title, Image
local TeleportsSection = TeleportsTab:CreateSection("Player")

local players = game:GetService("Players") -- Getting the Players service
local teleportService = game:GetService("TeleportService")
local playerNames = {}

-- Populate the playerNames table with the names of all players in the game
for _, player in pairs(players:GetPlayers()) do
    table.insert(playerNames, player.Name)
end

-- Create the dropdown with the list of players
local Dropdown = TeleportsTab:CreateDropdown({
    Name = "Player Dropdown",
    Options = playerNames,
    CurrentOption = {playerNames[1]}, -- Set the first player as the default selection
    MultipleOptions = false,
    Flag = "PlayerDropdown", -- A flag is the identifier for the configuration file
    Callback = function(Options)
        -- The function that takes place when the selected option is changed
        -- The variable (Options) is a table of strings for the current selected options
        selectedPlayerName = Options[1]
        print("Selected player: " .. selectedPlayerName)
    end,
})

-- Create a button to teleport to the selected player
local TeleportButton = TeleportsTab:CreateButton({
    Name = "Teleport to Player",
    Flag = "TeleportButton", -- A flag is the identifier for the configuration file
    Callback = function()
        local selectedPlayer = players:FindFirstChild(selectedPlayerName)
        if selectedPlayer then
            -- Teleport the local player to the selected player’s character
            local character = selectedPlayer.Character
            if character and character:FindFirstChild("HumanoidRootPart") then
                local humanoidRootPart = character.HumanoidRootPart
                players.LocalPlayer.Character:SetPrimaryPartCFrame(humanoidRootPart.CFrame)
            end
        else
            warn("Selected player not found!")
        end
    end,
})

local TeleportsSection = TeleportsTab:CreateSection("Teleports")

local teleportLocations = {
    {Name = "🚗dealership", Position = CFrame.new(842, 5, -7)},
    {Name = "🏩Apartments 2", Position = CFrame.new(739, 4, 199)},
    {Name = "🏨Apartments 1", Position = CFrame.new(4, 4, 52)},
    {Name = "🧹Paki Shop", Position = CFrame.new(-101, 4, 18)},
    {Name = "📦Box Job", Position = CFrame.new(-118, 4, 300)},
    {Name = "🍕Pizza Job", Position = CFrame.new(166, 5, 49)},
    {Name = "🏪Thrift Store", Position = CFrame.new(-42, 4, 36)},
    {Name = "🥊Boxing", Position = CFrame.new(259, 5, -100)},
    {Name = "🏆Casino", Position = CFrame.new(159, 5, 246)},
    {Name = "💎Ice Box", Position = CFrame.new(-11354, 4, 288)},
    {Name = "🤭Suit Shop", Position = CFrame.new(43, 4, -329)},
    {Name = "🏥Hospital", Position = CFrame.new(42, 4, -261)},
    {Name = "🔫Gun Store", Position = CFrame.new(-51807, 4, -11)},
    {Name = "🥷Bank Tools Etc", Position = CFrame.new(-142, 4, 189)},
    {Name = "💳Blanc Card Dealer", Position = CFrame.new(226, 4, -543)},
    {Name = "🍍TNT Locker", Position = CFrame.new(269, 5, 132)},
    {Name = "🩸ATB Locker", Position = CFrame.new(93, 4, -703)},
    {Name = "🩶SG Locker", Position = CFrame.new(188, 4, -395)},
    {Name = "💙KAO Locker", Position = CFrame.new(328, 7, 82)},
    {Name = "💙AF Locker", Position = CFrame.new(162, 5, 518)},
    {Name = "🧡EOS Locker", Position = CFrame.new(374, 22, 409)},
    {Name = "💚AOD Locker", Position = CFrame.new(6, 5, 509)},
    {Name = "❤️LAC Locker", Position = CFrame.new(-166, 4, -773)},
    {Name = "💙P9 Locker", Position = CFrame.new(459, 7, 160)},
    {Name = "💙TPL Locker", Position = CFrame.new(318, 7, 230)},
    {Name = "💛RGD Locker", Position = CFrame.new(599, 7, 223)},
    {Name = "NGF Locker", Position = CFrame.new(571, 20, 174)},
    {Name = "💙DF Locker", Position = CFrame.new(870, 5, 498)},
    {Name = "🎄Wheel Spin", Position = CFrame.new(142, 4, 91)}
}

local locationNames = {}

-- Populate location names
for _, location in pairs(teleportLocations) do
    table.insert(locationNames, location.Name)
end

local selectedLocation = teleportLocations[1] -- Default location

-- Create Dropdown
local Dropdown = TeleportsTab:CreateDropdown({
    Name = "Select Teleport Location",
    Options = locationNames,
    CurrentOption = {locationNames[1]}, -- Default selected option
    MultipleOptions = false,
    Flag = "TeleportLocationDropdown", -- Flag for config saving
    Callback = function(Options)
        -- Update selected location based on dropdown selection
        for _, location in pairs(teleportLocations) do
            if location.Name == Options[1] then
                selectedLocation = location
                break
            end
        end
    end
})

-- Create Button to Teleport to Selected Location
local TeleportButton = TeleportsTab:CreateButton({
    Name = "Teleport",
    Callback = function()
        if selectedLocation then
            -- Teleport player to selected location
            game.Players.LocalPlayer.Character.HumanoidRootPart.CFrame = selectedLocation.Position
        else
            warn("No location selected!")
        end
    end
})

local TeleportsSection = TeleportsTab:CreateSection("Car Spawns")


local PlayerTab = Window:CreateTab("Player", 4483362458)
local PlayerSection = PlayerTab:CreateSection("Extra")

local Toggle = PlayerTab:CreateToggle({
   Name = "Chage Username",
   CurrentValue = false,
   Flag = "Toggle1", -- A flag is the identifier for the configuration file, make sure every element has a different flag if you're using configuration saving to ensure no overlaps
   Callback = function(Value)
        local PlayerGui = game.Players.LocalPlayer:WaitForChild("PlayerGui")


local targetUsernameLabel = nil


local function findAndChangeUsername()
    for _, v in ipairs(PlayerGui:GetDescendants()) do
        if v:IsA("TextLabel") and v.Text:find(game.Players.LocalPlayer.Name) then
            targetUsernameLabel = v
            v.Text = "@leo"  -- Change the username to the desired text
            v.BackgroundColor3 = Color3.fromRGB(255, 0, 0)  -- Highlight the label in red
            v.BorderSizePixel = 2
            v.BorderColor3 = Color3.fromRGB(255, 255, 255)
            print("Username label found and changed to discord.gg/dkshub:", v:GetFullName())
            break
        end
    end
end


findAndChangeUsername()
   end,
})

local Toggle = PlayerTab:CreateToggle({
    Name = "Disable Camera Shake",
    CurrentValue = false,
    Flag = "DisableCameraShake",
    Callback = function(state)
        local char = game:GetService("Players").LocalPlayer.Character
        if char and char:FindFirstChild("CharacterScripts") then
            char.CharacterScripts.Enabled = not state
            cameraShakeDisabled = state
        end
    end
})

local Player = game.Players.LocalPlayer
local respawnLocation = nil  -- Initialize the respawn location variable

local Toggle = PlayerTab:CreateToggle({
    Name = "Respawn Where Died",
    CurrentValue = false,
    Flag = "Toggle1", -- A flag to store the toggle state
    Callback = function(Value)
        -- If the toggle is enabled, set up the respawn functionality
        if Value then
            -- Set the respawn point to the location where the player dies
            game.Players.PlayerAdded:Connect(function(player)
                player.CharacterAdded:Connect(function(character)
                    local humanoid = character:WaitForChild("Humanoid")

                    humanoid.Died:Connect(function()
                        respawnLocation = character:WaitForChild("HumanoidRootPart").Position
                        wait(5)  -- Delay before respawning the player (optional)

                        -- Destroy the character and respawn
                        character:Destroy()
                        wait(1)

                        -- Load a new character and position it at the respawn location
                        local newCharacter = player:LoadCharacter()
                        newCharacter:WaitForChild("HumanoidRootPart").CFrame = CFrame.new(respawnLocation)
                    end)
                end)
            end)
        else
            -- Disable respawn functionality when the toggle is turned off
            game.Players.PlayerAdded:Connect(function(player)
                player.CharacterAdded:Connect(function(character)
                    local humanoid = character:WaitForChild("Humanoid")

                    humanoid.Died:Disconnect() -- Disconnect the respawn logic
                end)
            end)
        end
    end
})

local PlayerSection = PlayerTab:CreateSection("Modify")

local Slider = PlayerTab:CreateSlider({
   Name = "Walkspeed",
   Range = {0, 300},
   Increment = 1,
   Suffix = "Speed",
   CurrentValue = 16,
   Flag = "Slider1", -- A flag is the identifier for the configuration file, make sure every element has a different flag if you're using configuration saving to ensure no overlaps
   Callback = function(Value)
        game.Players.LocalPlayer.Character.Humanoid.WalkSpeed = (Value)
   end,
})

local Slider = PlayerTab:CreateSlider({
   Name = "JumpHeight",
   Range = {0, 300},
   Increment = 1,
   Suffix = "Height",
   CurrentValue = 16,
   Flag = "Slider1", -- A flag is the identifier for the configuration file, make sure every element has a different flag if you're using configuration saving to ensure no overlaps
   Callback = function(Value)
        game.Players.LocalPlayer.Character.Humanoid.JumpPower = (Value)
   end,
})

PlayerTab:CreateToggle({
    Name = "Infinite Jump",
    Default = false,  -- Set to true if you want it enabled by default
    Callback = function(state)
        InfiniteJumpEnabled = state  -- Toggle the state when the button is clicked
    end
})

local ExtraTab = Window:CreateTab("Extra", 4483362458) -- Title, Image
local ExtraSection = ExtraTab:CreateSection("Quick Buy")

local Player = game.Players.LocalPlayer
local Camera = game.Workspace.CurrentCamera

local teleportLocations = {
    {Name = "Glock Drum", Position = Vector3.new(-51830, 7, -21)},
    {Name = "Glock 17 Switch", Position = Vector3.new(-51830, 7, -25)},
    {Name = "Tec9", Position = Vector3.new(-51821, 7, -25)},
    {Name = "Skorpion", Position = Vector3.new(-51830, 7, -18)}
}

local selectedLocation = nil  -- Variable to store the selected location

-- Callback for teleporting to selected location
local function teleportToLocation(position)
    local character = Player.Character
    if character and character:FindFirstChild("HumanoidRootPart") then
        -- Ensure the humanoid root part exists before attempting teleportation
        character:WaitForChild("HumanoidRootPart").CFrame = CFrame.new(position)
    else
        print("Error: HumanoidRootPart not found!")
    end
end


-- Create the dropdown for selecting teleport location
local TeleportDropdown = ExtraTab:CreateDropdown({
    Name = "Select Location to Teleport",
    Options = { "Glock Drum", "Glock 17 Switch", "Tec9", "Skorpion" },  -- The names of the locations
    CurrentOption = "Tec9",  -- Default option
    Flag = "TeleportDropdown",  -- Flag to save the user's selected option
    Callback = function(selectedOption)
        -- Find the selected location and store it
        for _, location in pairs(teleportLocations) do
            if location.Name == selectedOption then
                selectedLocation = location.Position
                break
            end
        end
    end
})

-- Create a button to teleport to the selected location
local TeleportButton = ExtraTab:CreateButton({
    Name = "Teleport To Gun",
    Callback = function()
        if selectedLocation then
            teleportToLocation(selectedLocation)  -- Teleport to the selected location
        else
            print("Please select a location first!")  -- Notify the player to select a location
        end
    end
})

local ExtraSection = ExtraTab:CreateSection("Car Spawn")

local Dropdown = ExtraTab:CreateDropdown({
   Name = "Car Spawner",
   Options = {"Rusty Rv","Dirtbike","Buggati","rollsroyce","audi","Van","Toyota","Niggas"},
   CurrentOption = {"Option 1"},
   MultipleOptions = false,
   Flag = "Dropdown1", -- A flag is the identifier for the configuration file, make sure every element has a different flag if you're using configuration saving to ensure no overlaps
   Callback = function(Options)
   -- The function that takes place when the selected option is changed
   -- The variable (Options) is a table of strings for the current selected options
   end,
})

local Button = ExtraTab:CreateButton({
   Name = "Goto Car",
   Callback = function()
        game.Players.LocalPlayer.Character.HumanoidRootPart.CFrame = CFrame.new(774, 5, 15)
   end,
})

local MiscTab = Window:CreateTab("Misc", 4483362458) -- Title, Image
local MiscSection = MiscTab:CreateSection("Modify Fly Etc")
