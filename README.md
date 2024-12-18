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
        Note = "The key is: berzin",
        FileName = "gogohubkey",
        SaveKey = true,
        GrabKeyFromSite = false,
        Key = {"berzin"}
    }
})

-- Abas especificadas
local GeneralTab = Window:CreateTab("General", 'construction')
local EspTab = Window:CreateTab("Esp", "eye")
local FruitsTab = Window:CreateTab("Fruits", "apple")
local MirageTab = Window:CreateTab("Mirage", "tree-palm")
local PvpTab = Window:CreateTab("PVP", "swords")
local RaidTab = Window:CreateTab("Raid", "skull")
local DragonTab = Window:CreateTab("Dragon", "egg")
local TeleportTab = Window:CreateTab("Teleport", 4483362458)
local MiscTab = Window:CreateTab("Misc", "user-cog")
------------- General


-- Adicionando o toggle para Auto Farm
local ToggleAutoFarm = GeneralTab:CreateToggle({
    Name = "Auto Farm",
    CurrentValue = false,
    Flag = "ToggleAutoFarm",
    Callback = function(Value)
        _G.AutoFarm = Value
    end,
})

-- Loop para executar o auto farm com base no valor do toggle
spawn(function()
    while wait(0.1) do
        if _G.AutoFarm then
            
        end
    end
end)



---------Tween

  function Tween2(P1)
    local Distance = (P1.Position - game.Players.LocalPlayer.Character.HumanoidRootPart.Position).Magnitude
    if Distance >= 1 then
    Speed = 300
    end
    game:GetService("TweenService"):Create(game.Players.LocalPlayer.Character.HumanoidRootPart,TweenInfo.new(Distance/Speed, Enum.EasingStyle.Linear), {
      CFrame = P1
    }):Play()
    if _G.CancelTween2 then
    game:GetService("TweenService"):Create(game.Players.LocalPlayer.Character.HumanoidRootPart,TweenInfo.new(Distance/Speed, Enum.EasingStyle.Linear), {
      CFrame = P1
    }):Cancel()
    end
    _G.Clip2 = true
    wait(Distance/Speed)
    _G.Clip2 = false
    end
   
-- [Function (Abandoned Quest , Others)]

function Com(com,...)
	local Remote = game:GetService('ReplicatedStorage').Remotes:FindFirstChild("Comm"..com)
	if Remote:IsA("RemoteEvent") then
		Remote:FireServer(...)
	elseif Remote:IsA("RemoteFunction") then
		Remote:InvokeServer(...)
	end
end

--BTP
function BTP(Position)
	game.Players.LocalPlayer.Character.Head:Destroy()
	game.Players.LocalPlayer.Character.HumanoidRootPart.CFrame = Position
	wait(0.5)
	game.Players.LocalPlayer.Character.HumanoidRootPart.CFrame = Position
	game:GetService("ReplicatedStorage").Remotes.CommF_:InvokeServer("SetSpawnPoint")
end
--BTPZ
function BTPZ(Point)
    game.Players.LocalPlayer.Character.HumanoidRootPart.CFrame = Point
    task.wait()
    game.Players.LocalPlayer.Character.HumanoidRootPart.CFrame = Point
        end
------Bypass TP 2
 function GetIsLand(...)
	local RealtargetPos = {...}
	local targetPos = RealtargetPos[1]
	local RealTarget
	if type(targetPos) == "vector" then
		RealTarget = targetPos
	elseif type(targetPos) == "userdata" then
		RealTarget = targetPos.Position
	elseif type(targetPos) == "number" then
		RealTarget = CFrame.new(unpack(RealtargetPos))
		RealTarget = RealTarget.p
	end

	local ReturnValue
	local CheckInOut = math.huge;
	if game.Players.LocalPlayer.Team then
		for i,v in pairs(game.Workspace._WorldOrigin.PlayerSpawns:FindFirstChild(tostring(game.Players.LocalPlayer.Team)):GetChildren()) do 
			local ReMagnitude = (RealTarget - v:GetModelCFrame().p).Magnitude;
			if ReMagnitude < CheckInOut then
				CheckInOut = ReMagnitude;
				ReturnValue = v.Name
			end
		end
		if ReturnValue then
			return ReturnValue
		end 
    end
