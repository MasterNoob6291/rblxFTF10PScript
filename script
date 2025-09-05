local Mercury = loadstring(game:HttpGet("https://raw.githubusercontent.com/deeeity/mercury-lib/master/src.lua"))()

-- FOR FLEE THE FACILITY 10 PLAYER ONLY
local Map = game.Workspace.Map

local Players = game:GetService("Players")
local LocalPlayer = Players.LocalPlayer
local RunService = game:GetService("RunService")
local UIS = game:GetService("UserInputService")

local TelePlayerName = ""
local TeleportDropdown

-- Create Window
local Window = Mercury:Create{
    Name = "Flee The Facility Hack UI",
    Size = UDim2.fromOffset(600, 400),
    Theme = Mercury.Themes.Amethyst,
    Link = "https://github.com/deeeity/mercury-lib"
}

local PlayerTab = Window:Tab{
    Name = "Player Controls",
    Icon = "rbxassetid://2795572800"
}

-- Player speed slider
PlayerTab:Slider{
    Name = "Speed",
    Min = 8,
    Max = 100,
    Default = 16,
    Callback = function(Value)
        local character = LocalPlayer.Character
        if character and character:FindFirstChild("Humanoid") then
            character.Humanoid.WalkSpeed = Value
        end
    end
}

-- Player jump slider
PlayerTab:Slider{
    Name = "Jump Power",
    Min = 5,
    Max = 30,
    Default = 7.2,
    Callback = function(Value)
        local character = LocalPlayer.Character
        if character and character:FindFirstChild("Humanoid") then
            character.Humanoid.JumpHeight = Value
        end
    end
}

-- Get player names
local function GetPlayerNames()
    local names = {}
    for _, player in pairs(Players:GetPlayers()) do
        if player ~= LocalPlayer and player.Name then
            table.insert(names, player.Name)
        end
    end
    return names
end

-- TELEPORT MENU
TeleportDropdown = PlayerTab:Dropdown{
    Name = "Teleport Player List",
    StartingText = "Select...",
    Items = GetPlayerNames(),
    Callback = function(selected)
        TelePlayerName = selected
    end
}

PlayerTab:Button{
    Name = "Teleport to Player",
    Callback = function()
        local targetPlayer = Players:FindFirstChild(TelePlayerName)
        if targetPlayer and targetPlayer.Character then
            local targetHRP = targetPlayer.Character:FindFirstChild("HumanoidRootPart")
            if targetHRP then
                LocalPlayer.Character:SetPrimaryPartCFrame(targetHRP.CFrame)
            end
        end
    end
}

PlayerTab:Button{
    Name = "Teleport to Random Computer",
    Description = nil,
    Callback = function()
        for _, part in pairs(Map:GetChildren()) do
            if part.Name == "ComputerTable"  then
                if part.Screen.Color ~= Color3.fromRGB(60, 255, 0) then
                    LocalPlayer.Character:SetPrimaryPartCFrame(part.ComputerTrigger1.CFrame)
                end
            end
        end
    end
}



Players.PlayerAdded:Connect(function(plr)
    TeleportDropdown:AddItems({plr.Name})
end)

Players.PlayerRemoving:Connect(function(plr)
    TeleportDropdown:RemoveItems({plr.Name})
end)

-- Noclip
local Noclip = false
PlayerTab:Toggle{
    Name = "Noclip",
    Default = false,
    Callback = function(Value)
        Noclip = Value
    end
}

RunService.Stepped:Connect(function()
    if LocalPlayer.Character and Noclip then
        for _, part in pairs(LocalPlayer.Character:GetDescendants()) do
            if part:IsA("BasePart") then
                part.CanCollide = false
            end
        end
    end
end)

-- Infinite Jump Toggle
local InfJump = false

PlayerTab:Toggle{
	Name = "Infinite Jump Toggle",
	StartingState = false,
	Callback = function(state) 
        InfJump = state
    end
}

UIS.InputBegan:Connect(function(input)
    local char = LocalPlayer.Character
    local hum = char:FindFirstChildOfClass("Humanoid")
    if InfJump and input.UserInputType == Enum.UserInputType.Keyboard and input.KeyCode == Enum.KeyCode.Space then
        hum:ChangeState(Enum.HumanoidStateType.Jumping)
    end
end)
