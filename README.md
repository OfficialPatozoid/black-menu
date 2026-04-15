– ============================================================ – BLACK
MENU - Sistema de Key – Interface simples e organizada –
============================================================

local Players = game:GetService(“Players”) local TweenService =
game:GetService(“TweenService”) local UserInputService =
game:GetService(“UserInputService”)

local player = Players.LocalPlayer local playerGui =
player:WaitForChild(“PlayerGui”)

– Banco de Keys local KEYS = {
    ["GS_GOSOTOSO"] = "KEY-EF1BF9C7-CD4FDBD8-2FA5ACB9",
    ["PATOZOID"] = "KEY-B4589BD9-4ACCDEBC-14B90510"
}

– Criar GUI local gui = Instance.new(“ScreenGui”) gui.Name = “BlackMenu”
gui.ResetOnSpawn = false gui.Parent = playerGui

local main = Instance.new(“Frame”) main.Size = UDim2.new(0,0,0,0)
main.Position = UDim2.new(.5,-250,.5,-200) main.BackgroundColor3 =
Color3.fromRGB(0,26,77) main.Parent = gui

Instance.new(“UICorner”,main)

– Animação de abertura TweenService:Create( main,
TweenInfo.new(.4,Enum.EasingStyle.Back), {Size = UDim2.new(0,500,0,400)}
):Play()

– Header local header = Instance.new(“TextLabel”) header.Size =
UDim2.new(1,0,0,50) header.BackgroundColor3 = Color3.fromRGB(0,0,0)
header.Text = “BLACK MENU” header.TextColor3 = Color3.new(1,1,1)
header.Font = Enum.Font.GothamBold header.TextSize = 24 header.Parent =
main

– Campo Key local keyBox = Instance.new(“TextBox”) keyBox.Size =
UDim2.new(.8,0,0,40) keyBox.Position = UDim2.new(.1,0,.3,0)
keyBox.PlaceholderText = “Digite sua Key” keyBox.BackgroundColor3 =
Color3.fromRGB(0,40,100) keyBox.TextColor3 = Color3.fromRGB(0,255,150)
keyBox.Parent = main Instance.new(“UICorner”,keyBox)

– Campo Usuário local userBox = Instance.new(“TextBox”) userBox.Size =
UDim2.new(.8,0,0,40) userBox.Position = UDim2.new(.1,0,.45,0)
userBox.PlaceholderText = “Usuário” userBox.BackgroundColor3 =
Color3.fromRGB(0,40,100) userBox.TextColor3 = Color3.fromRGB(0,255,150)
userBox.Parent = main Instance.new(“UICorner”,userBox)

– Status local status = Instance.new(“TextLabel”) status.Size =
UDim2.new(.8,0,0,30) status.Position = UDim2.new(.1,0,.6,0)
status.BackgroundTransparency = 1 status.Text = “Aguardando…”
status.TextColor3 = Color3.fromRGB(200,200,200) status.Parent = main

– Botão verificar local verify = Instance.new(“TextButton”) verify.Size
= UDim2.new(.35,0,0,40) verify.Position = UDim2.new(.1,0,.75,0)
verify.Text = “VERIFICAR” verify.BackgroundColor3 =
Color3.fromRGB(0,150,255) verify.Parent = main
Instance.new(“UICorner”,verify)

– Botão limpar local clear = Instance.new(“TextButton”) clear.Size =
UDim2.new(.35,0,0,40) clear.Position = UDim2.new(.55,0,.75,0) clear.Text
= “LIMPAR” clear.BackgroundColor3 = Color3.fromRGB(150,0,0)
clear.TextColor3 = Color3.new(1,1,1) clear.Parent = main
Instance.new(“UICorner”,clear)

– Barra de loading local barBg = Instance.new(“Frame”) barBg.Size =
UDim2.new(.8,0,0,25) barBg.Position = UDim2.new(.1,0,.9,0)
barBg.BackgroundColor3 = Color3.fromRGB(30,30,50) barBg.Parent = main

local bar = Instance.new(“Frame”) bar.Size = UDim2.new(0,0,1,0)
bar.BackgroundColor3 = Color3.fromRGB(0,200,255) bar.Parent = barBg

– Sistema draggable local dragging local dragStart local startPos

main.InputBegan:Connect(function(input) if input.UserInputType ==
Enum.UserInputType.MouseButton1 then dragging = true dragStart =
input.Position startPos = main.Position end end)

main.InputEnded:Connect(function(input) if input.UserInputType ==
Enum.UserInputType.MouseButton1 then dragging = false end end)

UserInputService.InputChanged:Connect(function(input) if dragging then
local delta = input.Position - dragStart main.Position = UDim2.new(
startPos.X.Scale, startPos.X.Offset + delta.X, startPos.Y.Scale,
startPos.Y.Offset + delta.Y ) end end)

– Loading local function loading() for i=1,100 do bar.Size =
UDim2.new(i/100,0,1,0) task.wait(.02) end end

– Verificação de key local function verifyKey()

local user = userBox.Text:upper() local key = keyBox.Text

if KEYS[user] and KEYS[user] == key then

status.Text = “Key válida” status.TextColor3 = Color3.fromRGB(0,255,100)

loading()

status.Text = “Acesso liberado”

print(“Sistema autenticado”) print(“Usuário:”,user)

else

status.Text = “Key inválida” status.TextColor3 = Color3.fromRGB(255,0,0)

end

end

verify.MouseButton1Click:Connect(verifyKey)

clear.MouseButton1Click:Connect(function() keyBox.Text = “” userBox.Text
= “” status.Text = “Campos limpos” status.TextColor3 =
Color3.fromRGB(0,200,255) end)

– Enter para verificar keyBox.FocusLost:Connect(function(enter) if enter
then verifyKey() end end)

userBox.FocusLost:Connect(function(enter) if enter then verifyKey() end
end)

– crédito discreto dentro da interface (quase invisível) local credit =
Instance.new(“TextLabel”) credit.Size = UDim2.new(1,0,0,20)
credit.Position = UDim2.new(0,0,1,-20) credit.BackgroundTransparency = 1
credit.Text = “progaming by @ guh_samuel” credit.TextTransparency = 0.85
credit.TextColor3 = Color3.fromRGB(255,255,255) credit.Font =
Enum.Font.Gotham credit.TextSize = 10 credit.Parent = main
