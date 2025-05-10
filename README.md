-- byby Hub - Rayfield GUI (Xeno X) - Complete Fixed Version

-- Rayfield Initialization
local Rayfield = nil
local ok, result = pcall(function()
    return loadstring(game:HttpGet('https://sirius.menu/rayfield'))()
end)
if ok and typeof(result) == "table" then
    Rayfield = result
else
    warn("byby Hub: Failed to load Rayfield.")
    return
end

-- Main Window
local Window = Rayfield:CreateWindow({
    Name = "byby Hub",
    LoadingTitle = "byby Hub - ESP & TP Menu",
    LoadingSubtitle = "by Rayfield & Lua Assistant",
    ConfigurationSaving = {
        Enabled = false,
        FolderName = "bybyHubConfigs",
        FileName = "settings.json"
    },
    Discord = {
        Enabled = false,
        Invite = "",
        RememberJoins = false
    },
    KeySystem = false
})

-- Global Variables
getgenv().bybyHubSelectedChapter = nil

-- Chapter Coordinates
local tpCoords = {
    [1] = {
        Exit = Vector3.new(-532.585, 140.72, -365.555),
        SecretRoom = Vector3.new(-414.314, 140.72, -304.094),
        Jail = Vector3.new(-457.791, 159.12, -370.115)
    },
    [2] = {
        Exit = Vector3.new(-134.08067321777344, 31.22078514099121, -591.3446655273438),
        SecretRoom = Vector3.new(-57.15787124633789, 25.520776748657227, -428.05889892578125),
        Jail = Vector3.new(-72.49606323242188, 25.59160041809082, -545.547607421875)
    },
    [3] = {
        Exit = Vector3.new(-69.16622161865234, 34.79659652709961, -1214.30078125),
        SecretRoom = Vector3.new(-85.52113342285156, 49.9326667856445, -1181.557373046875),
        Jail = Vector3.new(23.55693817138672, 31.33051300048828, -1102.6610107421875)
    },
    [4] = {
        Exit = Vector3.new(604.6543579101562, 226.8690643310547, -565.8380126953125),
        SecretRoom = Vector3.new(672.8678588867188, 171.8092803955078, -549.7329711914062),
        Jail = Vector3.new(818.5095825195312, 143.00930786132812, -477.64892578125)
    },
    [5] = {
        Exit = Vector3.new(646.42138671875, 366.5447998046875, -1559.5479736328125),
        SecretRoom = Vector3.new(716.4080200195312, 389.1798400878906, -1500.7994384765625),
        Jail = Vector3.new(739.3493041992188, 366.5447998046875, -1443.839111328125)
    },
    [6] = {
        Jail = Vector3.new(1363.5147705078125, 352.2150573730469, -1099.87255859375),
        SecretRoom = Vector3.new(-1337.9598388671875, 317.1018371582031, -971.1986694335938),
        Exit = Vector3.new(-1409.094482421875, 327.9960632324219, -1187.8861083984375)
    },
    [7] = {
        Jail = Vector3.new(-2231.973876953125, 418.868408203125, 339.1729736328125),
        SecretRoom = Vector3.new(-2315.53759765625, 410.1636962890625, 318.80731201171875),
        Exit = Vector3.new(-2334.33740234375, 343.2521667480469, 375.66534423828125)
    },
    [8] = {
        Jail = Vector3.new(660.3225708007812, 125.17597198486328, 738.5668334960938),
        SecretRoom = Vector3.new(580.8359985351562, 77.20822143554688, 650.8400268554688),
        Exit = Vector3.new(771.0807495117188, 122.89598083496094, 614.1559448242188)
    },
    [9] = {
        Jail = Vector3.new(-335.8167419433594, 313.5082702636719, -1137.0406494140625),
        SecretRoom = Vector3.new(-409.9374694824219, 328.9419860839844, -1180.7354736328125),
        Exit = Vector3.new(-428.9591064453125, 306.9100341796875, -1083.7926025390625)
    },
    [10] = {
        Jail = Vector3.new(1234.2657470703125, 566.747802734375, -1514.2554931640625),
        SecretRoom = Vector3.new(1295.29150390625, 559.7617797851562, -1462.9559326171875),
        Exit = Vector3.new(1080.3900146484375, 541.5155029296875, -1597.7586669921875)
    },
    [11] = {
        Jail = Vector3.new(-353.5691223144531, 69.00792694091797, 1746.9598388671875),
        SecretRoom = Vector3.new(-198.29249572753906, 130.97793579101562, 2087.26611328125),
        Exit = Vector3.new(-421.38201904296875, 105.10702514648438, 1841.6773681640625)
    },
    [12] = {
        Jail = Vector3.new(1223.8692626953125, 554.091796875, -3053.0771484375),
        SecretRoom = Vector3.new(1336.946044921875, 559.0518798828125, -3153.320068359375),
        Exit = Vector3.new(1321.4249267578125, 564.15478515625, -2876.21044921875)
    },
    [13] = {
        Jail = Vector3.new(-1377.604248046875, 47.40913391113281, 1822.1309814453125),
        SecretRoom = Vector3.new(-1629.793701171875, 31.60614776611328, 1858.04443359375),
        Exit = Vector3.new(-1469.019287109375, 13.844338417053223, 1665.5692138671875)
    },
    [14] = {
        Jail = Vector3.new(-300.2900695800781, 10.800016403198242, -471.6684265136719),
        SecretRoom = Vector3.new(-459.6105041503906, 10.517492294311523, -593.83544921875),
        Exit = Vector3.new(-398.0303955078125, 15.23984241855957, -567.8922729492188)
    },
    [15] = {
        Jail = Vector3.new(672.1546630859375, 445.53839111328125, -1619.6893310546875),
        SecretRoom = Vector3.new(527.2825927734375, 442.95904541015625, -1642.3265380859375),
        Exit = Vector3.new(635.2982788085938, 461.6323547363281, -1461.87890625)
    },
    [16] = {
        Jail = Vector3.new(-457.5530700683594, 164.93563842773438, 0),
        SecretRoom = Vector3.new(-415.25146484375, 151.6641387939453, -301.0619812011719),
        Exit = Vector3.new(-552.70556640625, 141.6520233154297, -367.8219909667969)
    }
}

