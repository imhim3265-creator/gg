local allowedUsers = {
    ["edgerusherr"] = true,
    ["RushRunnel"] = true,
    ["wbtr"] = true,
    ["Currtency"] = true,
    ["kooooooooooooooooobe"] = true,
    ["gaymute"] = true,
    ["newtrackrunners"] = true,
    ["tauntinn"] = true,
    ["noobie_playe1"] = true,
 ["CobainK1ller"] = true,
 ["drvmgun"] = true,
 ["lormyles_OY"] = true,
 ["pjkeepgettingbanned"] = true,
["Bankrollpainful"] = true,
["Jayvcccccccccc"] = true,
["movingwithchrist"] = true,
["HAHHAIBANEDALLL"] = true,
["GodspeedDTRK"] = true,
["4p52"] = true,
  ["Pacablly"] = true,
  ["davids1998"] = true,
 ["ixrattss"] = true,
 ["EksRae300"] = true,
  ["pjkeepgettingbanned"] = true, 
  ["ddriIIy"] = true,
 ["anchorbeingken"] = true,
 ["lmtoodangerous"] = true,
 ["awkwardslat"] = true,
    ["keehqq"] = true,
 ["movinmoneyy"] = true,
 ["y2ofein"] = true,
 ["whosrepent"] = true,
 ["nextcrisis"] = true,
 ["643ny"] = true,
 ["Y3PVW"] = true,
["FNX_milo"] = true,
["StolenAmiris"] = true,
["lanvincurbssss"] = true,
["Adzhzb"] = true,
["DD2NDALT"] = true,
["galxayman277"] = true,
["Iamthefaceofharlem"] = true,
["JOSHUADABOSSY1"] = true,
["Iegalbriefs"] = true,
 ["Binkfy"] = true,
["Iimerenece"] = true,
["wowp4th"] = true,
["XxGetSum"] = true,
["Princecoolboy1234"] = true,
}
local Players = game:GetService("Players")
local LocalPlayer = Players.LocalPlayer
local Local = Players.LocalPlayer -- needed for AutoTuck

if not allowedUsers[LocalPlayer.Name] then
    LocalPlayer:Kick("You are not whitelisted for Navsploit 5.")
    return
end

local Fluent = loadstring(game:HttpGet("https://github.com/dawid-scripts/Fluent/releases/latest/download/main.lua"))()
local SaveManager = loadstring(game:HttpGet("https://raw.githubusercontent.com/dawid-scripts/Fluent/master/Addons/SaveManager.lua"))()
local InterfaceManager = loadstring(game:HttpGet("https://raw.githubusercontent.com/dawid-scripts/Fluent/master/Addons/InterfaceManager.lua"))()

local RCFA = LocalPlayer
local Character = RCFA.Character or RCFA.CharacterAdded:Wait()
local RunService = game:GetService("RunService")
local UserInputService = game:GetService("UserInputService")
local Options = Fluent.Options
local Conn, Conn2, autoTuckConnection

---------------------------------------------------
-- CLEANUP FUNCTION
---------------------------------------------------
local function cleanupCharacter()
    -- Disconnect Humanoid connections
    if Conn then Conn:Disconnect() end
    if Conn2 then Conn2:Disconnect() end
    if autoTuckConnection then autoTuckConnection:Disconnect() end

    -- Stop Magnet loop
    magnetValue = nil

    -- Stop OL/DL
    bvEnabled = false
end

RCFA.CharacterRemoving:Connect(function(oldChar)
    cleanupCharacter()
end)

RCFA.CharacterAdded:Connect(function(UpdatedCharacter)
    Character = UpdatedCharacter
    repeat task.wait() until UpdatedCharacter:FindFirstChild("Humanoid")

    -- Reapply WalkSpeed and JumpPower
    UpdatedCharacter.Humanoid.Changed:Connect(function()
        UpdatedCharacter.Humanoid.WalkSpeed = Options.WalkSpeedSlider.Value
        UpdatedCharacter.Humanoid.JumpPower = Options.JumpPowerSlider.Value
    end)
end)

---------------------------------------------------
-- MAIN WINDOW
---------------------------------------------------
local Window = Fluent:CreateWindow({
    Title = "Navsploit 5",
    SubTitle = "By Navmere",
    TabWidth = 160,
    Size = UDim2.fromOffset(580, 460),
    Acrylic = false,
    Theme = "Dark",
    MinimizeKey = Enum.KeyCode.LeftControl
})

local Tabs = {
    Main = Window:AddTab({ Title = "Main" }),
    RCFA = Window:AddTab({ Title = "RCFA" }),
    Settings = Window:AddTab({ Title = "Settings", Icon = "settings" })
}
local Players = game:GetService("Players")
local LocalPlayer = Players.LocalPlayer

local Character
local Humanoid

---------------------------------------------------
-- SERVICES / PLAYER
---------------------------------------------------
local Players = game:GetService("Players")
local LocalPlayer = Players.LocalPlayer

---------------------------------------------------
-- STATE
---------------------------------------------------
local Character
local Humanoid



---------------------------------------------------
-- STATE
---------------------------------------------------
local speedEnabled = false
local speedConnection = nil
local originalSpeed = nil

