--// Criar uma função para verificar se um obstáculo é impossível ou não \\--
local function verificarImpossivel(obstaculo)
    --// Obter a posição e o tamanho do obstáculo \\--
    local posicao = obstaculo.Position
    local tamanho = obstaculo.Size
    
    --// Obter a distância entre o obstáculo e o jogador \\--
    local jogador = game.Players.LocalPlayer
    local distancia = (posicao - jogador.Character.HumanoidRootPart.Position).Magnitude
    
    --// Obter a velocidade do jogador \\--
    local velocidade = jogador.Character.Humanoid.WalkSpeed
    
    --// Calcular o tempo necessário para atravessar o obstáculo \\--
    local tempo = distancia / velocidade
    
    --// Verificar se o obstáculo tem alguma propriedade que o torne impossível \\--
    local impossivel = false
    
    --// Se o obstáculo for invisível, ele é impossível \\--
    if obstaculo.Transparency == 1 then
        impossivel = true
    end
    
    --// Se o obstáculo for muito pequeno, ele é impossível \\--
    if tamanho.X < 0.1 or tamanho.Y < 0.1 or tamanho.Z < 0.1 then
        impossivel = true
    end
    
    --// Se o obstáculo for muito rápido, ele é impossível \\--
    if obstaculo:IsA("BasePart") and obstaculo.Velocity.Magnitude > 100 then
        impossivel = true
    end
    
    --// Se o obstáculo for muito longe, ele é impossível \\--
    if distancia > 100 then
        impossivel = true
    end
    
    --// Se o obstáculo for muito alto, ele é impossível \\--
    if posicao.Y - jogador.Character.HumanoidRootPart.Position.Y > 50 then
        impossivel = true
    end
    
    --// Se o obstáculo for muito baixo, ele é impossível \\--
    if jogador.Character.HumanoidRootPart.Position.Y - posicao.Y > 50 then
        impossivel = true
    end
    
    --// Se o obstáculo for muito inclinado, ele é impossível \\--
    if obstaculo:IsA("BasePart") and math.abs(obstaculo.Rotation.X) > 45 or math.abs(obstaculo.Rotation.Y) > 45 or math.abs(obstaculo.Rotation.Z) > 45 then
        impossivel = true
    end
    
    --// Se o obstáculo for muito escorregadio, ele é impossível \\--
    if obstaculo:IsA("BasePart") and obstaculo.Friction < 0.1 then
        impossivel = true
    end
    
    --// Se o obstáculo for muito quente, ele é impossível \\--
    if obstaculo:IsA("BasePart") and obstaculo.Temperature > 100 then
        impossivel = true
    end
    
    --// Se o obstáculo for muito frio, ele é impossível \\--
    if obstaculo:IsA("BasePart") and obstaculo.Temperature < -100 then
        impossivel = true
    end
    
    --// Se o obstáculo for muito elétrico, ele é impossível \\--
    if obstaculo:IsA("BasePart") and obstaculo.Electricity > 100 then
        impossivel = true
    end
    
    --// Se o obstáculo for muito magnético, ele é impossível \\--
    if obstaculo:IsA("BasePart") and obstaculo.Magnetism > 100 then
        impossivel = true
    end
    
    --// Se o obstáculo for muito radioativo, ele é impossível \\--
    if obstaculo:IsA("BasePart") and obstaculo.Radiation > 100 then
        impossivel = true
    end
    
    --// Se o obstáculo for muito explosivo, ele é impossível \\--
    if obstaculo:IsA("BasePart") and obstaculo.Explosion > 100 then
        impossivel = true
    end
    
    --// Se o obstáculo for muito venenoso, ele é impossível \\--
    if obstaculo:IsA("BasePart") and obstaculo.Poison > 100 then
        impossivel = true
    end
    
    --// Se o obstáculo for muito ácido, ele é impossível \\--
    if obstaculo:IsA("BasePart") and obstaculo.Acid > 100 then
        impossivel = true
    end
    
    --// Se o obstáculo for muito pegajoso, ele é impossível \\--
    if obstaculo:IsA("BasePart") and obstaculo.Sticky > 100 then
        impossivel = true
    end
    
    --// Se o obstáculo for muito afiado, ele é impossível \\--
    if obstaculo:IsA("BasePart") and obstaculo.Sharpness > 100 then
        impossivel = true
    end
    
    --// Se o obstáculo for muito pesado, ele é impossível \\--
    if obstaculo:IsA("BasePart") and obstaculo.Mass > 100 then
        impossivel = true
    end
    
    --// Se o obstáculo for muito leve, ele é impossível \\--
    if obstaculo:IsA("BasePart") and obstaculo.Mass < 0.1 then
        impossivel = true
    end
    
    --// Se o obstáculo for muito barulhento, ele é impossível \\--
    if obstaculo:IsA("BasePart") and obstaculo.SoundLevel > 100 then
        impossivel = true
    end
    
    --// Se o obstáculo for muito silencioso, ele é impossível \\--
    if obstaculo:IsA("BasePart") and obstaculo.SoundLevel < 0.1 then
        impossivel = true
    end
    
    --// Se o obstáculo for muito brilhante, ele é impossível \\--
    if obstaculo:IsA("BasePart") and obstaculo.LightLevel > 100 then
        impossivel = true
    end
    
    --// Se o obstáculo for muito escuro, ele é impossível \\--
    if obstaculo:IsA("BasePart") and obstaculo.LightLevel < 0.1 then
        impossivel = true
    end
    
    --// Se o obstáculo for muito colorido, ele é impossível \\--
    if obstaculo:IsA("BasePart") and obstaculo.Color.Saturation > 0.9 then
        impossivel = true
    end
    
    --// Se o obstáculo for muito cinza, ele é impossível \\--
    if obstaculo:IsA("BasePart") and obstaculo.Color.Saturation < 0.1 then
        impossivel = true
    end
    
    --// Retornar o resultado \\--
    return impossivel
end

--// Criar uma função para marcar os obstáculos impossíveis com uma cor vermelha \\--
local function marcarImpossiveis()
    --// Obter todos os obstáculos do mapa \\--
    local mapa = game.Workspace:FindFirstChild("Map")
    local obstaculos = mapa:GetDescendants()
    
    --// Percorrer cada obstáculo \\--
    for i, obstaculo in ipairs(obstaculos) do
        --// Verificar se o obstáculo é impossível \\--
        local impossivel = verificarImpossivel(obstaculo)
        
        --// Se for impossível, mudar a cor para vermelho \\--
        if impossivel then
            obstaculo.Color = Color3.new(1, 0, 0)
        end
    end
end

--// Chamar a função para marcar os obstáculos impossíveis \\--
marcarImpossiveis()
