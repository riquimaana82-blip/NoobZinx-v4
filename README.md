-- @Noobzinx v4 - PARTE 1 (BOTÃO FECHAR CORRIGIDO)
local P = game:GetService("Players")
local RS = game:GetService("RunService")
local C = workspace.CurrentCamera
local LP = P.LocalPlayer

local S = {
    Aimbot = false,
    MostrarFOV = false,
    ESP = false,
    ESP_Caixa = false,
    ESP_Nome = false,
    ESP_Vida = false,
    ESP_Linha = false,
    ESP_Distancia = false,
    Speed = false,
    Rainbow = false,
    SuperJump = false,
    AtravessarParede = false,
    HitboxAmpliada = false,
    GirarRapido = false,
    KillAll = false,
    TargetPart = "Head",
    FOV = 150,
    Smooth = 0.2,
    SpeedMul = 50,
    AimType = "Ao Atirar"
}

local SG = Instance.new("ScreenGui")
SG.Parent = LP.PlayerGui
SG.ResetOnSpawn = false
SG.ZIndexBehavior = Enum.ZIndexBehavior.Sibling

local OB = Instance.new("TextButton")
OB.Parent = SG
OB.BackgroundColor3 = Color3.fromRGB(120,0,200)
OB.Size = UDim2.new(0,45,0,45)
OB.Position = UDim2.new(0,10,0,10)
OB.Text = "MENU"
OB.TextColor3 = Color3.fromRGB(255,255,255)
OB.Font = Enum.Font.GothamBold
OB.TextScaled = true
OB.Visible = false
Instance.new("UICorner",OB).CornerRadius = UDim.new(0,10)

local MF = Instance.new("Frame")
MF.Parent = SG
MF.BackgroundColor3 = Color3.fromRGB(15,15,15)
MF.Size = UDim2.new(0,340,0,420)
MF.Position = UDim2.new(0.5,-170,0.5,-210)
MF.Active = true
MF.Draggable = true
MF.BorderSizePixel = 1
MF.BorderColor3 = Color3.fromRGB(120,0,200)
Instance.new("UICorner",MF).CornerRadius = UDim.new(0,10)

local TB = Instance.new("Frame")
TB.Parent = MF
TB.BackgroundColor3 = Color3.fromRGB(120,0,200)
TB.Size = UDim2.new(1,0,0,36)
Instance.new("UICorner",TB).CornerRadius = UDim.new(0,10)

local T = Instance.new("TextLabel")
T.Parent = TB
T.BackgroundTransparency = 1
T.Size = UDim2.new(0.8,0,1,0)
T.Position = UDim2.new(0.1,0,0,0)
T.Text = "@Noobzinx v4"
T.TextColor3 = Color3.fromRGB(255,255,255)
T.TextScaled = true
T.Font = Enum.Font.GothamBold

-- 🔥 BOTÃO FECHAR CORRIGIDO: USA "X" EM VEZ DE "✕"
local X = Instance.new("TextButton")
X.Parent = TB
X.BackgroundColor3 = Color3.fromRGB(100,0,170)
X.Size = UDim2.new(0,36,1,0)
X.Position = UDim2.new(1,-36,0,0)
X.Text = "X"  -- ← MUDOU AQUI
X.TextColor3 = Color3.fromRGB(255,255,255)
X.TextScaled = true
X.Font = Enum.Font.GothamBold
X.BorderSizePixel = 0
Instance.new("UICorner",X).CornerRadius = UDim.new(0,10)
X.MouseButton1Click:Connect(function() MF.Visible=false; OB.Visible=true end)
OB.MouseButton1Click:Connect(function() MF.Visible=true; OB.Visible=false end)

local Lateral = Instance.new("Frame")
Lateral.Parent = MF
Lateral.BackgroundColor3 = Color3.fromRGB(25,25,25)
Lateral.Size = UDim2.new(0,55,1,-36)
Lateral.Position = UDim2.new(0,0,0,36)

local Conteudo = Instance.new("Frame")
Conteudo.Parent = MF
Conteudo.BackgroundTransparency = 1
Conteudo.Size = UDim2.new(1,-55,1,-36)
Conteudo.Position = UDim2.new(0,55,0,36)

local sep = function(pai, y)
    local s = Instance.new("Frame")
    s.Parent = pai
    s.BackgroundColor3 = Color3.fromRGB(120,0,200)
    s.Size = UDim2.new(0.92,0,0,1)
    s.Position = UDim2.new(0.04,0,0,y)
end