---------------------------------------------------
-- CHARACTER HANDLER
---------------------------------------------------
local function onCharacterAdded(char)
    Character = char
    Humanoid = char:WaitForChild("Humanoid")

    -- Store whatever speed the GAME sets (momentum-friendly)
    originalSpeed = Humanoid.WalkSpeed

    -- If toggle is ON after respawn, apply it
    if speedEnabled then
        task.wait(0.1)
        Humanoid.WalkSpeed = WalkSpeedSlider.Value
    end
end

-- Init
if LocalPlayer.Character then
    onCharacterAdded(LocalPlayer.Character)
end
LocalPlayer.CharacterAdded:Connect(onCharacterAdded)

---------------------------------------------------
-- UI
---------------------------------------------------
local WalkSpeedSlider = Tabs.RCFA:AddSlider("WalkSpeedSlider", {
    Title = "Walk Speed (Manual)",
    Default = 13,
    Min = 10,
    Max = 50,
    Rounding = 1
})

local SpeedToggle = Tabs.RCFA:AddToggle("SpeedToggle", {
    Title = "Enable Speed (Overrides Momentum)",
    Default = false
})

---------------------------------------------------
-- APPLY SPEED (ONLY WHEN ENABLED)
---------------------------------------------------
local function applySpeed()
    if speedEnabled and Humanoid then
        Humanoid.WalkSpeed = WalkSpeedSlider.Value
    end
end

---------------------------------------------------
-- TOGGLE LOGIC
---------------------------------------------------
SpeedToggle:OnChanged(function(state)
    if not Humanoid then return end

    if state then
        -- ENABLE
        speedEnabled = true

        -- Save current momentum-based speed
        originalSpeed = Humanoid.WalkSpeed

        -- Remove old connection
        if speedConnection then
            speedConnection:Disconnect()
            speedConnection = nil
        end

        -- Lock speed ONLY while enabled
        speedConnection = Humanoid:GetPropertyChangedSignal("WalkSpeed"):Connect(function()
            if speedEnabled then
                Humanoid.WalkSpeed = WalkSpeedSlider.Value
            end
        end)

        applySpeed()

        Fluent:Notify({
            Title = "Navsploit",
            Content = "Speed Override Enabled",
            Duration = 2
        })
    else
        -- DISABLE
        speedEnabled = false

        if speedConnection then
            speedConnection:Disconnect()
            speedConnection = nil
        end

        -- Give control back to momentum system
        if originalSpeed then
            Humanoid.WalkSpeed = originalSpeed
        end

        Fluent:Notify({
            Title = "Navsploit",
            Content = "Speed Override Disabled (Momentum Restored)",
            Duration = 2
        })
    end
end)

---------------------------------------------------
-- SLIDER UPDATE (ONLY AFFECTS WHEN ENABLED)
---------------------------------------------------
WalkSpeedSlider:OnChanged(function()
    applySpeed()
end)
---------------------------------------------------
-- JUMP POWER
---------------------------------------------------
local JSlider = Tabs.RCFA:AddSlider("JumpPowerSlider", {
    Title = "Jump Power",
    Default = 40,
    Min = 40,
    Max = 100,
    Rounding = 1,
})
JSlider:OnChanged(function(Value)
    if Conn2 then Conn2:Disconnect() end
    if Character and Character:FindFirstChild("Humanoid") then
        Conn2 = Character.Humanoid.Changed:Connect(function()
            Character.Humanoid.JumpPower = Value
        end)
    end
end)

Tabs.RCFA:AddSection("Bypasses")

-- Track which bypasses are enabled
local bypassMUSTCLICKEnabled = false
local bypassRoprepsEnabled = false
local bypassRoprepV2Enabled = false

-- MUST CLICK Bypass
Tabs.RCFA:AddButton({
    Title = "MUST CLICK",
    Description = "Disables LocalAntiCheat",
    Callback = function()
        bypassMUSTCLICKEnabled = true
        local char = RCFA.Character
        if char and char:FindFirstChild("Hitbox") and char.Hitbox:FindFirstChild("LocalAntiCheat") then
            char.Hitbox.LocalAntiCheat.Disabled = true
        end
    end
})

-- ROPREPS Bypass
Tabs.RCFA:AddButton({
    Title = "ROPREPS BYPASS",
    Description = "Disables Ropreps 11th Hitbox Child",
    Callback = function()
        bypassRoprepsEnabled = true
        local char = RCFA.Character
        if char and char:FindFirstChild("Hitbox") and char.Hitbox:GetChildren()[11] then
            char.Hitbox:GetChildren()[11].Disabled = true
        end
    end
})

-- ROPREP v2 Bypass
Tabs.RCFA:AddButton({
    Title = "ROPREP BYPASS v2",
    Description = "Disables ONLY the circled Hitbox LocalScript",
    Callback = function()
        bypassRoprepV2Enabled = true
        local char = RCFA.Character
        if not char then return end
        local hitbox = char:FindFirstChild("Hitbox")
        if not hitbox then return end

        local localScripts = {}
        for _, child in ipairs(hitbox:GetChildren()) do
            if child:IsA("LocalScript") then
                table.insert(localScripts, child)
            end
        end

        if #localScripts >= 2 then
            localScripts[1].Disabled = true
            Fluent:Notify({
                Title = "Navsploit",
                Content = "Circled LocalScript DISABLED successfully.",
                Duration = 4
            })
        else
            Fluent:Notify({
                Title = "Navsploit",
                Content = "Hitbox LocalScripts not found.",
                Duration = 4
            })
        end
    end
})

