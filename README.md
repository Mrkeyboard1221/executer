-- Simple Lua Executor (For educational purposes)
-- This will allow you to input a Lua script and execute it in your game.

-- Create GUI for the Executor
local player = game.Players.LocalPlayer
local playerGui = player:WaitForChild("PlayerGui")

-- Create the GUI
local gui = Instance.new("ScreenGui")
gui.Name = "LuaExecutor"
gui.Parent = playerGui

-- Create the main frame for the executor
local frame = Instance.new("Frame")
frame.Name = "ExecutorFrame"
frame.Size = UDim2.new(0, 400, 0, 250)
frame.Position = UDim2.new(0.5, -200, 0.5, -125)
frame.BackgroundColor3 = Color3.fromRGB(50, 50, 50)
frame.BackgroundTransparency = 0.3
frame.Parent = gui

-- Create a TextBox to input Lua code
local codeInput = Instance.new("TextBox")
codeInput.Name = "CodeInput"
codeInput.Size = UDim2.new(1, 0, 0, 150)
codeInput.Position = UDim2.new(0, 0, 0, 0)
codeInput.BackgroundColor3 = Color3.fromRGB(255, 255, 255)
codeInput.TextColor3 = Color3.fromRGB(0, 0, 0)
codeInput.Font = Enum.Font.SourceSans
codeInput.TextSize = 18
codeInput.Text = "-- Enter your Lua code here"
codeInput.TextWrapped = true
codeInput.Parent = frame

-- Create a Button to execute the Lua code
local executeButton = Instance.new("TextButton")
executeButton.Name = "ExecuteButton"
executeButton.Size = UDim2.new(1, 0, 0, 50)
executeButton.Position = UDim2.new(0, 0, 0, 150)
executeButton.BackgroundColor3 = Color3.fromRGB(0, 255, 0)
executeButton.TextColor3 = Color3.fromRGB(0, 0, 0)
executeButton.Font = Enum.Font.SourceSans
executeButton.TextSize = 18
executeButton.Text = "Execute Code"
executeButton.Parent = frame

-- Create a function to run the code
local function executeLuaCode(code)
    local func, err = loadstring(code)
    
    if func then
        -- Run the Lua code
        pcall(func)
    else
        -- Display error if the code is invalid
        warn("Error in Lua code: " .. err)
    end
end

-- Button click event to execute code
executeButton.MouseButton1Click:Connect(function()
    local code = codeInput.Text
    executeLuaCode(code)
end)