local function abaLateral(icone, indice)
    local btn = Instance.new("TextButton")
    btn.Parent = Lateral
    btn.BackgroundColor3 = indice == 1 and Color3.fromRGB(120,0,200) or Color3.fromRGB(35,35,35)
    btn.Size = UDim2.new(1,0,0,55)
    btn.Position = UDim2.new(0,0,0,(indice-1)*55)
    btn.Text = icone
    btn.TextColor3 = Color3.fromRGB(255,255,255)
    btn.Font = Enum.Font.GothamBold
    btn.TextScaled = true
    Instance.new("UICorner",btn).CornerRadius = UDim.new(0,8)
    return btn
end

local bAim = abaLateral("🎯",1)
local bEsp = abaLateral("👁",2)
local bConf = abaLateral("⚙",3)
local bInfo = abaLateral("📄",4)

local function criarBotaoSwitch(pai, posY, texto, valorAtual, funcaoMudar)
    local lblTexto = Instance.new("TextLabel")
    lblTexto.Parent = pai
    lblTexto.BackgroundTransparency = 1
    lblTexto.Size = UDim2.new(0.55,0,0,28)
    lblTexto.Position = UDim2.new(0.05,0,0,posY)
    lblTexto.Text = texto
    lblTexto.TextColor3 = Color3.fromRGB(255,255,255)
    lblTexto.TextScaled = true
    lblTexto.Font = Enum.Font.Gotham

    local fundo = Instance.new("Frame")
    fundo.Parent = pai
    fundo.Size = UDim2.new(0,48,0,24)
    fundo.Position = UDim2.new(0.75,0,0,posY+2)
    fundo.BackgroundColor3 = Color3.fromRGB(60,60,60)
    Instance.new("UICorner",fundo).CornerRadius = UDim.new(0,12)

    local botao = Instance.new("Frame")
    botao.Parent = fundo
    botao.Size = UDim2.new(0,18,0,18)
    botao.Position = UDim2.new(0,3,0.5,-9)
    botao.BackgroundColor3 = Color3.fromRGB(255,255,255)
    Instance.new("UICorner",botao).CornerRadius = UDim.new(1,0)

    local clique = Instance.new("TextButton")
    clique.Parent = fundo
    clique.Size = UDim2.new(1,0,1,0)
    clique.BackgroundTransparency = 1
    clique.Text = ""

    clique.MouseButton1Click:Connect(function()
        local novoValor = not valorAtual()
        funcaoMudar(novoValor)
        fundo.BackgroundColor3 = novoValor and Color3.fromRGB(120,0,200) or Color3.fromRGB(60,60,60)
        botao.Position = novoValor and UDim2.new(1,-21,0.5,-9) or UDim2.new(0,3,0.5,-9)
    end)
end

print("✅ PARTE 1 CARREGADA - BOTÃO FECHAR CORRIGIDO")
-- @Noobzinx v4 - PARTE 2
-- ABA AIMBOT
local AimConteudo = Instance.new("Frame")
AimConteudo.Parent = Conteudo
AimConteudo.BackgroundTransparency = 1
AimConteudo.Size = UDim2.new(1,0,1,0)
AimConteudo.Visible = true

criarBotaoSwitch(AimConteudo, 10, "Ativar Aimbot", function() return S.Aimbot end, function(v) S.Aimbot = v end)
sep(AimConteudo,48)
criarBotaoSwitch(AimConteudo, 58, "Exibir FOV", function() return S.MostrarFOV end, function(v) S.MostrarFOV = v end)
sep(AimConteudo,92)

local TipoMira = Instance.new("TextLabel")
TipoMira.Parent = AimConteudo
TipoMira.BackgroundTransparency = 1
TipoMira.Size = UDim2.new(0.35,0,0,26)
TipoMira.Position = UDim2.new(0.05,0,0,102)
TipoMira.Text = "Tipo de Mira"
TipoMira.TextColor3 = Color3.fromRGB(255,255,255)
TipoMira.TextScaled = true

local TipoBtn = Instance.new("TextButton")
TipoBtn.Parent = AimConteudo
TipoBtn.BackgroundColor3 = Color3.fromRGB(45,45,45)
TipoBtn.Size = UDim2.new(0.50,0,0,26)
TipoBtn.Position = UDim2.new(0.42,0,0,102)
TipoBtn.Text = S.AimType
TipoBtn.TextColor3 = Color3.fromRGB(255,255,255)
TipoBtn.TextScaled = true
Instance.new("UICorner",TipoBtn).CornerRadius = UDim.new(0,6)
TipoBtn.MouseButton1Click:Connect(function()
    S.AimType = S.AimType == "Ao Atirar" and "Ao Olhar" or "Ao Atirar"
    TipoBtn.Text = S.AimType
end)
sep(AimConteudo,136)

