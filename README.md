# -Tridentes-hunter
-- Auto Farm Script para Blox Fruits
local player = game.Players.LocalPlayer
local character = player.Character or player.CharacterAdded:Wait()
local humanoidRootPart = character:WaitForChild("HumanoidRootPart")

-- Função para teleportar o jogador
function teleportTo(position)
    humanoidRootPart.CFrame = CFrame.new(position)
end

-- Função para atacar inimigos
function attackEnemy(enemy)
    while enemy and enemy.Parent do
        humanoidRootPart.CFrame = enemy.HumanoidRootPart.CFrame
        game:GetService("VirtualUser"):CaptureController()
        game:GetService("VirtualUser"):Button1Down(Vector2.new(0,0), workspace.CurrentCamera.CFrame)
        wait(0.1)
    end
end

-- Loop principal para farmar
while true do
    for _, enemy in pairs(workspace.Enemies:GetChildren()) do
        if enemy:FindFirstChild("HumanoidRootPart") then
            teleportTo(enemy.HumanoidRootPart.Position)
            attackEnemy(enemy)
        end
    end
    wait(1)
end