-- ESP Scripts
local orderedScripts = {
    {name = "Chap 1 ESP", url = "https://pastebin.com/raw/TfjPzuWw", chap = 1},
    {name = "Chap 2 ESP", url = "https://pastebin.com/raw/VQGJmbL1", chap = 2},
    {name = "Chap 3 ESP", url = "https://pastebin.com/raw/SHxZWBtr", chap = 3},
    {name = "Chap 4 ESP", url = "https://pastebin.com/raw/W2jwBc3G", chap = 4},
    {name = "Chap 5 ESP", url = "https://pastebin.com/raw/txkx4EPb", chap = 5},
    {name = "Chap 6 ESP", url = "https://pastebin.com/raw/gNDLrf4f", chap = 6},
    {name = "Chap 7 ESP", url = "https://pastebin.com/raw/CQpEBGh1", chap = 7},
    {name = "Chap 8 ESP", url = "https://pastebin.com/raw/AhikCBmN", chap = 8},
    {name = "Chap 9 ESP", url = "https://pastebin.com/raw/TQmcfgQe", chap = 9},
    {name = "Chap 10 ESP", url = "https://pastebin.com/raw/ikRVJkzP", chap = 10},
    {name = "Chap 11 ESP", url = "https://pastebin.com/raw/hZhD08Cy", chap = 11},
    {name = "Chap 12 ESP", url = "https://pastebin.com/raw/BrHTtS6d", chap = 12},
    {name = "Chap 13 ESP", url = "https://pastebin.com/raw/GyzCyPQU", chap = 13},
    {name = "Chap 14 ESP", url = "https://pastebin.com/raw/mnUDis1a", chap = 14},
    {name = "Chap 15 ESP", url = "https://pastebin.com/raw/bVZ6nnvp", chap = 15},
    {name = "Chap House XMas ESP", url = "https://pastebin.com/raw/NYckaf2t", chap = 16}
}