local ParteCorpo = Instance.new("TextLabel")
ParteCorpo.Parent = AimConteudo
ParteCorpo.BackgroundTransparency = 1
ParteCorpo.Size = UDim2.new(0.35,0,0,26)
ParteCorpo.Position = UDim2.new(0.05,0,0,146)
ParteCorpo.Text = "Parte do Corpo"
ParteCorpo.TextColor3 = Color3.fromRGB(255,255,255)
ParteCorpo.TextScaled = true

local ParteBtn = Instance.new("TextButton")
ParteBtn.Parent = AimConteudo
ParteBtn.BackgroundColor3 = Color3.fromRGB(45,45,45)
ParteBtn.Size = UDim2.new(0.50,0,0,26)
ParteBtn.Position = UDim2.new(0.42,0,0,146)
ParteBtn.Text = "Cabeça"
ParteBtn.TextColor3 = Color3.fromRGB(255,255,255)
ParteBtn.TextScaled = true
Instance.new("UICorner",ParteBtn).CornerRadius = UDim.new(0,6)
ParteBtn.MouseButton1Click:Connect(function()
    S.TargetPart = S.TargetPart == "Head" and "Torso" or "Head"
    ParteBtn.Text = S.TargetPart == "Head" and "Cabeça" or "Tronco"
end)
sep(AimConteudo,180)

local lblFOV = Instance.new("TextLabel")
lblFOV.Parent = AimConteudo
lblFOV.BackgroundTransparency = 1
lblFOV.Size = UDim2.new(0.40,0,0,24)
lblFOV.Position = UDim2.new(0.05,0,0,190)
lblFOV.Text = "FOV: "..S.FOV
lblFOV.TextColor3 = Color3.fromRGB(255,255,255)
lblFOV.TextScaled = true

local bFovMenos = Instance.new("TextButton")
bFovMenos.Parent = AimConteudo
bFovMenos.BackgroundColor3 = Color3.fromRGB(50,50,50)
bFovMenos.Size = UDim2.new(0.12,0,0,24)
bFovMenos.Position = UDim2.new(0.55,0,0,190)
bFovMenos.Text = "-"
bFovMenos.TextColor3 = Color3.fromRGB(255,255,255)
bFovMenos.TextScaled = true
Instance.new("UICorner",bFovMenos).CornerRadius = UDim.new(0,6)
bFovMenos.MouseButton1Click:Connect(function()
    S.FOV = math.max(S.FOV-10,30)
    lblFOV.Text = "FOV: "..S.FOV
end)

local bFovMais = Instance.new("TextButton")
bFovMais.Parent = AimConteudo
bFovMais.BackgroundColor3 = Color3.fromRGB(120,0,200)
bFovMais.Size = UDim2.new(0.12,0,0,24)
bFovMais.Position = UDim2.new(0.70,0,0,190)
bFovMais.Text = "+"
bFovMais.TextColor3 = Color3.fromRGB(255,255,255)
bFovMais.TextScaled = true
Instance.new("UICorner",bFovMais).CornerRadius = UDim.new(0,6)
bFovMais.MouseButton1Click:Connect(function()
    S.FOV = math.min(S.FOV+10,400)
    lblFOV.Text = "FOV: "..S.FOV
end)
sep(AimConteudo,222)

local lblSmooth = Instance.new("TextLabel")
lblSmooth.Parent = AimConteudo
lblSmooth.BackgroundTransparency = 1
lblSmooth.Size = UDim2.new(0.45,0,0,24)
lblSmooth.Position = UDim2.new(0.05,0,0,232)
lblSmooth.Text = "Suavidade: "..string.format("%.1f",S.Smooth)
lblSmooth.TextColor3 = Color3.fromRGB(255,255,255)
lblSmooth.TextScaled = true

local bSmMenos = Instance.new("TextButton")
bSmMenos.Parent = AimConteudo
bSmMenos.BackgroundColor3 = Color3.fromRGB(50,50,50)
bSmMenos.Size = UDim2.new(0.12,0,0,24)
bSmMenos.Position = UDim2.new(0.55,0,0,232)
bSmMenos.Text = "-"
bSmMenos.TextColor3 = Color3.fromRGB(255,255,255)
bSmMenos.TextScaled = true
Instance.new("UICorner",bSmMenos).CornerRadius = UDim.new(0,6)
bSmMenos.MouseButton1Click:Connect(function()
    S.Smooth = math.max(S.Smooth-0.1,0.1)
    lblSmooth.Text = "Suavidade: "..string.format("%.1f",S.Smooth)
end)