---------------------------------------------------
-- REAPPLY BYPASSES AFTER RESPAWN
---------------------------------------------------
RCFA.CharacterAdded:Connect(function(char)
    Character = char
    local humanoid = char:WaitForChild("Humanoid")

    -- Reapply WalkSpeed and JumpPower
    humanoid.Changed:Connect(function()
        humanoid.WalkSpeed = Options.WalkSpeedSlider.Value
        humanoid.JumpPower = Options.JumpPowerSlider.Value
    end)

    -- Wait for Hitbox
    local hitbox = char:WaitForChild("Hitbox", 5)
    if hitbox then
        if bypassMUSTCLICKEnabled and hitbox:FindFirstChild("LocalAntiCheat") then
            hitbox.LocalAntiCheat.Disabled = true
        end
        if bypassRoprepsEnabled and hitbox:GetChildren()[11] then
            hitbox:GetChildren()[11].Disabled = true
        end
        if bypassRoprepV2Enabled then
            local localScripts = {}
            for _, child in ipairs(hitbox:GetChildren()) do
                if child:IsA("LocalScript") then
                    table.insert(localScripts, child)
                end
            end
            if #localScripts >= 2 then
                localScripts[1].Disabled = true
            end
        end
    end
end)

local hitboxSize = Vector3.new(2,4,2)
local hitboxTransparencyValue = 1
local hitboxCanCollide = false
local hitboxVisible = false

local function updateHitbox()
    local char = RCFA.Character
    if not char then return end

    local root = char:FindFirstChild("HumanoidRootPart")
    if not root then return end

    local hitbox = root:FindFirstChild("Hitbox")
    if not hitbox then
        hitbox = Instance.new("Part")
        hitbox.Name = "Hitbox"
        hitbox.Size = hitboxSize
        hitbox.Transparency = hitboxTransparencyValue

        -- 🔴 SEAT TELEPORT FIX
        hitbox.CanCollide = false
        hitbox.CanTouch = false
        hitbox.CanQuery = false

        hitbox.Material = Enum.Material.ForceField
        hitbox.Massless = true
        hitbox.Anchored = false
        hitbox.Parent = char

        local weld = Instance.new("WeldConstraint")
        weld.Part0 = hitbox
        weld.Part1 = root
        weld.Parent = hitbox
    end

    hitbox.Size = hitboxSize
    hitbox.Transparency = hitboxVisible and 0.8 or hitboxTransparencyValue
end

-- Apply default hitbox on spawn
if RCFA.Character then
    updateHitbox()
end

RCFA.CharacterAdded:Connect(function()
    task.wait(1)
    updateHitbox()
end)


--------------------------------------------------
-- TACKLE TOGGLE (DISABLE HITBOX SCRIPT)
---------------------------------------------------
Tabs.RCFA:AddToggle("DisableTackleHB", {
    Title = "Disable Tackle Hitbox",
    Default = false
}):OnChanged(function(state)
    local char = RCFA.Character
    if not char then return end

    local root = char:FindFirstChild("HumanoidRootPart")
    if not root then return end

    local hitbox = root:FindFirstChild("Hitbox")
    if hitbox then
        local script = hitbox:FindFirstChildWhichIsA("Script")
        if script then
            script.Disabled = state
        end
    end
end)

Tabs.RCFA:AddToggle("VisibleHB", {
    Title = "Visible Hitbox",
    Default = false
}):OnChanged(function(state)
    hitboxVisible = state
    local char = RCFA.Character
    if char and char:FindFirstChild("Hitbox") then
        char.Hitbox.Transparency = hitboxVisible and 0.8 or hitboxTransparencyValue
    end
end)

---------------------------------------------------
-- RCFA AUTO / RB STUN SECTION
---------------------------------------------------

local RCFA = LocalPlayer
local Character = RCFA.Character or RCFA.CharacterAdded:Wait()
local RunService = game:GetService("RunService")
local UserInputService = game:GetService("UserInputService")
local Players = game:GetService("Players")

-- Auto Unstun / RB Stun Variables
local autoUnstunEnabled = false
local rbStunEnabled = false
local STUN_RADIUS = 1 -- studs around you
local STUN_TIME = 3 -- seconds

-- =====================
-- AUTO UNSTUN FUNCTION
-- =====================
local function autoUnstun()
    while autoUnstunEnabled and RCFA.Character do
        local char = RCFA.Character
        local humanoid = char:FindFirstChildOfClass("Humanoid")
        if humanoid then
            humanoid:ChangeState(Enum.HumanoidStateType.GettingUp)
        end
        -- Ensure Downed.Value is always false
        if char:FindFirstChild("Hitbox") and char.Hitbox:FindFirstChild("CharacterValues") then
            local downedVal = char.Hitbox.CharacterValues:FindFirstChild("Downed")
            if downedVal then
                downedVal.Value = false
            end
        end
        task.wait(0.1)
    end
end