-- ESP Tab
local ESPsTab = Window:CreateTab("ESP's", 4483362458)
for _, entry in ipairs(orderedScripts) do
    ESPsTab:CreateButton({
        Name = entry.name,
        Callback = function()
            getgenv().bybyHubSelectedChapter = entry.chap
            local success, err = pcall(function()
                loadstring(game:HttpGet(entry.url))()
            end)
            local msg = success and (entry.name .. " ativado!\nTPs agora configurados para este capítulo.") or ("Erro: " .. tostring(err))
            Rayfield:Notify({
                Title = "byby Hub",
                Content = msg,
                Duration = success and 3 or 5,
                Image = 4483362458,
                Actions = {
                    Ignore = {
                        Name = "OK",
                        Callback = function() end
                    }
                }
            })
        end
    })
end

-- TP Tab
local TPsTab = Window:CreateTab("TP's", 4483362458)

-- Generic Teleport Function
local function teleportTo(posVector, label)
    local plr = game.Players.LocalPlayer
    if plr and plr.Character and plr.Character:FindFirstChild("HumanoidRootPart") then
        plr.Character.HumanoidRootPart.CFrame = CFrame.new(posVector)
        Rayfield:Notify({
            Title = "TP Realizado",
            Content = label,
            Duration = 2,
            Image = 4483362458,
            Actions = {
                OK = { Name = "Fechar", Callback = function() end }
            }
        })
    end
end

-- Location TP Buttons
local function tpButton(name, key)
    TPsTab:CreateButton({
        Name = name,
        Callback = function()
            local chap = getgenv().bybyHubSelectedChapter
            if not chap then
                Rayfield:Notify({
                    Title = "byby Hub",
                    Content = "Escolha um ESP do capítulo antes na TAB 'ESP's!",
                    Duration = 4,
                    Image = 4483362458,
                    Actions = {
                        OK = { Name = "Fechar", Callback = function() end }
                    }
                })
                return
            end
            if not tpCoords[chap] or not tpCoords[chap][key] then
                Rayfield:Notify({
                    Title = "byby Hub",
                    Content = "TP não disponível para este capítulo ainda!",
                    Duration = 4,
                    Image = 4483362458,
                    Actions = {
                        OK = { Name = "Fechar", Callback = function() end }
                    }
                })
                return
            end
            teleportTo(tpCoords[chap][key], name)
        end
    })
end

tpButton("Teleportar para Exit", "Exit")
tpButton("Teleportar para Secret Room", "SecretRoom")
tpButton("Teleportar para Jail", "Jail")

-- Exact Item Teleport via Textbox
local validMaps = {
    "House", "Club", "Neighborhood", "Carnival", "Bro Sponge", "Gumbomb", "Mansion",
    "Gravity False", "Sdan Mind", "Magic Friends", "Stevon Universe", "Paw Command",
    "Lapse Adventure", "Nick Buttonski", "The End", "HouseChristmas"
}

local function findExactItem(itemName)
    if not itemName or type(itemName) ~= "string" or itemName == "" then
        return nil
    end

    local ws = game:GetService("Workspace")
    local mapFolder = ws:FindFirstChild("Map")
    if not mapFolder then return nil end

    for _, mapName in ipairs(validMaps) do
        local map = mapFolder:FindFirstChild(mapName)
        if map then
            local tools = map:FindFirstChild("Tools")
            if tools then
                local item = tools:FindFirstChild(itemName)
                if item and item:IsA("Model") then
                    local part = item.PrimaryPart or item:FindFirstChildWhichIsA("BasePart", true)
                    if part then
                        return {
                            displayName = mapName .. " - " .. item.Name,
                            part = part,
                            item = item
                        }
                    end
                end
            end
        end
    end
    return nil