local bSmMais = Instance.new("TextButton")
bSmMais.Parent = AimConteudo
bSmMais.BackgroundColor3 = Color3.fromRGB(120,0,200)
bSmMais.Size = UDim2.new(0.12,0,0,24)
bSmMais.Position = UDim2.new(0.70,0,0,232)
bSmMais.Text = "+"
bSmMais.TextColor3 = Color3.fromRGB(255,255,255)
bSmMais.TextScaled = true
Instance.new("UICorner",bSmMais).CornerRadius = UDim.new(0,6)
bSmMais.MouseButton1Click:Connect(function()
    S.Smooth = math.min(S.Smooth+0.1,1)
    lblSmooth.Text = "Suavidade: "..string.format("%.1f",S.Smooth)
end)

-- ABA ESP
local EspConteudo = Instance.new("Frame")
EspConteudo.Parent = Conteudo
EspConteudo.BackgroundTransparency = 1
EspConteudo.Size = UDim2.new(1,0,1,0)
EspConteudo.Visible = false

criarBotaoSwitch(EspConteudo, 10, "Ativar ESP", function() return S.ESP end, function(v) S.ESP = v end)
sep(EspConteudo,48)
criarBotaoSwitch(EspConteudo, 58, "ESP Caixa", function() return S.ESP_Caixa end, function(v) S.ESP_Caixa = v end)
sep(EspConteudo,92)
criarBotaoSwitch(EspConteudo, 102, "ESP Nome", function() return S.ESP_Nome end, function(v) S.ESP_Nome = v end)
sep(EspConteudo,136)
criarBotaoSwitch(EspConteudo, 146, "ESP Vida", function() return S.ESP_Vida end, function(v) S.ESP_Vida = v end)
sep(EspConteudo,180)
criarBotaoSwitch(EspConteudo, 190, "ESP Linha", function() return S.ESP_Linha end, function(v) S.ESP_Linha = v end)
sep(EspConteudo,222)
criarBotaoSwitch(EspConteudo, 232, "Mostrar Distância", function() return S.ESP_Distancia end, function(v) S.ESP_Distancia = v end)

print("✅ PARTE 2 CARREGADA - ABA AIMBOT + ESP")
-- @Noobzinx v4 - PARTE 3
-- ABA CONFIGURAÇÕES
local ConfConteudo = Instance.new("Frame")
ConfConteudo.Parent = Conteudo
ConfConteudo.BackgroundTransparency = 1
ConfConteudo.Size = UDim2.new(1,0,1,0)
ConfConteudo.Visible = false

criarBotaoSwitch(ConfConteudo, 10, "Modo Veloz", function() return S.Speed end, function(v) S.Speed = v end)
sep(ConfConteudo,48)
local lblVel = Instance.new("TextLabel")
lblVel.Parent = ConfConteudo
lblVel.BackgroundTransparency = 1
lblVel.Size = UDim2.new(0.40,0,0,24)
lblVel.Position = UDim2.new(0.05,0,0,58)
lblVel.Text = "Velocidade: "..S.SpeedMul
lblVel.TextColor3 = Color3.fromRGB(255,255,255)
lblVel.TextScaled = true

local bVelMenos = Instance.new("TextButton")
bVelMenos.Parent = ConfConteudo
bVelMenos.BackgroundColor3 = Color3.fromRGB(50,50,50)
bVelMenos.Size = UDim2.new(0.12,0,0,24)
bVelMenos.Position = UDim2.new(0.55,0,0,58)
bVelMenos.Text = "-"
bVelMenos.TextScaled = true
Instance.new("UICorner",bVelMenos).CornerRadius = UDim.new(0,6)
bVelMenos.MouseButton1Click:Connect(function()
    S.SpeedMul = math.max(S.SpeedMul-5,16)
    lblVel.Text = "Velocidade: "..S.SpeedMul
end)

