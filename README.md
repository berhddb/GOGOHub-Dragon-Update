local World1, World2, World3 = false, false, false

if game.PlaceId == 2753915549 then
    World1 = true
elseif game.PlaceId == 4442272183 then
    World2 = true
elseif game.PlaceId == 7449423635 then
    World3 = true
else
    game:GetService("Players").LocalPlayer:Kick("Do not Support, Please wait...")
end

local Rayfield = loadstring(game:HttpGet('https://sirius.menu/rayfield'))()

local Window = Rayfield:CreateWindow({
    Name = "GOGO HUB | DRAGON UPDATE",
    LoadingTitle = "GOGO Hub",
    LoadingSubtitle = "by berhddb",
    ConfigurationSaving = {
        Enabled = true,
        FolderName = nil,
        FileName = 'GOGO Hub'
    },
    KeySystem = true,
    KeySettings = {
        Title = "GOGO Hub | Key",
        Subtitle = "Key System",
        Note = "Não há nenhum método para obter a key",
        FileName = "gogohubkey",
        SaveKey = true,
        GrabKeyFromSite = false,
        Key = {"berzin"}
    }
})

-- Abas especificadas
local GeneralTab = Window:CreateTab("General", nil)
local EspTab = Window:CreateTab("Esp", nil)
local FruitsTab = Window:CreateTab("Fruits", nil)
local MirageTab = Window:CreateTab("Mirage", nil)
local PvpTab = Window:CreateTab("PVP", nil)
local DragonTab = Window:CreateTab("Dragon", nil)
local TeleportTab = Window:CreateTab("Teleport", nil)

-- Função de Auto Farm (Placeholder)
GeneralTab:CreateToggle({
    Name = "Auto Farm",
    CurrentValue = false,
    Flag = "autoFarm",
    Callback = function(Value)
        if Value then
            -- Adicionar lógica de auto farm
        end
    end
})

-- Variável para controlar o estado do ESP
local espEnabled = {
    players = false,
    fruits = false,
    advancedNPC = false
}

-- Função para criar ESP
local function createESP(object, color, text)
    if not object:FindFirstChild("ESP") then
        local billboardGui = Instance.new("BillboardGui", object)
        billboardGui.Name = "ESP"
        billboardGui.Size = UDim2.new(0, 200, 0, 50)
        billboardGui.StudsOffset = Vector3.new(0, 2, 0)
        billboardGui.AlwaysOnTop = true

        local textLabel = Instance.new("TextLabel", billboardGui)
        textLabel.Size = UDim2.new(1, 0, 1, 0)
        textLabel.BackgroundTransparency = 1
        textLabel.Text = text
        textLabel.TextColor3 = color
        textLabel.TextStrokeTransparency = 0.5
        textLabel.TextScaled = true
    else
        object.ESP.TextLabel.Text = text
    end
end

-- Função para remover ESP
local function removeESP(object)
    if object:FindFirstChild("ESP") then
        object.ESP:Destroy()
    end
end

-- Função para atualizar o ESP de jogadores
local function updatePlayerESP()
    for _, player in pairs(game.Players:GetPlayers()) do
        if player.Character and player.Character:FindFirstChild("HumanoidRootPart") and player ~= game.Players.LocalPlayer then
            local distance = math.floor((game.Players.LocalPlayer.Character.HumanoidRootPart.Position - player.Character.HumanoidRootPart.Position).Magnitude)
            if espEnabled.players then
                createESP(player.Character.HumanoidRootPart, Color3.fromRGB(0, 255, 0), player.Name .. " [" .. distance .. "m]")
            else
                removeESP(player.Character.HumanoidRootPart)
            end
        end
    end
end

-- Função para atualizar o ESP de frutas
local function updateFruitESP()
    for _, fruit in pairs(game.Workspace:GetChildren()) do
        if fruit:IsA("Tool") and fruit:FindFirstChild("Handle") then
            local distance = math.floor((game.Players.LocalPlayer.Character.HumanoidRootPart.Position - fruit.Handle.Position).Magnitude)
            if espEnabled.fruits then
                createESP(fruit.Handle, Color3.fromRGB(255, 165, 0), fruit.Name .. " [" .. distance .. "m]")
            else
                removeESP(fruit.Handle)
            end
        end
    end