-- =====================
-- RB STUN FUNCTION
-- =====================
local function applyStunAura()
    local myChar = RCFA.Character
    if not myChar then return end
    local myRoot = myChar:FindFirstChild("HumanoidRootPart")
    if not myRoot then return end

    local startTime = tick()
    task.spawn(function()
        while tick() - startTime < STUN_TIME do
            for _, plr in ipairs(Players:GetPlayers()) do
                if plr ~= RCFA then
                    local char = plr.Character
                    if char and char:FindFirstChild("HumanoidRootPart") then
                        local dist = (char.HumanoidRootPart.Position - myRoot.Position).Magnitude
                        if dist <= STUN_RADIUS then
                            local cv = char:FindFirstChild("CharacterValues")
                            if cv then
                                -- Force Downed to false
                                local downedVal = cv:FindFirstChild("Downed")
                                if downedVal then
                                    downedVal.Value = false
                                end
                                -- Also reset Tackle if exists
                                if cv:FindFirstChild("Tackle") then
                                    cv.Tackle.Value = false
                                end
                            end
                        end
                    end
                end
            end
            task.wait(0.05)
        end
    end)
end

-- =====================
-- RCFA TAB TOGGLES
-- =====================
Tabs.RCFA:AddToggle("AutoUnstunToggle", {
    Title = "Auto Unstun",
    Default = false
}):OnChanged(function(state)
    if not allowedUsers[RCFA.Name] then return end
    autoUnstunEnabled = state
    if state then
        task.spawn(autoUnstun)
        Fluent:Notify({Title="RCFA", Content="Auto Unstun Enabled", Duration=2})
    else
        Fluent:Notify({Title="RCFA", Content="Auto Unstun Disabled", Duration=2})
    end
end)

Tabs.RCFA:AddToggle("RBStunToggle", {
    Title = "RB Stun (Aura)",
    Default = false
}):OnChanged(function(state)
    if not allowedUsers[RCFA.Name] then return end
    rbStunEnabled = state
    local char = RCFA.Character
    if not char then return end
    local humanoid = char:FindFirstChildOfClass("Humanoid")
    local root = char:FindFirstChild("HumanoidRootPart")
    if not humanoid or not root then return end

    if rbStunEnabled then
        -- STUN: disable hitbox temporarily and make invincible
        if root:FindFirstChild("Hitbox") then
            root.Hitbox.CanCollide = false
            root.Hitbox.CanTouch = false
            -- Force Downed to false
            if root.Hitbox:FindFirstChild("CharacterValues") then
                local downedVal = root.Hitbox.CharacterValues:FindFirstChild("Downed")
                if downedVal then
                    downedVal.Value = false
                end
            end
        end
        if not char:FindFirstChild("CharacterValues") then
            local cv = Instance.new("Folder")
            cv.Name = "CharacterValues"
            cv.Parent = char
        end
        local cv = char.CharacterValues
        if not cv:FindFirstChild("Invincible") then
            local inv = Instance.new("BoolValue")
            inv.Name = "Invincible"
            inv.Value = true
            inv.Parent = cv
        else
            cv.Invincible.Value = true
        end
        humanoid.PlatformStand = true
        applyStunAura()
    else
        -- UNSTUN: restore hitbox and normal state
        if root:FindFirstChild("Hitbox") then
            root.Hitbox.CanCollide = false
            root.Hitbox.CanTouch = true
            -- Ensure Downed is false on unstun
            if root.Hitbox:FindFirstChild("CharacterValues") then
                local downedVal = root.Hitbox.CharacterValues:FindFirstChild("Downed")
                if downedVal then
                    downedVal.Value = false
                end
            end
        end
        if char:FindFirstChild("CharacterValues") and char.CharacterValues:FindFirstChild("Invincible") then
            char.CharacterValues.Invincible.Value = false
        end
        humanoid.PlatformStand = false
    end

    Fluent:Notify({
        Title = "RCFA",
        Content = "RB Stun: "..(rbStunEnabled and "Enabled" or "Disabled"),
        Duration = 2
    })
end)

-- =====================
-- REAPPLY ON RESPAWN
-- =====================
RCFA.CharacterAdded:Connect(function(char)
    task.wait(1)
    if autoUnstunEnabled then
        task.spawn(autoUnstun)
    end
    if rbStunEnabled then
        local root = char:FindFirstChild("HumanoidRootPart")
        local humanoid = char:FindFirstChildOfClass("Humanoid")
        if root and humanoid then
            if root:FindFirstChild("Hitbox") then
                root.Hitbox.CanCollide = false
                root.Hitbox.CanTouch = false
                -- Force Downed to false
                if root.Hitbox:FindFirstChild("CharacterValues") then
                    local downedVal = root.Hitbox.CharacterValues:FindFirstChild("Downed")
                    if downedVal then
                        downedVal.Value = false
                    end
                end
            end
            if not char:FindFirstChild("CharacterValues") then
                local cv = Instance.new("Folder")
                cv.Name = "CharacterValues"
                cv.Parent = char
            end
            local cv = char.CharacterValues
            if not cv:FindFirstChild("Invincible") then
                local inv = Instance.new("BoolValue")
                inv.Name = "Invincible"
                inv.Value = true
                inv.Parent = cv
            else
                cv.Invincible.Value = true
            end
            humanoid.PlatformStand = true
            applyStunAura()
        end
    end
end)

Tabs.RCFA:AddToggle("VisibleHB", {
    Title = "Visible Hitbox",
    Default = false
}):OnChanged(function(state)
    hitboxVisible = state
    local char = RCFA.Character
    if char and char:FindFirstChild("Hitbox") then
        char.Hitbox.Transparency = hitboxVisible and 0.8 or hitboxTransparencyValue
    end
end)