local bVelMais = Instance.new("TextButton")
bVelMais.Parent = ConfConteudo
bVelMais.BackgroundColor3 = Color3.fromRGB(120,0,200)
bVelMais.Size = UDim2.new(0.12,0,0,24)
bVelMais.Position = UDim2.new(0.70,0,0,58)
bVelMais.Text = "+"
bVelMais.TextScaled = true
Instance.new("UICorner",bVelMais).CornerRadius = UDim.new(0,6)
bVelMais.MouseButton1Click:Connect(function()
    S.SpeedMul = math.min(S.SpeedMul+5,200)
    lblVel.Text = "Velocidade: "..S.SpeedMul
end)
sep(ConfConteudo,92)
criarBotaoSwitch(ConfConteudo, 102, "Super Pulo", function() return S.SuperJump end, function(v) S.SuperJump = v end)
sep(ConfConteudo,136)
criarBotaoSwitch(ConfConteudo, 146, "Atravessar Paredes", function() return S.AtravessarParede end, function(v) S.AtravessarParede = v end)
sep(ConfConteudo,180)
criarBotaoSwitch(ConfConteudo, 190, "Cores Arco-Íris", function() return S.Rainbow end, function(v) S.Rainbow = v end)
sep(ConfConteudo,222)
criarBotaoSwitch(ConfConteudo, 232, "🎯 Hitbox Ampliada", function() return S.HitboxAmpliada end, function(v) 
    S.HitboxAmpliada = v 
    if v then
        print("🎯 Hitbox Ampliada ATIVADA - Players congelam!")
        ativarHitbox()
    else
        print("🎯 Hitbox Ampliada DESATIVADA")
        desativarHitbox()
    end
end)
sep(ConfConteudo,266)
criarBotaoSwitch(ConfConteudo, 276, "🔄 Girar Rápido", function() return S.GirarRapido end, function(v) 
    S.GirarRapido = v 
    if v then
        print("🔄 Girar Rápido ATIVADO - Giro turbo!")
        ativarGirar()
    else
        print("🔄 Girar Rápido DESATIVADO")
        desativarGirar()
    end
end)
sep(ConfConteudo,310)
criarBotaoSwitch(ConfConteudo, 320, "💀 Puxar Players", function() return S.KillAll end, function(v) 
    S.KillAll = v 
    if v then
        print("💀 Puxar Players ATIVADO - Puxando todos para sua frente!")
        puxarPlayers()
    else
        print("💀 Puxar Players DESATIVADO")
    end
end)

-- ABA INFO
local InfoConteudo = Instance.new("Frame")
InfoConteudo.Parent = Conteudo
InfoConteudo.BackgroundTransparency = 1
InfoConteudo.Size = UDim2.new(1,0,1,0)
InfoConteudo.Visible = false

local avisoTopo = Instance.new("TextLabel")
avisoTopo.Parent = InfoConteudo
avisoTopo.BackgroundTransparency = 1
avisoTopo.Size = UDim2.new(0.9,0,0,30)
avisoTopo.Position = UDim2.new(0.05,0,0,10)
avisoTopo.Text = "⚠️ USO POR CONTA E RISCO DO USUÁRIO"
avisoTopo.TextColor3 = Color3.fromRGB(255,60,60)
avisoTopo.Font = Enum.Font.GothamBold
avisoTopo.TextScaled = true

local lblFPS = Instance.new("TextLabel")
lblFPS.Parent = InfoConteudo
lblFPS.BackgroundTransparency = 1
lblFPS.Size = UDim2.new(0.8,0,0,26)
lblFPS.Position = UDim2.new(0.1,0,0,52)
lblFPS.Text = "FPS: Carregando..."
lblFPS.TextColor3 = Color3.fromRGB(80,255,80)
lblFPS.TextScaled = true

local dados = {
    {"Script:","Noobzinx"},
    {"Versão:","v4"},
    {"Desenvolvedor:","@Noobzinx"},
    {"Data:",os.date("%d/%m/%Y")},
    {"Status:","Operacional"}
}

for i,item in ipairs(dados) do
    local y = 88 + ((i-1)*32)
    local tEsq = Instance.new("TextLabel")
    tEsq.Parent = InfoConteudo
    tEsq.BackgroundTransparency = 1
    tEsq.Size = UDim2.new(0.35,0,0,26)
    tEsq.Position = UDim2.new(0.08,0,0,y)
    tEsq.Text = item[1]
    tEsq.TextColor3 = Color3.fromRGB(120,0,200)
    tEsq.TextScaled = true
    tEsq.TextXAlignment = Enum.TextXAlignment.Right

    local tDir = Instance.new("TextLabel")
    tDir.Parent = InfoConteudo
    tDir.BackgroundTransparency = 1
    tDir.Size = UDim2.new(0.45,0,0,26)
    tDir.Position = UDim2.new(0.50,0,0,y)
    tDir.Text = item[2]
    tDir.TextColor3 = Color3.fromRGB(255,255,255)
    tDir.TextScaled = true