end


   function toTarget(...)
    local RealtargetPos = { ... }
    local targetPos = RealtargetPos[1]
    local RealTarget
    if type(targetPos) == "vector" then
        RealTarget = CFrame.new(targetPos)
    elseif type(targetPos) == "userdata" then
        RealTarget = targetPos
    elseif type(targetPos) == "number" then
        RealTarget = CFrame.new(unpack(RealtargetPos))
    end
    if game.Players.LocalPlayer.Character:WaitForChild("Humanoid").Health == 0 then
        if tween then tween:Cancel() end
        repeat wait() until game.Players.LocalPlayer.Character:WaitForChild("Humanoid").Health > 0; wait(0.2)
    end
    local tweenfunc = {}
    local Distance = (RealTarget.Position - game:GetService("Players").LocalPlayer.Character:WaitForChild("HumanoidRootPart").Position)
        .Magnitude
    if Distance < 1000 then
        Speed = 315
    elseif Distance >= 1000 then
        Speed = 300
    end
    if BypassTP then
        if Distance > 3000 and not AutoNextIsland and not (game.Players.LocalPlayer.Backpack:FindFirstChild("Special Microchip") or game.Players.LocalPlayer.Character:FindFirstChild("Special Microchip") or game.Players.LocalPlayer.Backpack:FindFirstChild("God's Chalice") or game.Players.LocalPlayer.Character:FindFirstChild("God's Chalice") or game.Players.LocalPlayer.Backpack:FindFirstChild("Hallow Essence") or game.Players.LocalPlayer.Character:FindFirstChild("Hallow Essence") or game.Players.LocalPlayer.Character:FindFirstChild("Sweet Chalice") or game.Players.LocalPlayer.Backpack:FindFirstChild("Sweet Chalice")) and not (Name == "Fishman Commando" or Name == "Fishman Warrior") then
            pcall(function()
                tween:Cancel()
                fkwarp = false
                if game:GetService("Players")["LocalPlayer"].Data:FindFirstChild("SpawnPoint").Value == tostring(GetIsLand(RealTarget)) then
                    wait(.1)
                    Com("F_", "TeleportToSpawn")
                elseif game:GetService("Players")["LocalPlayer"].Data:FindFirstChild("LastSpawnPoint").Value == tostring(GetIsLand(RealTarget)) then
                    game:GetService("Players").LocalPlayer.Character:WaitForChild("Humanoid"):ChangeState(15)
                    wait(0.1)
                    repeat wait() until game:GetService("Players").LocalPlayer.Character:WaitForChild("Humanoid").Health > 0
                else
                    if game:GetService("Players").LocalPlayer.Character:WaitForChild("Humanoid").Health > 0 then
                        if fkwarp == false then
                            game.Players.LocalPlayer.Character.HumanoidRootPart.CFrame = RealTarget
                        end
                        fkwarp = true
                    end
                    wait(.08)
                    game:GetService("Players").LocalPlayer.Character:WaitForChild("Humanoid"):ChangeState(15)
                    repeat wait() until game:GetService("Players").LocalPlayer.Character:WaitForChild("Humanoid").Health > 0
                    wait(.1)
                    Com("F_", "SetSpawnPoint")
                end
                wait(0.2)

                return
            end)
        end
    end

    local tween_s = game:service "TweenService"
    local info = TweenInfo.new(
        (RealTarget.Position - game:GetService("Players").LocalPlayer.Character:WaitForChild("HumanoidRootPart").Position)
        .Magnitude / Speed, Enum.EasingStyle.Linear)
    local tweenw, err = pcall(function()
        tween = tween_s:Create(game.Players.LocalPlayer.Character["HumanoidRootPart"], info, { CFrame = RealTarget })
        tween:Play()
    end)

    function tweenfunc:Stop()
        tween:Cancel()
    end

    function tweenfunc:Wait()
        tween.Completed:Wait()
    end

    return tweenfunc
end

------

function Tween(Pos)
    Distance = (Pos.Position - game.Players.LocalPlayer.Character.HumanoidRootPart.Position).Magnitude
    if game.Players.LocalPlayer.Character.Humanoid.Sit == true then game.Players.LocalPlayer.Character.Humanoid.Sit = false end
    pcall(function() tween = game:GetService("TweenService"):Create(game.Players.LocalPlayer.Character.HumanoidRootPart,TweenInfo.new(Distance/300, Enum.EasingStyle.Linear),{CFrame = Pos}) end)
    tween:Play()
    if Distance <= 300 then
        tween:Cancel()
        game.Players.LocalPlayer.Character.HumanoidRootPart.CFrame = Pos
    end
    if _G.StopTween == true then
        tween:Cancel()
        _G.Clip = false
    end
end


---------

