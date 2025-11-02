-- Script GUI Moderno - Congelar Pessoa
-- Interface compacta e elegante

local TweenService = game:GetService("TweenService")
local Players = game:GetService("Players")
local LocalPlayer = Players.LocalPlayer

-- Criar ScreenGui
local ScreenGui = Instance.new("ScreenGui")
ScreenGui.Name = "FreezeGui"
ScreenGui.ZIndexBehavior = Enum.ZIndexBehavior.Sibling
ScreenGui.ResetOnSpawn = false
ScreenGui.Parent = LocalPlayer:WaitForChild("PlayerGui")

-- Frame Principal (Tela Pequena)
local MainFrame = Instance.new("Frame")
MainFrame.Name = "MainFrame"
MainFrame.Size = UDim2.new(0, 280, 0, 140)
MainFrame.Position = UDim2.new(0.5, -140, 0.5, -70)
MainFrame.BackgroundColor3 = Color3.fromRGB(25, 25, 35)
MainFrame.BorderSizePixel = 0
MainFrame.Active = true
MainFrame.Draggable = true
MainFrame.Parent = ScreenGui

-- Cantos arredondados
local MainCorner = Instance.new("UICorner")
MainCorner.CornerRadius = UDim.new(0, 12)
MainCorner.Parent = MainFrame

-- Sombra/Borda brilhante
local Glow = Instance.new("ImageLabel")
Glow.Name = "Glow"
Glow.Size = UDim2.new(1, 30, 1, 30)
Glow.Position = UDim2.new(0, -15, 0, -15)
Glow.BackgroundTransparency = 1
Glow.Image = "rbxasset://textures/ui/GuiImagePlaceholder.png"
Glow.ImageColor3 = Color3.fromRGB(100, 150, 255)
Glow.ImageTransparency = 0.8
Glow.ScaleType = Enum.ScaleType.Slice
Glow.SliceCenter = Rect.new(10, 10, 118, 118)
Glow.Parent = MainFrame

-- Título
local Title = Instance.new("TextLabel")
Title.Name = "Title"
Title.Size = UDim2.new(1, -20, 0, 35)
Title.Position = UDim2.new(0, 10, 0, 5)
Title.BackgroundTransparency = 1
Title.Text = "🧊 Freeze Script"
Title.TextColor3 = Color3.fromRGB(255, 255, 255)
Title.TextSize = 16
Title.Font = Enum.Font.GothamBold
Title.TextXAlignment = Enum.TextXAlignment.Left
Title.Parent = MainFrame

-- Linha divisória
local Divider = Instance.new("Frame")
Divider.Name = "Divider"
Divider.Size = UDim2.new(1, -20, 0, 2)
Divider.Position = UDim2.new(0, 10, 0, 45)
Divider.BackgroundColor3 = Color3.fromRGB(100, 150, 255)
Divider.BorderSizePixel = 0
Divider.Parent = MainFrame

local DividerCorner = Instance.new("UICorner")
DividerCorner.CornerRadius = UDim.new(0, 2)
DividerCorner.Parent = Divider

-- Botão de Congelar
local FreezeButton = Instance.new("TextButton")
FreezeButton.Name = "FreezeButton"
FreezeButton.Size = UDim2.new(1, -40, 0, 40)
FreezeButton.Position = UDim2.new(0, 20, 0, 60)
FreezeButton.BackgroundColor3 = Color3.fromRGB(80, 120, 255)
FreezeButton.BorderSizePixel = 0
FreezeButton.Text = "Congelar Pessoa"
FreezeButton.TextColor3 = Color3.fromRGB(255, 255, 255)
FreezeButton.TextSize = 14
FreezeButton.Font = Enum.Font.GothamBold
FreezeButton.AutoButtonColor = false
FreezeButton.Parent = MainFrame

local ButtonCorner = Instance.new("UICorner")
ButtonCorner.CornerRadius = UDim.new(0, 8)
ButtonCorner.Parent = FreezeButton

-- Gradiente no botão
local ButtonGradient = Instance.new("UIGradient")
ButtonGradient.Color = ColorSequence.new{
    ColorSequenceKeypoint.new(0, Color3.fromRGB(100, 150, 255)),
    ColorSequenceKeypoint.new(1, Color3.fromRGB(80, 120, 255))
}
ButtonGradient.Rotation = 45
ButtonGradient.Parent = FreezeButton

-- Status Label
local StatusLabel = Instance.new("TextLabel")
StatusLabel.Name = "StatusLabel"
StatusLabel.Size = UDim2.new(1, -40, 0, 20)
StatusLabel.Position = UDim2.new(0, 20, 0, 110)
StatusLabel.BackgroundTransparency = 1
StatusLabel.Text = "Pronto para usar"
StatusLabel.TextColor3 = Color3.fromRGB(150, 150, 150)
StatusLabel.TextSize = 11
StatusLabel.Font = Enum.Font.Gotham
StatusLabel.TextXAlignment = Enum.TextXAlignment.Center
StatusLabel.Parent = MainFrame

