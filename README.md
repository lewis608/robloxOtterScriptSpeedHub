# robloxOtterScriptSpeedHub


local player = game.Players.LocalPlayer
local userInputService = game:GetService("UserInputService")
local runService = game:GetService("RunService")

local speed = 16
local defaultSpeed = 16
local guiVisible = true

local gui = Instance.new("ScreenGui")
gui.ResetOnSpawn = false
gui.Parent = player:WaitForChild("PlayerGui")

local frame = Instance.new("Frame")
frame.Size = UDim2.new(0, 200, 0, 130)
frame.Position = UDim2.new(0.5, -100, 0.5, -65)
frame.BackgroundColor3 = Color3.fromRGB(30, 30, 30)
frame.BorderSizePixel = 0
frame.Active = true
frame.Draggable = true
frame.Parent = gui

local header = Instance.new("Frame")
header.Size = UDim2.new(1, 0, 0, 30)
header.BackgroundColor3 = Color3.fromRGB(20, 20, 20)
header.BorderSizePixel = 0
header.Parent = frame

local label = Instance.new("TextLabel")
label.Size = UDim2.new(1, 0, 1, 0)
label.Text = "made by Otter Hub"
label.TextColor3 = Color3.fromRGB(255, 255, 255)
label.BackgroundTransparency = 1
label.Parent = header

local textBox = Instance.new("TextBox")
textBox.Size = UDim2.new(0, 180, 0, 40)
textBox.Position = UDim2.new(0, 10, 0, 40)
textBox.Text = "Enter Speed"
textBox.BackgroundColor3 = Color3.fromRGB(50, 50, 50)
textBox.TextColor3 = Color3.fromRGB(255, 255, 255)
textBox.Parent = frame

local button = Instance.new("TextButton")
button.Size = UDim2.new(0, 180, 0, 30)
button.Position = UDim2.new(0, 10, 0, 90)
button.Text = "Set Default Speed"
button.BackgroundColor3 = Color3.fromRGB(50, 50, 50)
button.TextColor3 = Color3.fromRGB(255, 255, 255)
button.Parent = frame

local function setSpeed(newSpeed)
    speed = newSpeed
    if player.Character and player.Character:FindFirstChild("Humanoid") then
        player.Character.Humanoid.WalkSpeed = speed
    end
end

textBox.FocusLost:Connect(function(enterPressed)
    if enterPressed then
        local newSpeed = tonumber(textBox.Text)
        if newSpeed then
            setSpeed(newSpeed)
        end
    end
end)

button.MouseButton1Click:Connect(function()
    setSpeed(defaultSpeed)
    textBox.Text = tostring(defaultSpeed)
end)

runService.Stepped:Connect(function()
    if player.Character and player.Character:FindFirstChild("Humanoid") then
        player.Character.Humanoid.WalkSpeed = speed
    end
end)

userInputService.InputBegan:Connect(function(input, gameProcessed)
    if input.KeyCode == Enum.KeyCode.V and not gameProcessed then
        guiVisible = not guiVisible
        gui.Enabled = guiVisible
    end
end)