function toTargetP(CFgo)
	if game.Players.LocalPlayer.Character:WaitForChild("Humanoid").Health <= 0 or not game:GetService("Players").LocalPlayer.Character:WaitForChild("Humanoid") then tween:Cancel() repeat wait() until game:GetService("Players").LocalPlayer.Character:WaitForChild("Humanoid") and game:GetService("Players").LocalPlayer.Character:WaitForChild("Humanoid").Health > 0 wait(7) return end
	if (game:GetService("Players")["LocalPlayer"].Character.HumanoidRootPart.Position - CFgo.Position).Magnitude <= 150 then
		pcall(function()
			tween:Cancel()

			game:GetService("Players")["LocalPlayer"].Character.HumanoidRootPart.CFrame = CFgo

			return
		end)
	end
	local tween_s = game:service"TweenService"
	local info = TweenInfo.new((game:GetService("Players")["LocalPlayer"].Character.HumanoidRootPart.Position - CFgo.Position).Magnitude/325, Enum.EasingStyle.Linear)
	tween = tween_s:Create(game.Players.LocalPlayer.Character["HumanoidRootPart"], info, {CFrame = CFgo})
	tween:Play()

	local tweenfunc = {}

	function tweenfunc:Stop()
		tween:Cancel()
	end

	return tweenfunc
end

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
    Callback = function
    (Value)
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

-- Notificar jogador quando uma nova fruta aparecer
game.Workspace.ChildAdded:Connect(function(child)
    if child:IsA("Tool") and child:FindFirstChild("Handle") then
        Rayfield:Notify({
            Title = "Fruta Spawned!",
            Content = child.Name .. " foi gerada!",
            Duration = 5
        })
    end
end)

-- Variável para ativar/desativar o Auto Haki
local autoHakiEnabled = false

-- Função para ativar o Buso Haki
local function AutoHaki()
    if not game:GetService("Players").LocalPlayer.Character:FindFirstChild("HasBuso") then
        game:GetService("ReplicatedStorage").Remotes.CommF_:InvokeServer("Buso")
    end
end

-- Função para verificar e ativar o Buso Haki continuamente se desativado
local function checkHaki()
    while autoHakiEnabled do
        pcall(function()
            AutoHaki()
        end)
        wait(1) -- Verificar a cada 1 segundo
    end
end

-- Botão para ativar/desativar o Auto Haki na aba Misc
MiscTab:CreateToggle({
    Name = "Auto Haki",
    CurrentValue = false,
    Flag = "autoHaki",
    Callback = function(Value)
        autoHakiEnabled = Value
        if autoHakiEnabled then
            checkHaki()
        end
    end
})

-- Função para obter a textura da lua
local function MoonTextureId()
    if World1 then
        return game:GetService("Lighting").FantasySky.MoonTextureId
    elseif World2 then
        return game:GetService("Lighting").FantasySky.MoonTextureId
    elseif World3 then
        return game:GetService("Lighting").Sky.MoonTextureId
    end
end

-- Função para verificar o estado da lua
local function CheckMoon()
    local moon8 = "http://www.roblox.com/asset/?id=9709150401"
    local moon7 = "http://www.roblox.com/asset/?id=9709150086"
    local moon6 = "http://www.roblox.com/asset/?id=9709149680"
    local moon5 = "http://www.roblox.com/asset/?id=9709149431"
    local moon4 = "http://www.roblox.com/asset/?id=9709149052"
    local moon3 = "http://www.roblox.com/asset/?id=9709143733"
    local moon2 = "http://www.roblox.com/asset/?id=9709139597"
    local moon1 = "http://www.roblox.com/asset/?id=9709135895"
    local moonreal = MoonTextureId()
    local cofullmoonkothangbeo = "Lua ruim"

    if moonreal == moon5 or moonreal == moon4 then
        if moonreal == moon5 then
            cofullmoonkothangbeo = "Está lua"
        elseif moonreal == moon4 then
            cofullmoonkothangbeo = "Próxima lua"
      elseif moonreal == moon3 then
            cofullmoonkothangbeo = "2 Luas"
    elseif moonreal == moon2 then
         cofullmoonkothangbeo = "3 Luas"
        end
    end
    return cofullmoonkothangbeo, moonreal
end

-- Botão para verificar a lua na aba Misc
MiscTab:CreateButton({
    Name = "Check Moon",
    Callback = function()
        local moonState, moonName = CheckMoon()
        Rayfield:Notify({
            Title = "Estado da Lua",
            Content = "O estado para lua cheia é: " .. moonState,
            Duration = 6.5
        })
    end
})

local TabDivider = RaidTab:CreateSection("Select Chip")

local Chips = {"Flame", "Ice", "Quake", "Light", "Dark", "Spider", "Rumble", "Magma", "Buddha", "Sand", "Phoenix", "Dough"}

-- Função para criar botões para cada chip
for _, chip in ipairs(Chips) do
    RaidTab:CreateButton({
        Name = chip,
        Callback = function()
            SelectChip = chip
            game.StarterGui:SetCore("SendNotification", {
                Title = "Chip Selection",
                Text = "Selected Chip: " .. chip,
                Duration = 5
            })
        end,
    })
