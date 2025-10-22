local Players = game:GetSPlayers")
local TweenService = game:GetService("TweenService")
local CoreGui = game:GetService("CoreGui")
local StarterGui = game:GetService("StarterGui")
local lp = Players.LocalPlayer

-- FunÃ§Ã£o que cria a tela de loading e retorna uma promise
local function createLoadingScreen()
    local promise = {}
    promise.completed = false
    promise.connection = nil
    
    -- Remove GUI antiga se existir
    pcall(function()
        if CoreGui:FindFirstChild("LoadingScreen") then
            CoreGui.LoadingScreen:Destroy()
        end
    end)

    -- Cria a UI de carregamento
    local gui = Instance.new("ScreenGui")
    gui.Name = "LoadingScreen"
    gui.IgnoreGuiInset = true
    gui.ResetOnSpawn = false
    gui.Parent = CoreGui
    pcall(function() syn.protect_gui(gui) end)

    local frame = Instance.new("Frame")
    frame.BackgroundColor3 = Color3.new(0, 0, 0)
    frame.BackgroundTransparency = 0.3
    frame.Size = UDim2.new(1, 0, 1, 0)
    frame.Parent = gui

    local image = Instance.new("ImageLabel")
    image.Size = UDim2.new(0, 300, 0, 300)
    image.Position = UDim2.new(0.5, -150, 0.35, -150)
    image.BackgroundTransparency = 1
    image.Image = "rbxassetid://75732220851513"
    image.Parent = frame

    local nameText = Instance.new("TextLabel")
    nameText.Size = UDim2.new(1, 0, 0, 40)
    nameText.Position = UDim2.new(0, 0, 0.65, 0)
    nameText.TextColor3 = Color3.fromRGB(255, 255, 255)
    nameText.TextStrokeTransparency = 0.3
    nameText.BackgroundTransparency = 1
    nameText.Font = Enum.Font.FredokaOne
    nameText.TextScaled = true
    nameText.Text = "Verificando usuÃ¡rio: "..lp.Name.." (Conta: "..tostring(lp.AccountAge).." dias)"
    nameText.Parent = frame

    local barBG = Instance.new("Frame")
    barBG.Size = UDim2.new(0.6, 0, 0.03, 0)
    barBG.Position = UDim2.new(0.2, 0, 0.8, 0)
    barBG.BackgroundColor3 = Color3.new(1, 1, 1)
    barBG.BorderSizePixel = 0
    barBG.Parent = frame

    local bar = Instance.new("Frame")
    bar.Size = UDim2.new(0, 0, 1, 0)
    bar.BackgroundColor3 = Color3.new(0.7, 0.2, 0.6)
    bar.BorderSizePixel = 0
    bar.Parent = barBG

    -- AnimaÃ§Ã£o da barra de carregamento
    local tween = TweenService:Create(
        bar,
        TweenInfo.new(4, Enum.EasingStyle.Quad, Enum.EasingDirection.Out),
        {Size = UDim2.new(1, 0, 1, 0)}
    )
    tween:Play()

    -- FunÃ§Ã£o para limpar a UI
    local function cleanup()
        if gui then
            gui:Destroy()
        end
        if promise.connection then
            promise.connection:Disconnect()
        end
    end

    -- ApÃ³s a barra carregar, faz o fade out e destrÃ³i a UI
    promise.connection = tween.Completed:Connect(function()
        -- Fade out suave da UI
        TweenService:Create(frame, TweenInfo.new(1, Enum.EasingStyle.Quad, Enum.EasingDirection.Out), {BackgroundTransparency = 1}):Play()
        TweenService:Create(barBG, TweenInfo.new(1, Enum.EasingStyle.Quad, Enum.EasingDirection.Out), {BackgroundTransparency = 1}):Play()
        TweenService:Create(bar, TweenInfo.new(1, Enum.EasingStyle.Quad, Enum.EasingDirection.Out), {BackgroundTransparency = 1}):Play()
        TweenService:Create(image, TweenInfo.new(1, Enum.EasingStyle.Quad, Enum.EasingDirection.Out), {ImageTransparency = 1}):Play()
        TweenService:Create(nameText, TweenInfo.new(1, Enum.EasingStyle.Quad, Enum.EasingDirection.Out), {TextTransparency = 1}):Play()
        
        -- Aguarda o fade out terminar
        task.delay(1.2, function()
            -- Toca som de conclusÃ£o
            local sound = Instance.new("Sound")
            sound.SoundId = "rbxassetid://8486683243"
            sound.Volume = 0.5
            sound.PlayOnRemove = true
            sound.Parent = workspace
            sound:Destroy()
            
            -- Exibe a notificaÃ§Ã£o de boas-vindas
            StarterGui:SetCore("SendNotification", {
                Title = "h4x hub",
                Text = "Bem-vindo Ã  h4x Hub ",
                Duration = 4
            })
            
            -- Marca como concluÃ­do e limpa
            promise.completed = true
            cleanup()
        end)
    end)
    
    return promise