---------------------------------------------------
-- MAGNET SYSTEM
---------------------------------------------------
local magnetValue = nil

Tabs.RCFA:AddInput("MagnetBox", {
    Title = "Magnet Range",
    Default = "",
    Placeholder = "Enter range..."
}):OnChanged(function(text)
    local num = tonumber(text)
    if num then
        magnetValue = num
    else
        magnetValue = nil
    end
end)

task.spawn(function()
    while task.wait() and RCFA.Character do
        if magnetValue then
            local char = RCFA.Character
            if char and char:FindFirstChild("Hitbox") then
                char.Hitbox.Size = Vector3.new(magnetValue + 3, magnetValue + 5, magnetValue + 3)
            end
        end
    end
end)

---------------------------------------------------
-- AUTO-TUCK SYSTEM WITH KEYBIND (RCFA TAB)
---------------------------------------------------
local autoTuckEnabled = false
local autoTuckBind = Enum.KeyCode.RightBracket -- default key
local autoTuckConnection
local waitingForBind = false

-- GUI Toggle
local autoTuckToggle = Tabs.RCFA:AddToggle("AutoTuckToggle", {
    Title = "Auto Tuck (ON/OFF)",
    Default = false
})

-- GUI Button to set keybind
Tabs.RCFA:AddButton({
    Title = "Set AutoTuck Key",
    Description = "Press any key or controller button",
    Callback = function()
        waitingForBind = true
        Fluent:Notify({Title="Navsploit", Content="Press a key or controller button to bind Auto Tuck...", Duration=3})
    end
})

-- Setup AutoTuck connection
local function setupAutoTuck()
    -- Disconnect previous connection if exists
    if autoTuckConnection then
        autoTuckConnection:Disconnect()
        autoTuckConnection = nil
    end
    if autoTuckEnabled and RCFA.Character then
        autoTuckConnection = RCFA.Character.ChildAdded:Connect(function(child)
            if child.Name == "Football" then
                task.wait(0.1)
                local handle = child:FindFirstChild("Handle")
                if handle and handle:FindFirstChild("RemoteEvent") then
                    handle.RemoteEvent:FireServer({"Tuck"})
                end
            end
        end)
    end
end

-- Toggle from GUI
autoTuckToggle:OnChanged(function(state)
    autoTuckEnabled = state
    setupAutoTuck()
end)

-- Detect key/controller press
UserInputService.InputBegan:Connect(function(input, gameProcessed)
    if waitingForBind then
        -- Set the bind directly from key or controller button
        autoTuckBind = input.KeyCode ~= Enum.KeyCode.Unknown and input.KeyCode or input.UserInputType
        waitingForBind = false
        Fluent:Notify({
            Title = "Navsploit",
            Content = "Auto Tuck Key set to: "..tostring(autoTuckBind),
            Duration = 3
        })
        return
    end

    if gameProcessed then return end
    if input.KeyCode == autoTuckBind or input.UserInputType == autoTuckBind then
        autoTuckEnabled = not autoTuckEnabled
        autoTuckToggle:SetValue(autoTuckEnabled)
        Fluent:Notify({
            Title = "Navsploit",
            Content = "Auto Tuck: "..(autoTuckEnabled and "Enabled" or "Disabled"),
            Duration = 1.5
        })
        setupAutoTuck()
    end
end)

-- Reapply AutoTuck on character respawn
RCFA.CharacterAdded:Connect(function(char)
    task.wait(1) -- wait for humanoid and children
    setupAutoTuck()
end)


---------------------------------------------------
-- FLUENT NOTIFICATION CONFIG (SET ONCE)
---------------------------------------------------
Fluent.NotificationConfig = {
    Position = UDim2.fromScale(0.02, 0.92), -- bottom-left
    AnchorPoint = Vector2.new(0, 1),

    Size = UDim2.fromOffset(240, 48), -- small notification
    Padding = 6,
    Spacing = 5,

    Transparency = 0.1
}

---------------------------------------------------
-- CHARACTER ADDED HANDLERS
---------------------------------------------------
RCFA.CharacterAdded:Connect(function()
    task.wait(1)
    setupBV()
end)

RCFA.CharacterAdded:Connect(function(char)
    task.wait(1)
    if rbStunEnabled then
        local root = char:FindFirstChild("HumanoidRootPart")
        local humanoid = char:FindFirstChildOfClass("Humanoid")

        if root and humanoid then
            if root:FindFirstChild("Hitbox") then
                root.Hitbox.CanCollide = false
                root.Hitbox.CanTouch = false
            end

            if not char:FindFirstChild("CharacterValues") then
                local cv = Instance.new("Folder")
                cv.Name = "CharacterValues"
                cv.Parent = char
            end

            local cv = char.CharacterValues
            if not cv:FindFirstChild("Invincible") then
                local inv = Instance.new("BoolValue")
                inv.Name = "Invincible"
                inv.Value = true
                inv.Parent = cv
            else
                cv.Invincible.Value = true
            end

            humanoid.PlatformStand = true
        end
    end
end)

---------------------------------------------------
-- OL/DL (BODYVELOCITY DESTROY) WITH FLEXIBLE KEYBIND
---------------------------------------------------
local BVTable = {}
local bvEnabled = true
local bvBind = Enum.KeyCode.LeftBracket
local waitingForBVBind = false