end

-- Toggle para comprar o chip
local ToggleBuy = RaidTab:CreateToggle({
    Name = "Auto Buy Chip",
    CurrentValue = false,
    Flag = "ToggleBuy",
    Callback = function(Value)
        if SelectChip then
            _G.Auto_Buy_Chips_Dungeon = Value
        else
            game.StarterGui:SetCore("SendNotification", {
                Title = "Warning",
                Text = "No chip selected!",
                Duration = 5
            })
        end
    end,
})

spawn(function()
    while wait() do
        if _G.Auto_Buy_Chips_Dungeon and SelectChip then
            pcall(function()
                local args = {
                    [1] = "RaidsNpc",
                    [2] = "Select",
                    [3] = SelectChip
                }
                game:GetService("ReplicatedStorage").Remotes.CommF_:InvokeServer(unpack(args))
            end)
        end
    end
end)

local TabDivider = RaidTab:CreateDivider()
local TabSection = RaidTab:CreateSection("Raid")

spawn(function()
    while wait() do
        if _G.Auto_Buy_Chips_Dungeon then
            pcall(function()
                local args = {
                    [1] = "RaidsNpc",
                    [2] = "Select",
                    [3] = SelectChip
                }
                game:GetService("ReplicatedStorage").Remotes.CommF_:InvokeServer(unpack(args))
            end)
        end
    end
end)

-- Toggle para iniciar o raid
local ToggleStart = RaidTab:CreateToggle({
    Name = "Start Raid",
    CurrentValue = false,
    Flag = "ToggleStart",
    Callback = function(Value)
        _G.Auto_StartRaid = Value
    end,
})

spawn(function()
    while wait(0.1) do
        pcall(function()
            if _G.Auto_StartRaid then
                if game:GetService("Players").LocalPlayer.PlayerGui.Main.Timer.Visible == false then
                    if not game:GetService("Workspace")["_WorldOrigin"].Locations:FindFirstChild("Island 1") and (game:GetService("Players").LocalPlayer.Backpack:FindFirstChild("Special Microchip") or game:GetService("Players").LocalPlayer.Character:FindFirstChild("Special Microchip")) then
                        if World1 then
                            fireclickdetector(game:GetService("Workspace").Map.CircleIsland.RaidSummon2.Button.Main.ClickDetector)
                        elseif World3 then
                            fireclickdetector(game:GetService("Workspace").Map["Boat Castle"].RaidSummon2.Button.Main.ClickDetector)
                        end
                    end
                end
            end
        end)
    end
end)

-- Toggle para Kill Aura
local ToggleKillAura = RaidTab:CreateToggle({
    Name = "Kill Aura",
    CurrentValue = false,
    Flag = "ToggleKillAura",
    Callback = function(Value)
        KillAura = Value
    end,
})

spawn(function()
    while wait() do
        if KillAura then
            pcall(function()
                for i, v in pairs(game.Workspace.Enemies:GetDescendants()) do
                    if v:FindFirstChild("Humanoid") and v:FindFirstChild("HumanoidRootPart") and v.Humanoid.Health > 0 then
                        repeat task.wait()
                            sethiddenproperty(game:GetService('Players').LocalPlayer, "SimulationRadius", math.huge)
                            v.Humanoid.Health = 0
                            v.HumanoidRootPart.CanCollide = false
                        until not KillAura or not v.Parent or v.Humanoid.Health <= 0
                    end
                end
            end)
        end
    end
end)

local ToggleNextIsland = RaidTab:CreateToggle({
    Name = "Next Island",
    CurrentValue = false,
    Flag = "ToggleNextIsland",
    Callback = function(Value)
        AutoNextIsland = Value
    end,
})

spawn(function()
    while task.wait() do
        if AutoNextIsland then
            pcall(function()
                if game.Players.LocalPlayer.PlayerGui.Main.TopHUDList.RaidTimer.Visible == true then
                    if game:GetService("Workspace")["_WorldOrigin"].Locations:FindFirstChild("Island 5") then
                        Tween(game:GetService("Workspace")["_WorldOrigin"].Locations:FindFirstChild("Island 5").CFrame * CFrame.new(0, 70, 100))
                    elseif game:GetService("Workspace")["_WorldOrigin"].Locations:FindFirstChild("Island 4") then
                        Tween(game:GetService("Workspace")["_WorldOrigin"].Locations:FindFirstChild("Island 4").CFrame * CFrame.new(0, 70, 100))
                    elseif game:GetService("Workspace")["_WorldOrigin"].Locations:FindFirstChild("Island 3") then
                        Tween(game:GetService("Workspace")["_WorldOrigin"].Locations:FindFirstChild("Island 3").CFrame * CFrame.new(0, 70, 100))
                    elseif game:GetService("Workspace")["_WorldOrigin"].Locations:FindFirstChild("Island 2") then
                        Tween(game:GetService("Workspace")["_WorldOrigin"].Locations:FindFirstChild("Island 2").CFrame * CFrame.new(0, 70, 100))
                    elseif game:GetService("Workspace")["_WorldOrigin"].Locations:FindFirstChild("Island 1") then
                        Tween(game:GetService("Workspace")["_WorldOrigin"].Locations:FindFirstChild("Island 1").CFrame * CFrame.new(0, 70, 100))
                    end
                end
            end)
        end
    end
end)