end

local function mudarAba(btnAtivo, painelVisivel)
    bAim.BackgroundColor3 = Color3.fromRGB(35,35,35)
    bEsp.BackgroundColor3 = Color3.fromRGB(35,35,35)
    bConf.BackgroundColor3 = Color3.fromRGB(35,35,35)
    bInfo.BackgroundColor3 = Color3.fromRGB(35,35,35)
    btnAtivo.BackgroundColor3 = Color3.fromRGB(120,0,200)
    AimConteudo.Visible = false
    EspConteudo.Visible = false
    ConfConteudo.Visible = false
    InfoConteudo.Visible = false
    painelVisivel.Visible = true
end

bAim.MouseButton1Click:Connect(function() mudarAba(bAim,AimConteudo) end)
bEsp.MouseButton1Click:Connect(function() mudarAba(bEsp,EspConteudo) end)
bConf.MouseButton1Click:Connect(function() mudarAba(bConf,ConfConteudo) end)
bInfo.MouseButton1Click:Connect(function() mudarAba(bInfo,InfoConteudo) end)

print("✅ PARTE 3 CARREGADA - ABA CONFIGURAÇÕES + INFO")
-- @Noobzinx v4 - PARTE 4 (FPS MAIS LENTO)
-- ════════════ HITBOX AMPLIADA (CONGELA PLAYERS) ════════════
local hitboxConnection = nil

function ativarHitbox()
    if hitboxConnection then 
        hitboxConnection:Disconnect()
        hitboxConnection = nil
    end
    if not S.HitboxAmpliada then return end
    
    hitboxConnection = RS.RenderStepped:Connect(function()
        if not S.HitboxAmpliada then 
            desativarHitbox()
            return 
        end
        
        for _, p in pairs(P:GetPlayers()) do
            if p == LP then continue end
            if not p.Character then continue end
            local hum = p.Character:FindFirstChild("Humanoid")
            if not hum or hum.Health <= 0 then continue end
            
            for _, parte in pairs(p.Character:GetChildren()) do
                if parte:IsA("BasePart") and parte.Name ~= "HumanoidRootPart" then
                    parte.Size = Vector3.new(8, 8, 8)
                    parte.Transparency = 0
                    parte.CanCollide = true
                end
            end
        end
    end)
end

function desativarHitbox()
    if hitboxConnection then
        hitboxConnection:Disconnect()
        hitboxConnection = nil
    end
    for _, p in pairs(P:GetPlayers()) do
        if p == LP then continue end
        if not p.Character then continue end
        for _, parte in pairs(p.Character:GetChildren()) do
            if parte:IsA("BasePart") and parte.Name ~= "HumanoidRootPart" then
                parte.Size = Vector3.new(2, 2, 2)
                parte.Transparency = 0
                parte.CanCollide = true
            end
        end
    end
end

-- ════════════ GIRAR RÁPIDO ════════════
local girarConnection = nil

function ativarGirar()
    if girarConnection then
        girarConnection:Disconnect()
        girarConnection = nil
    end
    if not S.GirarRapido then return end
    
    girarConnection = RS.RenderStepped:Connect(function()
        if not S.GirarRapido then
            if girarConnection then
                girarConnection:Disconnect()
                girarConnection = nil
            end
            return
        end
        
        local char = LP.Character
        if not char then return end
        local root = char:FindFirstChild("HumanoidRootPart")
        if not root then return end
        local hum = char:FindFirstChild("Humanoid")
        if not hum or hum.Health <= 0 then return end
        
        local rootJoint = char:FindFirstChild("RootJoint")
        if rootJoint then
            local anguloAtual = rootJoint.C0
            local novoAngulo = anguloAtual * CFrame.Angles(0, math.rad(50), 0)
            rootJoint.C0 = novoAngulo
        else
            root.CFrame = root.CFrame * CFrame.Angles(0, math.rad(50), 0)
        end
    end)
end

function desativarGirar()
    if girarConnection then
        girarConnection:Disconnect()
        girarConnection = nil
    end
    local char = LP.Character
    if char then
        local rootJoint = char:FindFirstChild("RootJoint")
        if rootJoint then
            rootJoint.C0 = CFrame.new(0, 0, 0) * CFrame.Angles(0, 0, 0)
        end
    end
end