end

-- Função para atualizar o ESP do Advanced Fruit Dealer
local function updateAdvancedNPCESP()
    local npc = game.Workspace.NPCs:FindFirstChild("Advanced Fruit Dealer")
    if npc and npc:FindFirstChild("HumanoidRootPart") then
        local distance = math.floor((game.Players.LocalPlayer.Character.HumanoidRootPart.Position - npc.HumanoidRootPart.Position).Magnitude)
        if espEnabled.advancedNPC then
            createESP(npc.HumanoidRootPart, Color3.fromRGB(255, 0, 0), "Advanced Fruit Dealer [" .. distance .. "m]")
        else
            removeESP(npc.HumanoidRootPart)
        end
    end
end

-- Toggle do ESP na aba Esp
EspTab:CreateToggle({
    Name = "ESP Players",
    CurrentValue = false,
    Flag = "espPlayers",
    Callback = function(Value)
        espEnabled.players = Value
        if not Value then
            for _, player in pairs(game.Players:GetPlayers()) do
                if player.Character and player.Character:FindFirstChild("HumanoidRootPart") then
                    removeESP(player.Character.HumanoidRootPart)
                end
            end
        end
        updatePlayerESP()
    end
})

EspTab:CreateToggle({
    Name = "ESP Fruits",
    CurrentValue = false,
    Flag = "espFruits",
    Callback = function(Value)
        espEnabled.fruits = Value
        if not Value then
            for _, fruit in pairs(game.Workspace:GetChildren()) do
                if fruit:IsA("Tool") and fruit:FindFirstChild("Handle") then
                    removeESP(fruit.Handle)
                end
            end
        end
        updateFruitESP()
    end
})

-- Toggle do ESP na aba Mirage
MirageTab:CreateToggle({
    Name = "ESP Advanced NPC Dealer",
    CurrentValue = false,
    Flag = "espAdvancedNPC",
    Callback = function(Value)
        espEnabled.advancedNPC = Value
        if not Value then
            local npc = game.Workspace.NPCs:FindFirstChild("Advanced Fruit Dealer")
            if npc then
                removeESP(npc:FindFirstChild("HumanoidRootPart"))
            end
        end
        updateAdvancedNPCESP()
    end
})

-- Conexão com o RunService para verificar constantemente o estado do ESP
game:GetService("RunService").Heartbeat:Connect(function()
    if espEnabled.players then
        updatePlayerESP()
    end
    if espEnabled.fruits then
        updateFruitESP()
    end
    if espEnabled.advancedNPC then
        updateAdvancedNPCESP()
    end
end)

-- Função para encontrar o jogador mais próximo
local function getClosestPlayer()
    local closestPlayer = nil
    local shortestDistance = math.huge -- Inicia com o valor mais alto possível

    for _, player in pairs(game.Workspace.Characters:GetChildren()) do
        if player:FindFirstChild("HumanoidRootPart") and player ~= game.Players.LocalPlayer.Character then
            local distance = (game.Players.LocalPlayer.Character.HumanoidRootPart.Position - player.HumanoidRootPart.Position).Magnitude
            if distance < shortestDistance then
                shortestDistance = distance
                closestPlayer = player
            end
        end
    end

    return closestPlayer
end

-- Variável para controlar o estado do aimbot
local aimbotEnabled = false
local aimbotActive = false

-- Função para ativar o Aimbot
local function aimbot()
    -- Verifica se o aimbot está ativado e ativo
    if aimbotEnabled and aimbotActive then
        local closestPlayer = getClosestPlayer()

        if closestPlayer and closestPlayer:FindFirstChild("HumanoidRootPart") then
            -- Faz o mouse seguir o jogador mais próximo
            local player = game.Players.LocalPlayer
            local camera = game.Workspace.CurrentCamera
            local playerPos = player.Character.HumanoidRootPart.Position
            local closestPos = closestPlayer.HumanoidRootPart.Position

            -- Calcula a direção entre o jogador e o alvo mais próximo
            local direction = (closestPos - playerPos).unit
            local lookAtPos = playerPos + direction * 1000

            -- Faz a câmera olhar para o alvo mais próximo
            camera.CFrame = CFrame.new(camera.CFrame.Position, lookAtPos)
        end
    end
