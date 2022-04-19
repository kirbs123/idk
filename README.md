--Fire Triggers
workspace.__THINGS.__REMOTES.MAIN:FireServer("b", "bank deposit")

getgenv().IfNameList = {
    "Pixel Demon";
}

function Depo()
local PettoRarity = {}
local IdToName = {}
local a = require(game:GetService("ReplicatedStorage").Framework.Modules["1 | Directory"].Pets["Grab All Pets"])
for i, v in pairs(a) do
    PettoRarity[i] = v.rarity
    IdToName[i] = v.name
end

local PetsList = {}

--Locals
local lib = require(game.ReplicatedStorage:WaitForChild('Framework'):WaitForChild('Library'))
local mybanks = lib.Network.Invoke("get my banks")
local BankID = mybanks[1]['BUID']

local mydiamonds = 0
local lib = require(game.ReplicatedStorage:WaitForChild('Framework'):WaitForChild('Library'))
local mybanks = lib.Network.Invoke("get my banks")

for i,v in pairs(lib.Save.Get().Pets) do
    if (table.find(getgenv().IfNameList, IdToName[v.id])) then
        if(i > 49) then
            lib.Network.Invoke("Bank Deposit", BankID, PetsList, mydiamonds);
            print("Deposited")
            return nil
        end
        table.insert(PetsList, v.uid)
    end
end
end--end of function

getgenv().StartDeposit = true

while wait(10) and StartDeposit do
    Depo()
end