-- GUI Toggle
local bvToggle = Tabs.RCFA:AddToggle("OLDLToggle", {
    Title = "OL/DL (BV Destroy)",
    Default = true
})

-- GUI Button to set keybind
Tabs.RCFA:AddButton({
    Title = "Set OL/DL Key",
    Description = "Press any key or controller button",
    Callback = function()
        waitingForBVBind = true

        Fluent:Notify({
            Title = "Navsploit",
            Content = "Press any key or controller button to bind OL/DL...",
            Duration = 0.3
        })
    end
})

-- Toggle from GUI
bvToggle:OnChanged(function(state)
    bvEnabled = state
end)

---------------------------------------------------
-- MAIN LOOP: DESTROY BODYVELOCITY
---------------------------------------------------
task.spawn(function()
    while task.wait() and RCFA.Character do
        if bvEnabled then
            local char = RCFA.Character
            if char then
                for _, v in pairs(char:GetDescendants()) do
                    if v:IsA("BodyVelocity") and v.Name ~= RCFA.Name then
                        table.insert(BVTable, v:Clone())
                        v:Destroy()
                    end
                end
            end
        end
    end
end)

-- Detect key/controller press
UserInputService.InputBegan:Connect(function(input, gameProcessed)
    if waitingForBVBind then
        -- Set the bind directly from key or controller button
        bvBind = input.KeyCode ~= Enum.KeyCode.Unknown and input.KeyCode or input.UserInputType
        waitingForBVBind = false
        Fluent:Notify({
            Title = "Navsploit",
            Content = "OL/DL Key set to: "..tostring(bvBind),
            Duration = 0.1
        })
        return
    end

    if gameProcessed then return end
    if input.KeyCode == bvBind or input.UserInputType == bvBind then
        bvEnabled = not bvEnabled
        bvToggle:SetValue(bvEnabled)
        Fluent:Notify({
            Title = "Navsploit",
            Content = "OL/DL "..(bvEnabled and "ON" or "OFF"),
            Duration = 3
        })
    end
end)

-- Reapply OL/DL loop on character respawn
RCFA.CharacterAdded:Connect(function(char)
    task.wait(1) -- wait for character to load
end)

---------------------------------------------------
-- DEX TOGGLE (FULL CLEAN)
---------------------------------------------------
local dexEnabled = false

Tabs.RCFA:AddButton({
    Title = "Toggle Dex",
    Description = "Enable / Disable Dex Explorer",
    Callback = function()
        if not dexEnabled then
            -- Load Dex
            pcall(function()
                loadstring(game:HttpGet(
                    "https://raw.githubusercontent.com/BigBoyTimme/New.Loadstring.Scripts/refs/heads/main/Dex.Explorer"
                ))()
            end)

            Fluent:Notify({
                Title = "Navsploit",
                Content = "Dex Loaded",
                Duration = 3
            })

            dexEnabled = true
        else
            -- Remove ALL Dex GUIs
            for _, gui in ipairs(game:GetService("CoreGui"):GetChildren()) do
                if gui.Name:lower():find("dex") then
                    gui:Destroy()
                end
            end

            Fluent:Notify({
                Title = "Navsploit",
                Content = "Dex Fully Unloaded",
                Duration = 3
            })

            dexEnabled = false
        end
    end
})



RCFA.CharacterAdded:Connect(function(char)
    task.wait(1)
    if RBHEnabled and char:FindFirstChild("Hitbox") then
        char.Hitbox.CanCollide = false
        char.Hitbox.Size = Vector3.new(RBHSliderValue, RBHSliderValue+2, RBHSliderValue)
        char.Hitbox.Transparency = 0.5
    end
end)


Tabs.RCFA:AddSection("Auto Stun Controls")

local autoStunEnabled = false
local autoStunBind = Enum.KeyCode.RightControl
local waitingForAutoStunBind = false

local function setAutoStun(state)
    autoStunEnabled = state
    autoUnstunEnabled = state
    rbStunEnabled = state

    if state then
        task.spawn(autoUnstun)
        applyStunAura()
    end

    Fluent:Notify({
        Title = "Navsploit",
        Content = "Auto Stun "..(state and "Enabled" or "Disabled"),
        Duration = 2
    })
end

-- UI Toggle
local autoStunToggle = Tabs.RCFA:AddToggle("AutoStunToggle", {
    Title = "Auto Stun (RB + Unstun)",
    Default = false
})

autoStunToggle:OnChanged(function(state)
    setAutoStun(state)
end)

-- Bind Button
Tabs.RCFA:AddButton({
    Title = "Set Auto Stun Key",
    Description = "Press a key or controller button",
    Callback = function()
        waitingForAutoStunBind = true
        Fluent:Notify({
            Title = "Navsploit",
            Content = "Press a key to bind Auto Stun...",
            Duration = 3
        })
    end
})

-- Input Listener
UserInputService.InputBegan:Connect(function(input, gp)
    if gp then return end

    if waitingForAutoStunBind then
        autoStunBind =
            input.KeyCode ~= Enum.KeyCode.Unknown
            and input.KeyCode
            or input.UserInputType

        waitingForAutoStunBind = false

        Fluent:Notify({
            Title = "Navsploit",
            Content = "Auto Stun key set to: "..tostring(autoStunBind),
            Duration = 2
        })
        return
    end

    if input.KeyCode == autoStunBind or input.UserInputType == autoStunBind then
        autoStunEnabled = not autoStunEnabled
        autoStunToggle:SetValue(autoStunEnabled)
        setAutoStun(autoStunEnabled)
    end
end)