-- Variável para ativar/desativar a caminhada sobre a água
local walkOnWaterEnabled = false

-- Adicionando o toggle para Walk on Water na aba Misc
MiscTab:CreateToggle({
    Name = "Walk on Water",
    CurrentValue = false,
    Flag = "walkOnWater",
    Callback = function(Value)
        walkOnWaterEnabled = Value
    end    
})

-- Função para ajustar a altura da água
local function adjustWaterHeight()
    while walkOnWaterEnabled do
        pcall(function()
            if walkOnWaterEnabled then
                game:GetService("Workspace").Map["WaterBase-Plane"].Size = Vector3.new(1000, 112, 1000)
            else
                game:GetService("Workspace").Map["WaterBase-Plane"].Size = Vector3.new(1000, 80, 1000)
            end
        end)
        wait(1) -- Ajustar a cada 1 segundo
    end
end

-- Iniciar o ajuste da água em uma nova thread
spawn(function()
    while true do
        if walkOnWaterEnabled then
            adjustWaterHeight()
        else
            pcall(function()
                game:GetService("Workspace").Map["WaterBase-Plane"].Size = Vector3.new(1000, 80, 1000)
            end)
        end
        wait(1)
    end
end)

local TabSection = TeleportTab:CreateSection("Sea Travel")

if World2 or World3 then
-- Adicionando os botões de teleporte
TeleportTab:CreateButton({
    Name = "First Sea",
    Description = "Sea 1",
    Callback = function()
        game:GetService("ReplicatedStorage").Remotes.CommF_:InvokeServer("TravelMain")
    end
})
end

if World3 or World1 then
TeleportTab:CreateButton({
    Name = "Second Sea",
    Description = "Sea 2",
    Callback = function()
        game:GetService("ReplicatedStorage").Remotes.CommF_:InvokeServer("TravelDressrosa")
    end
})
end

if World2 or World1 then
TeleportTab:CreateButton({
    Name = "Third Sea",
    Description = "Sea 3",
    Callback = function()
        game:GetService("ReplicatedStorage").Remotes.CommF_:InvokeServer("TravelZou")
    end
})
end

-- Seção de Teleport World
local TabDivider = TeleportTab:CreateDivider()
local TabSection = TeleportTab:CreateSection("Island Travel")

MiscTab:CreateButton({
    Name = "Redeem All Code",
        Callback = function()
            UseCode()
        end
    })

    function UseCode(Text)
        game:GetService("ReplicatedStorage").Remotes.Redeem:InvokeServer(Text)
    end
    UseCode("Sub2Fer999")
    UseCode("Enyu_is_Pro")
    UseCode("Magicbus")
    UseCode("JCWK")
    UseCode("Starcodeheo")
    UseCode("Bluxxy")
    UseCode("THEGREATACE")
    UseCode("SUB2GAMERROBOT_EXP1")
    UseCode("StrawHatMaine")
    UseCode("Sub2OfficialNoobie")
    UseCode("SUB2NOOBMASTER123")
    UseCode("Sub2Daigrock")
    UseCode("Axiore")
    UseCode("TantaiGaming")
    UseCode("STRAWHATMAINE")

-- Variável para ativar/desativar o Auto Store Fruit
local autoStoreFruitEnabled = false

-- Adicionando o toggle para Auto Store Fruit na aba de Fruit
FruitsTab:CreateToggle({
    Name = "Auto Store Fruit",
    CurrentValue = false,
    Flag = "autoStoreFruit",
    Callback = function(Value)
        autoStoreFruitEnabled = Value
    end    
})

-- Função para armazenar as frutas
local function storeFruit(fruitName, fruitInstance)
    game:GetService("ReplicatedStorage").Remotes.CommF_:InvokeServer("StoreFruit", fruitName, fruitInstance)
end

