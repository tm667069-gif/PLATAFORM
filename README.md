-- Cria o botão na tela
local player = game.Players.LocalPlayer
local screenGui = Instance.new("ScreenGui", player.PlayerGui)
screenGui.Name = "PlataformGui"

local button = Instance.new("TextButton", screenGui)
button.Position = UDim2.new(0.5, -75, 0.8, 0)
button.Size = UDim2.new(0, 150, 0, 50)
button.Text = "PLATAFORM"
button.BackgroundColor3 = Color3.fromRGB(0, 170, 255)
button.TextSize = 28
button.Font = Enum.Font.SourceSansBold

button.MouseButton1Click:Connect(function()
    local character = player.Character or player.CharacterAdded:Wait()
    local root = character:WaitForChild("HumanoidRootPart")

    -- Cria a plataforma embaixo do jogador
    local platform = Instance.new("Part")
    platform.Size = Vector3.new(6, 1, 6)
    platform.Position = root.Position - Vector3.new(0, 3, 0)
    platform.Anchored = true
    platform.BrickColor = BrickColor.new("Bright blue")
    platform.Parent = workspace

    -- Sobe a plataforma
    local targetHeight = root.Position.Y + 15
    local speed = 1
    while platform.Position.Y < targetHeight do
        platform.Position = platform.Position + Vector3.new(0, speed, 0)
        wait(0.02)
    end

    -- Opcional: destruir plataforma após alguns segundos
    wait(4)
    platform:Destroy()
end)