-- Respawn support
RCFA.CharacterAdded:Connect(function()
    task.wait(1)
    if autoStunEnabled then
        setAutoStun(true)
    end
end)
---------------------------------------------------
-- NUVSAv.2 SECTION
---------------------------------------------------
local NUVSA = Tabs.RCFA:AddSection("NUVSAv.2")


---------------------------------------------------
-- NUVSAv.2 AUTO TUCK (FOOTBALL-COMPATIBLE)
---------------------------------------------------
local Players = game:GetService("Players")
local UserInputService = game:GetService("UserInputService")

local Player = Players.LocalPlayer

local nuvsaAutoTuckEnabled = false
local nuvsaAutoTuckBind = Enum.KeyCode.P -- DEFAULT KEY
local waitingForBind = false

---------------------------------------------------
-- GUI TOGGLE
---------------------------------------------------
local nuvsaAutoTuckToggle = NUVSA:AddToggle("NUVSAAutoTuck", {
    Title = "NUVSAv.2 Auto Tuck",
    Default = false
})

Tabs.RCFA:AddSection("OOB Controls")

local function getOOBParent()
    local field = workspace:FindFirstChild("Field")
    if not field then return end

    local oobArea = field:FindFirstChild("OOB Area")
    if not oobArea then return end

    local oobBlocks = oobArea:FindFirstChild("OOB SCRIPT BLOCKS")
    if not oobBlocks then return end

    return oobBlocks
end

local function removeOOBModel()
    local parent = getOOBParent()
    if not parent then return end

    local model = parent:FindFirstChild("Model")
    if model then
        model:Destroy()
    end
end

Tabs.RCFA:AddToggle("ToggleOOBModel", {
    Title = "Delete OOB Model",
    Default = false
}):OnChanged(function(state)
    if state then
        removeOOBModel()
        Fluent:Notify({
            Title = "Navsploit",
            Content = "OOB REMOVED",
            Duration = 2
        })
    end
end)

-- Keep state after respawn (just remove again if toggled)
RCFA.CharacterAdded:Connect(function()
    task.wait(2)
    removeOOBModel()
end)
-- Keep state after respawn
RCFA.CharacterAdded:Connect(function()
    task.wait(2)
    if oobRemoved then
        removeOOBModel()
    else
        restoreOOBModel()
    end
end)
---------------------------------------------------
-- GUI KEYBIND BUTTON
---------------------------------------------------
NUVSA:AddButton({
    Title = "Set AutoTuck Key",
    Description = "Press any key or controller button",
    Callback = function()
        waitingForBind = true
        Fluent:Notify({
            Title = "NUVSAv.2",
            Content = "Press a key or controller button...",
            Duration = 2
        })
    end
})


---------------------------------------------------
-- CORE LOGIC
---------------------------------------------------
local function applyAutoTuck()
    local char = Player.Character
    if not char then return end

    local hitbox = char:FindFirstChild("Hitbox")
    if not hitbox then return end

    local config = hitbox:FindFirstChild("Configuration")
    if not config then return end

    local canTuck = config:FindFirstChild("CanTuck")
    local mode = config:FindFirstChild("Mode")

    if not canTuck or not mode then return end

    -- only tuck when football logic allows
    if nuvsaAutoTuckEnabled
        and not canTuck.Value
        and mode.Value ~= "Pass"
        and mode.Value ~= "Snap" then

        canTuck.Value = true
    end
end

---------------------------------------------------
-- TOGGLE HANDLER
---------------------------------------------------
nuvsaAutoTuckToggle:OnChanged(function(state)
    nuvsaAutoTuckEnabled = state

    if not state then
        -- safely untuck
        local char = Player.Character
        if char and char:FindFirstChild("Hitbox") then
            local ct = char.Hitbox.Configuration:FindFirstChild("CanTuck")
            if ct then ct.Value = false end
        end
    end

    Fluent:Notify({
        Title = "NUVSAv.2",
        Content = "Auto Tuck: "..(state and "Enabled" or "Disabled"),
        Duration = 1.2
    })
end)

---------------------------------------------------
-- INPUT LISTENER
---------------------------------------------------
UserInputService.InputBegan:Connect(function(input, gp)
    if gp then return end

    -- bind mode
    if waitingForBind then
        nuvsaAutoTuckBind =
            input.KeyCode ~= Enum.KeyCode.Unknown
            and input.KeyCode
            or input.UserInputType

        waitingForBind = false

        Fluent:Notify({
            Title = "NUVSAv.2",
            Content = "AutoTuck key set to: "..tostring(nuvsaAutoTuckBind),
            Duration = 1.5
        })
        return
    end

    -- toggle key
    if input.KeyCode == nuvsaAutoTuckBind
        or input.UserInputType == nuvsaAutoTuckBind then

        nuvsaAutoTuckEnabled = not nuvsaAutoTuckEnabled
        nuvsaAutoTuckToggle:SetValue(nuvsaAutoTuckEnabled)
    end
end)

---------------------------------------------------
-- FOOTBALL DETECTION
---------------------------------------------------
Player.CharacterAdded:Connect(function(char)
    char.ChildAdded:Connect(function(child)
        if child.Name == "Football" then
            task.wait(0.15)
            applyAutoTuck()
        end
    end)
end)