-- Função para verificar e armazenar frutas
local function checkAndStoreFruits()
    local player = game.Players.LocalPlayer
    local character = player.Character or player.CharacterAdded:Wait()
    local backpack = player.Backpack

    local fruits = {
        ["Bomb Fruit"] = "Bomb-Bomb",
        ["Spike Fruit"] = "Spike-Spike",
        ["Blade Fruit"] = "Blade-Blade",
        ["Spring Fruit"] = "Spring-Spring",
        ["Rocket Fruit"] = "Rocket-Rocket",
        ["Smoke Fruit"] = "Smoke-Smoke",
        ["Spin Fruit"] = "Spin-Spin",
        ["Flame Fruit"] = "Flame-Flame",
        ["Falcon Fruit"] = "Falcon-Falcon",
        ["Ice Fruit"] = "Ice-Ice",
        ["Sand Fruit"] = "Sand-Sand",
        ["Dark Fruit"] = "Dark-Dark",
        ["Ghost Fruit"] = "Ghost-Ghost",
        ["Diamond Fruit"] = "Diamond-Diamond",
        ["Light Fruit"] = "Light-Light",
        ["Love Fruit"] = "Love-Love",
        ["Rubber Fruit"] = "Rubber-Rubber",
        ["Rumble Fruit"] = "Rumble-Rumble",
        ["Barrier Fruit"] = "Barrier-Barrier",
        ["Sound Fruit"] = "Sound-Sound",
        ["Magma Fruit"] = "Magma-Magma",
        ["Pain Fruit"] = "Pain-Pain",
        ["Blizzard Fruit"] = "Blizzard-Blizzard",
        ["Portal Fruit"] = "Portal-Portal",
        ["Quake Fruit"] = "Quake-Quake",
        ["Buddha Fruit"] = "Buddha-Buddha",
        ["Spider Fruit"] = "Spider-Spider",
        ["Phoenix Fruit"] = "Pheonix-Pheonix",
        ["Gravity Fruit"] = "Gravity-Gravity",
        ["T-Rex Fruit"] = "Trex-Trex",
        ["Mammoth Fruit"] = "Mammoth-Mammoth",
        ["Dough Fruit"] = "Dough-Dough",
        ["Spirit Fruit"] = "Spirit-Spirit",
        ["Gas Fruit"] = "Gas-Gas",
        ["Shadow Fruit"] = "Shadow-Shadow",
        ["Venom Fruit"] = "Venom-Venom",
        ["Control Fruit"] = "Control-Control",
        ["Kitsune Fruit"] = "Kitsune-Kitsune",
        ["Leopard Fruit"] = "Leopard-Leopard",
        ["Dragon Fruit"] = "Dragon-Dragon"
    }

    for fruit, name in pairs(fruits) do
        if character:FindFirstChild(fruit) or backpack:FindFirstChild(fruit) then
            storeFruit(name, backpack:FindFirstChild(fruit) or character:FindFirstChild(fruit))
        end
    end
end

-- Verificar e armazenar frutas continuamente enquanto o toggle estiver ativado
spawn(function()
    while wait(0.3) do
        if autoStoreFruitEnabled then
            pcall(checkAndStoreFruits)
        end
    end
end)

-- Variável para ativar/desativar o Random Fruit
local randomFruitEnabled = false

-- Adicionando o toggle para Random Fruit na aba de Fruit
FruitsTab:CreateToggle({
    Name = "Random Fruit",
    CurrentValue = false,
    Flag = "randomFruit",
    Callback = function(Value)
        randomFruitEnabled = Value
    end    
})

-- Função para comprar frutas aleatórias
local function buyRandomFruit()
    game:GetService("ReplicatedStorage").Remotes.CommF_:InvokeServer("Cousin", "Buy")
end

-- Verificar continuamente enquanto o toggle estiver ativado
spawn(function()
    while wait(0.1) do
        if randomFruitEnabled then
            pcall(buyRandomFruit)
        end
    end
end)

MiscTab:CreateButton({
	Name = "Join Pirates Team",
	Callback = function()
        game:GetService("ReplicatedStorage").Remotes.CommF_:InvokeServer("SetTeam","Pirates") 
	end
})


MiscTab:CreateButton({
	Name = "Join Marines Team",
	Callback = function()
        game:GetService("ReplicatedStorage").Remotes.CommF_:InvokeServer("SetTeam","Marines") 
	end
})

-- Variável para armazenar a ilha selecionada
local selectedIsland

-- Definindo a lista de ilhas com base no mundo
local IslandList = {}
if World1 then
    IslandList = {
        "WindMill", "Marine", "Middle Town", "Jungle", "Pirate Village", "Desert", "Snow Island",
        "MarineFord", "Colosseum", "Sky Island 1", "Sky Island 2", "Sky Island 3", "Prison",
        "Magma Village", "Under Water Island", "Fountain City", "Shank Room", "Mob Island"
    }
