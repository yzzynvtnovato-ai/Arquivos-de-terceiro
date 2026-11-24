
local Players = game:GetService("Players")
local UserInputService = game:GetService("UserInputService")

local player = Players.LocalPlayer

local gui = Instance.new("ScreenGui")
gui.Name = "BKMenuGui"
gui.ResetOnSpawn = false
gui.Parent = player:WaitForChild("PlayerGui")

-- =====================================
-- BOTÃO FLUTUANTE BK MENU
-- =====================================

local button = Instance.new("TextButton")
button.Name = "BKMenuButton"
button.Size = UDim2.fromOffset(145, 45)
button.Position = UDim2.new(0, 20, 0.5, -22)
button.BackgroundColor3 = Color3.fromRGB(12, 12, 12)
button.Text = "BK MENU"
button.TextColor3 = Color3.fromRGB(205, 205, 215)
button.TextSize = 18
button.Font = Enum.Font.GothamBold
button.AutoButtonColor = true
button.Active = true
button.Parent = gui

local corner = Instance.new("UICorner")
corner.CornerRadius = UDim.new(0, 12)
corner.Parent = button

local stroke = Instance.new("UIStroke")
stroke.Color = Color3.fromRGB(160, 160, 170)
stroke.Thickness = 1.3
stroke.Parent = button

-- =====================================
-- PAINEL PRINCIPAL
-- =====================================

local panel = Instance.new("Frame")
panel.Name = "BKMainPanel"
panel.Size = UDim2.fromOffset(340, 310)
panel.Position = UDim2.new(0.5, -170, 0.5, -155)
panel.BackgroundColor3 = Color3.fromRGB(15, 20, 27)
panel.Visible = false
panel.Parent = gui

local panelCorner = Instance.new("UICorner")
panelCorner.CornerRadius = UDim.new(0, 14)
panelCorner.Parent = panel

local panelStroke = Instance.new("UIStroke")
panelStroke.Color = Color3.fromRGB(120, 220, 240)
panelStroke.Thickness = 1.5
panelStroke.Parent = panel

-- =====================================
-- BARRA LATERAL
-- =====================================

local sidebar = Instance.new("Frame")
sidebar.Name = "Sidebar"
sidebar.Size = UDim2.new(0, 105, 1, -16)
sidebar.Position = UDim2.new(0, 8, 0, 8)
sidebar.BackgroundColor3 = Color3.fromRGB(15, 65, 80)
sidebar.Parent = panel

local sidebarCorner = Instance.new("UICorner")
sidebarCorner.CornerRadius = UDim.new(0, 10)
sidebarCorner.Parent = sidebar

local sidebarStroke = Instance.new("UIStroke")
sidebarStroke.Color = Color3.fromRGB(100, 225, 245)
sidebarStroke.Thickness = 1.2
sidebarStroke.Parent = sidebar

-- =====================================
-- BOTÃO ID
-- =====================================

local idButton = Instance.new("TextButton")
idButton.Name = "IDButton"
idButton.Size = UDim2.fromOffset(85, 38)
idButton.Position = UDim2.new(0, 10, 0, 12)
idButton.BackgroundColor3 = Color3.fromRGB(10, 105, 130)
idButton.Text = "ID"
idButton.TextColor3 = Color3.fromRGB(230, 250, 255)
idButton.TextSize = 15
idButton.Font = Enum.Font.GothamBold
idButton.Parent = sidebar

local idCorner = Instance.new("UICorner")
idCorner.CornerRadius = UDim.new(0, 8)
idCorner.Parent = idButton

local idStroke = Instance.new("UIStroke")
idStroke.Color = Color3.fromRGB(150, 240, 255)
idStroke.Thickness = 1.2
idStroke.Parent = idButton

-- =====================================
-- ÁREA DE CONTEÚDO
-- =====================================

local content = Instance.new("Frame")
content.Name = "Content"
content.Size = UDim2.new(1, -130, 1, -16)
content.Position = UDim2.new(0, 122, 0, 8)
content.BackgroundColor3 = Color3.fromRGB(22, 30, 39)
content.Parent = panel

local contentCorner = Instance.new("UICorner")
contentCorner.CornerRadius = UDim.new(0, 10)
contentCorner.Parent = content

local contentStroke = Instance.new("UIStroke")
contentStroke.Color = Color3.fromRGB(100, 225, 245)
contentStroke.Thickness = 1
contentStroke.Parent = content

local title = Instance.new("TextLabel")
title.Size = UDim2.new(1, 0, 0, 35)
title.BackgroundTransparency = 1
title.Text = "BK MENU"
title.TextColor3 = Color3.fromRGB(180, 235, 245)
title.TextSize = 17
title.Font = Enum.Font.GothamBold
title.Parent = content

-- =====================================
-- ABRIR E FECHAR O PAINEL
-- =====================================

button.Activated:Connect(function()
    panel.Visible = not panel.Visible
end)

-- =====================================
-- ARRASTAR BOTÃO FLUTUANTE
-- =====================================

local dragging = false
local dragStart
local startPosition

button.InputBegan:Connect(function(input)
    if input.UserInputType == Enum.UserInputType.MouseButton1
    or input.UserInputType == Enum.UserInputType.Touch then

        dragging = true
        dragStart = input.Position
        startPosition = button.Position

        input.Changed:Connect(function()
            if input.UserInputState == Enum.UserInputState.End then
                dragging = false
            end
        end)
    end
end)

UserInputService.InputChanged:Connect(function(input)
    if dragging and (
        input.UserInputType == Enum.UserInputType.MouseMovement
        or input.UserInputType == Enum.UserInputType.Touch
    ) then

        local delta = input.Position - dragStart

        button.Position = UDim2.new(
            startPosition.X.Scale,
            startPosition.X.Offset + delta.X,
            startPosition.Y.Scale,
            startPosition.Y.Offset + delta.Y
        )
    end
end)