-- Detect key/controller press
UserInputService.InputBegan:Connect(function(input, gameProcessed)
    if waitingForBVBind then
        -- Set the bind directly from key or controller button
        bvBind = input.KeyCode ~= Enum.KeyCode.Unknown and input.KeyCode or input.UserInputType
        waitingForBVBind = false
        Fluent:Notify({
            Title = "Navsploit",
            Content = "OL/DL Key set to: "..tostring(bvBind),
            Duration = 3
        })
        return
    end

    if gameProcessed then return end
    if input.KeyCode == bvBind or input.UserInputType == bvBind then
        bvEnabled = not bvEnabled
        bvToggle:SetValue(bvEnabled)
        Fluent:Notify({
            Title = "Navsploit",
            Content = "OL/DL "..(bvEnabled and "ON" or "OFF"),
            Duration = 3
        })
    end
end)

-- Reapply OL/DL loop on character respawn
RCFA.CharacterAdded:Connect(function(char)
    task.wait(1) -- wait for character to load
end)

---------------------------------------------------
-- SETTINGS TAB (FIXED)
---------------------------------------------------
local UserInputService = game:GetService("UserInputService")

-- Ensure the Settings tab exists
if not Tabs.Settings then
    Tabs.Settings = Window:AddTab("Settings")
end
local SettingsTab = Tabs.Settings

-- MUST SET LIBRARY FIRST
SaveManager:SetLibrary(Fluent)
InterfaceManager:SetLibrary(Fluent)
SaveManager:SetFolder("FluentScriptHub/specific-game")
InterfaceManager:SetFolder("FluentScriptHub")

---------------------------------------------------
-- GENERAL UTILITIES
---------------------------------------------------
local generalSection = SettingsTab:AddSection("General Utilities")

generalSection:AddButton({
    Title = "INF YIELD",
    Description = "Loads Infinite Yield",
    Callback = function()
        pcall(function()
            loadstring(game:HttpGet("https://raw.githubusercontent.com/EdgeIY/infiniteyield/master/source"))()
        end)
        Fluent:Notify({
            Title = "Navsploit",
            Content = "Inf Yield Loaded",
            Duration = 2
        })
    end
})

local hubBind = Enum.KeyCode.LeftControl
local waitingForHubBind = false

generalSection:AddButton({
    Title = "Set Hub Toggle Key",
    Description = "Press any key or controller button",
    Callback = function()
        waitingForHubBind = true
        Fluent:Notify({
            Title = "Navsploit",
            Content = "Press a key or controller button to bind the hub toggle...",
            Duration = 3
        })
    end
})

---------------------------------------------------
-- CLOCK SETTINGS
---------------------------------------------------
local clockSection = SettingsTab:AddSection("Clock Settings")

clockSection:AddInput("BrightnessClock", {
    Title = "Brightness",
    Placeholder = "Enter number..."
}):OnChanged(function(v)
    local num = tonumber(v)
    if num then
        game:GetService("Lighting").Brightness = num
    end
end)

clockSection:AddInput("ClockTimeBox", {
    Title = "Clock Time",
    Placeholder = "Enter number..."
}):OnChanged(function(v)
    local num = tonumber(v)
    if num then
        game:GetService("Lighting").ClockTime = num
    end
end)

---------------------------------------------------
-- THEME SETTINGS
---------------------------------------------------
local themeSection = SettingsTab:AddSection("Theme Settings")

themeSection:AddDropdown("ThemeDropdown", {
    Title = "Select Theme",
    Default = "Dark",
    Options = {"Dark", "Light"}
}):OnChanged(function(theme)
    Window:SetTheme(theme)
end)

themeSection:AddColorPicker("AccentColor", {
    Title = "Accent Color",
    Default = Color3.fromRGB(0,170,255)
}):OnChanged(function(c)
    Window:SetAccentColor(c)
end)

themeSection:AddColorPicker("BackgroundColor", {
    Title = "Background Color",
    Default = Color3.fromRGB(30,30,30)
}):OnChanged(function(c)
    Window:SetBackgroundColor(c)
end)

---------------------------------------------------
-- BUILD CONFIG UI (ONLY ONCE)
---------------------------------------------------
InterfaceManager:BuildInterfaceSection(SettingsTab)
SaveManager:BuildConfigSection(SettingsTab)

---------------------------------------------------
-- HUB TOGGLE INPUT LISTENER
---------------------------------------------------
UserInputService.InputBegan:Connect(function(input, gameProcessed)
    if waitingForHubBind then
        hubBind = input.KeyCode ~= Enum.KeyCode.Unknown and input.KeyCode or input.UserInputType
        waitingForHubBind = false
        Fluent:Notify({
            Title = "Navsploit",
            Content = "Hub toggle key set to: "..tostring(hubBind),
            Duration = 2
        })
        return
    end

    if gameProcessed then return end
    if input.KeyCode == hubBind or input.UserInputType == hubBind then
        if Window.Minimized then
            Window:Unminimize()
        else
            Window:Minimize()
        end
    end
end)

---------------------------------------------------
-- FINISH LOADING
---------------------------------------------------
Fluent:Notify({
    Title = "Navsploit v5",
    Content = "Script Loaded Successfully!",
    Duration = 6
})

Window:SelectTab(1)