end

TPsTab:CreateInput({
    Name = "TP para Item (Nome Exato)",
    PlaceholderText = "Digite o nome EXATO como aparece no Explorer",
    RemoveTextAfterFocusLost = false,
    Callback = function(inputText)
        -- Input validation
        if not inputText or inputText == "" then
            Rayfield:Notify({
                Title = "Erro",
                Content = "Por favor digite um nome de item!",
                Duration = 3,
                Image = 4483362458
            })
            return
        end

        -- Find item safely
        local success, foundItem = pcall(function()
            return findExactItem(inputText)
        end)

        if not success then
            Rayfield:Notify({
                Title = "Erro na Busca",
                Content = "Ocorreu um erro ao procurar o item: "..tostring(foundItem),
                Duration = 5,
                Image = 4483362458
            })
            return
        end

        -- Item validation
        if not foundItem or not foundItem.part or not foundItem.part.Parent then
            Rayfield:Notify({
                Title = "Item Não Encontrado",
                Content = "Nenhum item com o nome exato '"..inputText.."' foi encontrado!",
                Duration = 4,
                Image = 4483362458
            })
            return
        end

        -- Player validation
        local plr = game.Players.LocalPlayer
        if not plr or not plr.Character or not plr.Character:FindFirstChild("HumanoidRootPart") then
            Rayfield:Notify({
                Title = "Erro de Personagem",
                Content = "Seu personagem não está pronto para teleportar!",
                Duration = 3,
                Image = 4483362458
            })
            return
        end

        -- Final teleport with safety checks
        if foundItem.part and foundItem.part:IsA("BasePart") and foundItem.part:IsDescendantOf(game) then
            local targetCFrame = foundItem.part.CFrame * CFrame.new(0, 3, 0)
            local teleportSuccess, teleportError = pcall(function()
                plr.Character.HumanoidRootPart.CFrame = targetCFrame
            end)

            if teleportSuccess then
                Rayfield:Notify({
                    Title = "TP Realizado",
                    Content = "Teleportado para: "..foundItem.displayName,
                    Duration = 4,
                    Image = 4483362458
                })
            else
                Rayfield:Notify({
                    Title = "Erro no Teleporte",
                    Content = "Falha ao teleportar: "..tostring(teleportError),
                    Duration = 5,
                    Image = 4483362458
                })
            end
        else
            Rayfield:Notify({
                Title = "Item Inválido",
                Content = "O item encontrado não é mais válido para teleporte!",
                Duration = 3,
                Image = 4483362458
            })
        end
    end
})

-- TAB dos anti's
local AntisTab = Window:CreateTab("anti's", 4483362458)

-- Botão funcional Anti-attack
AntisTab:CreateButton({
    Name = "Anti-attack",
    Callback = function()
        local ReplicatedStorage = game:GetService("ReplicatedStorage")
        local attackRemote = ReplicatedStorage:FindFirstChild("Events") and ReplicatedStorage.Events:FindFirstChild("Attack")

        -- Protege contra RemoteEvent de ataque
        if attackRemote and attackRemote:IsA("RemoteEvent") then
            local oldNamecall
            oldNamecall = hookmetamethod(game, "__namecall", function(self, ...)
                if self == attackRemote and getnamecallmethod() == "FireServer" then
                    return nil -- bloqueia o ataque
                end
                return oldNamecall(self, ...)
            end)
        end

        -- Desativa scripts que tenham "attack" no nome
        for _, obj in ipairs(game:GetDescendants()) do
            if (obj:IsA("Script") or obj:IsA("LocalScript")) and string.lower(obj.Name):find("attack") then
                obj.Disabled = true
            end
        end

        Rayfield:Notify({
            Title = "Anti-attack Ativado",
            Content = "RemoteEvent e scripts de ataque foram bloqueados!",
            Duration = 5,
            Image = 4483362458
        })
    end
})

-- Load configuration
Rayfield:LoadConfiguration()