end

-- FunÃ§Ã£o para esperar atÃ© que a promise seja resolvida
local function waitForPromise(promise)
    while not promise.completed do
        task.wait()
    end
end

-- Uso:
local loadingPromise = createLoadingScreen()

local Window = redzlib:MakeWindow({
    Title = "h4x 1.0_Nova_era",
    SubTitle = "by megumi ",
    SaveFolder = "teste"
  })

  Window:AddMinimizeButton({
    Button = { Image = "rbxassetid://89018617324929", BackgroundTransparency = 0 },
    Corner = { CornerRadius = UDim.new(35, 1) },
})



local Tab1 = Window:MakeTab({"Credits", "info"})
local Tab2= Window:MakeTab({"Fun", "fun"})
local Tab3 = Window:MakeTab({"Avatar", "shirt"})
local Tab4 = Window:MakeTab({"House", "Home"})
local Tab5 = Window:MakeTab({"Car", "Car"})
local Tab6 = Window:MakeTab({"RGB", "brush"})
local Tab7 = Window:MakeTab({"Music All", "radio"})    
local Tab8 = Window:MakeTab({"Music", "music"}) 
local Tab9 = Window:MakeTab({"Troll", "skull"}) 
local Tab10 = Window:MakeTab({"Lag Server", "bomb"})
local Tab11 = Window:MakeTab({"Scripts", "scroll"})
local Tab12 = Window:MakeTab({"Teleportes", "map-pin"})





--------------------------------------------------------------------------------------------------------------------------------
                                                   -- === Tab 1: credits === --
---------------------------------------------------------------------------------------------------------------------------------

  
local function detectExecutor()
    if identifyexecutor then
        return identifyexecutor()
    elseif syn then
        return "Synapse X"
    elseif KRNL_LOADED then
        return "KRNL"
    elseif is_sirhurt_closure then
        return "SirHurt"
    elseif pebc_execute then
        return "ProtoSmasher"
    elseif getexecutorname then
        return getexecutorname()
    else
        return "Executor Desconhecido"
    end
end

local executorName = detectExecutor()

local Paragraph = Tab1:AddParagraph({"Execultor", executorName})

local Section = Tab1:AddSection({"versao do Hub 1.0"})