elseif World2 then
    IslandList = {
        "The Cafe", "Frist Spot", "Dark Area", "Flamingo Mansion", "Flamingo Room", "Green Zone",
        "Factory", "Colossuim", "Zombie Island", "Two Snow Mountain", "Punk Hazard", "Cursed Ship",
        "Ice Castle", "Forgotten Island", "Ussop Island", "Mini Sky Island"
    }
elseif World3 then
    IslandList = {
        "Mansion", "Port Town", "Great Tree", "Castle On The Sea", "MiniSky", "Hydra Island",
        "Floating Turtle", "Haunted Castle", "Ice Cream Island", "Peanut Island", "Cake Island",
        "Cocoa Island", "Candy Island", "Tiki Outpost"
    }
end

-- Função para criar os botões de teleporte
local function createTeleportButtons(islands)
    for _, island in ipairs(islands) do
        TeleportTab:CreateButton({
            Name = island,
            Callback = function()
                if island == "WindMill" then
                    toTarget(CFrame.new(979.79895019531, 16.516613006592, 1429.0466308594))
                elseif island == "Marine" then
                    toTarget(CFrame.new(-2566.4296875, 6.8556680679321, 2045.2561035156))
                elseif island == "Middle Town" then
                    toTarget(CFrame.new(-690.33081054688, 15.09425163269, 1582.2380371094))
                elseif island == "Jungle" then
                    toTarget(CFrame.new(-1612.7957763672, 36.852081298828, 149.12843322754))
                elseif island == "Pirate Village" then
                    toTarget(CFrame.new(-1181.3093261719, 4.7514905929565, 3803.5456542969))
                elseif island == "Desert" then
                    toTarget(CFrame.new(944.15789794922, 20.919729232788, 4373.3002929688))
                elseif island == "Snow Island" then
                    toTarget(CFrame.new(1347.8067626953, 104.66806030273, -1319.7370605469))
                elseif island == "MarineFord" then
                    toTarget(CFrame.new(-4914.8212890625, 50.963626861572, 4281.0278320313))
                elseif island == "Colosseum" then
                    toTarget(CFrame.new(-1427.6203613281, 7.2881078720093, -2792.7722167969))
                elseif island == "Sky Island 1" then
                    toTarget(CFrame.new(-4869.1025390625, 733.46051025391, -2667.0180664063))
                elseif island == "Sky Island 2" then  
                    game:GetService("ReplicatedStorage").Remotes.CommF_:InvokeServer("requestEntrance", Vector3.new(-4607.82275, 872.54248, -1667.55688))
                elseif island == "Sky Island 3" then
                    game:GetService("ReplicatedStorage").Remotes.CommF_:InvokeServer("requestEntrance", Vector3.new(-7894.6176757813, 5547.1416015625, -380.29119873047))
                elseif island == "Prison" then
                    toTarget(CFrame.new(4875.330078125, 5.6519818305969, 734.85021972656))
                elseif island == "Magma Village" then
                    toTarget(CFrame.new(-5247.7163085938, 12.883934020996, 8504.96875))
                elseif island == "Under Water Island" then
                    game:GetService("ReplicatedStorage").Remotes.CommF_:InvokeServer("requestEntrance", Vector3.new(61163.8515625, 11.6796875, 1819.7841796875))
                elseif island == "Fountain City" then
                    toTarget(CFrame.new(5127.1284179688, 59.501365661621, 4105.4458007813))
                elseif island == "Shank Room" then
                    toTarget(CFrame.new(-1442.16553, 29.8788261, -28.3547478))
                elseif island == "Mob Island" then
                    toTarget(CFrame.new(-2850.20068, 7.39224768, 5354.99268))
                elseif island == "The Cafe" then
                    game:GetService("ReplicatedStorage").Remotes.CommF_:InvokeServer("requestEntrance", Vector3.new(-281.93707275390625, 306.130615234375, 609.280029296875))
                    wait(0.5)
                    toTarget(CFrame.new(-380.47927856445, 77.220390319824, 255.82550048828))
                elseif island == "Frist Spot" then
                    toTarget(CFrame.new(-11.311455726624, 29.276733398438, 2771.5224609375))
                elseif island == "Dark Area" then
                    toTarget(CFrame.new(3780.0302734375, 22.652164459229, -3498.5859375))
                elseif island == "Flamingo Mansion" then
                    game:GetService("ReplicatedStorage").Remotes.CommF_:InvokeServer("requestEntrance", Vector3.new(-281.93707275390625, 306.130615234375, 609.280029296875))
                elseif island == "Flamingo Room" then
                    game:GetService("ReplicatedStorage").Remotes.CommF_:InvokeServer("requestEntrance", Vector3.new(2284.912109375, 15.152034759521484, 905.48291015625))
                elseif island == "Green Zone" then
                    toTarget(CFrame.new(-2448.5300292969, 73.016105651855, -3210.6306152344))
                elseif island == "Factory" then
                    toTarget(CFrame.new(424.12698364258, 211.16171264648, -427.54049682617))
                elseif island == "Colossuim" then
                    toTarget(CFrame.new(-1503.6224365234, 219.7956237793, 1369.3101806641))
                elseif island == "Zombie Island" then
                    toTarget(CFrame.new(-5622.033203125, 492.19604492188, -781.78552246094))
                elseif island == "Two Snow Mountain" then
                    toTarget(CFrame.new(753.14288330078, 408.23559570313, -5274.6147460938))
                elseif island == "Punk Hazard" then
                    toTarget(CFrame.new(-6127.654296875, 15.951762199402, -5040.2861328125))
                elseif island == "Cursed Ship" then
                    game:GetService("ReplicatedStorage").Remotes.CommF_:InvokeServer("requestEntrance", Vector3.new(923.40197753906, 125.05712890625, 32885.875))
                elseif island == "Ice Castle" then
                    toTarget(CFrame.new(6148.4116210938, 294.38687133789, -6741.1166992188))
                elseif island == "Forgotten Island" then
                    toTarget(CFrame.new(-3032.7641601563, 317.89672851563, -10075.373046875))
                elseif island == "Ussop Island" then
                    toTarget(CFrame.new(4816.8618164063, 8.4599885940552, 2863.8195800781))
                elseif island == "Mini Sky Island" then
                    Tween2(CFrame.new(-288.74060058594, 49326.31640625, -35248.59375))
                                    toTarget(CFrame.new(2681.2736816406, 1682.8092041016, -7190.9853515625))
                elseif island == "Castle On The Sea" then
                    game:GetService("ReplicatedStorage").Remotes.CommF_:InvokeServer("requestEntrance", Vector3.new(-5075.50927734375, 314.5155029296875, -3150.0224609375))
                elseif island == "MiniSky" then
                    Tween2(CFrame.new(-260.65557861328, 49325.8046875, -35253.5703125))
                elseif island == "Port Town" then
                    toTarget(CFrame.new(-290.7376708984375, 6.729952812194824, 5343.5537109375))
                elseif island == "Hydra Island" then
                    game:GetService("ReplicatedStorage").Remotes.CommF_:InvokeServer("requestEntrance", Vector3.new(5753.5478515625, 610.7880859375, -282.33172607421875))
                elseif island == "Floating Turtle" then
                    toTarget(CFrame.new(-13274.528320313, 531.82073974609, -7579.22265625))
                elseif island == "Mansion" then
                    game:GetService("ReplicatedStorage").Remotes.CommF_:InvokeServer("requestEntrance", Vector3.new(-12468.5380859375, 375.0094299316406, -7554.62548828125))
                elseif island == "Haunted Castle" then
                    toTarget(CFrame.new(-9515.3720703125, 164.00624084473, 5786.0610351562))
                elseif island == "Ice Cream Island" then
                    toTarget(CFrame.new(-902.56817626953, 79.93204498291, -10988.84765625))
                elseif island == "Peanut Island" then
                    toTarget(CFrame.new(-2062.7475585938, 50.473892211914, -10232.568359375))
                elseif island == "Cake Island" then
                    toTarget(CFrame.new(-1884.7747802734375, 19.327526092529297, -11666.8974609375))
                elseif island == "Cocoa Island" then
                    toTarget(CFrame.new(87.94276428222656, 73.55451202392578, -12319.46484375))
                elseif island == "Candy Island" then
                    toTarget(CFrame.new(-1014.4241943359375, 149.11068725585938, -14555.962890625))
                elseif island == "Tiki Outpost" then
                    toTarget(CFrame.new(-16542.447265625, 55.68632888793945, 1044.41650390625))
                end
            end
        })
    end
end

-- Criar botões de teleporte com base na lista de ilhas do mundo atual
createTeleportButtons(IslandList)

-- Botão para parar o Tween
TeleportTab:CreateButton({
    Name = "Stop Tween",
    Callback = function()
        toTarget(game:GetService("Players").LocalPlayer.Character.HumanoidRootPart.CFrame)
    end
})


-- Finalização do script
Rayfield:Notify({
    Title = "Script Carregado",
    Content = "O script foi carregado corretamente!",
    Duration = 5
})