-- ════════════ PUXAR PLAYERS (SÓ PUXA, NÃO MATA) ════════════
function puxarPlayers()
    if not S.KillAll then return end
    
    local players = P:GetPlayers()
    local puxados = 0
    
    for _, p in pairs(players) do
        if p ~= LP and p.Character then
            local hum = p.Character:FindFirstChild("Humanoid")
            if hum and hum.Health > 0 then
                local root = p.Character:FindFirstChild("HumanoidRootPart")
                if root then
                    local pos = C.CFrame.Position + C.CFrame.LookVector * 3
                    root.CFrame = CFrame.new(pos)
                    puxados = puxados + 1
                end
            end
        end
    end
    
    print("💀 "..puxados.." players puxados para sua frente!")
end

-- ════════════ FIM PUXAR PLAYERS ════════════

-- ESP
local desenhosESP = {}
local tempoCor = 0

local function pegarCorRainbow()
    tempoCor = tempoCor + 0.015
    return Color3.fromHSV(tempoCor % 1, 1, 1)
end

P.PlayerRemoving:Connect(function(p)
    if desenhosESP[p] then
        for _,obj in pairs(desenhosESP[p]) do obj:Remove() end
        desenhosESP[p] = nil
    end
end)

-- 🔥 CONTADOR DE FPS MAIS LENTO (ATUALIZA A CADA 1 SEGUNDO)
local fpsTimer = 0
local fpsAtual = 0

RS.Heartbeat:Connect(function(delta)
    -- Atualiza FPS a cada 1 segundo (em vez de todo frame)
    fpsTimer = fpsTimer + delta
    if fpsTimer >= 1 then
        fpsAtual = math.floor(1/delta)
        fpsTimer = 0
        if lblFPS then
            lblFPS.Text = "FPS: "..fpsAtual
        end
    end

    local char = LP.Character
    if char and char:FindFirstChild("Humanoid") then
        local hum = char.Humanoid
        hum.WalkSpeed = S.Speed and S.SpeedMul or 16
        hum.JumpHeight = S.SuperJump and 35 or 2
        
        for _,parte in pairs(char:GetChildren()) do
            if parte:IsA("BasePart") then parte.CanCollide = not S.AtravessarParede end
        end
    end

    for ply in pairs(desenhosESP) do
        if not ply.Character or not ply.Character:FindFirstChild("Humanoid") or ply.Character.Humanoid.Health <= 0 then
            for _,obj in pairs(desenhosESP[ply]) do obj:Remove() end
            desenhosESP[ply] = nil
        end
    end

    if not S.ESP then
        for _,d in pairs(desenhosESP) do
            d.box.Visible = false
            d.bgVida.Visible = false
            d.barraVida.Visible = false
            d.name.Visible = false
            d.linha.Visible = false
            d.dist.Visible = false
        end
        return
    end

    for _,p in pairs(P:GetPlayers()) do
        if p ~= LP and not desenhosESP[p] then
            desenhosESP[p] = {
                box = Drawing.new("Square"),
                bgVida = Drawing.new("Square"),
                barraVida = Drawing.new("Square"),
                name = Drawing.new("Text"),
                linha = Drawing.new("Line"),
                dist = Drawing.new("Text")
            }
            desenhosESP[p].box.Thickness = 3
            desenhosESP[p].bgVida.Filled = true
            desenhosESP[p].bgVida.Color = Color3.fromRGB(30,30,30)
            desenhosESP[p].barraVida.Filled = true
            desenhosESP[p].barraVida.Color = Color3.fromRGB(0,210,0)
            desenhosESP[p].name.Color = Color3.fromRGB(255,200,0)
            desenhosESP[p].linha.Thickness = 2
            desenhosESP[p].dist.Color = Color3.fromRGB(255,255,255)
        end
    end

    for p,d in pairs(desenhosESP) do
        if not p.Character then continue end
        local root = p.Character:FindFirstChild("HumanoidRootPart")
        local hum = p.Character:FindFirstChild("Humanoid")
        if not root or not hum or hum.Health <= 0 then continue end
        local pos,on = C:WorldToViewportPoint(root.Position)
        if not on then d.box.Visible=false; continue end

        local cor = S.Rainbow and pegarCorRainbow() or Color3.fromRGB(255,0,0)
        d.box.Color = cor
        d.linha.Color = cor

        d.box.Visible = S.ESP_Caixa
        d.name.Visible = S.ESP_Nome
        d.bgVida.Visible = S.ESP_Vida
        d.barraVida.Visible = S.ESP_Vida
        d.linha.Visible = S.ESP_Linha
        d.dist.Visible = S.ESP_Distancia

        if S.ESP_Caixa then
            local tam = math.clamp(380/pos.Z,8,700)
            d.box.Size = Vector2.new(tam,tam*1.8)
            d.box.Position = Vector2.new(pos.X-tam/2,pos.Y-tam)
        end
        if S.ESP_Nome then
            d.name.Text = p.Name
            d.name.Position = Vector2.new(pos.X,pos.Y-50)
        end
        if S.ESP_Vida then
            local porc = math.max(hum.Health/hum.MaxHealth,0)
            d.bgVida.Size = Vector2.new(5,50)
            d.bgVida.Position = Vector2.new(pos.X-45,pos.Y-35)
            d.barraVida.Size = Vector2.new(5,50*porc)
            d.barraVida.Position = Vector2.new(pos.X-45,pos.Y-35+(50*(1-porc)))
        end
        if S.ESP_Linha then
            d.linha.From = Vector2.new(C.ViewportSize.X/2,C.ViewportSize.Y)
            d.linha.To = Vector2.new(pos.X,pos.Y)
        end
        if S.ESP_Distancia then
            d.dist.Text = math.floor((root.Position - C.CFrame.Position).Magnitude).."m"
            d.dist.Position = Vector2.new(pos.X,pos.Y+40)
        end
    end
end)

