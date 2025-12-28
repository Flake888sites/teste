local OrionLib = loadstring(game:HttpGet(('raw.githubusercontent.com')))()
local Window = OrionLib:MakeWindow({Name = "Teste Anti-Cheat: Kick System", HidePremium = false, SaveConfig = true, ConfigFolder = "AC_Test"})

local targetPlayer = ""

local Tab = Window:MakeTab({
	Name = "Admin Abuse Test",
	Icon = "rbxassetid://4483345998",
	PremiumOnly = false
})

Tab:AddTextbox({
	Name = "Nome do Jogador",
	Default = "",
	TextDisappear = false,
	Callback = function(Value)
		targetPlayer = Value
	end	
})

Tab:AddButton({
	Name = "Executar Kick (Remote Test)",
	Callback = function()
        -- NOTA: Para funcionar, você deve ajustar o caminho abaixo para o RemoteEvent do SEU jogo
        -- Exemplo genérico de tentativa de abuso de RemoteEvent:
        local playerToKick = game.Players:FindFirstChild(targetPlayer)
        
        if playerToKick then
            -- Tenta disparar um evento que seu jogo possui (ex: 'AdminEvent', 'KickPlayer')
            -- Se o seu anti-cheat for bom, ele deve bloquear essa chamada vinda do cliente
            game.ReplicatedStorage.RemoteEvent:FireServer("Kick", playerToKick, "Teste de Vulnerabilidade")
            
            OrionLib:MakeNotification({
                Name = "Comando Enviado",
                Content = "Tentativa de kick enviada para: " .. targetPlayer,
                Image = "rbxassetid://4483345998",
                Duration = 5
            })
        else
            OrionLib:MakeNotification({
                Name = "Erro",
                Content = "Jogador não encontrado.",
                Image = "rbxassetid://4483345998",
                Duration = 5
            })
        end
	end
})

OrionLib:Init()
