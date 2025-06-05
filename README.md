local ScreenGui = Instance.new("ScreenGui")
ScreenGui.Parent = game.CoreGui

local Frame = Instance.new("Frame")
Frame.Size = UDim2.new(0, 200, 0, 100)
Frame.Position = UDim2.new(0.5, -100, 0.5, -50)
Frame.BackgroundColor3 = Color3.new(0, 0, 1) -- Azul
Frame.Parent = ScreenGui

local Button = Instance.new("TextButton")
Button.Size = UDim2.new(0, 150, 0, 30)
Button.Position = UDim2.new(0.5, -75, 0.5, -15)
Button.Text = "AUTO LEVEL"
Button.Parent = Frame

-- Variáveis para controlar o auto level
local autoLevelAtivo = false

-- Função para auto level
local function autoLevel()
    while autoLevelAtivo do
        -- Coloque aqui o código para fazer o personagem subir de level
        -- Por exemplo:
        game:GetService("Players").LocalPlayer.Character.Humanoid.MaxHealth = math.huge
        game:GetService("Players").LocalPlayer.Character.Humanoid.Health = math.huge
        wait(1)
    end
end

-- Ativar o auto level quando o botão for pressionado
Button.MouseButton1Click:Connect(function()
    if Button.Text == "AUTO LEVEL" then
        Button.Text = "PARAR AUTO LEVEL"
        autoLevelAtivo = true
        spawn(autoLevel)
    else
        Button.Text = "AUTO LEVEL"
        autoLevelAtivo = false
    end
end)

-- Fazer a interface se mover na tela
local velocidade = 2
local direcao = 1
game:GetService("RunService").RenderStepped:Connect(function(dt)
    Frame.Position = Frame.Position + UDim2.new(0, velocidade * direcao * dt, 0, 0)
    if Frame.Position.X.Offset > 400 or Frame.Position.X.Offset < -200 then
        direcao = direcao * -1
    end
end)