-- ════════════ AIMBOT (SÓ MIRA EM INIMIGOS) ════════════
local circuloFOV = Drawing.new("Circle")
circuloFOV.Thickness = 4
circuloFOV.Color = Color3.fromRGB(255,0,0)

function jogadorValido(p)
    if not p or p == LP then return false end
    if not p.Character then return false end
    
    local hum = p.Character:FindFirstChild("Humanoid")
    if not hum or hum.Health <= 0 then return false end
    
    if not p.Character:FindFirstChild(S.TargetPart) then return false end
    
    local meuTime = LP.Team
    local timeInimigo = p.Team
    
    if meuTime and timeInimigo and meuTime ~= timeInimigo then
        return true
    end
    
    if not meuTime and not timeInimigo then
        return true
    end
    
    if meuTime and not timeInimigo then
        return true
    end
    
    if not meuTime and timeInimigo then
        return true
    end
    
    if meuTime == timeInimigo then
        return false
    end
    
    return true
end

function visivel(p)
    local pt = p.Character[S.TargetPart]
    if not pt then return false end
    local ray = RaycastParams.new()
    ray.FilterDescendantsInstances = {LP.Character}
    ray.FilterType = Enum.RaycastFilterType.Exclude
    local res = workspace:Raycast(C.CFrame.Position, (pt.Position - C.CFrame.Position)*1000, ray)
    return not res or res.Instance:IsDescendantOf(p.Character)
end

function pegarAlvo()
    local alvo,dist = nil,S.FOV
    local centro = Vector2.new(C.ViewportSize.X/2,C.ViewportSize.Y/2)
    for _,p in pairs(P:GetPlayers()) do
        if jogadorValido(p) then
            local part = p.Character:FindFirstChild(S.TargetPart)
            if part then
                local pos,tela = C:WorldToViewportPoint(part.Position)
                if tela then
                    local d = (Vector2.new(pos.X,pos.Y)-centro).Magnitude
                    if d < dist and visivel(p) then dist=d; alvo=p end
                end
            end
        end
    end
    return alvo
end

RS.RenderStepped:Connect(function()
    circuloFOV.Position = Vector2.new(C.ViewportSize.X/2,C.ViewportSize.Y/2)
    circuloFOV.Radius = S.FOV
    circuloFOV.Visible = S.MostrarFOV

    if S.Aimbot then
        local alvo = pegarAlvo()
        if alvo then
            local part = alvo.Character:FindFirstChild(S.TargetPart)
            if part then
                local nova = CFrame.new(C.CFrame.Position, part.Position)
                C.CFrame = C.CFrame:Lerp(nova,1 - S.Smooth)
            end
        end
    end
end)

-- Inicia funções se já estiverem ativadas
if S.HitboxAmpliada then ativarHitbox() end
if S.GirarRapido then ativarGirar() end

print("✅ @Noobzinx v4 - PARTE 4 CARREGADA!")
print("🦘 SUPER JUMP AUMENTADO!")
print("🎯 AIMBOT SÓ MIRA EM INIMIGOS!")
print("📊 FPS ATUALIZA A CADA 1 SEGUNDO!")