local Paragraph = Tab1:AddParagraph({"Criadores", "megumi \n ?????"})


  
  Tab1:AddButton({
    Name = " - Copiar @ do TikTok",
    Callback = function()
      setclipboard("@embreve") -- Copia o @

 ---------------------------------------------------------------------------------------------------------------------------------
                                                   -- === Tab 2: Fun === --
-----------------------------------------------------------------------------------------------------------------------------------



local Section = Tab2:AddSection({"Player Character"})


local Players = game:GetService("Players")
local localPlayer = Players.LocalPlayer

local selectedPlayerName = nil
local headsitActive = false

local function headsitOnPlayer(targetPlayer)
    local character = localPlayer.Character or localPlayer.CharacterAdded:Wait()
    local humanoid = character:FindFirstChildOfClass("Humanoid")

    if not targetPlayer.Character or not targetPlayer.Character:FindFirstChild("Head") then
        warn("Jogador alvo sem cabeÃ§a ou personagem.")
        return false
    end
    local targetHead = targetPlayer.Character.Head
    local localRoot = character:FindFirstChild("HumanoidRootPart")
    if not localRoot then
        warn("Seu personagem nÃ£o tem HumanoidRootPart.")
        return false
    end

    localRoot.CFrame = targetHead.CFrame * CFrame.new(0, 2.2, 0)

    for _, v in pairs(localRoot:GetChildren()) do
        if v:IsA("WeldConstraint") then
            v:Destroy()
        end
    end

    local weld = Instance.new("WeldConstraint")
    weld.Part0 = localRoot
    weld.Part1 = targetHead
    weld.Parent = localRoot

    if humanoid then
        humanoid.Sit = true
    end

    print("Headsit ativado em " .. targetPlayer.Name)
    return true
end

local function removeHeadsit()
    local character = localPlayer.Character or localPlayer.CharacterAdded:Wait()
    local humanoid = character:FindFirstChildOfClass("Humanoid")
    local localRoot = character:FindFirstChild("HumanoidRootPart")
    if localRoot then
        for _, v in pairs(localRoot:GetChildren()) do
            if v:IsA("WeldConstraint") then
                v:Destroy()
            end
        end
    end
    if humanoid then
        humanoid.Sit = false
    end

    print("Headsit desativado.")
end

-- FunÃ§Ã£o para encontrar jogador por nome parcial
local function findPlayerByPartialName(partial)
    partial = partial:lower()
    for _, player in pairs(Players:GetPlayers()) do
        if player ~= localPlayer and player.Name:lower():sub(1, #partial) == partial then
            return player
        end
    end
    return nil
end

-- NotificaÃ§Ã£o com imagem do jogador
local function notifyPlayerSelected(player)
    local StarterGui = game:GetService("StarterGui")
    local thumbType = Enum.ThumbnailType.HeadShot
    local thumbSize = Enum.ThumbnailSize.Size100x100
    local content, _ = Players:GetUserThumbnailAsync(player.UserId, thumbType, thumbSize)

    StarterGui:SetCore("SendNotification", {
        Title = "Player Selecionado",
        Text = player.Name .. " foi selecionado!",
        Icon = content,
        Duration = 5
    })
end

-- TextBox para digitar nome do player
Tab2:AddTextBox({
    Name = "Nome do Jogador",
    Description = "Digite parte do nome",
    PlaceholderText = "ex: lo â†’ megumi",
    Callback = function(Value)
        local foundPlayer = findPlayerByPartialName(Value)
        if foundPlayer then
            selectedPlayerName = foundPlayer.Name
            notifyPlayerSelected(foundPlayer)
        else
            warn("Nenhum jogador encontrado com esse nome.")
        end
    end
})

-- BotÃ£o para ativar/desativar headsit
-- BotÃ£o para ativar/desativar headsit (versÃ£o simplificada)
Tab2:AddButton({"", function()
    if not selectedPlayerName then
    
        return
    end

    if not headsitActive then
        local target = Players:FindFirstChild(selectedPlayerName)
        if target and headsitOnPlayer(target) then
            headsitActive = true
        end
    else
        removeHeadsit()
        headsitActive = false
    end
end})




Tab2:AddSlider({
    Name = "Speed Player",
    Increase = 1,
    MinValue = 16,
    MaxValue = 888,
    Default = 16,
    Callback = function(Value)
        local player = game.Players.LocalPlayer
        local character = player.Character or player.CharacterAdded:Wait()
        local humanoid = character:FindFirstChildOfClass("Humanoid")
        
        if humanoid then
            humanoid.WalkSpeed = Value
        end
    end
 })
 
 Tab2:AddSlider({
    Name = "Jumppower",
    Increase = 1,
    MinValue = 50,
    MaxValue = 500,
    Default = 50,
    Callback = function(Value)
        local player = game.Players.LocalPlayer
        local character = player.Character or player.CharacterAdded:Wait()
        local humanoid = character:FindFirstChildOfClass("Humanoid")
        
        if humanoid then
            humanoid.JumpPower = Value
        end
    end
 })
 
 Tab2:AddSlider({
    Name = "Gravity",
    Increase = 1,
    MinValue = 0,
    MaxValue = 10000,
    Default = 196.2,
    Callback = function(Value)
        game.Workspace.Gravity = Value
    end
 })
 
 local InfiniteJumpEnabled = false
 
 game:GetService("UserInputService").JumpRequest:Connect(function()
    if InfiniteJumpEnabled then
       local character = game.Players.LocalPlayer.Character
       if character and character:FindFirstChild("Humanoid") then
          character.Humanoid:ChangeState(Enum.HumanoidStateType.Jumping)
       end
    end
 end)

 Tab2:AddButton({
    Name = "Reset Speed/Gravity/Jumppower.âœ…",
    Callback = function()
        -- Resetar Speed
        local player = game.Players.LocalPlayer
        local character = player.Character or player.CharacterAdded:Wait()
        local humanoid = character:FindFirstChildOfClass("Humanoid")
        if humanoid then
            humanoid.WalkSpeed = 16 -- Valor padrÃ£o do Speed
            humanoid.JumpPower = 50 -- Valor padrÃ£o do JumpPower
        end
        
        -- Resetar Gravity
        game.Workspace.Gravity = 196.2 -- Valor padrÃ£o da gravidade
        
        -- Desativar Infinite Jump
        InfiniteJumpEnabled = false
    end
})
 
 Tab2:AddToggle({
    Name = "Infinite Jump",
    Default = false,
    Callback = function(Value)
       InfiniteJumpEnabled = Value
    end
 })

 local UltimateNoclip = {
    Enabled = false,
    Connections = {},
    SoccerBalls = {}
}

local Players = game:GetService("Players")
local RunService = game:GetService("RunService")
local Workspace = game:GetService("Workspace")
local LocalPlayer = Players.LocalPlayer

-- FunÃ§Ã£o para controle de colisÃµes do jogador
local function managePlayerCollisions(character)
    if not character then return end
    
    for _, part in ipairs(character:GetDescendants()) do
        if part:IsA("BasePart") then
            part.CanCollide = not UltimateNoclip.Enabled
            part.Anchored = false
        end
    end
end

-- Sistema anti-void melhorado
local function voidProtection(rootPart)
    if rootPart.Position.Y < -500 then
        local safeCFrame = CFrame.new(0, 100, 0)
        local rayParams = RaycastParams.new()
        rayParams.FilterDescendantsInstances = {LocalPlayer.Character}
        
        local result = Workspace:Raycast(rootPart.Position, Vector3.new(0, 500, 0), rayParams)
        rootPart.CFrame = result and CFrame.new(result.Position + Vector3.new(0, 5, 0)) or safeCFrame
    end
end

-- Controle das bolas de futebol
local function manageSoccerBalls()
    local soccerFolder = Workspace:FindFirstChild("Com", true)
                      and Workspace.Com:FindFirstChild("001_SoccerBalls")
    
    if soccerFolder then
        -- Atualiza bolas existentes
        for _, ball in ipairs(soccerFolder:GetChildren()) do
            if ball.Name:match("^Soccer") then
                pcall(function()
                    ball.CanCollide = not UltimateNoclip.Enabled
                    ball.Anchored = UltimateNoclip.Enabled
                end)
                UltimateNoclip.SoccerBalls[ball] = true
            end
        end
        
        -- Monitora novas bolas
        if not UltimateNoclip.Connections.BallAdded then
            UltimateNoclip.Connections.BallAdded = soccerFolder.ChildAdded:Connect(function(ball)
                if ball.Name:match("^Soccer") then
                    task.wait(0.3)
                    pcall(function()
                        ball.CanCollide = not UltimateNoclip.Enabled
                        ball.Anchored = UltimateNoclip.Enabled
                    end)
                end
            end)
        end
    end
end

-- Loop principal do sistema
local function mainLoop()
    UltimateNoclip.Connections.Heartbeat = RunService.Heartbeat:Connect(function()
        local character = LocalPlayer.Character
        
        -- Controle do jogador
        if character then
            managePlayerCollisions(character)
            
            local rootPart = character:FindFirstChild("HumanoidRootPart")
            if rootPart then
                voidProtection(rootPart)
            end
        end
        
        -- Atualiza bolas a cada 2 segundos
        if tick() % 2 < 0.1 then
            manageSoccerBalls()
        end
    end)
end

-- ConfiguraÃ§Ã£o do toggle
local NoclipToggle = Tab2:AddToggle({
    Name = "Ultimate Noclip",
    Description = "Noclip + Controle de bolas integrado",
    Default = false
})

NoclipToggle:Callback(function(state)
    UltimateNoclip.Enabled = state
    
    if state then
        -- Inicia sistemas
        mainLoop()
        manageSoccerBalls()
        
        -- Configura respawn
        UltimateNoclip.Connections.CharAdded = LocalPlayer.CharacterAdded:Connect(function()
            task.wait(0.5)
            managePlayerCollisions(LocalPlayer.Character)
        end)
    else
        -- Desativa tudo
        for _, conn in pairs(UltimateNoclip.Connections) do
            conn:Disconnect()
        end
        
        -- Restaura colisÃµes
        if LocalPlayer.Character then
            managePlayerCollisions(LocalPlayer.Character)
        end
        
        -- Restaura bolas
        for ball in pairs(UltimateNoclip.SoccerBalls) do
            if ball.Parent then
                pcall(function()
                    ball.CanCollide = true
                    ball.Anchored = false
                end)
            end
        end
    end
end)
-------------------------------------------------------------------------------
-- Toggle para Anti-Sit
local antiSitConnection = nil
local antiSitEnabled = false

Tab2:AddToggle({
    Name = "Anti-Sit",
    Description = "Impede o jogador de sentar",
    Default = false,
    Callback = function(state)
        antiSitEnabled = state
        local LocalPlayer = game:GetService("Players").LocalPlayer

        if state then
            local function applyAntiSit(character)
                local humanoid = character:FindFirstChild("Humanoid")
                if humanoid then
                    humanoid.Sit = false
                    humanoid:SetStateEnabled(Enum.HumanoidStateType.Seated, false)
                    if antiSitConnection then
                        antiSitConnection:Disconnect()
                    end
                    antiSitConnection = humanoid.Seated:Connect(function(isSeated)
                        if isSeated then
                            humanoid.Sit = false
                            humanoid:ChangeState(Enum.HumanoidStateType.GettingUp)
                        end
                    end)
                end
            end

            if LocalPlayer.Character then
                applyAntiSit(LocalPlayer.Character)
            end

            local characterAddedConnection
            characterAddedConnection = LocalPlayer.CharacterAdded:Connect(function(character)
                if not antiSitEnabled then
                    characterAddedConnection:Disconnect()
                    return
                end
                local humanoid = character:WaitForChild("Humanoid", 5)
                if humanoid then
                    applyAntiSit(character)
                end
            end)
        else
            if antiSitConnection then
                antiSitConnection:Disconnect()
                antiSitConnection = nil
            end

            if LocalPlayer.Character then
                local humanoid = LocalPlayer.Character:FindFirstChild("Humanoid")
                if humanoid then
                    humanoid:SetStateEnabled(Enum.HumanoidStateType.Seated, true)
                end
            end
        end
    end
})

-- ServiÃ§os
local Players = game:GetService("Players")
local RunService = game:GetService("RunService")

-- VariÃ¡veis
local billboardGuis = {}
local connections = {}
local espEnabled = false
local selectedColor = "RGB Suave"

-- BotÃ£o para Fly GUI
Tab2:AddButton({
    Name = "Ativar Fly GUI",
    Description = "Carrega um GUI de fly universal",
    Callback = function()
        local success, _ = pcall(function()
            
