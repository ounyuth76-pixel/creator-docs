-- HP 200 System

game.Players.PlayerAdded:Connect(function(player)

	player.CharacterAdded:Connect(function(character)

		local humanoid = character:WaitForChild("Humanoid")

		humanoid.MaxHealth = 200
		humanoid.Health = 200

	end)

end)
-- Morning / Night System

while true do

	-- Morning
	game.Lighting.ClockTime = 7
	game.Lighting.Brightness = 3
	game.Lighting.GlobalShadows = true

	wait(300) -- 5 នាទី

	-- Night
	game.Lighting.ClockTime = 20
	game.Lighting.Brightness = 2
	game.Lighting.GlobalShadows = true

	wait(300) -- 5 នាទី

end
-- DTL FPS Map Vote
-- Maps: Tokyo / Cambodia / China

local Maps = {
	"Tokyo",
	"Cambodia",
	"China"
}

while true do

	wait(10) -- Lobby Time

	local WinningMap = Maps[math.random(1, #Maps)]

	print("Map Selected: "..WinningMap)

	for _, player in pairs(game.Players:GetPlayers()) do
		if player.Character then

			local HRP = player.Character:FindFirstChild("HumanoidRootPart")

			if HRP then
				if workspace:FindFirstChild(WinningMap) then

					local Spawn = workspace[WinningMap]:FindFirstChild("Spawn")

					if Spawn then
						HRP.CFrame = Spawn.CFrame
					end

				end
			end

		end
	end

	wait(300) -- Match Time (5 minutes)

end
Workspace
├── Tokyo
│   └── Spawn
├── Cambodia
│   └── Spawn
└── China
    └── Spaw
    -- DTL FPS Robux Shop

local MarketplaceService = game:GetService("MarketplaceService")
local ReplicatedStorage = game:GetService("ReplicatedStorage")

local BuyItem = Instance.new("RemoteEvent")
BuyItem.Name = "BuyItem"
BuyItem.Parent = ReplicatedStorage

-- Developer Product IDs
local Products = {
	["Rare"] = 1234567890,        -- 49 Robux
	["Epic"] = 1234567891,        -- 99 Robux
	["Legendary"] = 1234567892,  -- 199 Robux
	["DragonAK"] = 1234567893,   -- 399 Robux
	["Karambit"] = 1234567894    -- 699 Robux
}

BuyItem.OnServerEvent:Connect(function(player, ItemName)

	local ProductId = Products[ItemName]

	if ProductId then
		MarketplaceService:PromptProductPurchase(player, ProductId)
	end
end)
local ReplicatedStorage = game:GetService("ReplicatedStorage")
local BuyItem = ReplicatedStorage:WaitForChild("BuyItem")

script.Parent.MouseButton1Click:Connect(function()
	BuyItem:FireServer("Karambit")
end)
-- DTL FPS Box Spin

local ReplicatedStorage = game:GetService("ReplicatedStorage")

local OpenBox = Instance.new("RemoteEvent")
OpenBox.Name = "OpenBox"
OpenBox.Parent = ReplicatedStorage

local Rewards = {
	{Name = "Blood Splash", Chance = 50},
	{Name = "Blue Impact", Chance = 30},
	{Name = "Dragon Impact", Chance = 15},
	{Name = "AK-47 Dragon Inferno", Chance = 4},
	{Name = "Karambit Stely", Chance = 1}
}

OpenBox.OnServerEvent:Connect(function(player)

	local Roll = math.random(1,100)
	local Total = 0

	for _,Reward in pairs(Rewards) do
		Total = Total + Reward.Chance

		if Roll <= Total then
			print(player.Name.." won "..Reward.Name)

			-- នៅទីនេះអាចបន្ថែម Save ទៅ Inventory ពេលក្រោយ

			OpenBox:FireClient(player, Reward.Name)
			break
		end
	end

end)
