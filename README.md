local ScreenGui = Instance.new("ScreenGui")
ScreenGui.Name = "DeltaCustomMenu"
ScreenGui.ResetOnSpawn = false
ScreenGui.Parent = game:GetService("Players").LocalPlayer:WaitForChild("PlayerGui", 10) or game:GetService("CoreGui")

local MenuButton = Instance.new("TextButton")
MenuButton.Name = "ToggleButton"
MenuButton.BackgroundColor3 = Color3.fromRGB(0, 0, 0)
MenuButton.BackgroundTransparency = 0.5
MenuButton.Position = UDim2.new(0.1, 0, 0.2, 0)
MenuButton.Size = UDim2.new(0, 45, 0, 45)
MenuButton.Font = Enum.Font.SourceSansBold
MenuButton.Text = "J"
MenuButton.TextColor3 = Color3.fromRGB(255, 255, 255)
MenuButton.TextSize = 29
MenuButton.ZIndex = 10
MenuButton.Parent = ScreenGui

local UIStroke = Instance.new("UIStroke")
UIStroke.Thickness = 2
UIStroke.Color = Color3.fromRGB(255, 0, 0)
UIStroke.Parent = MenuButton

local localPlayer = game:GetService("Players").LocalPlayer
local isOn = false

game:GetService("RunService").PreSimulation:Connect(function()
    if isOn and localPlayer and localPlayer.Character then
        local humanoid = localPlayer.Character:FindFirstChildOfClass("Humanoid")
        if humanoid then
            humanoid.Sit = true
            humanoid:SetStateEnabled(Enum.HumanoidStateType.Seated, false)
        end
    end
end)

MenuButton.MouseButton1Click:Connect(function()
    isOn = not isOn
    local humanoid = localPlayer.Character and localPlayer.Character:FindFirstChildOfClass("Humanoid")

    if isOn then
        UIStroke.Color = Color3.fromRGB(0, 255, 0)
    else
        UIStroke.Color = Color3.fromRGB(255, 0, 0)
        if humanoid then
            humanoid.Sit = false
            humanoid:SetStateEnabled(Enum.HumanoidStateType.Seated, true)
            humanoid:ChangeState(Enum.HumanoidStateType.GettingUp)
        end
    end
end)
