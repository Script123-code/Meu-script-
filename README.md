local RS = game:GetService("ReplicatedStorage")
local LP = game.Players.LocalPlayer
local RSP = RS.Players[LP.Name]

local ItemX = RSP.Inventory.WastelandShirt.Inventory["Rubles"] -- Change WatelandBackpack to any item you wanna put into the trade.

local tradeList = {}
for i = 1, 6 do
    table.insert(tradeList, ItemX)
end

RS.Remotes.Trade:InvokeServer({
    Action = "Update",
    TradeList = tradeList
})

RS.Remotes.Trade:InvokeServer({
    Action = "Confirm"
})