end

-- Toggle do Aimbot na aba PVP
PvpTab:CreateToggle({
    Name = "Aimbot",
    CurrentValue = false,
    Flag = "aimbot",
    Callback = function(Value)
        aimbotEnabled = Value
        if not aimbotEnabled then
            aimbotActive = false  -- Desativa o aimbot se o toggle for desligado
        end
    end
})

-- Função de controle para a tecla G
game:GetService("UserInputService").InputBegan:Connect(function(input, gameProcessed)
    if gameProcessed then return end

    if input.KeyCode == Enum.KeyCode.G and aimbotEnabled then
        aimbotActive = not aimbotActive
        Rayfield:Notify({
            Title = aimbotActive and "Aimbot Ativado" or "Aimbot Desativado",
            Content = aimbotActive and "O Aimbot está agora ativado!" or "O Aimbot foi desativado!",
            Duration = 3
        })
    end
end)

-- Conexão com o RunService para verificar constantemente o estado do aimbot
game:GetService("RunService").Heartbeat:Connect(function()
    aimbot() -- Chama a função de aimbot
end)

-- Opção "Change to draco race" na aba Dragon
DragonTab:CreateButton({
    Name = "Change to draco race",
    Callback = function()
        local player = game.Players.LocalPlayer
        if player.Data.Race.Value ~= "Draco" then
            player.Data.Race.Value = "Draco"
            Rayfield:Notify({
                Title = "Raça Alterada",
                Content = "Você agora pertence à raça Draco!",
                Duration = 3
            })
        else
            Rayfield:Notify({
                Title = "Já é Draco",
                Content = "Você já pertence à raça Draco.",
                Duration = 3
            })
        end
    end
})

-- Função para coletar frutas
local collectFruitsEnabled = false

local function collectFruits()
    local player = game.Players.LocalPlayer
    local character = player.Character
    local humanoidRootPart = character:FindFirstChild("HumanoidRootPart")

    while collectFruitsEnabled do
        local foundFruit = false
        for _, fruit in pairs(game.Workspace:GetChildren()) do
            if fruit:IsA("Tool") and fruit:FindFirstChild("Handle") then
                foundFruit = true
                -- Move player to the fruit with dynamic tween speed based on distance
                local distance = (humanoidRootPart.Position - fruit.Handle.Position).Magnitude
                local tweenSpeed = 7 + (distance / 2000) * 2
                local goal = {}
                goal.CFrame = CFrame.new(fruit.Handle.Position)
                local tween = game:GetService("TweenService"):Create(humanoidRootPart, TweenInfo.new(tweenSpeed), goal)
                tween:Play()
                tween.Completed:Wait()
                if not collectFruitsEnabled then break end
            end
        end
        if not foundFruit then
            wait(1) -- Espera um segundo antes de verificar novamente
        end
    end
end

-- Toggle para coletar frutas na aba Fruits
FruitsTab:CreateToggle({
    Name = "Collect Fruit",
    CurrentValue = false,
    Flag = "collectFruits",
    Callback = function(Value)
        collectFruitsEnabled = Value
        if collectFruitsEnabled then
            collectFruits()
        end
    end
})

-- Notificar jogador quando uma nova fruta aparecer
game.Workspace.ChildAdded:Connect(function(child)
    if child:IsA("Tool") and child:FindFirstChild("Handle") then
        Rayfield:Notify({
            Title = "Fruta Spawned!",
            Content = child.Name .. " foi gerada!",
            Duration = 5
        })
        collectFruits()
    end
end)

-- Finalização do script
Rayfield:Notify({
    Title = "Script Carregado",
    Content = "O script foi carregado corretamente!",
    Duration = 5
})