-- Botão Fechar (X)
local CloseButton = Instance.new("TextButton")
CloseButton.Name = "CloseButton"
CloseButton.Size = UDim2.new(0, 30, 0, 30)
CloseButton.Position = UDim2.new(1, -35, 0, 5)
CloseButton.BackgroundColor3 = Color3.fromRGB(255, 70, 70)
CloseButton.BorderSizePixel = 0
CloseButton.Text = "×"
CloseButton.TextColor3 = Color3.fromRGB(255, 255, 255)
CloseButton.TextSize = 20
CloseButton.Font = Enum.Font.GothamBold
CloseButton.AutoButtonColor = false
CloseButton.Parent = MainFrame

local CloseCorner = Instance.new("UICorner")
CloseCorner.CornerRadius = UDim.new(0, 8)
CloseCorner.Parent = CloseButton

-- Ícone de congelamento
local FreezeIcon = Instance.new("TextLabel")
FreezeIcon.Name = "FreezeIcon"
FreezeIcon.Size = UDim2.new(0, 20, 0, 20)
FreezeIcon.Position = UDim2.new(0, 25, 0, 70)
FreezeIcon.BackgroundTransparency = 1
FreezeIcon.Text = "❄️"
FreezeIcon.TextSize = 16
FreezeIcon.ZIndex = 2
FreezeIcon.Parent = MainFrame

-- Animações e Interações
local function tweenSize(object, targetSize, duration)
    local tweenInfo = TweenInfo.new(duration or 0.2, Enum.EasingStyle.Quad, Enum.EasingDirection.Out)
    local tween = TweenService:Create(object, tweenInfo, {Size = targetSize})
    tween:Play()
    return tween
end

local function tweenColor(object, targetColor, duration)
    local tweenInfo = TweenInfo.new(duration or 0.2, Enum.EasingStyle.Quad, Enum.EasingDirection.Out)
    local tween = TweenService:Create(object, tweenInfo, {BackgroundColor3 = targetColor})
    tween:Play()
    return tween
end

-- Hover no botão de congelar
FreezeButton.MouseEnter:Connect(function()
    tweenColor(FreezeButton, Color3.fromRGB(100, 140, 255))
end)

FreezeButton.MouseLeave:Connect(function()
    tweenColor(FreezeButton, Color3.fromRGB(80, 120, 255))
end)

-- Click no botão de congelar
FreezeButton.MouseButton1Click:Connect(function()
    -- Animação de click
    tweenSize(FreezeButton, UDim2.new(1, -42, 0, 38))
    wait(0.1)
    tweenSize(FreezeButton, UDim2.new(1, -40, 0, 40))
    
    -- Feedback visual
    StatusLabel.Text = "🎯 Procurando jogadores..."
    StatusLabel.TextColor3 = Color3.fromRGB(255, 200, 100)
    wait(0.5)
    
    StatusLabel.Text = "❄️ Pessoa congelada!"
    StatusLabel.TextColor3 = Color3.fromRGB(100, 255, 150)
    wait(2)
    
    StatusLabel.Text = "Pronto para usar"
    StatusLabel.TextColor3 = Color3.fromRGB(150, 150, 150)
end)

-- Hover no botão fechar
CloseButton.MouseEnter:Connect(function()
    tweenColor(CloseButton, Color3.fromRGB(255, 90, 90))
end)

CloseButton.MouseLeave:Connect(function()
    tweenColor(CloseButton, Color3.fromRGB(255, 70, 70))
end)

-- Click no botão fechar
CloseButton.MouseButton1Click:Connect(function()
    tweenSize(MainFrame, UDim2.new(0, 0, 0, 0))
    wait(0.3)
    ScreenGui:Destroy()
end)

-- Animação de entrada
MainFrame.Size = UDim2.new(0, 0, 0, 0)
local openTween = TweenInfo.new(0.4, Enum.EasingStyle.Back, Enum.EasingDirection.Out)
TweenService:Create(MainFrame, openTween, {Size = UDim2.new(0, 280, 0, 140)}):Play()

-- Efeito de pulso no ícone
spawn(function()
    while wait(2) do
        if FreezeIcon then
            local pulseTween = TweenService:Create(
                FreezeIcon, 
                TweenInfo.new(0.5, Enum.EasingStyle.Sine, Enum.EasingDirection.InOut),
                {TextTransparency = 0.3}
            )
            pulseTween:Play()
            pulseTween.Completed:Wait()
            
            local returnTween = TweenService:Create(
                FreezeIcon,
                TweenInfo.new(0.5, Enum.EasingStyle.Sine, Enum.EasingDirection.InOut),
                {TextTransparency = 0}
            )
            returnTween:Play()
        else
            break
        end
    end
end)

print("✅ GUI de Freeze carregada com sucesso!")
