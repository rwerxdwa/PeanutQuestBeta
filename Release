 while not game:IsLoaded() do
  wait(.1)
end

while not game.Players do
  wait(.1)
end

local gamer = {game.CollectionService, game:GetService("PathfindingService"), table.insert, table.remove} 
local sDebug = false


while not game.Players.LocalPlayer do
  wait(.1)
end

repeat wait() until game:IsLoaded() -- you know what this does

local getPlayerInvy = function(player) -- gets inventory stats
  return game.ReplicatedStorage.remotes.reloadInvy:InvokeServer()
end

local function generateRandomString()
  local chars = {"q","w","e","r","t","y","u","i","o","p","a","s","d","f","g","h","j","k","l","z","x","c","v","b","n","m","1","2","3","4","5","6","7","8","9","0","X","A","B","V","R","I","O","P","L"}
  local str = ""

  for i = 1, 16 do
    str = str .. chars[math.random(1, #chars)]
  end
  return str
end
local regionPartName = generateRandomString()

local function waitForExist(obj, objName, waitTime)
  if waitTime ~= nil then
    local timer = 0
    while not obj:FindFirstChild(objName) and waitTime > timer  do
      wait(.1)
      timer = timer + .1
    end
    return obj:FindFirstChild(objName)
  else
    while not obj:FindFirstChild(objName) do
      wait()
    end
    return obj:FindFirstChild(objName)
  end
end

local function comparestrtolist(str, list)
  for i, v in pairs(list) do
    if str == v then
      return true
    end
  end
  return false
end

while not game.ReplicatedStorage:FindFirstChild("remotes") do
  wait(.1)
end

while not game:FindFirstChild("Lighting") do
  wait(.1)
end

while not game.Players.LocalPlayer:FindFirstChild("PlayerScripts") do
  wait(.1)
end

function ScriptDebug(a)
    warn(a)
end

local plrs = game:GetService'Players'
local me = plrs.LocalPlayer;

    local stuffTransparency = 1
    local abilityRange = 70
    local mobRange = 4
    local bossRange = 6
    local extremelyFast = _G.extremelyFast
    local walkspeed = 33
    local insert = gamer[3]
    local remove = gamer[4]

    local bossRaid = false
    local normalDungeon = true
    local waveDefense = false
    local eggEvent = false
    if sDebug then
      stuffTransparency = .5
    end
    -- stops loops when dungeon progress changes
    local gameOver = false
    -- variable for hitbox
    local bossPresent = false
    -- follow path variables
    _G.auto_attack  = true
    _G.smallTeleportVal = 100

    -- expiermental instakilltable
    local instakillTable = {
      ["Sand Peasant"] = true,
      ["Sand Giant"] = true,
      ["Frost Minion"] = true,
      ["Frost Wizard"] = true,
      ["Pirate Rifleman"] = true,
      ["Pirate Savage"] = true,
      ["Elementalist"] = true,
      ["King's Guard"] = true,
      ["Dark Mage"] = true,
      ["Demon Warrior"] = true,
      ["Samurai Swordsman"] = true,
      ["Bodyguard"] = true,
      ["Burly Enforcer"] = true,
      ["Raider"] = true,
      ["Harpoon Gunner"] = true,
      ["Cannon Crab"] = true,
      ["Spinner Bot"] = true,
      ["Fighter Bot"] = true,
      ["Cog Shooter"] = true,
      ["Hammer Bot"] = true,
      ["Hologram Assassin"] = true,
      ["Hologram Warrior"] = true,
      ["Chicken Mage"] = true,
      ["Chicken Brawler"] = true,
    }


    local VirtualUser=game:service'VirtualUser' -- afk
    game:service'Players'.LocalPlayer.Idled:connect(function()
        VirtualUser:CaptureController()
        VirtualUser:ClickButton2(Vector2.new())
      end)

    local vu = game:GetService("VirtualUser") -- second afk script
    game:GetService("Players").LocalPlayer.Idled:connect(function()
        vu:Button2Down(Vector2.new(0,0),workspace.CurrentCamera.CFrame)
        wait(1)
        vu:Button2Up(Vector2.new(0,0),workspace.CurrentCamera.CFrame)
      end)

    function AIMovementInLobby()
      local clock = 0
      local doneMoving = false
      _G.ai_done = false
      local zombie = game.Players.LocalPlayer.Character
      local Zombiehumanoid = zombie.Humanoid
      spawn(function()
          local PathfindingService = game:GetService("PathfindingService")
          local randomWayPoints = {
            {
              Vector3.new(29.4448986, 10.6809521, 1005.28198),
            },
            {
              Vector3.new(120.158272, 5.05413818, 1005.26672),
            },
            {
              Vector3.new(145.121567, 4.79999876, 1028.203),
            },
            {
              Vector3.new(138.910416, 4.85120726, 1080.46936),
            },
            {
              Vector3.new(50.0033913, 5.40119982, 1025.59448),
              Vector3.new(12.7496023, 4.94986296, 1046.24768),
            },
            {
              Vector3.new(56.9857826, 5.10824966, 1066.79846),
              Vector3.new(40.124321, 5, 1055.27551),
            },
            {
              Vector3.new(28.1154366, 4.8208971, 1041.24829),
            },
            {
              Vector3.new(8.27422428, 4.80000019, 1034.32092),
              Vector3.new(-36.9196014, 4.80000019, 1022.45972),
              Vector3.new(-93.4016876, 5.84888077, 1107.07776),
              Vector3.new(-134.147461, 5.84888077, 1080.1228),
            },
            {
              Vector3.new(8.27422428, 4.80000019, 1034.32092),
              Vector3.new(-36.9196014, 4.80000019, 1022.45972),
              Vector3.new(-69.0564728, 5.87887812, 1101.21545),
            },
            {
              Vector3.new(8.27422428, 4.80000019, 1034.32092),
              Vector3.new(-36.9196014, 4.80000019, 1022.45972),
              Vector3.new(-57.2358208, 5.81887817, 1059.91345),
            },
            {
              Vector3.new(104.851845, 4.80013657, 1029.08655),
              Vector3.new(66.5649185, 11.1366758, 981.947205),
              Vector3.new(58.9183998, 15.5042267, 969.327759),
            },
            {
              Vector3.new(106.917046, 5.1029253, 1033.20129),
              Vector3.new(126.421371, 4.80742407, 1017.41754),
              Vector3.new(109.249374, 4.99999857, 998.975525),
            },
            {
              Vector3.new(37.6123543, 5.1142168, 1041.55664),
              Vector3.new(8.08811092, 11.3835154, 1087.04956),
              Vector3.new(3.8377471, 4.81672573, 1051.76331),
            },
            {
              Vector3.new(74.2765732, 4.79785824, 1034.74109),
              Vector3.new(59.2142448, 5, 1081.58557),
              Vector3.new(23.250845, 5.6657753, 1021.79108),
            },
            {
              Vector3.new(75.4334259, 5.07404947, 1048.54626),
              Vector3.new(59.5415268, 9.24949932, 1002.75214),
              Vector3.new(21.7118225, 26.9064331, 982.54895),
            },
            {
              Vector3.new(86.8510361, 4.95114946, 1012.60217),
              Vector3.new(78.8645248, 5.21786928, 1063.84338),
              Vector3.new(39.1454849, 5, 1062.37744),
            },
            {
              Vector3.new(85.5781631, 5.19999838, 1044.32336),
              Vector3.new(7.32494354, 4.79999876, 1031.84668),
              Vector3.new(-16.918314, 7.10381889, 999.609253),
            },
            {
              Vector3.new(85.5781631, 5.19999838, 1044.32336),
              Vector3.new(7.32494354, 4.79999876, 1031.84668),
              Vector3.new(-60.5333252, 4.90647602, 1025.54321),
            },
            {
              Vector3.new(85.5781631, 5.19999838, 1044.32336),
              Vector3.new(7.32494354, 4.79999876, 1031.84668),
              Vector3.new(-76.8479233, 4.87704134, 1009.79724),
            },
            {
              Vector3.new(116.443657, 5.34364605, 1031.54187),
              Vector3.new(136.55043, 4.80000019, 1068.89758),
              Vector3.new(96.5291367, 5.04907751, 1055.71301),
            },
            {
              Vector3.new(136.55043, 4.80000019, 1068.89758),
              Vector3.new(96.5291367, 5.04907751, 1055.71301),
              Vector3.new(116.443657, 5.34364605, 1031.54187),
            },
            {
              Vector3.new(84.3650131, 4.95895767, 1011.05023),
              Vector3.new(28.3323727, 5.77999735, 1021.42993),
              Vector3.new(32.4552689, 5, 1067.22888),
            },
          }
          -- Variables for the zombie, its humanoid, and destination



          for i,v in pairs(randomWayPoints[math.random(1,#randomWayPoints)]) do
            local path = PathfindingService:CreatePath()
            -- Compute the path
            path:ComputeAsync(zombie.HumanoidRootPart.Position, v)
            local waypoints = path:GetWaypoints()
            -- Get the path waypoints

            local wayPointParts = {}
            -- Loop through waypoints
            local number2 = 0
            for _, waypoint in pairs(waypoints) do
              if _G.ai_done then break end
              number2 = number2 + .5
              local part = Instance.new("Part")
              part.Shape = "Ball"
              part.Material = "Neon"
              part.Color = Color3.new(1,120,1)
              local number = (math.sin(number2) + 1.5) /2
              part.Size = Vector3.new(number, number, number)
              part.Position = waypoint.Position
              part.Anchored = true
              part.CanCollide = false
              part.Parent = game.Workspace
              insert(wayPointParts, part)
            end

            for i, waypoint in pairs(waypoints) do
              if _G.ai_done then break end
              wayPointParts[i].BrickColor = BrickColor.new("Bright blue")
              Zombiehumanoid:MoveTo(waypoint.Position)
              Zombiehumanoid.MoveToFinished:Wait()
              wayPointParts[i].BrickColor = BrickColor.new("Fire Yellow")
            end
          end
          doneMoving = true
        end)
      while not(doneMoving or clock >_G.maxWaitTimeInLobby)  do
        clock = clock+.1
        wait(.1)
      end
      _G.ai_done = true
      Zombiehumanoid:MoveTo(zombie.HumanoidRootPart.Position)
    end

    function autoupgrade()
      if	_G.auto_stat_upgrade then
        if game.Players.LocalPlayer.skillPoints.Value > 0 then
          while game.Players.LocalPlayer.skillPoints.Value > 0 do
            game:GetService("ReplicatedStorage").remotes.spendSkillPoint:FireServer(_G.stat)
            wait()
          end
        end
      end
    end

    function getItemType(v, includeHealth)
      if v.health == nil then -- is a weapon
        if v.spellPower < v.physicalDamage then
          return "physical"
        else
          return "mage"
        end
      else -- is an armor
        if v.spellPower > v.physicalPower then
          if includeHealth then
            if v.spellPower > v.health then
              return "mage"
            else
              return "guardian"
            end
          else
            return "mage"
          end
        else
          if includeHealth then
            if v.physicalPower > v.health then
              return "physical"
            else
              return "guardian"
            end
          else
            return "physical"
          end      
        end
      end
    end

    function lobbyStrCheck(a, b)
      local la, lb = string.lower(a), string.lower(b)
      la = string.gsub(la, "'", "") -- remove ' from item name
      lb = string.gsub(lb, "'", "") -- remove ' from item name
      la = string.gsub(la, "s", "") -- remove s from item name
      lb = string.gsub(lb, "s", "") -- remove s from item name
      return la == lb
    end

    function checkSell(rare, name) -- vital function
      for itemName,rareTable in pairs(_G.itemlist) do
        if lobbyStrCheck(itemName, name) then
          for _, j in pairs(rareTable) do
            if rare == j then
              return false
            end
          end
        end
      end
      return not _G.keeprarities[rare]
    end

    local function sell() -- autosell script bring all together
      if _G.autosell then
        local tallyList = {}
        local itemType, gitems
        gitems = getPlayerInvy(game.Players.LocalPlayer)
        for itemFolderName,itemFolder in pairs(gitems) do
          gitems = getPlayerInvy(game.Players.LocalPlayer)
          if itemFolderName == "weapons" or itemFolderName == "chests" or itemFolderName == "helmets" then
            for i, item in pairs(itemFolder) do
              itemType = getItemType(item, false)
              local itemTypeCheck = not _G.keep_items_from_class[itemType]
              if not item.equipped and (checkSell(item.rarity, item.name) and item.levelReq < _G.keep_items_level_requirement and itemTypeCheck) then
                if itemFolderName == "weapons" then
                  if _G.testSell then
                    print('MROBSWAG Selling: ', item.name)
                  else
                    game:GetService("ReplicatedStorage").remotes.sellItemEvent:FireServer({ ["ability"]= { }, ["helmet"]= { }, ["chest"]= { }, ["weapon"]= { (tonumber(string.sub(i, 8))) } })
                  end
                elseif itemFolderName == "chests" then
                  if _G.testSell then
                    print('MROBSWAG Selling: ', item.name)
                  else
                    game:GetService("ReplicatedStorage").remotes.sellItemEvent:FireServer({ ["ability"]= { }, ["helmet"]= { }, ["chest"]= { (tonumber(string.sub(i, 7))) }, ["weapon"]= { } })
                  end
                elseif itemFolderName == "helmets" then
                  if _G.testSell then
                    print('MROBSWAG Selling: ', item.name)
                  else
                    game:GetService("ReplicatedStorage").remotes.sellItemEvent:FireServer({ ["ability"]= { }, ["helmet"]= { (tonumber(string.sub(i, 8))) }, ["chest"]= { }, ["weapon"]= { } })
                  end
                end
              end
            end
          end
          if itemFolderName == "abilities" then
            for i, item in pairs(gitems.abilities) do
              if tallyList[item.name] then
                tallyList[item.name] = tallyList[item.name] +1
              else
                tallyList[item.name] = 1
              end
              if not item.equipped.q and not item.equipped.e then
                if (checkSell(item.rarity, item.name) and item.levelReq < _G.keep_items_level_requirement) or (((tallyList[item.name] > 2) and _G.keep2spells))  then
                  if _G.testSell then
                    print('MROBSWAG Selling: ', item.name)
                  else
                    game:GetService("ReplicatedStorage").remotes.sellItemEvent:FireServer({ ["ability"]= {(tonumber(string.sub(i, 9))) }, ["helmet"]= { }, ["chest"]= { }, ["weapon"]= { } })
                  end
                end
              end
            end
          end
        end
      end
    end


    local function calculatePot(baseStat, maxUpgrade)
      local upgradeLevel = 1
      for i= 1, maxUpgrade do
        upgradeLevel = baseStat * .05
        if upgradeLevel >10 then
          upgradeLevel = 10
        end
        baseStat = baseStat + upgradeLevel
      end
      return math.floor(baseStat)
    end

    local function calcCost(totalUpg, currentUpgrade)
      local i = 0
      local r = 100
      for o = 1, totalUpg, 1 do
        local a = 0
        if (o > 1) then
          local s = 1.06 * r + 50
          if (220 < s - r) then
            a = r + 220
          else
            a = s
          end
        else
          a = r
        end
        if currentUpgrade < o then 
          if o <= 466 then
            i = i + a
          else
            i = i + 100000
            a = 100000
          end
        end
        r = a
      end
      return i
    end

    function autoUpgradeEquip(equipType)
      if _G.auto_upgrade_equip then

        local gitems = getPlayerInvy(game.Players.LocalPlayer)
        if equipType == "chests" then
          for i,v in pairs(gitems.chests) do
            local upgradeAmount = v.maxUpgrades - v.currentUpgrade
            if v.equipped and upgradeAmount ~= 0 then
              if v.spellPower > v.physicalPower then
                game:GetService("ReplicatedStorage").remotes.upgradeItem:FireServer("chest", (tonumber(string.sub(i, 7))), "spell", upgradeAmount)
              else
                game:GetService("ReplicatedStorage").remotes.upgradeItem:FireServer("chest", (tonumber(string.sub(i, 7))), "physical", upgradeAmount)
              end
            end
          end
        elseif equipType == "helmets" then
          for i,v in pairs(gitems.helmets) do
            local upgradeAmount = v.maxUpgrades - v.currentUpgrade
            if v.equipped and upgradeAmount ~= 0 then
              if v.spellPower > v.physicalPower then
                game:GetService("ReplicatedStorage").remotes.upgradeItem:FireServer("helmet", (tonumber(string.sub(i, 8))), "spell", upgradeAmount)
              else
                game:GetService("ReplicatedStorage").remotes.upgradeItem:FireServer("helmet", (tonumber(string.sub(i, 8))), "physical", upgradeAmount)
              end
            end
          end
        elseif equipType == "weapons" then
          for i,v in pairs(gitems.weapons) do
            local upgradeAmount = v.maxUpgrades - v.currentUpgrade
            if v.equipped and upgradeAmount ~= 0 then
              if v.spellPower > v.physicalDamage then
                game:GetService("ReplicatedStorage").remotes.upgradeItem:FireServer("weapon", (tonumber(string.sub(i, 8))), "spell", upgradeAmount)
              else
                game:GetService("ReplicatedStorage").remotes.upgradeItem:FireServer("weapon", (tonumber(string.sub(i, 8))), "physical", upgradeAmount)
              end
            end
          end
        end
      end
    end


    local function _equipBestSpell(spellArray, typ)
      local bestVal, best, b = 0, nil
      for i,v in pairs(spellArray) do
        if v.name ~= "skip" then -- if i renamed a item to skip then dont compare it
          local d = v.description:lower()
          if d:find("spell") and typ == "spell" then -- if the description contains spell, then its probably a spellpower one
            if v.levelReq > bestVal then
              bestVal = v.levelReq
              best = i
              b = v.name
            end
          elseif d:find("physical") and typ == "physical"  then -- if the description contains phyiscal, then its probably a phyiscal one
            if v.levelReq > bestVal then
              bestVal = v.levelReq
              best = i
              b = v.name
            end      
          end
        end
      end
      return best, b
    end

    local function equipBestSpell()
      if _G.autoEquipSpell then
        local gitems = getPlayerInvy(game.Players.LocalPlayer)
        local gabil = gitems.abilities
        local aBest, aName = _equipBestSpell(gabil, _G.spellType:lower()) -- finds ability with highest level
        for i,v in pairs(gitems.abilities) do -- remove one ability
          if v.name == aName then
            v.name = "skip"
            break
          end
        end
        local bBest, bName = _equipBestSpell(gabil, _G.spellType:lower()) -- finds another ability with highest level
        if aBest ~= nil and bBest ~= nil then
          print(bBest, aBest)
          game:GetService("ReplicatedStorage").remotes.equipItem:InvokeServer("ability", (tonumber(string.sub(aBest, 9))), "q") -- equips ability 
          wait(1)
          game:GetService("ReplicatedStorage").remotes.equipItem:InvokeServer("ability", (tonumber(string.sub(bBest, 9))), "e") -- equips ability 
        end
      end
    end

    local function autoEquipLvlGear()
      if _G.auto_equip_gear then
        print('autoEquip')
        local playerLevel = game.Players.LocalPlayer.leaderstats.Level.Value
        local gitems = getPlayerInvy(game.Players.LocalPlayer)
        local bestDamage = 0 -- CHESTS
        local bestEquip = nil
        if gitems.chests ~= nil then
          local gold = game.Players.LocalPlayer.leaderstats.Gold.Value
          for i,v in pairs(gitems.chests) do
            local upgradeAmount = v.maxUpgrades - v.currentUpgrade
            if _G.equip_type == "spell" and v.levelReq <= playerLevel and v.spellPower > v.physicalPower then
              local upgradeAmount = v.maxUpgrades - upgradeAmount
              local tempNum = calculatePot(v.spellPower, v.maxUpgrades, i)
              local canAfford = false
              if calcCost(v.maxUpgrades, v.currentUpgrade) < gold then
                canAfford = true
              end
              if (tempNum > bestDamage and canAfford) or (bestDamage < v.spellPower)  then
                bestDamage = tempNum
                bestEquip = i
              end
            end
            if _G.equip_type == "physical" and v.levelReq <= playerLevel and v.physicalPower > v.spellPower then
              local tempNum = calculatePot(v.physicalPower, upgradeAmount)
              local canAfford = false
              if calcCost(v.maxUpgrades, v.currentUpgrade) < gold then
                canAfford = true
              end
              if (tempNum > bestDamage and canAfford) or (bestDamage < v.physicalPower) then
                bestDamage = tempNum
                bestEquip = i
              end
            end
          end
          if not (bestEquip == nil) then
            game:GetService("ReplicatedStorage").remotes.equipItem:InvokeServer("chest", (tonumber(string.sub(bestEquip, 7))))
          end
        end
        wait(1)
        autoUpgradeEquip("helmets")
        wait(1)
        local bestDamage = 0 -- HELMETS
        local bestEquip = nil
        if gitems.helmets ~= nil then
          local gold = game.Players.LocalPlayer.leaderstats.Gold.Value
          for i,v in pairs(gitems.helmets) do
            local upgradeAmount = v.maxUpgrades - v.currentUpgrade
            if _G.equip_type == "spell" and v.levelReq <= playerLevel and v.spellPower > v.physicalPower then
              local tempNum = calculatePot(v.spellPower, upgradeAmount)
              local canAfford = false
              if calcCost(v.maxUpgrades, v.currentUpgrade) < gold then
                canAfford = true
              end
              if (tempNum > bestDamage and canAfford) or (bestDamage < v.spellPower) then
                bestDamage = tempNum
                bestEquip = i
              end
            end
            if _G.equip_type == "physical" and v.levelReq <= playerLevel and v.physicalPower > v.spellPower then
              local tempNum = calculatePot(v.physicalPower, upgradeAmount)
              local canAfford = false
              if calcCost(v.maxUpgrades, v.currentUpgrade) < gold then
                canAfford = true
              end
              if (tempNum > bestDamage and canAfford) or (bestDamage < v.physicalPower)  then
                bestDamage = tempNum
                bestEquip = i
              end
            end
          end
          if not (bestEquip == nil) then
            game:GetService("ReplicatedStorage").remotes.equipItem:InvokeServer("helmet", (tonumber(string.sub(bestEquip, 8))))
          end
        end
        wait(1)
        autoUpgradeEquip("chests")
        wait(1)
        local bestDamage = 0 -- WEAPONS
        local bestEquip = nil
        if gitems.weapons ~= nil then
          local gold = game.Players.LocalPlayer.leaderstats.Gold.Value
          for i,v in pairs(gitems.weapons) do
            local upgradeAmount = v.maxUpgrades - v.currentUpgrade
            if _G.equip_type == "spell" and v.levelReq <= playerLevel and v.spellPower > v.physicalDamage then
              local tempNum = calculatePot(v.spellPower, v.maxUpgrades)
              local canAfford = false
              if calcCost(v.maxUpgrades, upgradeAmount) < gold then
                canAfford = true
              end
              if (tempNum > bestDamage and canAfford) or (bestDamage < v.spellPower)  then
                bestDamage = tempNum
                bestEquip = i
              end
            end
            if _G.equip_type == "physical" and v.levelReq <= playerLevel and v.physicalDamage > v.spellPower then
              local tempNum = calculatePot(v.physicalDamage, upgradeAmount)
              local canAfford = false
              if calcCost(v.maxUpgrades, v.currentUpgrade) < gold then
                canAfford = true
              end
              if (tempNum > bestDamage and canAfford) or (bestDamage < v.physicalDamage)  then
                bestDamage = tempNum
                bestEquip = i
              end
            end
          end
          if not (bestEquip == nil) then
            game:GetService("ReplicatedStorage").remotes.equipItem:InvokeServer("weapon", (tonumber(string.sub(bestEquip, 8))))
          end
        end
        wait(1)
        autoUpgradeEquip("weapons")
        wait(1)
      end
    end


    local function autochoosedungeon()
      if _G.auto_choose_dungeon_and_difficulty then
        game.Players.LocalPlayer:WaitForChild("leaderstats")
        game.Players.LocalPlayer.leaderstats:WaitForChild("Level")
        lvl = game.Players.LocalPlayer.leaderstats.Level.Value
        print(lvl)
        if lvl <= 5 then
          _G.dungeon = "Desert Temple"
          _G.difficulty = "Easy"
        elseif lvl <= 11 then
          _G.dungeon = "Desert Temple"
          _G.difficulty = "Medium"
        elseif lvl <= 19 then
          _G.dungeon = "Desert Temple"
          _G.difficulty = "Hard"
        elseif lvl <= 26 then
          _G.dungeon = "Desert Temple"
          _G.difficulty = "Insane"
        elseif lvl <= 32 then
          _G.dungeon = "Desert Temple"
          _G.difficulty = "Nightmare"
        elseif lvl <= 39 then
          _G.dungeon = "Winter Outpost"
          _G.difficulty = "Easy"
        elseif lvl <= 44 then
          _G.dungeon = "Winter Outpost"
          _G.difficulty = "Medium"
        elseif lvl <= 49 then
          _G.dungeon = "Winter Outpost"
          _G.difficulty = "Hard"
        elseif lvl <= 54 then
          _G.dungeon = "Winter Outpost"
          _G.difficulty = "Insane"
        elseif lvl <= 59 then
          _G.dungeon = "Winter Outpost"
          _G.difficulty = "Nightmare"
        elseif lvl <= 64 then
          _G.dungeon = "Pirate Island"
          _G.difficulty = "Insane"
        elseif lvl <= 69 then
          _G.dungeon = "Pirate Island"
          _G.difficulty = "Nightmare"
        elseif lvl <= 74 then
          _G.dungeon = "King's Castle"
          _G.difficulty = "Insane"
        elseif lvl <= 79 then
          _G.dungeon = "King's Castle"
          _G.difficulty = "Nightmare"
        elseif lvl <= 84 then
          _G.dungeon = "The Underworld"
          _G.difficulty = "Insane"
        elseif lvl <= 89 then
          _G.dungeon = "The Underworld"
          _G.difficulty = "Nightmare"
        elseif lvl <= 94 then
          _G.dungeon = "Samurai Palace"
          _G.difficulty = "Insane"
        elseif lvl <= 99 then
          _G.dungeon = "Samurai Palace"
          _G.difficulty = "Nightmare"
        elseif lvl <= 104 then
          _G.dungeon = "The Canals"
          _G.difficulty = "Insane"
        elseif lvl <= 109 then
          _G.dungeon = "The Canals"
          _G.difficulty = "Nightmare"
        elseif lvl <= 114 then
          _G.dungeon = "Ghastly Harbor"
          _G.difficulty = "Insane"
        elseif lvl <= 119 then
          _G.dungeon = "Ghastly Harbor"
          _G.difficulty = "Nightmare"
        elseif lvl <= 124 then
          _G.dungeon = "Steampunk Sewers"
          _G.difficulty = "Insane"
        elseif lvl <= 139 then
          _G.dungeon = "Steampunk Sewers"
          _G.difficulty = "Nightmare"
        elseif lvl <= 145 then
          _G.dungeon = "Orbital Outpost"
          _G.difficulty = "Insane"
        elseif lvl <= 149 then
          _G.dungeon = "Orbital Outpost"
          _G.difficulty = "Nightmare"
        elseif lvl <= 154 then
          _G.dungeon = "Volcanic Chambers"
          _G.difficulty = "Insane"
        else
          _G.dungeon = "Volcanic Chambers"
          _G.difficulty = "Nightmare"
        end
      end
    end

    function autoChooseBossRaidTier()
      if _G.auto_choose_raid_boss_tier then
        local gitems = getPlayerInvy(game.Players.LocalPlayer)
        local largestKey = 0
        if gitems.keys ~= nil then
          if gitems.keys then
            for i, v in pairs(gitems.keys) do
              if tonumber(i) > largestKey and v then
                largestKey = tonumber(i)
                _G.boss_raid_tier = tonumber(i)
              end
            end
          end
        end
      end
    end

    local function del_armor_ui() -- deletes armor and ui
      spawn(function()
          pgui = game.Players.LocalPlayer.PlayerGui
          if game.CoreGui.RobloxGui:FindFirstChild("TopBarContainer") then
            game.CoreGui.RobloxGui.TopBarContainer:WaitForChild("NameHealthContainer")
            if game.CoreGui.RobloxGui.TopBarContainer.NameHealthContainer:FindFirstChild("Username") then
              game.CoreGui.RobloxGui.TopBarContainer.NameHealthContainer.Username:Destroy()
            end
          end
          while not game.Players.LocalPlayer.PlayerGui:FindFirstChild("playerStatus") do
            wait(.1)
          end
          pstat = pgui.playerStatus.Frame
          --pstat:Destroy()

          if _G.edit_ui then
            while not game.Players.LocalPlayer.PlayerGui:FindFirstChild("playerStatus") do
              wait(.1)
            end
            pstat = pgui.playerStatus.Frame
            while not pstat.portraitBorder:FindFirstChild("portrait") do
              wait(.1)
            end
            pstat.portraitBorder.portrait.Image = _G.UI_portait_image
            if pstat.moneyMain:FindFirstChild("updateMoney") then
              pstat.moneyMain.updateMoney:Destroy()
            end
            pstat.moneyMain.TextLabel.Text = _G.UI_money
            pstat.healthFrame.health.Text = _G.UI_health
            if pstat.healthFrame.health:FindFirstChild("label") then
              pstat.healthFrame.health.label:Destroy()
              pstat.healthFrame.healthUpdater:Destroy()
            end
            pstat.playerName.Text = _G.UI_name
            pstat.xpFrame.xp.Text = _G.UI_xp
            if pstat.xpFrame:FindFirstChild("xpUpdater") then
              pstat.xpFrame.xp.label:Destroy()
              pstat.xpFrame.xpUpdater:Destroy()
            end
            pstat.levelBorder.level.Text = _G.UI_lvl

            game.Players.LocalPlayer.PlayerGui:WaitForChild("abilities")
          end
        end)
      game.Players.LocalPlayer.Character:WaitForChild("playerNameplate", 5)
      if game.Players.LocalPlayer.Character:FindFirstChild("playerNameplate") then
        game.Players.LocalPlayer.Character["playerNameplate"]:Destroy()
      end

      while not game.Players.LocalPlayer.Character do
        wait()
      end
      while not game.Players.LocalPlayer.Character:FindFirstChildOfClass("Accessory") do
        wait()
      end
      wait()
      pchar = game.Players.LocalPlayer.Character
      for i,v in next, game.Players.LocalPlayer.Character:GetChildren() do 
        if v.ClassName == 'Accessory' then 

        end
      for _, v in pairs(pchar:GetChildren()) do
        if v.ClassName == "Accessory" then
          if not v:FindFirstChild("swing") then
            if _G.del_weapon then
              v:Destroy()
            end
          else
            if _G.del_armor then
                if(v:FindFirstChildOfClass("Model")) then
                    v:FindFirstChildOfClass("Model"):Destroy()
                end
            end
          end
        end
      end
    end
  end
    warn('place id check')
    if game.PlaceId == 2414851778 or game.PlaceId == 3220968688 then	
      warn('place id check done')
      while not workspace:FindFirstChild(game.Players.LocalPlayer.Name) do
        wait(.1)

        local Event = game:GetService("ReplicatedStorage").remotes.loadPlayerCharacter
        Event:FireServer()
      end
      warn("pressed start")
      spawn(function()
          while not workspace:FindFirstChild(game.Players.LocalPlayer.Name):FindFirstChild("Humanoid") do
            wait(.1)
          end
          spawn(function()
              while not game.Lighting:FindFirstChild("Blur") do
                wait(.1)
              end
              while not game.Players.LocalPlayer.PlayerGui:FindFirstChild("introGui") do
                wait(.1)
              end
              game.Players.LocalPlayer.PlayerGui:FindFirstChild("introGui"):Destroy() 
              local s = workspace.CurrentCamera
              s.CameraType = Enum.CameraType.Track;
              s.CameraSubject = game.Players.LocalPlayer.Character.Humanoid
              game.Lighting.Blur:Destroy()
            end)
          spawn(function()
              AIMovementInLobby()
            end)
        end)
      warn("player loaded")
      --[[
    spawn(function()
    del_armor_ui()
    end)
    warn("armor del")
    ]]
      if _G.collect_daily_reward then
        while not workspace:FindFirstChild(game.Players.LocalPlayer.Name):FindFirstChild("HumanoidRootPart") do
          wait(.1)
        end
        workspace.dailyRewardTouchPart.CFrame = game.Players.LocalPlayer.Character.HumanoidRootPart.CFrame
        wait(.1)
        workspace.dailyRewardTouchPart.Size = Vector3.new(10,10,10)
        workspace.dailyRewardTouchPart.CFrame = game.Players.LocalPlayer.Character.HumanoidRootPart.CFrame * CFrame.new(0,1,0)
        wait(.1)
        spawn(function()
            game.CoreGui:WaitForChild("PurchasePromptApp"):Destroy()
          end)
      end
      warn("daily reward")
      if _G.boss_raid and _G.auto_choose_raid_boss_tier then
        local gitems = getPlayerInvy(game.Players.LocalPlayer)
        if gitems.keys == nil then
          _G.auto_choose_dungeon_and_difficulty = true
          _G.boss_raid = false
          _G.wavedefense = false
        end
        if gitems.keys["1"] ~= nil then
          if gitems.keys["1"] == false then
            _G.auto_choose_dungeon_and_difficulty = true
            _G.boss_raid = false
            _G.wavedefense = false
          end
        end
      end
      warn("key check")
      autochoosedungeon()
      warn("choose dungeon")
      autoChooseBossRaidTier()
      warn("choose boss raid tier")
      equipBestSpell()
      warn("auto spell swap")
      autoEquipLvlGear()
      warn("equip gear")
      sell()
      warn("sell done")
      autoupgrade()
      warn("auto upgrade done")
      if _G.easter_enable then
        _G.dungeon = "Egg Island"
        _G.difficulty = "Nightmare"
        _G.hardcore = false
      end
      print("JOINING DUNGEON")
      while not _G.ai_done do -- movement AI
        wait(.1)
      end
      if _G.auto_join_dungeon then
        if _G.wait_for_friends_to_host then	
          if _G.boss_raid then
            while not workspace.bossLobbies:FindFirstChild(_G.host_name) do
              wait()
            end
            while wait(.1) do
              game:GetService("ReplicatedStorage").remotes.playerJoinBossLobby:InvokeServer(workspace.bossLobbies:FindFirstChild(_G.host_name))
            end	
          else
            while not workspace.games.inLobby:FindFirstChild(_G.host_name) do
              wait()
            end
            while wait(.1) do
              game:GetService("ReplicatedStorage").remotes.joinDungeon:InvokeServer(_G.host_name)
            end
          end
        end
        if _G.multi_roblox then
          if game.Players.LocalPlayer.Name == _G.host_name_key[1] then -- what the hosts does
            if _G.boss_raid then
              local Event = game:GetService("ReplicatedStorage").remotes.createBossLobby
              Event:InvokeServer(_G.boss_raid_tier, true, 0)
            else
              local Event = game:GetService("ReplicatedStorage").remotes.createLobby
              
              Event:InvokeServer(_G.dungeon, _G.difficulty, 0, _G.hardcore, true, _G.wavedefense)
            end
            wait(.1)
            if _G.boss_raid then
              for i, v in pairs(_G.name_key_list) do -- whitelist everyone
                game:GetService("ReplicatedStorage").remotes.addPlayerToBossWhitelist:FireServer(v[1])
              end
            else
              for i, v in pairs(_G.name_key_list) do -- whitelist everyone
                game:GetService("ReplicatedStorage").remotes.addPlayerToWhitelist:FireServer(v[1])
              end
            end
            if _G.boss_raid then
              while (#(workspace.bossLobbies:FindFirstChild(game.Players.LocalPlayer.Name).players:GetChildren())) ~= (#_G.name_key_list + 1) do -- wait for lobby to be full
                wait()
              end
            else
              while (#(workspace.games.inLobby:FindFirstChild(game.Players.LocalPlayer.Name):GetChildren()) - 1) ~= (#_G.name_key_list + 1) do -- wait for lobby to be full
                wait()
              end
            end
            if _G.boss_raid then
              game:GetService("ReplicatedStorage").remotes.startBossRaid:FireServer()
            else
              game:GetService("ReplicatedStorage").remotes.startDungeon:FireServer()
            end
          else -- what the joiners do
            if _G.boss_raid then
              while not workspace.bossLobbies:FindFirstChild(_G.host_name_key[1]) do
                wait()
              end
              while wait(.1) do
                game:GetService("ReplicatedStorage").remotes.playerJoinBossLobby:InvokeServer(workspace.bossLobbies:FindFirstChild(_G.host_name_key[1]))
              end
            else
              while not workspace.games.inLobby:FindFirstChild(_G.host_name_key[1]) do
                wait()
              end
              while wait(.1) do
                game:GetService("ReplicatedStorage").remotes.joinDungeon:InvokeServer(_G.host_name_key[1])
              end
            end
          end
        end


        if _G.wait_for_friends then
          if _G.boss_raid then
            local Event = game:GetService("ReplicatedStorage").remotes.createBossLobby
            Event:InvokeServer(_G.boss_raid_tier, true, 0)
          else
            local Event = game:GetService("ReplicatedStorage").remotes.createLobby
            Event:InvokeServer(_G.dungeon, _G.difficulty, 0, _G.hardcore, true, _G.wavedefense)
          end
          wait(.1)
          if _G.boss_raid then
            for i, v in pairs(_G.friends) do -- whitelist everyone
              game:GetService("ReplicatedStorage").remotes.addPlayerToBossWhitelist:FireServer(v)
            end
          else
            for i, v in pairs(_G.friends) do -- whitelist everyone
              game:GetService("ReplicatedStorage").remotes.addPlayerToWhitelist:FireServer(v)
            end
          end
          wait(.1)
          if _G.boss_raid then
            while (#(workspace.bossLobbies:FindFirstChild(game.Players.LocalPlayer.Name).players:GetChildren())) ~= (#_G.friends + 1) do -- wait for lobby to be full
              wait()
            end
          else
            while (#(workspace.games.inLobby:FindFirstChild(game.Players.LocalPlayer.Name):GetChildren()) - 1) ~= (#_G.friends + 1) do -- wait for lobby to be full
              wait()
            end
          end
          if _G.boss_raid then
            local Event = game:GetService("ReplicatedStorage").remotes.startBossRaid
            Event:FireServer()
          else
            local Event = game:GetService("ReplicatedStorage").remotes.startDungeon
            Event:FireServer()
          end
          wait(20)
        end

        if _G.boss_raid then -- boss raid
          print("make boss lobby")
          local Event = game:GetService("ReplicatedStorage").remotes.createBossLobby
          Event:InvokeServer(_G.boss_raid_tier, true, 0)
          wait(1)
          local Event = game:GetService("ReplicatedStorage").remotes.startBossRaid
          Event:FireServer()
          wait(20)
        elseif not _G.boss_raid then -- normal dungeons/wavedefense
          local Event = game:GetService("ReplicatedStorage").remotes.createLobby
          Event:InvokeServer(_G.dungeon, _G.difficulty, 0, _G.hardcore, true, _G.wavedefense)
          wait(1)
          local Event = game:GetService("ReplicatedStorage").remotes.startDungeon
          Event:FireServer()
          wait(20)
        end
      else
        while wait(.1) do
        end
      end
      while wait(.1) do
      end
    end


    while not game.Players.LocalPlayer do
      wait(.1)
    end

    while not game.Players.LocalPlayer.Character do
      wait(.1)
    end

    while not game.Players.LocalPlayer.Character:FindFirstChild("HumanoidRootPart") do
      wait(.1)
    end

    while not game.Players.LocalPlayer.Character:FindFirstChild("Humanoid") do
      wait(.1)
    end

    while not workspace:FindFirstChild(game.Players.LocalPlayer.Name) do
      wait(.1)
    end
    -- dungeon specific waits
    while not workspace:FindFirstChild("dungeon") and not workspace:FindFirstChild("tier") and not workspace:FindFirstChild("currentWave") do
      wait(1)
    end

    while not game:GetService("Workspace"):FindFirstChild("dungeonProgress") and not game:GetService("Workspace"):FindFirstChild("raidProgress")  do
      wait()
    end

    wait(.5)


    local pathargs = {
      ["AgentHeight"] = 5,
      ["AgentRadius"] = 3,
      ["AgentCanJump"] = true
    }
    local PathfindingService = gamer[2]
    local cs = gamer[1]
    local localPlayer = game.Players.LocalPlayer.Character
    local path = PathfindingService:CreatePath(pathargs)
    local waypoints = {}
    local currentWaypointIndex = 0
    local weaponCooldown = 1
    local enemy
    local ballArray = {}

    function stringInTable(st, tb)
      if tb[st] ~= nil then return true else return false end
      for i,v in pairs(tb) do
        if st == v then
          return true
        end
      end
      return false
    end


    local function createWall(cf, sz)
      if _G.loadSlow then
        game:GetService("RunService").RenderStepped:wait()
      end
      local part = Instance.new("Part")
      cs:AddTag(part, "RayWhitelist")
      part.Size = sz
      part.CFrame = cf
      part.Name = regionPartName
      part.Anchored = true
      part.Transparency = _G.wall_transparency--stuffTransparency
      part.CanCollide = true
      part.Parent = workspace
      return part
    end

    local function antiTransChange(property)
      report("ANTI SKID, TransChange", property)
    end

    local function antiChildChange(child)
      if child.ClassName ~= "TouchTransmitter" then
        report("ANTI SKID, ChildChange", child)
      end
    end

    local function createPart(cframe, size, name, shape) -- this is the part we walk to
      local part = Instance.new("Part")
      part.Shape = shape
      cs:AddTag(part, "RayIgnore")
      part.Material = "Neon"
      if _G.showPath then
        part.Transparency = .5
      else
        part.Transparency = stuffTransparency
      end
      
      part.Size = size
      part.CFrame = cframe
      part.Name = name
      part.Anchored = true
      part.CanCollide = false
      part.Parent = workspace
      part:GetPropertyChangedSignal("Transparency"):Connect(antiTransChange)
      part.ChildAdded:Connect(antiChildChange)
      return part
    end

    local function createHitBoxPart(size, cframe, obj)
      local part = Instance.new("Part")
      cs:AddTag(part, "RayIgnore")
      part.Size = size
      part.CFrame = cframe
      part.Parent = obj
      part.Name = "enemyRadius"
      part.Anchored = false
      part.CanCollide = false
      part.Material = "SmoothPlastic"
      part.Transparency = stuffTransparency
      part:GetPropertyChangedSignal("Transparency"):Connect(antiTransChange)
      part.ChildAdded:Connect(antiChildChange)
      part.CustomPhysicalProperties = PhysicalProperties.new(0, 0, 0, 0, 0)
      local weld = Instance.new("WeldConstraint")
      if obj.ClassName == "Model" then
        weld.Part1 = obj.PrimaryPart
      else
        weld.Part1 = obj  
      end
      weld.Part0 = part
      weld.Parent = obj
      return part
    end

    local function addHitBox(obj, size, shape)
      local psize, cframe
      if shape == nil then
        local t = {
          {size, size}, {0, size}, {-size, size},
          {size, 0}, {-size, 0},
          {size, -size}, {0, -size}, {-size, -size},
        }
        for i,v in pairs(t) do
          psize = Vector3.new(1, 1, (size))
          local pos1 = (obj.PrimaryPart.CFrame * CFrame.new(v[1],0,v[2])).Position
          cframe =  CFrame.new(pos1, obj.PrimaryPart.Position)
          cframe = cframe * CFrame.new(0,0,(-size/2) + 2)
          createHitBoxPart(psize, cframe, obj)
        end
      elseif shape =="square" then -- this is for when things shoot ball projectiles
        psize = Vector3.new(size, size, size)
        cframe = CFrame.new(0,0,0)
        if obj.ClassName == "Model" then
          obj:WaitForChild("PrimaryPart", .5)
          cframe = obj.PrimaryPart.CFrame
        else
          cframe = obj.CFrame
        end
        createHitBoxPart(psize, cframe, obj)
      elseif shape == "rectangle" then
        psize = Vector3.new(size, size, size) -- create square around projectile
        cframe = CFrame.new(0,0,0)
        if obj.ClassName == "Model" then
          obj:WaitForChild("PrimaryPart", .5)
          cframe = obj.PrimaryPart.CFrame
        else
          cframe = obj.CFrame
        end
        createHitBoxPart(psize, cframe, obj)

        psize = Vector3.new(1, size, size*2)
        cframe = CFrame.new(0,0,0)
        if obj.ClassName == "Model" then -- add the pointy thing
          obj:WaitForChild("PrimaryPart", .5)
          cframe = obj.PrimaryPart.CFrame * CFrame.new(0, 0, (size - 5) * -1)
        else
          cframe = obj.CFrame * CFrame.new(0, 0, (size - 5) * -1)
        end
        createHitBoxPart(psize, cframe, obj)

      elseif shape == "rectanglev2" then
        psize = Vector3.new(size, size, size)
        cframe = CFrame.new(0,0,0)
        if obj.ClassName == "Model" then
          obj:WaitForChild("PrimaryPart", .5)
          cframe = obj.PrimaryPart.CFrame
        else
          cframe = obj.CFrame
        end
        createHitBoxPart(psize, cframe, obj)

        psize = Vector3.new(size, size, size)
        cframe = CFrame.new(0,0,0)
        if obj.ClassName == "Model" then
          obj:WaitForChild("PrimaryPart", .5)
          cframe = (obj.PrimaryPart.CFrame * CFrame.new(0, 0, (size - 10) * -1)) * CFrame.Angles(math.rad(45), 0,math.rad(90))
        else
          cframe = (obj.CFrame * CFrame.new(0, 0, (size - 10) * -1))* CFrame.Angles(math.rad(45), 0,math.rad(90))
        end
        createHitBoxPart(psize, cframe, obj)
      elseif shape == "rectanglev3" then
        psize = Vector3.new(size, size, size)
        cframe = CFrame.new(0,0,0)
        if obj.ClassName == "Model" then
          obj:WaitForChild("PrimaryPart", .5)
          cframe = obj.PrimaryPart.CFrame
        else
          cframe = obj.CFrame
        end
        createHitBoxPart(psize, cframe, obj)

        psize = Vector3.new(size -5 , size - 5, size - 5)
        cframe = CFrame.new(0,0,0)
        if obj.ClassName == "Model" then
          obj:WaitForChild("PrimaryPart", .5)
          cframe = (obj.PrimaryPart.CFrame * CFrame.new(0, 0, (size - 5) * -1)) * CFrame.Angles(0, math.rad(45),0)
        else
          cframe = (obj.CFrame * CFrame.new(0, 0, (size - 5) * -1))* CFrame.Angles(0, math.rad(45),0)
        end
        createHitBoxPart(psize, cframe, obj)

      elseif shape == "rectangle-2" then -- rectnagle with no offset
        psize = Vector3.new(size, size, size)
        cframe = CFrame.new(0,0,0)
        if obj.ClassName == "Model" then
          obj:WaitForChild("PrimaryPart", .5)
          cframe = obj.PrimaryPart.CFrame
          cframe = cframe * CFrame.Angles(0, math.rad(45), 0)
        else
          cframe = obj.CFrame
          cframe = cframe * CFrame.Angles(0, math.rad(45), 0)
        end
        createHitBoxPart(psize, cframe, obj)
      end
    end

    local function cleanMobUp(t)
      if _G.optimize_mobs then
        for i,v in pairs(t:GetChildren()) do
          if v.ClassName == "Model" then
            v:Destroy()
          end
        end
        if t:FindFirstChild("HumanoidRootPart") then
          t.HumanoidRootPart.Transparency = 0
        end
        if t:FindFirstChild("Head") then
          t.Head.Transparency = 0
        end
      end
    end

    local function _initHitBox(instance)
      if instance.ClassName == "Model" then
        while instance.PrimaryPart == nil do wait() end
        while not instance:FindFirstChild(instance.PrimaryPart.Name) do wait() end
        instance:WaitForChild("HumanoidRootPart")
        instance:WaitForChild("enemyStyle", 1.5)
        if not instance:FindFirstChild("enemyStyle") then print('no enemy style') return end
        local mobType = instance.enemyStyle.Value
        if mobType == "mob" or mobType == "ranged" or mobType == "melee" or mobType == "burly" then --f if mob
          if eggEvent then -- egg event only has one tag on each mob
            while (#cs:GetTags(instance) == 0) do
              wait(.1)
            end
          else
            while (#cs:GetTags(instance) < 2) do -- normally each mob has two
              ScriptDebug("waiting for mob to add tag" )
              wait(.1)
            end
          end
          cs:AddTag(instance, "Enemy")
          if _G.doInstakill then
            if instance:FindFirstChild("Humanoid") and instakillTable[instance.Name] then
              instance.Humanoid.Health = 0
            end
          end
          if mobType ~= "ranged" then
            if game.PlaceId == 5281215714 then -- if volcanic mob
              if instance.Name == "Explosive Lava Walker" or instance.Name == "Aggressive Lava Walker" then
                addHitBox(instance, 8.5)
              end
            elseif game.PlaceId == 6216785535 then
              if instance.Name == "Temple Guard" then
                addHitBox(instance, 3)
              end                
            else
              addHitBox(instance, 7)
            end
          end
        else -- if not mob then
          if eggEvent then -- egg event has 0 tagso n boss
            while #cs:GetTags(instance) ~= 0 do
              wait()
            end
          else
            while #cs:GetTags(instance) < 1 do
              wait()
            end          
          end
          if _G.doInstakill then
            if instance:FindFirstChild("Humanoid") and instakillTable[instance.Name] then
              instance.Humanoid.Health = 0
            end
          end
          cs:AddTag(instance, "Enemy")             
        end
      end  
    end

    local function initHitBox()
      if workspace:FindFirstChild("tier") or workspace:FindFirstChild("currentWave") then -- boss raid or wave defense ( they work the same )
        workspace.enemies.ChildAdded:Connect(function(instance)
            if instance.Name == "Stone Warrior" then -- instakill in mob folder
              instance:WaitForChild("Humanoid")
              addHitBox(instance, 5)
              wait(1)
              instance.Humanoid.Health = 0
            else
              _initHitBox(instance)
              cleanMobUp(instance)
            end
          end)
      else
        for i,room in pairs(workspace.dungeon:GetChildren()) do -- normal dungeon handler
          if room:FindFirstChild("enemyFolder") then
            local efold = room:FindFirstChild("enemyFolder")
            if efold then
              local e = efold:FindFirstChildOfClass("Model")
              if e then
                if e:FindFirstChild("Humanoid") then -- if folder already has mobs then add hit box
                  wait(.5)
                  for i,instance in pairs(efold:GetChildren()) do
                    _initHitBox(instance)
                    cleanMobUp(instance)
                  end
                end
              end
              efold.ChildAdded:Connect(function(instance) -- all future folders, if mob spawned, give hitbox
                  _initHitBox(instance)
                  cleanMobUp(instance)
                end)
            end
          end
        end
      end
    end

    local projNameList = {} -- important
    local enemyProjNameList = {}

    local function updateProjsList()
      if game.ReplicatedStorage:FindFirstChild("projectiles") then
        local n1 = game:GetService("ReplicatedStorage").projectiles:GetChildren()
        local n2 = game:GetService("ReplicatedStorage").enemyProjectiles:GetChildren()
        for i,v in pairs(n1) do
          projNameList[v.Name] = true
        end
        for i,v in pairs(n2) do
          enemyProjNameList[v.Name] = true
        end
        enemyProjNameList["secondBossSlamHitbox"] = true
      end
    end

    updateProjsList()

    local function createBall(vector) -- balls that pathfinding places
      local part = Instance.new("Part")
      cs:AddTag(part, "RayIgnore")
      part.Shape = "Ball"
      part.Material = "Neon"
      part.Size = Vector3.new(0.6, 0.6, 0.6)
      part.Position = vector
      part.Anchored = true
      part.CanCollide = false
      part.Name = regionPartName
      part.Parent = game.Workspace
      ballArray[#ballArray+1] = part
    end

    local thePart = createPart(CFrame.new(0,0,0), Vector3.new(3,3,3), regionPartName, "Ball")
    local selectionBox = Instance.new("SelectionBox")

    local function getMag(vector1, vector2)
      -- removes sqrt because time, reduces function complexity
      local newV2 = Vector3.new(vector2.X, vector1.Y, vector2.Z)
      --return (vector1 - newV2).magnitude
      return (vector1 - vector2).magnitude
      --return ((vector1.X - vector2.X)^2)+((vector1.Y - vector2.Y)^2)+((vector1.Z - vector2.Z)^2) 
    end

    local function getPlayer()
      local play, chara, hum, root = nil, nil, nil, nil
      while not game.Players.LocalPlayer do
        wait()
      end
      if game.Players.LocalPlayer then
        play = game.Players.LocalPlayer
        while not game.Players.LocalPlayer.Character do
          wait()
        end
        if game.Players.LocalPlayer.Character then
          chara = game.Players.LocalPlayer.character
          while not game.Players.LocalPlayer.Character:FindFirstChild("Humanoid") do
            wait()
          end          
          if game.Players.LocalPlayer.Character:FindFirstChild("Humanoid") then
            hum = game.Players.LocalPlayer.Character.Humanoid
          end
          while not game.Players.LocalPlayer.Character:FindFirstChild("HumanoidRootPart") do
            wait()
          end    
          if game.Players.LocalPlayer.Character:FindFirstChild("HumanoidRootPart") then
            root = game.Players.LocalPlayer.Character.HumanoidRootPart
          end
        end
      end
      return play, chara, hum, root
    end

    -- discord webhook stuff
    local webhookLocals = {
      itemsEarned = {},
      startingInventory = getPlayerInvy(game.Players.LocalPlayer),
      dungeonName = nil,
      timeLeft = nil,
      endingInventory = nil,
      colorTable = {
        ['legendary'] = "16426522",
        ['epic'] = "14031610",
        ['rare'] = "39423",
        ['uncommon'] = "2096896",
        ['common'] = "15859184",
      }
    }

    function Format(Int)
      return string.format("%02i", Int)
    end

    local function convertToHMS(Seconds)
      local Minutes = (Seconds - Seconds%60)/60
      Seconds = Seconds - Minutes*60
      return Format(Minutes)..":"..Format(Seconds)
    end

    local function sendWebhookItem()
      (syn and syn.request or http_request) {
        Url = _G.webhookLink;
        Method = 'POST';
        Headers = {
          ['Content-Type'] = 'application/json';
        };
        Body = game:GetService'HttpService':JSONEncode( {  embeds =  webhookLocals.itemsEarned  } );
      };
    end

    local function capFirstLetter(word)
      local done = ""
      local firstLetter = word:sub(1,1) --get the 1st letter of the word
      local theRest = word:sub(2) --grt everything except the first letter
      return firstLetter:upper() .. theRest
    end


    local function getNewItems(firstTable, secondTable)
      for i ,item in pairs (secondTable) do
        if firstTable[i] then
        else
          local s = {}
          s.description = "```\n"..capFirstLetter(item.name).."```"
          s.color = webhookLocals.colorTable[item.rarity]
          table.insert(webhookLocals.itemsEarned, s)
        end
      end
    end


    local function webHookOnEnd()
      if _G.webhookEnabled then
        webhookLocals.timeLeft = convertToHMS(workspace.timeLeft.Value)
        webhookLocals.itemsEarned = {
          {
            color = '0';
            author = {
              name = 'MRobSwag Item Notifier';
            };
            fields = {
              {
                name = "Dungeon: ",
                value = tostring(webhookLocals.dungeonName)
              },
              {
                name = "Clear Time: ",
                value = webhookLocals.timeLeft
              },
            };
          },
        };
        wait(2)
        print('doing webhook')
        webhookLocals.endingInventory = getPlayerInvy(game.Players.LocalPlayer)
        getNewItems(webhookLocals.startingInventory.weapons, webhookLocals.endingInventory.weapons)
        getNewItems(webhookLocals.startingInventory.abilities, webhookLocals.endingInventory.abilities)
        getNewItems(webhookLocals.startingInventory.chests, webhookLocals.endingInventory.chests)
        getNewItems(webhookLocals.startingInventory.helmets, webhookLocals.endingInventory.helmets)
        sendWebhookItem()
        print('done webhook')
      end
    end

    -- discord webhook stuff ending

    if workspace:FindFirstChild("dungeonProgress") then
      game:GetService("Workspace"):FindFirstChild("dungeonProgress").Changed:Connect(function(NewValue)
          if NewValue ~= "" and NewValue ~= "inProgress" and NewValue ~=  "playersNotReady" then
            gameOver = true
            if regionTable ~= nil then
              for i,v in pairs(regionTable) do
                for j, k in pairs(v) do
                  regionTable[i][j]['obj']:Destroy()
                end
              end
            end
            if readyPartTable ~= nil then
              for i,v in pairs(readyPartTable) do
                v:Destroy()
              end
            end
            spawn(webHookOnEnd)
            print('set timeout')
            wait(.5)
            game:GetService("ScriptContext"):SetTimeout(0)
          end
        end)
    elseif workspace:FindFirstChild("raidPorgress") then
      game:GetService("Workspace"):FindFirstChild("raidProgress").Changed:Connect(function(NewValue)
          if NewValue ~= "" and NewValue ~= "inProgress" and NewValue ~=  "playersNotReady" then
            gameOver = true
            if regionTable ~= nil then
              for i,v in pairs(regionTable) do
                for j, k in pairs(v) do
                  regionTable[i][j]['obj']:Destroy()
                end
              end
            end
            if readyPartTable ~= nil then
              for i,v in pairs(readyPartTable) do
                v:Destroy()
              end
            end
            spawn(webHookOnEnd)
            print('set timeout')
            wait(.5)
            game:GetService("ScriptContext"):SetTimeout(0)
          end
        end) 

    end


    function SelectBoxChange(adornee)
      selectionBox.Adornee = adornee
      selectionBox.Color3 = Color3.new(1,0,0)
      selectionBox.Parent = adornee
    end

    local function findCloseEnemy()
      local bestMob = nil
      local bestDist = math.huge
      if #cs:GetTagged("Prio-Enemy") > 0 then
        return cs:GetTagged("Prio-Enemy")[1]
      end
      while #cs:GetTagged("Enemy") < 1 do
        -- script should enter a dodge mode
        ScriptDebug("Waiting for enemies...")
        if extremelyFast then
          game:GetService("RunService").RenderStepped:wait()
        else
          wait()
        end
      end
      while bestMob == nil do
        local enemies = cs:GetTagged("Enemy")
        local _, _, _, root = getPlayer()
        for i, mob in pairs(enemies) do
          if mob:FindFirstChild("HumanoidRootPart") and root ~= nil then
            local dst = getMag(root.Position, mob.HumanoidRootPart.Position)
            if dst < bestDist then
              bestMob = mob
              bestDist = dst
            end
          end
        end
        if bestMob ~= nil then break end
        if extremelyFast then
          game:GetService("RunService").RenderStepped:wait()
        else
          wait()
        end
      end
      if _G.showTarget then
        SelectBoxChange(bestMob.HumanoidRootPart)
      end
      --targetPart.CFrame = bestMob.HumanoidRootPart.CFrame * CFrame.new(0,5,0)
      return bestMob
    end


    function charLookAt(chr,target) --assume chr is a character and target is a brick to look towards
      if chr.PrimaryPart and target and target.Position then --just make sure the character's HRP has loaded
        local chrPos=chr.PrimaryPart.Position --get the position of the HRP
        local tPos=target.Position --get the position of the target
        local newCF=CFrame.new(Vector3.new(chrPos.x,chrPos.y,chrPos.z),Vector3.new(tPos.x,chrPos.y,tPos.z)) --create our CFrame
        chr:SetPrimaryPartCFrame(newCF) --set the HRP's CFrame to our result, thus moving the character!
      end
    end

    local function clearBalls()
      for i, v in pairs(ballArray) do
        v:Destroy()
      end
      ballArray = {}
    end


    local function followPath(position)
      local root = game.Players.LocalPlayer.Character.HumanoidRootPart
      local hum = game.Players.LocalPlayer.Character.Humanoid
      path:ComputeAsync(root.Position, position)
      waypoints = {}
      if path.Status == Enum.PathStatus.Success then
        waypoints = path:GetWaypoints()
        if sDebug then
          clearBalls()
          for i, v in pairs(waypoints) do
            createBall(v.Position)
          end
        end
        currentWaypointIndex = 2
        if waypoints[currentWaypointIndex] == Enum.PathWaypointAction.Jump then
          hum.Jump = true
        end
        hum:MoveTo(waypoints[currentWaypointIndex].Position)

      else
        print('path not success')
        if enemy then
          hum:MoveTo(enemy.PrimaryPart.Position)
        else
          hum:MoveTo(root.Position)
        end
        
      end
    end

    local function onWaypointReached(reached)
      local play, chara, hum, root = getPlayer()
      if chara ~= nil and hum ~= nil and reached and currentWaypointIndex < #waypoints then
        currentWaypointIndex = currentWaypointIndex + 1
        charLookAt(chara, enemy.HumanoidRootPart)
        hum:MoveTo(waypoints[currentWaypointIndex].Position)
      elseif chara ~= nil and hum ~= ni and enemy and enemy:FindFirstChild("HumanoidRootPart") then
        charLookAt(chara, enemy.HumanoidRootPart)
      end
    end

    local function onPathBlocked(blockedWaypointIndex)
      print('path blocked')
      local play, chara, hum, root = getPlayer()
      if chara ~= nil and enemy ~= nil then
        charLookAt(chara, enemy.HumanoidRootPart)
      end
      if blockedWaypointIndex > currentWaypointIndex then
        followPath(destination)
      end
    end

    local function rayCollectionService()
      local play, chara, hum, root = getPlayer()
      if chara == nil then return end
      cs:AddTag(chara, "RayIgnore")
      cs:AddTag(workspace.Terrain, "RayWhitelist")
      if workspace:FindFirstChild("tier") then -- boss raid 
        for i,v in pairs(game:GetService("Workspace").mapModel:GetChildren()) do
          if v.ClassName == "Part" or v.ClassName == "UnionOperation" or v.ClassName == "WedgePart" then
            if v ~= chara and v.Name ~= regionPartName and v.Transparency < 1 and v.Name ~= "enemyRadius" then
              cs:AddTag(v, "RayWhitelist")
            end
          elseif  v.ClassName == "Model" then
            if v ~= chara then
              cs:AddTag(v, "RayWhitelist")
            end
          end
        end
      elseif workspace:FindFirstChild("currentWave") then -- wave defense
        for i,v in pairs(workspace:GetChildren()) do
          if string.find(v.Name, "Arena") then
            cs:AddTag(v, "RayWhitelist")
          end
        end
      else -- normal dungeon
        local dun = waitForExist(workspace, "dungeon")
        for i,room in pairs(dun:GetChildren()) do
          for j, v in pairs(room:GetChildren()) do
            if v.ClassName == "Part" or v.ClassName == "UnionOperation" or v.ClassName == "WedgePart"  then
              if v.Transparency < 1 then
                cs:AddTag(v, "RayWhitelist")
              end
            elseif v.ClassName == "Model" then
              cs:AddTag(v, "RayWhitelist")      
            end      
          end
        end
        for i,v in pairs(workspace:GetChildren()) do
          if v.ClassName == "Part" or v.ClassName == "UnionOperation" or v.ClassName == "WedgePart" then
            if v ~= chara and v.Name ~= regionPartName and v.Transparency < 1 and v.Name ~= "enemyRadius" then
              cs:AddTag(v, "RayWhitelist")
            end
          elseif  v.ClassName == "Model" then
            if v ~= chara then
              cs:AddTag(v, "RayWhitelist")
            end
          end
        end
      end
    end


    local function lookAt(target, eye)
      local forwardVector = (target - eye).Unit
      local upVector = Vector3.new(0, 1, 0)
      -- Remember the right-hand rule
      local rightVector = forwardVector:Cross(upVector)
      local upVector2 = rightVector:Cross(forwardVector)

      return CFrame.fromMatrix(eye, rightVector, upVector2)
    end

    function round(num)
      return math.floor(num + 0.5)
    end

    function roundVector(vector)
      return Vector3.new(round(vector.X), round(vector.Y), round(vector.Z))
    end

    local oldTargetPos = Vector3.new(0,0,0)
    local targetPos = Vector3.new(1,0,0)
    local function makePath(target, value)
      if value == nil then value = false end
      local play, chara, hum, root = getPlayer()
      if target.ClassName == "Model" then
        targetPos = roundVector(target.PrimaryPart.Position)
      else
        targetPos = roundVector(target.Position)
      end
      if hum ~= nil and root ~= nil then
        oldTargetPos = targetPos
        destination = targetPos
        if value then
          if enemy ~= nil then
            charLookAt(chara, enemy.PrimaryPart)
          end
          spawn(clearBalls)
          hum:MoveTo(targetPos)
        else
          followPath(targetPos)
        end
      end
    end

    function visualRay(long)
      local p = Instance.new("Part")
      cs:AddTag(p, "RayIgnore")
      p.Size = Vector3.new(2,2,2) 
      p.Name = "Ray"
      p.Anchored = true
      p.Material = "Neon"
      p.CanCollide = false
      p.Parent = workspace
      local Debris = game:GetService("Debris")
      Debris:AddItem(p, long)
      return p
    end

    function rayCast(sCF, eCF, ignoreName, whitelist)
      local endGoal = eCF.p
      local start = sCF.p
      local Ray = Ray.new(start, (endGoal - start))
      local list = cs:GetTagged(ignoreName)
      local part, hitPosition
      if whitelist then
        part, hitPosition = workspace:FindPartOnRayWithWhitelist(Ray,list)
      else
        part, hitPosition = workspace:FindPartOnRayWithIgnoreList(Ray,list)
      end
      --if ignoreName == "directionWL" then
      --[[ ray visualize
        local p = visualRay(.005)
        local distance = (start - hitPosition).Magnitude
        p.Size = Vector3.new(0.3, 0.3, distance)
        p.CFrame = lookAt(start, hitPosition)*CFrame.new(0, 0, -distance/2)
      end]]

      return hitPosition, part
    end
    -- false is blacklist, true is whitelist
    local whiteListBlackList = {
      ["laserBeam"] = true, 
      ["bossRiflePreCast"] = true, 
      ["bossRifleShot"] = true, 
      ["hitIndicatorIceAOE"] = true, 
      ["iceBeamIndicator"] = true, 
      ["projectile"] = true, 
      ["mageProjectileBall"] = true, 
      ["thirdBossSafeSpots"] = true, 
      ["secondBossOrb"] = true, 
      ["thirdBossOrbShot"] = true, 
      ["spikePrecast"] = true, 
      ["kolvumarTrail"] = true, 
      ["Kraken Tentacle"] = true,
      ["secondBossRandomSquare"] = true,
      ["initialMageBossEntry"] = false, 
      ["initialKingBossEntry"] = false, 
      ["initialHunterBossEntry"] = false, 
      ["thirdBossSafeSpot"] = false, 
      ["forceField"] = false, 
      ["safeSpotCircle"] = false, 
      ["secondBossSafeSpots"] = false

    }
    local lastCheckList = {
      ["glowPart"] = true, 
      ["outerPrecast"] = true, 
      ["beam"] = true, 
      ["Beam"] = true, 
      ["precast"] = true, 
      ["preCast"] = true, 
      ["HumanoidRootPart"] = true
    }

    local checkProjResult = nil
    local checkProjResult1 = nil
    local checkProjResult2 = nil
    local projNameTemp = nil
    local projNameParentTemp = nil

    local function checkIfProjectile(obj)
      projNameTemp = obj.Name
      if projNameTemp == "enemyRadius" then
        return true
      end
      if obj.Transparency == 1 then
        return false
      end

      checkProjResult = whiteListBlackList[projNameTemp]
      if checkProjResult ~= nil then
        if checkProjResult then
          return checkProjResult
        end
      end
      projNameParentTemp = obj.Parent
      checkProjResult1 = whiteListBlackList[obj.Parent.Name]
      if checkProjResult1 ~= nil then
        return checkProjResult1
      end

      if stringInTable(projNameTemp, projNameList) then
        return false
      end

      checkProjResult2 = lastCheckList[projNameTemp]
      if checkProjResult2 ~= nil and (obj.ClassName == "Part" ) and projNameParentTemp ~= game.Players.LocalPlayer.Character and (checkProjResult2) then --or obj.ClassName == "Union"
        return true
      else
        return false
      end
    end


    local regionPartSize = 4
    local regionStartSize = 5--5
    local regionPartDivisor = 1.4--1.5
    local readyPartTable = {}
    local randomNum = math.random(0,4)
    local function createRegionPart()
      if _G.loadSlow then
        game:GetService("RunService").RenderStepped:wait()
      end
      local part = Instance.new("Part")
      cs:AddTag(part, "RayIgnore")
      part.Size = Vector3.new(regionPartSize, 50, regionPartSize)
      part.CFrame = CFrame.new(0,100,0)
      part.Name = regionPartName
      part.Anchored = true
      part.CanCollide = false
      part.Material = "SmoothPlastic"
      part.Transparency = stuffTransparency --.9
      part:GetPropertyChangedSignal("Transparency"):Connect(antiTransChange)
      part.ChildAdded:Connect(antiChildChange)
      part.BrickColor = BrickColor.new("Black")

      if randomNum == 0 then
        if workspace:FindFirstChild("hardcore") then
          part.Parent = workspace.hardcore
        else
          part.Parent = workspace.raidProgress
        end
      elseif randomNum== 1 then
        part.Parent = workspace.timeLeft
      elseif randomNum == 2 then
        part.Parent = workspace.stats
      elseif randomNum==3 then
        if workspace:FindFirstChild("start") then
          part.Parent = workspace.start
        else
          part.Parent = workspace.dungeonStarted
        end
      elseif randomNum == 4 then
        part.Parent = workspace.Camera
      end


      local connection = part.Touched:Connect(function() end)
      insert(readyPartTable, part)
      return part
    end

    local function getTableSetup(size)
      local t = {}
      for j = 1, size do -- these loops actually make the table
        for l = 1, size do
          if t[j] == nil then -- if not obj, make obj
            t[j] = {}
          end
          if t[j][l] == nil then -- if not obj, make obj
            t[j][l] = {['obj'] = nil, ['safe'] = nil} 
          end
        end
      end
      return t
    end

    local function createInitalRegionTable(size)
      --441
      for i= 1, 441 do
        createRegionPart()
      end
      local root = game.Players.LocalPlayer.Character.HumanoidRootPart
      local regionTable = getTableSetup(size)
      local midPoint = (size/2) + .5 --get center cords
      for i = 1, size do
        for j = 1, size do
          local part = remove(readyPartTable)
          regionTable[i][j]['obj'] = part
          regionTable[i][j]['safe'] = true
          if i ~= midPoint or j ~= midPoint then
            cs:AddTag(regionTable[i][j]['obj'], "directionWL")
          end
        end
      end
      return regionTable
    end

    local regionTable = createInitalRegionTable(regionStartSize)


    local function GenerateSpiral(size)
      --local _,_,_,root = getPlayer()
      local size = #regionTable
      local _,_,_,root = getPlayer()
      if root ~= nil then
        local x = 0
        local y = 0
        local d = 0
        local c = 0
        local s = 0
        local tableIndex, part, parts
        for k = 1, size - 1 do 
          for j = 0, (k < (size - 1) and 2 or 3) do 
            for i = 0, s do 
              local Vector = root.Position + Vector3.new(x, 0, y)

              local Part = Instance.new("Part")
              Part.Anchored = true 
              Part.CanCollide = false 
              Part.Position = Vector 
              Part.Size = Vector3.new(2, 2, 2)
              Part.Parent = workspace

              if d == 0 then 
                y = y + 5 
              elseif d == 1 then 
                x = x + 5 
              elseif d == 2 then 
                y = y - 5 
              elseif d == 3 then 
                x = x - 5 
              end 
            end
            d = (d + 1) % 4
          end
          s = s + 1
        end
      end
    end 

    local function updateRegionTable()
      local _,_,_,root = getPlayer()
      if root ~= nil then
        local size = #regionTable
        local x = (((size - 1) * regionPartSize) / 2) * -1/regionPartDivisor -- size minus one because the number has to be odd for the player to be centered, *5 because thats size of part being crreated, /2 to get how far back it muist go, *-1 to get negative #
        local z = (((size - 1) * regionPartSize) / 2) * -1/regionPartDivisor
        local tableIndex, part, parts
        for i, v in pairs(regionTable) do
          for j, k in pairs(v) do
            tableIndex = k
            part = tableIndex['obj']
            if root ~= nil and part ~= nil  then
              part.CFrame = root.CFrame * CFrame.new(x,0,z)
              --part.Position = (root.CFrame * CFrame.new(x,-1,z)).Position
              parts = part:GetTouchingParts() -- local parts = GetTouchingParts(part)
              part.BrickColor = BrickColor.new("Black")
              tableIndex['safe'] = true
              for m, k in pairs(parts) do
                if checkIfProjectile(k) then
                  part.BrickColor = BrickColor.new("Bright red")
                  tableIndex['safe'] = false
                  break
                end        
              end
            end
            z = z + regionPartSize/regionPartDivisor
          end
          z = (((size - 1) * regionPartSize) / 2) * -1/regionPartDivisor
          x = x + regionPartSize/regionPartDivisor
        end
      end
    end

--[[
    local function updateRegionTable()
      local _,_,_,root = getPlayer()
      if root ~= nil then
        local size = #regionTable
        local x = (((size - 1) * regionPartSize) / 2) * -1/regionPartDivisor -- size minus one because the number has to be odd for the player to be centered, *5 because thats size of part being crreated, /2 to get how far back it muist go, *-1 to get negative #
        local z = (((size - 1) * regionPartSize) / 2) * -1/regionPartDivisor
        local tableIndex, part, parts
        for i, v in pairs(regionTable) do
          for j, k in pairs(v) do
            tableIndex = k
            part = tableIndex['obj']
            if root ~= nil and part ~= nil  then
              part.CFrame = root.CFrame * CFrame.new(x,0,z)
              --part.Position = (root.CFrame * CFrame.new(x,-1,z)).Position
              parts = part:GetTouchingParts() -- local parts = GetTouchingParts(part)
              part.BrickColor = BrickColor.new("Black")
              tableIndex['safe'] = true
              for m, k in pairs(parts) do
                if checkIfProjectile(k) then
                  part.BrickColor = BrickColor.new("Bright red")
                  tableIndex['safe'] = false
                  break
                end        
              end
            end
            z = z + regionPartSize/regionPartDivisor
          end
          z = (((size - 1) * regionPartSize) / 2) * -1/regionPartDivisor
          x = x + regionPartSize/regionPartDivisor
        end
      end
    end
]]

    local function increaseRegionTable()
      local p, new
      for i,col in pairs(regionTable) do
        if #readyPartTable == 0 then
          createRegionPart()
        end
        p = remove(readyPartTable)
        new = {}
        new['obj'] = p
        insert(regionTable[i], 1, new)
        if #readyPartTable == 0 then
          createRegionPart()
        end
        p = remove(readyPartTable)
        new = {}
        new['obj'] = p
        insert(regionTable[i], new)
      end
      local topColumn = {}
      for i, row in pairs(regionTable[1]) do
        if #readyPartTable == 0 then
          createRegionPart()
        end
        p = remove(readyPartTable)
        new = {}
        new['obj'] = p
        insert(topColumn, new)
      end
      local botColumn = {}
      for i, row in pairs(regionTable[1]) do
        if #readyPartTable == 0 then
          createRegionPart()
        end
        p = remove(readyPartTable)
        local new = {}
        new['obj'] = p
        insert(botColumn, new)
      end
      insert(regionTable, 1, topColumn)
      insert(regionTable, botColumn)
    end

    local function decreaseRegionTable()
      local tr
      for i,col in pairs(regionTable) do
        tr = remove(regionTable[i], #regionTable[i])
        if tr ~= nil then
          tr['obj'].CFrame = CFrame.new(0,0,0)
          insert(readyPartTable, tr['obj'])
          local tr = remove(regionTable[i], 1)
          tr['obj'].CFrame = CFrame.new(0,0,0)
          insert(readyPartTable, tr['obj'])
        end
      end
      tr = remove(regionTable, #regionTable)
      for i, v in pairs(tr) do
        if v ~= nil then
          v['obj'].CFrame = CFrame.new(0,0,0)
          insert(readyPartTable, v['obj'])
        end
      end
      tr = remove(regionTable, 1)
      for i, v in pairs(tr) do
        if v ~= nil then
          v['obj'].CFrame = CFrame.new(0,0,0)
          insert(readyPartTable, v['obj'])
        end
      end
    end



    local objectiveExists = false
    local objectiveObject = nil
    local forceObjectiveExists = false
    function checkAroundPlayer(regionTable, s)
      s = (s/2) + .5 --get center cords
      for i = #regionTable - s, regionStartSize do
        if not regionTable[i][i]['safe'] then return false end
      end
      return true
    end

    local function checkCenter(regionTable, s)
      s = (s/2) + .5 --get center cords
      return regionTable[s][s]['safe']
    end

    local function decide()
      enemy = findCloseEnemy()
      local num = mobRange
      if enemy ~= nil and enemy.Name ~= "Azrallik's Heart" and enemy.Name ~= "Dragon Orb" then
        enemy:WaitForChild("enemyStyle")
        local mobType = enemy.enemyStyle.Value
        if mobType ~= "mob" and mobType ~= "ranged" and mobType ~= "melee" and mobType ~= "burly" then -- if boss then
          num = bossRange
          bossPresent = true
        else -- if mob
          if bossPresent then -- if boss did exist but now didnt, that means boss died
            for i,v in pairs(workspace:GetChildren()) do
              if enemyProjNameList[v.Name] then
                v:Destroy()
              end
            end
          end
          bossPresent = false
        end 
      end
      --if enemy.Name == "Ancient Lava Mage" then num = 25 end
      local _,_, hum,root = getPlayer()
      if root ~= nil and enemy ~= nil then
        local ePos = enemy.PrimaryPart.Position
        local eNVec = Vector3.new(ePos.X, root.Position.Y, ePos.z)
        local actualDist = getMag(eNVec, root.Position)  - (enemy.PrimaryPart.Size.Z/2) 
        updateRegionTable()
        print(actualDist)
        print(num)
        if forceObjectiveExists then
          return 'chase_fobjective', nil
        elseif not checkAroundPlayer(regionTable, #regionTable)  then
          if not bossPresent and _G.teleportDuringBossOnly then
            game.Players.LocalPlayer.Character.Humanoid.WalkSpeed = 33
          else
            game.Players.LocalPlayer.Character.Humanoid.WalkSpeed = 24
          end
          return 'dodge', nil
        elseif objectiveExists and objectiveObject ~= nil then
          game.Players.LocalPlayer.Character.Humanoid.WalkSpeed = 24
          return 'chase_objective', nil
        elseif actualDist < num - 5  then --elseif actualDist < num - 5 and bossPresent then
          game.Players.LocalPlayer.Character.Humanoid.WalkSpeed = 24
          return "run", nil
        elseif actualDist < num then
          game.Players.LocalPlayer.Character.Humanoid.WalkSpeed = 24
          return "strafe", nil
        else
          if bossPresent then
            game.Players.LocalPlayer.Character.Humanoid.WalkSpeed = 24
          else
            game.Players.LocalPlayer.Character.Humanoid.WalkSpeed = 30
          end
          return "chase", nil
        end
      else
        return "nothing"
      end
    end

    if _G.doInstakill then
      game:GetService("RunService").RenderStepped:connect(function()
          if (sethiddenproperty) then
            sethiddenproperty(game:GetService("Players").LocalPlayer, 'SimulationRadius', math.huge)
          end
        end)
    end
    local _, p, height
    local smalltpdebuff = true
    local function mainLoop()
      spawn(function()
          local _,_,hum,root = getPlayer()
          while not gameOver do
            _,_,hum,root = getPlayer()
            if root ~= nil and hum ~= nil and hum.Health > 0 then
              spawn(function()
                  game.Players.LocalPlayer.Character.Humanoid.WalkSpeed = walkspeed
                end)
                print("uh")
              local thought, data = decide()
              ScriptDebug("Thought: ".. thought .. ", Enemy: " .. enemy.Name)
              if thought == "chase" then
                _, p = rayCast(root.CFrame, enemy.PrimaryPart.CFrame, "RayWhitelist", true) 
                if p == nil then -- if no walls between player and enemy then use moveto instead of pathfinding it
                  makePath(enemy, true)
                else
                  makePath(enemy)
                end
              elseif thought == "chase_objective" then
                if objectiveObject ~= nil and objectiveObject.ClassName == "Model" then
                  _, p = rayCast(root.CFrame * CFrame.new(0,0,0), objectiveObject.PrimaryPart.CFrame * CFrame.new(0,4,0), "RayWhitelist", true)
                elseif objectiveObject ~= nil then
                  _, p = rayCast(root.CFrame * CFrame.new(0,0,0), objectiveObject.CFrame * CFrame.new(0,4,0), "RayWhitelist", true)
                end
                if p == nil then -- if no walls between player and objective then use moveto instead of pathfinding it
                  makePath(objectiveObject, true)
                else
                  makePath(objectiveObject)
                end
              elseif thought == "chase_fobjective" then
                _, p = rayCast(root.CFrame, thePart.CFrame, "RayWhitelist", true)
                if p == nil then -- if no walls between player and objective then use moveto instead of pathfinding it
                  makePath(thePart, true)
                else
                  makePath(thePart)
                end
              elseif thought == "strafe" then
                local left, p = rayCast(root.CFrame, root.CFrame * CFrame.new(1000,0,0), "RayWhitelist",  true) -- left
                local right = rayCast(root.CFrame, root.CFrame * CFrame.new(-1000,0,0), "RayWhitelist", true)-- right
                local leftDist = getMag(root.Position, left)
                local rightDist = getMag(root.Position, right)
                if math.abs(leftDist - rightDist) < 5 then 
                  thePart.CFrame = root.CFrame
                else
                  if rightDist < leftDist then
                    thePart.CFrame = root.CFrame * CFrame.new(5,0,0)
                  else
                    thePart.CFrame = root.CFrame * CFrame.new(-5,0,0)
                  end                  
                end
                makePath(thePart, true) 		
              elseif thought == "run" then
                _, p = rayCast(root.CFrame * CFrame.new(0,0,0), root.CFrame * CFrame.new(0,0,25), "RayWhitelist", true) 
                if p == nil then -- if nothing is behind me, then run backwards
                  thePart.CFrame = root.CFrame * CFrame.new(0,0,25)
                  makePath(thePart, true)
                else -- keep looking to the left and right till we find a point with no part
                  local found = false
                  for i = 1, 20 do
                    if found then
                      break
                    end
                    for j = 1, 2 do
                      local studVal = i * 9
                      if j == 1 then
                        studVal = studVal * -1
                      end
                      _, p = rayCast(root.CFrame, root.CFrame * CFrame.new(studVal,-2,25 - i), "RayWhitelist", true) 
                      if p == nil then -- location found!
                        found = true
                        thePart.CFrame = root.CFrame * CFrame.new(studVal,-2,25 - i)
                        break
                      end
                    end
                  end
                  makePath(thePart, true)
                end
              elseif thought == "dodge" then
                local cSafe = nil -- gets the nearest safe spot
                local cSafeVal = math.huge
                local temp, temp1
                local inCenter = false
                local s = (#regionTable/2) + .5 --get center cords
                while cSafe == nil and root ~= nil and hum ~= nil and hum.Health > 0 do
                  if regionTable[s][s]['safe'] then inCenter = true cSafe = regionTable[s][s]['obj'] break end -- if its 1, break cause it has to be best
                  for x,rowObj in pairs(regionTable) do
                    for y, colObj in pairs(rowObj) do
                      temp = regionTable[x][y]
                      temp1 = math.floor(getMag(root.Position, temp['obj'].Position) + .5)
                      if temp['safe'] and temp1 < cSafeVal then
                        --print("Cur Val: ".. temp1 .. " Best Val: " .. cSafeVal)
                        _, p = rayCast(root.CFrame * CFrame.new(0,0,0), CFrame.new(temp['obj'].Position, root.Position) * CFrame.new(0,0,regionPartSize/2), "RayWhitelist", true) 
                        if p == nil then
                          cSafe = temp['obj']
                          cSafeVal = temp1
                        else
                          temp['obj'].BrickColor = BrickColor.new("Bright yellow")
                        end
                      end          
                    end
                  end
                  if cSafe ~= nil then -- if safe found break loop,
                    break
                  else -- if no safe found, increase scope and loop over everything again
                    increaseRegionTable()
                    updateRegionTable()
                    if extremelyFast then
                      game:GetService("RunService").RenderStepped:wait()
                    else
                      wait()
                    end
                  end
                end -- while loop done here, searching done
                _,_,hum,root = getPlayer()
                if cSafe ~= nil and root ~= nil and hum ~= nil then
                  if inCenter then
                    if objectiveExists then
                      if objectiveObject ~= nil and objectiveObject.ClassName == "Model" then
                        height = Vector3.new(objectiveObject.PrimaryPart.Position.X, root.Position.Y, objectiveObject.PrimaryPart.Position.Z)
                      elseif objectiveObject ~= nil then
                        height = Vector3.new(objectiveObject.Position.X, root.Position.Y, objectiveObject.Position.Z)
                      end
                    else
                      height = Vector3.new(enemy.PrimaryPart.Position.X, root.Position.Y, enemy.PrimaryPart.Position.Z)
                    end
                    _, p = rayCast(root.CFrame * CFrame.new(0,0,0), CFrame.new(height), "directionWL", true)
                    if p ~= nil and p.BrickColor == BrickColor.new("Black") then
                      if objectiveExists then
                        thePart.CFrame = p.CFrame -- move thepart to the thing safe thats towards objective
                      elseif getMag(enemy.PrimaryPart.Position, root.Position) > bossRange then -- if the enemy isnt within ability range then set thepart to the closet safe spot
                        --print('move closer')
                        thePart.CFrame = p.CFrame
                      else -- if everything is wrong then go to safe spot
                        --print('stay')
                        thePart.CFrame = root.CFrame
                      end
                    else -- safe spot towards objectives/enemy is not safe/ dont do shit
                      --print('dont move')
                      thePart.CFrame = cSafe.CFrame
                    end
                  else
                    thePart.CFrame = cSafe.CFrame
                  end
                  cSafe.BrickColor = BrickColor.new("Lime green")
                  if inCenter then -- if incenter then just path to the part (since it might be towards an enemy or objective
                    game.Players.LocalPlayer.Character.HumanoidRootPart.CFrame = cSafe.CFrame
                    makePath(thePart, true)
                  else
                    if (cSafeVal < _G.smallTeleportVal) and _G.smallTeleports and smalltpdebuff then -- if not incenter and the dodge is close, just TP to it -- > 9
                      if not _G.teleportDuringBossOnly or bossPresent then
                        smalltpdebuff = false
                        game.Players.LocalPlayer.Character.HumanoidRootPart.CFrame = thePart.CFrame
                        makePath(thePart, true)
                        spawn(function()
                            wait(.1)
                            smalltpdebuff = true
                          end)
                      else -- if neither just play normal
                        makePath(thePart, true)
                      end
                    else -- if neither just play normal
                      makePath(thePart, true)
                    end
                  end
                end
                while #regionTable > regionStartSize do
                  decreaseRegionTable()
                  if extremelyFast then
                    game:GetService("RunService").RenderStepped:wait()
                  else
                    wait()
                  end
                end
              end
            end
            if extremelyFast then
              game:GetService("RunService").RenderStepped:wait()
            else
              wait()
            end
          end
        end)  
    end
    --PSU_FAST_EXECUTION(function() mainLoop() end)
    mainLoop()

    local function useabilities()
      while not game.Players.LocalPlayer:FindFirstChild("Backpack") do
        wait()
      end
      while not gameOver do
        if _G.ignoreAbilityRange then
          game:GetService("RunService").RenderStepped:wait()
        else
          wait()
        end
        char = game.Players.LocalPlayer.Character
        if enemy ~= nil and enemy.PrimaryPart ~= nil and char ~= nil and char.PrimaryPart ~= nil then
          if (getMag(enemy.PrimaryPart.Position, char.PrimaryPart.Position) - (enemy.PrimaryPart.Size.Z/2) ) < abilityRange or _G.ignoreAbilityRange then -- 25, 65 is the range in which we attack
            for _, v in pairs(game.Players.LocalPlayer.Backpack:GetChildren()) do
              if v:FindFirstChildOfClass("RemoteEvent") and v.cooldown.Value <= 0 then
                v:FindFirstChildOfClass("RemoteEvent"):FireServer()
              end
            end
          end
        end
      end
    end

    local function getswordstats()
      player = game.Players.LocalPlayer.Character:GetChildren()
      for _, v in pairs(player) do
        if v.ClassName == "Accessory" then
          if v:FindFirstChild("swing") then
            if v:FindFirstChild("attackSpeed") then
              return v.swing, v.attackSpeed.Value
            end
          end
        end
      end
    end	

    if _G.auto_attack then
      spawn(useabilities)
      spawn(function()
          while not gameOver do
            sword, cooldown = getswordstats()
            player = game.Players.LocalPlayer.Character
            if enemy ~= nil and enemy.PrimaryPart ~= nil and player ~= nil and player.PrimaryPart ~= nil then
              if cooldown ~= nil and (getMag(enemy.PrimaryPart.Position, player.PrimaryPart.Position) - (enemy.PrimaryPart.Size.Z/2) ) < 13 then
                wait(cooldown/10)
                sword:FireServer()
              end
            end
            wait()
          end
        end)
    end

    local function steamPunkLast(instance) -- finds the four spots and returns the best one
      instance:WaitForChild("precast")
      --wait(.5)
      local steamTable = {
        bestVal = math.huge,
        bestObj = nil,
        dist = nil,
        newPoint = nil,
      }

      local _, _, _, root = getPlayer()
      for i,v in pairs(instance:GetChildren()) do
        if v.Name == "hitBox" then
          steamTable.dist = getMag(game.Players.LocalPlayer.Character.HumanoidRootPart.Position, v.Position)
          v.Transparency = .9
          if steamTable.dist < steamTable.bestVal then
            steamTable.bestVal = steamTable.dist
            steamTable.bestObj = v
          end
        elseif v.Name == "cog" then
          v:Destroy()
        end
      end
      steamTable.bestObj.BrickColor = BrickColor.new("Lime Green")
      local a = (steamTable.bestObj.CFrame * CFrame.new(0,0,(steamTable.bestObj.Size.Z/-2) + 5)).Position
      local b = (steamTable.bestObj.CFrame * CFrame.new(0,0,(steamTable.bestObj.Size.Z/2) - 5)).Position
      if getMag(enemy.PrimaryPart.Position, a) < getMag(enemy.PrimaryPart.Position, b) then
        return a
      else
        return b
      end
    end

    -- secondBossGeyser
    local function findClosestRockPile(i)
      local a = workspace.secondBossRockPile2.Union
      local b = workspace.secondBossRockPile1.Union
      if (a.Position - i.PrimaryPart.Position).Magnitude < (b.Position - i.PrimaryPart.Position).Magnitude then
        return a
      else
        return b
      end
    end



    local childAddedT = {
      forceFieldCounter = 0,
      gotRock = false,
      gyzerTable = {},
      gyzerLoopRunning = false,
    }

    local function createTentacleAttack(tentacle)
      local r = game.Players.LocalPlayer.Character.HumanoidRootPart
      local t = tentacle.PrimaryPart
      local part = Instance.new("Part")
      part.CFrame = CFrame.new(part.Position, r.Position)
      part.CFrame = t.CFrame * CFrame.new(0,10,-60)
      part.Size = Vector3.new(14,5,128)
      part.Parent = workspace
      part.CanCollide = false
      part.Transparency = 1
      part.Anchored = true
      part.Name = "enemyRadius"
      wait(3)
      part:Destroy()        
    end


    workspace.ChildAdded:Connect(function(instance)
        if instance.Name == regionPartName then return end
        --print(instance.Name)
        if instance.Name == "firstBossMoveOrb" then -- ocean 1
          addHitBox(instance, 27, "rectanglev3")
        elseif instance.Name == "secondBossSlamHitbox" then 
            local hitBox = instance:WaitForChild("hitBox")
    
            if hitBox.Size.Z == 10 and hitBox.Size.Y == 150 and hitBox.Size.X % 10 == 0 and hitBox.Size.X >= 10 and hitBox.Size.X <= 150 then
                local partHitBox = Instance.new("Part")
                partHitBox.Anchored = true
                partHitBox.CanCollide = false
                partHitBox.Transparency = 0.5
                partHitBox.CFrame = hitBox.CFrame
                partHitBox.Size = Vector3.new(hitBox.Size.X + 7, 5, 800)
                partHitBox.Name = "enemyRadius"
                partHitBox.Parent = workspace
                
                repeat 
                    wait() 
                until instance == nil or not instance:IsDescendantOf(workspace)
                partHitBox:Destroy() 
            end
        elseif instance.Name == "thirdBossOrbCircle" or instance.Name == "finalBossOrbShot" then -- ocean 3
          addHitBox(instance, 30, "rectangle-2") 
        elseif instance.Name == "firstBossFollowOrb" then -- volcanic 1
          addHitBox(instance, 25, "rectangle-2")
        elseif instance.Name == "mageProjectileBall" then -- canals 1
          addHitBox(instance, 10, "rectangle")
        elseif instance.Name == "secondBossCrescent" then -- canals 2
          addHitBox(instance, 12, "square")
        elseif instance.Name == "secondBossOrb" then -- orbital 2
          addHitBox(instance, 12, "rectanglev3")
        elseif instance.Name == "secondBossStabProjectile" then -- bos raid, ancient stone guardian
          addHitBox(instance, 15, "rectangle-2")
        elseif instance.Name == "gasBall" then -- egg event
          addHitBox(instance, 10, "rectangle")
        elseif instance.Name == "tornado" then -- boss raid, dragon
          addHitBox(instance, 20, "square")
        elseif instance.Name == "thirdBossOrbShot" then -- orbital 3
          addHitBox(instance, 26, "rectanglev2")
        elseif instance.Name == "Kraken Tentacle" then -- ghastly 1
          local debuff = true
          instance:WaitForChild("Humanoid")
          while instance.Parent ~= nil and instance:FindFirstChild("Humanoid") and instance.Humanoid.Health > 0 do
            if #instance.Humanoid:GetPlayingAnimationTracks() == 2 and debuff then
              debuff = false
              createTentacleAttack(instance)
              wait(3)
              debuff = true
            else
              print('not attacking')
            end
            wait()
          end
        elseif instance.Name == "Kraken Tentacle" then -- ghastly 1
          local debuff = true
          instance:WaitForChild("Humanoid")
          while instance.Parent ~= nil and instance:FindFirstChild("Humanoid") and instance.Humanoid.Health > 0 do
            if #instance.Humanoid:GetPlayingAnimationTracks() == 2 and debuff then
              debuff = false
              createTentacleAttack(instance)
              wait(3)
              debuff = true
            else
              print('not attacking')
            end
            wait()
          end
        elseif instance.Name == "overheadCannon" then -- ghastly 2
          print('got cannon')
          objectiveExists = true
          objectiveObject = game:GetService("Workspace").playerFireCannon.ring
          spawn(function()
              while instance ~= nil and instance.Parent ~= nil do
                wait()
              end
              if workspace.playerFireCannonHitMark.Transparency == 1 then
                print('obj done')
                objectiveObject = nil
                objectiveExists = false
              else
                print('chara prob died, get new cannon')
                objectiveObject = workspace.playerPickupCannonballRing
                objectiveExists = true              
              end
              -- used cannon shot
            end)
        elseif instance.Name == "secondBossGeyser" then -- volcanic 2
          instance:WaitForChild("PrimaryPart")
          spawn(function()
              local gyzerPos = #childAddedT.gyzerTable+1
              insert(childAddedT.gyzerTable, instance)
              while instance ~= nil and instance.Parent ~= nil do
                wait()
              end
              print('remove gyzzer instance')
              remove(childAddedT.gyzerTable, gyzerPos)
            end)
          spawn(function()
              if not childAddedT.gyzerLoopRunning then
                -- gyzer has spawned
                objectiveExists = true
                childAddedT.gyzerLoopRunning = true
                while workspace.secondBossRockPile2.Union.Transparency ~= 1 and #childAddedT.gyzerTable ~= 0 do -- while gyzer active do
                  if childAddedT.gotRock then
                    objectiveObject = childAddedT.gyzerTable[#childAddedT.gyzerTable]
                  else
                    objectiveObject = findClosestRockPile(childAddedT.gyzerTable[#childAddedT.gyzerTable])
                  end
                  wait()
                end
                childAddedT.gyzerLoopRunning = false
                if #childAddedT.gyzerTable == 0 or workspace.secondBossRockPile2.Union.Transparency == 1 then
                  objectiveObject = nil
                  objectiveExists = false
                end
              end
            end)
        elseif instance.Name == "secondBossOverheadRock" then -- volcanic 2
          -- player got the rock
          childAddedT.gotRock = true
          while workspace:FindFirstChild("secondBossOverheadRock") and workspace.secondBossRockPile2.Union.Transparency ~= 1 do -- while rock exists wait
            wait()
          end
          childAddedT.gotRock = false
        elseif instance.Name == "thirdBossSafeSpots" then -- steampunk 3
          forceObjectiveExists = true
          local safe = steamPunkLast(instance)
          thePart.CFrame = CFrame.new(safe)
          while workspace:FindFirstChild(instance.Name) and workspace[instance.Name]:FindFirstChild("precast") and workspace[instance.Name]:FindFirstChild("precast").Transparency < 1 do
            safe = steamPunkLast(instance)
            thePart.CFrame = CFrame.new(safe)
            wait()
          end
          forceObjectiveExists = false
        elseif instance.Name == "thirdBossSpreadLine" then -- volcanic 3
          instance:WaitForChild("precast")
          local s = instance.precast:Clone()
          s.Parent = workspace
          s.Transparency = 1
          s.Size = instance.precast.Size + Vector3.new(2,0,0)
          s.Name = "enemyRadius"
          wait(1.4)
          s:Destroy()
          instance.precast.Name = "precast"
        elseif instance.Name == "firstBossLaserPrecast" then -- ocean 1
          instance:WaitForChild("precast")
          wait(.5)
          if instance:FindFirstChild("precast") then
            local s = instance.precast:Clone()
            s.Parent = workspace
            s.Transparency = 1
            s.Size = instance.precast.Size
            s.Name = "enemyRadius"
            wait(1)
            s:Destroy()
          end
        elseif instance.Name == "secondBossSlamHitbox" then -- ocean 2
          local a = instance:WaitForChild("precast")
          local sum = 0
          sum = sum + a.Size.X + a.Size.Z + a.Size.Y
          warn(sum)
          if sum == 46.431163787842 then
            forceObjectiveExists = true
            thePart.CFrame = CFrame.new(-2653.086, 196.526, 2325.825)
            wait(5)
            forceObjectiveExists = false
          end
        elseif instance.Name == "preCast" then -- winter mob
          instance:WaitForChild("preCast")
          instance.preCast.Size = instance.preCast.Size + Vector3.new(0,0,3)
        elseif instance.Name == "riflemanShot" then -- pirate mob
          instance:WaitForChild("hitBox")
          instance.hitBox.Size = instance.hitBox.Size + Vector3.new(0,0,3)
        elseif instance.Name == "firstBossGatlingGunShot" then -- orbital 1
          instance:WaitForChild("precast")
          instance.precast.Size = instance.precast.Size + Vector3.new(1,0,0)
        elseif instance.Name == "firstBossFlameShot" then -- orbital 1
          instance:WaitForChild("precast")
          instance.precast.Size = instance.precast.Size + Vector3.new(1,0,0)
        elseif instance.Name == "chickenMage" then -- egg event
          instance:WaitForChild("precast")
          instance.precast.Size = instance.precast.Size + Vector3.new(0,0,3)
        elseif instance.Name == "droneShot" then -- orbital mob
          instance:WaitForChild("shot")
          wait()
          for i,c in pairs(instance:GetChildren()) do
            if c.Name == "shot" then
              c.precast.Size = c.precast.Size + Vector3.new(1.2,0,0)
            end
          end

        elseif instance.Name == "poisonBomb" then -- egg event
          instance:WaitForChild("eggPart")
          instance:WaitForChild("fuse")
          instance:WaitForChild("PrimaryPart")
          instance:WaitForChild("Union")
          instance.eggPart.Name = "enemyRadius"
          instance.fuse.Name = "enemyRadius"
          instance.PrimaryPart.Name = "enemyRadius"
          instance.Union.Name = "enemyRadius"
        elseif instance.Name == "rangeMobShot" then -- egg event
          instance:WaitForChild("precast")
          instance.precast.Size = instance.precast.Size + Vector3.new(1.5,0,3)
        elseif instance.Name == "chickenMage" then -- egg event
          instance:WaitForChild("precast")
          instance.precast.Size = instance.precast.Size + Vector3.new(0,0,3)
        elseif instance.Name == "npcMageShot" then -- kings castle mob
          instance:WaitForChild("precast")
          instance.precast.Size = instance.precast.Size + Vector3.new(0,0,3)
        elseif instance.Name == "iceBeamIndicator" then -- winter boss
          instance:WaitForChild("Part")
          instance.Part.Size = instance.Part.Size + Vector3.new(0,3,3)
        elseif instance.Name == "hitIndicatorIceAOE" then -- winter boss
          instance:WaitForChild("Part")
          instance.Part.Transparency = 0
        elseif instance.Name == "thirdBossLifeStealBeams" then -- orbital 3
          local thePart = createPart(enemy.PrimaryPart.CFrame * CFrame.new(0,0,-75), Vector3.new(40,40,150), "enemyRadius", "Block")
          wait(1.5)
          thePart:Destroy()
        elseif instance.Name == "silkBlast" then -- pirate 2
          local s = instance:WaitForChild("precast"):Clone()
          s.Size = instance.precast.Size + Vector3.new(3,5,3)
          s.Name = "enemyRadius"
          s.Transparency = 0
          s.Parent = workspace
          wait(5.5)
          s:Destroy()
        elseif instance.Name == "thirdBossSafeSpot" then -- volcanic 3
          objectiveExists = true
          while not instance:FindFirstChild("precast") do
            wait()
          end
          objectiveObject = instance
          while workspace:FindFirstChild(objectiveObject.Name) and workspace:FindFirstChild(objectiveObject.Name):FindFirstChild("precast") and workspace:FindFirstChild(objectiveObject.Name).precast.Transparency > 0 do
            wait()
          end
          objectiveObject = nil
          objectiveExists = false

        elseif instance.Name == "safeSpotCircle" then -- canals 2?
          objectiveExists = true
          objectiveObject = instance
          while instance ~= nil and workspace:FindFirstChild(instance.Name) and workspace:FindFirstChild(instance.Name).Transparency > 0 do
            wait()
          end
          objectiveObject = nil
          objectiveExists = false

        elseif instance.Name == "forceField" then -- canals 3
          childAddedT.forceFieldCounter = childAddedT.forceFieldCounter + 1
          objectiveExists = true
          objectiveObject = instance
          if childAddedT.forceFieldCounter == 2 then
            childAddedT.forceFieldCounter = 0
            objectiveExists = false
            objectiveObject = nil
          end
        elseif instance.ClassName == "Model" then -- if a mob spawns in workspace
          if instance.Name == "Kraken Tentacle" then return end -- has no enemy style
          instance:WaitForChild("HumanoidRootPart", 10)
          if instance ~= nil and instance:FindFirstChild("HumanoidRootPart") and instance ~= game.Players.LocalPlayer.Character then
            if instance.Name == "Azrallik's Heart" or instance.Name == "Dragon Orb" then
              cs:AddTag(instance, "Prio-Enemy")
            elseif instance.Name == "Blood Minion" or instance.Name == "Infected Pirate" or instance.Name == "Ice Minion" or instance.Name == "Tracking Minion" or instance.Name == "Stone Minion" or instance.Name == "Flame Minion" then -- insta kill
              instance:WaitForChild("Humanoid")
              addHitBox(instance, 5, "square")
              instance.Humanoid.Health = 0
              wait(3)
              instance:Destroy()
            else
              local isPlayer = false
              for i,v in pairs(game.Players:GetChildren()) do
                if instance.name == v.Name then
                  isPlayer = true
                end
              end
              if not isPlayer then
                cs:AddTag(instance, "Enemy")
                addHitBox(instance, 7)
              end
            end
          end
        end
      end)
    Game:GetService("LogService").MessageOut:Connect(function(Message)
        --[[=table.foreach(strings, function(i,v)
          if Message == v then
              game:GetService('TeleportService'):Teleport(2414851778)
          end
      end)]]
        if string.find(Message,"Server Kick Message:") then
          game:GetService('TeleportService'):Teleport(2414851778)
        end
      end)
    spawn(del_armor_ui)

    path.Blocked:Connect(onPathBlocked)
    local Players = game:GetService("Players")
    game.Players.LocalPlayer.Character.Humanoid.MoveToFinished:Connect(onWaypointReached)

    local function onCharacterAdded(character)
      local _, vchar, hum, root = getPlayer()
      hum.MoveToFinished:Connect(onWaypointReached)
      hum.WalkSpeed = walkspeed
      hum.AutoRotate = false
      spawn(del_armor_ui) 
    end

    game.Players.LocalPlayer.CharacterAdded:Connect(onCharacterAdded)

    function oceanFix()
      createWall(CFrame.new(-2530.18213, 217.300583, 2292.73022, 0.978144467, 0, 0.207926437, 0, 1, 0, -0.207926437, 0, 0.978144467), Vector3.new(19.569891, 131.600006, 27.9050236))
      createWall(CFrame.new(-783.23999, 69.9086685, 2350.23462, -1, 0, 0, 0, 1, 0, 0, 0, -1), Vector3.new(372.139984, 128.209991, 15.29)) 
      createWall(CFrame.new(-2038.21997, 198.318665, 2348.7041, 1, 0, 0, 0, 1, 0, 0, 0, 1), Vector3.new(50.9199371, 138.75, 9.52999496)) 
      createWall(CFrame.new(-2032.505, 198.318665, 2303.51416, 1, 0, 0, 0, 1, 0, 0, 0, 1), Vector3.new(39.4899368, 138.75, 9.52999496)) 
      createWall(CFrame.new(-1876.875, 54.728653, 2323.83374, 1, 0, 0, 0, 1, 0, 0, 0, 1), Vector3.new(3.30993915, 161.48999, 138.289993)) 
      createWall(CFrame.new(-1944.46509, 54.728653, 2256.06372, 0, 0, -1, 0, 1, 0, 1, 0, 0), Vector3.new(3.30993915, 161.48999, 138.289993)) 
      createWall(CFrame.new(-2013.51514, 54.728653, 2323.55371, -1, 0, 0, 0, 1, 0, 0, 0, -1), Vector3.new(3.30993915, 161.48999, 138.289993)) 
      createWall(CFrame.new(-1940.46277, 186.948654, 2392.69385, 0, 0, 1, 0, 1, 0, -1, 0, 0), Vector3.new(3.30993915, 161.48999, 149.454834)) 
      createWall(CFrame.new(-2018.40503, 198.318665, 2369.28418, 1, 0, 0, 0, 1, 0, 0, 0, 1), Vector3.new(11.2899389, 138.75, 50.3699913)) 
      createWall(CFrame.new(-2018.40503, 198.318665, 2276.61914, 1, 0, 0, 0, 1, 0, 0, 0, 1), Vector3.new(11.2899389, 138.75, 63.3199921)) 
      createWall(CFrame.new(-1936.995, 162.913666, 2251.38916, 0, 0, -1, 0, 1, 0, 1, 0, 0), Vector3.new(11.2899389, 67.9399948, 155.979996)) 
      createWall(CFrame.new(-1855.01501, 162.913666, 2254.21924, 0, 0, -1, 0, 1, 0, 1, 0, 0), Vector3.new(11.2899389, 67.9399948, 44.0399971)) 
      createWall(CFrame.new(-1835.495, 162.913666, 2321.28931, -1, 0, 0, 0, 1, 0, 0, 0, -1), Vector3.new(11.2899389, 67.9399948, 129.720001)) 
      createWall(CFrame.new(-1270.09351, 52.6868362, 2227.28467, -0.998307824, 0, 0.058156427, 0, 1, 0, -0.058156427, 0, -0.998307824), Vector3.new(2.08999944, 162.653656, 36.7399902)) 
      createWall(CFrame.new(-1277.76965, 52.6868362, 2242.85889, 0.0161704421, 0, 0.999869287, 0, 1, 0, -0.999869287, 0, 0.0161704421), Vector3.new(9.21999931, 162.653656, 26.4699898)) 
      createWall(CFrame.new(-1238.92224, 52.6868362, 2468.63843, -0.999989033, 0, 0.00474769808, 0, 1, 0, -0.00474769808, 0, -0.999989033), Vector3.new(9.21999931, 162.653656, 107.419983)) 
      createWall(CFrame.new(-1241.41284, 52.6868362, 2419.99854, 0.0148379207, 0, 0.999890029, 0, 1, 0, -0.999890029, 0, 0.0148379207), Vector3.new(10.3999996, 162.653656, 28.6099815)) 
      createWall(CFrame.new(-1261.41321, 52.6868362, 2393.58862, 0.891518176, 0, 0.452984959, 0, 1, 0, -0.452984959, 0, 0.891518176), Vector3.new(9.21999931, 162.653656, 65.5099792)) 
      createWall(CFrame.new(-1284.52197, 52.6868362, 2302.46655, 0.990956247, 0, 0.134185284, 0, 1, 0, -0.134185284, 0, 0.990956247), Vector3.new(9.21999931, 162.653656, 129.029984)) 
      createWall(CFrame.new(-1263.70508, 69.9086685, 2329.61914, 0, 0, -1, 0, 1, 0, 1, 0, 0), Vector3.new(46.2999954, 128.209991, 13.9499998)) 
      createWall(CFrame.new(-1265.06799, 52.6868362, 2238.36621, 0.993771136, 0, 0.111440428, 0, 1, 0, -0.111440428, 0, 0.993771136), Vector3.new(1.61999965, 162.653656, 139.828094)) 
      createWall(CFrame.new(-1227.82751, 52.6868362, 2201.66064, 0.993771136, 0, 0.111440428, 0, 1, 0, -0.111440428, 0, 0.993771136), Vector3.new(9.21999931, 162.653656, 212.23999)) 
      createWall(CFrame.new(-1292.28625, 52.6868362, 2105.9895, 0, 0, -1, 0, 1, 0, 1, 0, 0), Vector3.new(9.21999931, 162.653656, 141.559982)) 
      createWall(CFrame.new(-1364.03931, 52.6868362, 2176.00854, -1, 0, 0, 0, 1, 0, 0, 0, -1), Vector3.new(9.21999931, 162.653656, 141.559982)) 
      createWall(CFrame.new(-1348.71521, 52.6868362, 2243.71948, 0, 0, 1, 0, 1, -0, -1, 0, 0), Vector3.new(9.21999931, 162.653656, 29.5399895)) 
      createWall(CFrame.new(-1332.10864, 52.6868362, 2284.60376, 0.990956247, 0, 0.134185284, 0, 1, 0, -0.134185284, 0, 0.990956247), Vector3.new(9.21999931, 162.653656, 90.7599869)) 
      createWall(CFrame.new(-1331.63562, 52.6868362, 2374.04199, 0.991267025, -0, -0.131870151, 0, 1, -0, 0.131870151, 0, 0.991267025), Vector3.new(9.21999931, 162.653656, 92.5399857)) 
      createWall(CFrame.new(-1337.19312, 52.6868362, 2448.06567, 0.999832571, 0, 0.0182995033, 0, 1, 0, -0.0182995033, 0, 0.999832571), Vector3.new(9.21999931, 162.653656, 64.6399918)) 
      createWall(CFrame.new(-1397.48499, 65.1518402, 2454.98486, 0, 0, -1, 0, 1, 0, 1, 0, 0), Vector3.new(60.1099968, 137.723663, 7.00999975)) 
      createWall(CFrame.new(-1413.17004, 65.1518402, 2428.40991, 0, 0, -1, 0, 1, 0, 1, 0, 0), Vector3.new(6.95999908, 137.723663, 38.3799973)) 
      createWall(CFrame.new(-1482.84009, 65.1518402, 2428.40991, 0, 0, -1, 0, 1, 0, 1, 0, 0), Vector3.new(6.95999908, 137.723663, 21.1599998)) 
      createWall(CFrame.new(-1491.44507, 65.1518402, 2475.6748, 0, 0, -1, 0, 1, 0, 1, 0, 0), Vector3.new(101.489998, 137.723663, 3.94999886)) 
      createWall(CFrame.new(-1443.73999, 65.1518402, 2525.38989, 0, 0, -1, 0, 1, 0, 1, 0, 0), Vector3.new(9.71999931, 137.723663, 99.5199966)) 
      createWall(CFrame.new(-1831.43005, 101.343674, 2414.46924, -1, 0, 0, 0, 1, 0, 0, 0, -1), Vector3.new(10.3799305, 191.080002, 57.9199944)) 
      createWall(CFrame.new(-1360.9574, 52.6868362, 2520.39917, 0.0592788458, -0, -0.998241484, 0, 1, -0, 0.998241484, 0, 0.0592788458), Vector3.new(9.71999931, 162.653656, 86.7799988)) 
      createWall(CFrame.new(-1364.93335, 52.6868362, 2477.90015, 0.0592788458, -0, -0.998241484, 0, 1, -0, 0.998241484, 0, 0.0592788458), Vector3.new(9.21999931, 162.653656, 64.6399918)) 
      createWall(CFrame.new(-1280.71997, 52.6868362, 2518.2002, 0, 0, -1, 0, 1, 0, 1, 0, 0), Vector3.new(9.71999931, 162.653656, 86.7799988)) 
      createWall(CFrame.new(-1835.495, 101.343674, 2365.10938, -1, 0, 0, 0, 1, 0, 0, 0, -1), Vector3.new(11.2899389, 191.080002, 42.0799942)) 
      createWall(CFrame.new(-1853.7251, 101.343674, 2437.48438, -1, 0, 0, 0, 1, 0, 0, 0, -1), Vector3.new(54.9699287, 191.080002, 11.8899946)) 
      createWall(CFrame.new(-1467.53931, 65.1518402, 2402.24146, 0.979213893, -0, -0.202830359, 0, 1, -0, 0.202830359, 0, 0.979213893), Vector3.new(6.95999908, 137.723663, 60.1899948)) 
      createWall(CFrame.new(-1858.97498, 62.0486679, 2350.79932, -1, 0, 0, 0, 1, 0, 0, 0, -1), Vector3.new(38.1499329, 112.48999, 13.4599934)) 
      createWall(CFrame.new(-1853.11987, 101.343674, 2213.18994, 0, 0, -1, 0, 1, 0, 1, 0, 0), Vector3.new(10.3799305, 191.080002, 57.9199944)) 
      createWall(CFrame.new(-2055.80542, 101.343674, 2279.81958, 0, 0, 1, 0, 1, -0, -1, 0, 0), Vector3.new(35.4999313, 191.080002, 11.8899946)) 
      createWall(CFrame.new(-2058.75537, 101.343674, 2238.39453, 0, 0, 1, 0, 1, -0, -1, 0, 0), Vector3.new(54.9699287, 191.080002, 11.8899946)) 
      createWall(CFrame.new(-2031.19507, 101.343674, 2212.02441, -1, 0, 0, 0, 1, 0, 0, 0, -1), Vector3.new(48.0899277, 191.080002, 11.8899946)) 
      createWall(CFrame.new(-1830.10474, 101.343674, 2253.21997, 0, 0, -1, 0, 1, 0, 1, 0, 0), Vector3.new(90.4399261, 191.080002, 11.8899946)) 
      createWall(CFrame.new(-1944.03992, 101.343674, 2216.88501, -1, 0, 0, 0, 1, 0, 0, 0, -1), Vector3.new(126.819931, 191.080002, 11.8899946)) 
      createWall(CFrame.new(-2034.54504, 101.343674, 2439.59448, -1, 0, 0, 0, 1, 0, 0, 0, -1), Vector3.new(54.9699287, 191.080002, 11.8899946)) 
      createWall(CFrame.new(-2056.00513, 101.343674, 2367.26953, 0, 0, -1, 0, 1, 0, 1, 0, 0), Vector3.new(42.0799294, 191.080002, 11.8899946)) 
      createWall(CFrame.new(-2060.91504, 101.343674, 2409.96436, 0, 0, -1, 0, 1, 0, 1, 0, 0), Vector3.new(48.0899277, 191.080002, 11.8899946)) 
      createWall(CFrame.new(-2530.13501, 217.300583, 2359.55347, -0.978144407, 0, 0.207926437, 0, 1, 0, -0.207926437, 0, -0.978144407), Vector3.new(19.569891, 131.600006, 28.2675056)) 
      createWall(CFrame.new(-2814.97021, 217.300583, 2295.89038, -0.978144407, 0, 0.207926437, 0, 1, 0, -0.207926437, 0, -0.978144407), Vector3.new(19.569891, 131.600006, 34.3708916)) 
      createWall(CFrame.new(-2538.92798, 217.300583, 2385.58179, -0.913549781, 0, 0.406727046, 0, 1, 0, -0.406727046, 0, -0.913549781), Vector3.new(19.569891, 131.600006, 34.3708916)) 
      createWall(CFrame.new(-2805.54321, 217.300583, 2266.87744, -0.913549781, 0, 0.406727046, 0, 1, 0, -0.406727046, 0, -0.913549781), Vector3.new(19.569891, 131.600006, 34.3708916)) 
      createWall(CFrame.new(-2554.1814, 217.300583, 2412.00098, -0.808997631, 0, 0.587812185, 0, 1, 0, -0.587812185, 0, -0.808997631), Vector3.new(19.569891, 131.600006, 34.3708916)) 
      createWall(CFrame.new(-2790.29028, 217.300583, 2240.4585, -0.808997631, 0, 0.587812185, 0, 1, 0, -0.587812185, 0, -0.808997631), Vector3.new(19.569891, 131.600006, 34.3708916)) 
      createWall(CFrame.new(-2574.59448, 217.300583, 2434.67188, -0.66911006, 0, 0.743163466, 0, 1, 0, -0.743163466, 0, -0.66911006), Vector3.new(19.569891, 131.600006, 34.3708916)) 
      createWall(CFrame.new(-2769.87793, 217.300583, 2217.78784, -0.66911006, 0, 0.743163466, 0, 1, 0, -0.743163466, 0, -0.66911006), Vector3.new(19.569891, 131.600006, 34.3708916)) 
      createWall(CFrame.new(-2599.27612, 217.300583, 2452.60132, -0.499959469, 0, 0.866048813, 0, 1, 0, -0.866048813, 0, -0.499959469), Vector3.new(19.569891, 131.600006, 34.3708916)) 
      createWall(CFrame.new(-2745.19702, 217.300583, 2199.85962, -0.499959469, 0, 0.866048813, 0, 1, 0, -0.866048813, 0, -0.499959469), Vector3.new(19.569891, 131.600006, 34.3708916)) 
      createWall(CFrame.new(-2717.32861, 217.300583, 2187.45264, -0.309060812, 0, 0.951042235, 0, 1, 0, -0.951042235, 0, -0.309060812), Vector3.new(19.569891, 131.600006, 34.3708916)) 
      createWall(CFrame.new(-2627.14502, 217.300583, 2465.00854, -0.309060812, 0, 0.951042235, 0, 1, 0, -0.951042235, 0, -0.309060812), Vector3.new(19.569891, 131.600006, 34.3708916)) 
      createWall(CFrame.new(-2687.49023, 217.300583, 2181.1106, -0.104543328, 0, 0.994520426, 0, 1, 0, -0.994520426, 0, -0.104543328), Vector3.new(19.569891, 131.600006, 34.3708916)) 
      createWall(CFrame.new(-2656.98462, 217.300583, 2471.35083, -0.104543328, 0, 0.994520426, 0, 1, 0, -0.994520426, 0, -0.104543328), Vector3.new(19.569891, 131.600006, 34.3708916)) 
      createWall(CFrame.new(-2687.48999, 217.300583, 2471.35059, 0.10454309, 0, 0.994520426, 0, 1, 0, -0.994520426, 0, 0.10454309), Vector3.new(19.569891, 131.600006, 34.3708916)) 
      createWall(CFrame.new(-2656.98462, 217.300583, 2181.11084, 0.10454309, 0, 0.994520426, 0, 1, 0, -0.994520426, 0, 0.10454309), Vector3.new(19.569891, 131.600006, 34.3708916)) 
      createWall(CFrame.new(-2717.32886, 217.300583, 2465.00806, 0.309060872, 0, 0.951042235, 0, 1, 0, -0.951042235, 0, 0.309060872), Vector3.new(19.569891, 131.600006, 34.3708916)) 
      createWall(CFrame.new(-2627.146, 217.300583, 2187.45313, 0.309060872, 0, 0.951042235, 0, 1, 0, -0.951042235, 0, 0.309060872), Vector3.new(19.569891, 131.600006, 34.3708916)) 
      createWall(CFrame.new(-2745.19629, 217.300583, 2452.59839, 0.499959469, 0, 0.866048813, 0, 1, 0, -0.866048813, 0, 0.499959469), Vector3.new(19.569891, 131.600006, 34.3708916)) 
      createWall(CFrame.new(-2599.27905, 217.300583, 2199.8623, 0.499959469, 0, 0.866048813, 0, 1, 0, -0.866048813, 0, 0.499959469), Vector3.new(19.569891, 131.600006, 34.3708916)) 
      createWall(CFrame.new(-2769.875, 217.300583, 2434.66724, 0.669109941, 0, 0.743163466, 0, 1, 0, -0.743163466, 0, 0.669109941), Vector3.new(19.569891, 131.600006, 34.3708916)) 
      createWall(CFrame.new(-2574.60059, 217.300583, 2217.79272, 0.669109941, 0, 0.743163466, 0, 1, 0, -0.743163466, 0, 0.669109941), Vector3.new(19.569891, 131.600006, 34.3708916)) 
      createWall(CFrame.new(-2554.18921, 217.300583, 2240.4624, 0.808997452, 0, 0.587812185, 0, 1, 0, -0.587812185, 0, 0.808997452), Vector3.new(19.569891, 131.600006, 34.3708916)) 
      createWall(CFrame.new(-2790.28687, 217.300583, 2411.99756, 0.808997452, 0, 0.587812185, 0, 1, 0, -0.587812185, 0, 0.808997452), Vector3.new(19.569891, 131.600006, 34.3708916)) 
      createWall(CFrame.new(-2538.93652, 217.300583, 2266.88037, 0.913549721, 0, 0.406727046, 0, 1, 0, -0.406727046, 0, 0.913549721), Vector3.new(19.569891, 131.600006, 34.3708916)) 
      createWall(CFrame.new(-2805.53906, 217.300583, 2385.57935, 0.913549721, 0, 0.406727046, 0, 1, 0, -0.406727046, 0, 0.913549721), Vector3.new(19.569891, 131.600006, 34.3708916)) 
      createWall(CFrame.new(-2814.96558, 217.300583, 2356.56763, 0.978144467, 0, 0.207926437, 0, 1, 0, -0.207926437, 0, 0.978144467), Vector3.new(19.569891, 131.600006, 34.3708916)) 
      createWall(CFrame.new(-1465.67212, 65.1518402, 2326.36108, 0.418038607, 0, 0.908429265, 0, 1, 0, -0.908429265, 0, 0.418038607), Vector3.new(6.95999908, 137.723663, 119.360001)) 
      createWall(CFrame.new(-1945.50989, 101.343674, 2432.42505, -1, 0, 0, 0, 1, 0, 0, 0, -1), Vector3.new(128.319931, 191.080002, 11.8899946)) 
      createWall(CFrame.new(-2297.98022, 144.288208, 2350.95459, -1, 0, 0, 0, 1, 0, 0, 0, -1), Vector3.new(476.47998, 282.413544, 13.9443436)) 
      createWall(CFrame.new(-2818.1543, 217.300583, 2326.22998, 1, 0, 0, 0, 1, 0, 0, 0, 1), Vector3.new(19.569891, 131.600006, 34.3708916)) 
      createWall(CFrame.new(-1131.17993, 69.9086685, 2381.5293, -1, 0, 0, 0, 1, 0, 0, 0, -1), Vector3.new(20.5199738, 128.209991, 74.9199982)) 
      createWall(CFrame.new(-1420.72083, 65.1518402, 2388.11353, 0.979213893, -0, -0.202830359, 0, 1, -0, 0.202830359, 0, 0.979213893), Vector3.new(6.95999908, 137.723663, 81.0299988)) 
      createWall(CFrame.new(-961.265015, 69.9086685, 2380.78955, -1, 0, 0, 0, 1, 0, 0, 0, -1), Vector3.new(16.0899849, 128.209991, 76.3999939)) 
      createWall(CFrame.new(-1189.79504, 69.9086685, 2350.74414, -1, 0, 0, 0, 1, 0, 0, 0, -1), Vector3.new(137.75, 128.209991, 13.9499998)) 
      createWall(CFrame.new(-1169.94495, 69.9086685, 2300.8855, 1, 0, 0, 0, 1, 0, 0, 0, 1), Vector3.new(98.0499878, 128.209991, 13.9499998)) 
      createWall(CFrame.new(-1680.02002, 101.343666, 2350.79932, -1, 0, 0, 0, 1, 0, 0, 0, -1), Vector3.new(322.239929, 191.079987, 13.4599934)) 
      createWall(CFrame.new(-1676.88501, 101.343666, 2301.47925, -1, 0, 0, 0, 1, 0, 0, 0, -1), Vector3.new(328.509979, 191.079987, 13.4599934)) 
      createWall(CFrame.new(-783.23999, 69.9086685, 2301.69507, 1, 0, 0, 0, 1, 0, 0, 0, 1), Vector3.new(372.139984, 128.209991, 15.29)) 
      createWall(CFrame.new(-961.265015, 69.9086685, 2271.14014, 1, 0, 0, 0, 1, 0, 0, 0, 1), Vector3.new(16.0899849, 128.209991, 76.3999939)) 
      createWall(CFrame.new(-1489.99719, 65.1518402, 2361.78638, 0.418038607, 0, 0.908429265, 0, 1, 0, -0.908429265, 0, 0.418038607), Vector3.new(6.95999908, 137.723663, 67.8799973)) 
      createWall(CFrame.new(-1131.17993, 69.9086685, 2270.40039, 1, 0, 0, 0, 1, 0, 0, 0, 1), Vector3.new(20.5199738, 128.209991, 74.9199982)) 
      createWall(CFrame.new(-1047.32996, 69.9086685, 2241.58521, 1, 0, 0, 0, 1, 0, 0, 0, 1), Vector3.new(188.219971, 128.209991, 17.2899971)) 
      createWall(CFrame.new(-2294.77515, 144.288223, 2300.9751, 1, 0, 0, 0, 1, 0, 0, 0, 1), Vector3.new(489.929993, 282.413544, 13.9443436)) 
      createWall(CFrame.new(-1047.32996, 69.9086685, 2410.34448, -1, 0, 0, 0, 1, 0, 0, 0, -1), Vector3.new(188.219971, 128.209991, 17.2899971)) 
      createWall(CFrame.new(-2055.80542, 63.3636742, 2325.40967, 0, 0, 1, 0, 1, -0, -1, 0, 0), Vector3.new(126.679932, 115.119995, 11.8899946)) 
      createWall(CFrame.new(-605.989746, 69.9086685, 2325.82007, -1, 0, 0, 0, 1, 0, 0, 0, -1), Vector3.new(17.639555, 128.209991, 64.1190643)) 
      createWall(CFrame.new(-908.832153, 19.1552086, 2328.98291, -1, 0, 0, 0, 1, 0, 0, 0, -1), Vector3.new(623.32428, 26.7030716, 180.023346)) 
      createWall(CFrame.new(-1240.33691, 19.1552086, 2326.72632, -1, 0, 0, 0, 1, 0, 0, 0, -1), Vector3.new(44.9513016, 26.7030716, 38.2773705)) 
      createWall(CFrame.new(-1246.12073, 2.28969336, 2217.56665, -0.994147718, -0.0294061154, -0.103950247, 0.00436780788, 0.950511336, -0.310659111, 0.107941173, -0.309295058, -0.944820225), Vector3.new(43.4626274, 0.818213403, 196.637329)) 
      createWall(CFrame.new(-1283.27283, -26.5007706, 2155.53857, -0.785861552, -0.612678826, -0.0839429274, -0.561007082, 0.763435185, -0.320059299, 0.260178566, -0.204429671, -0.943671346), Vector3.new(22.6772556, 2.00851345, 39.9963722)) 
      createWall(CFrame.new(-1277.3429, -23.8319092, 2181.02539, -0.785853446, -0.528600097, 0.320961922, -0.561008096, 0.390993059, -0.729653716, 0.260201216, -0.75346303, -0.603811979), Vector3.new(24.3937035, 18.8500004, 1.07342899)) 
      createWall(CFrame.new(-1279.44299, -28.572773, 2173.7793, -1.00000024, 0, 0, 0, 1, -5.96046448e-08, 0, 5.96046448e-08, -1), Vector3.new(171.743622, 4.61810207, 136.415924)) 
      createWall(CFrame.new(-1312.07739, -23.9459343, 2329.72607, -0.99006927, 0.0131960101, -0.13996321, 0.0200383328, 0.998665988, -0.0475906916, 0.139148533, -0.0499224477, -0.98901242), Vector3.new(93.4838867, 4.94735384, 208.818771)) 
      createWall(CFrame.new(-1286.50586, -19.7647514, 2468.22461, -1.00000107, -2.79396772e-09, 0, 2.79396772e-09, 1.00000012, -2.38418579e-07, 0, 2.38418579e-07, -1.00000012), Vector3.new(93.4838867, 7.73166227, 87.2299957)) 
      createWall(CFrame.new(-1286.50586, -20.5263233, 2466.67285, -1.00000107, -2.79396772e-09, 0, 2.79396772e-09, 1.00000012, -2.38418579e-07, 0, 2.38418579e-07, -1.00000012), Vector3.new(93.4838867, 8.40604877, 90.3334351)) 
      createWall(CFrame.new(-1286.50586, -20.8730373, 2463.3562, -1.00000107, -2.79396772e-09, 0, 2.79396772e-09, 1.00000012, -2.38418579e-07, 0, 2.38418579e-07, -1.00000012), Vector3.new(93.4838867, 7.71262121, 96.9668121)) 
      createWall(CFrame.new(-1286.50586, -21.1191273, 2460.82324, -1.00000107, -2.79396772e-09, 0, 2.79396772e-09, 1.00000012, -2.38418579e-07, 0, 2.38418579e-07, -1.00000012), Vector3.new(93.4838867, 7.21999979, 102.032936)) 
      createWall(CFrame.new(-1357.41565, -10.7322168, 2529.74609, -0.974118412, 0.215022326, -0.0697357282, 0.21412079, 0.976597607, 0.0202486329, 0.0724577755, 0.00479363743, -0.99736017), Vector3.new(87.857872, 5.51671267, 107.359512)) 
      createWall(CFrame.new(-1349.19824, 38.4995384, 2479.56812, -0.974118412, 0.215022326, -0.0697357282, 0.21412079, 0.976597607, 0.0202486329, 0.0724577755, 0.00479363743, -0.99736017), Vector3.new(85.6598358, 104.72879, 6.42000008)) 
      createWall(CFrame.new(-1453.97693, 1.46386302, 2476.76196, -1.00000453, 9.7497832e-09, -1.49011612e-08, -9.7497832e-09, 1.00000048, -9.550713e-07, -1.49011612e-08, 9.550713e-07, -1.00000036), Vector3.new(109.169998, 0.424085021, 108.226189)) 
      createWall(CFrame.new(-1454.32715, 1.63537717, 2476.76196, -1.00000453, 9.7497832e-09, -1.49011612e-08, -9.7497832e-09, 1.00000048, -9.550713e-07, -1.49011612e-08, 9.550713e-07, -1.00000036), Vector3.new(108.46965, 0.767113209, 108.226189)) 
      createWall(CFrame.new(-1454.69763, 1.91353273, 2476.76196, -1.00000453, 9.7497832e-09, -1.49011612e-08, -9.7497832e-09, 1.00000048, -9.550713e-07, -1.49011612e-08, 9.550713e-07, -1.00000036), Vector3.new(107.728615, 1.32342398, 108.226189)) 
      createWall(CFrame.new(-1443.73267, 10.8826275, 2394.87671, -0.977953851, -0.0425007194, 0.204492941, 0.00425821915, 0.974818051, 0.222961426, -0.208821028, 0.218918473, -0.953138232), Vector3.new(36.4249535, 6.1712513, 130.547668)) 
      createWall(CFrame.new(-1427.18213, 70.4603043, 2405.68164, -0.977953851, -0.0425007194, 0.204492941, 0.00425821915, 0.974818051, 0.222961426, -0.208821028, 0.218918473, -0.953138232), Vector3.new(0.0500000007, 125.649826, 117.808311)) 
      createWall(CFrame.new(-1487.76672, 20.8402691, 2338.7666, -0.893995583, 0.14297086, 0.424654365, 0.145493388, 0.988999486, -0.0266750585, -0.423796773, 0.0379370227, -0.90496242), Vector3.new(88.661377, 9.92626381, 41.2240219)) 
      createWall(CFrame.new(-1700.78955, 29.0303326, 2325.34424, -1.00000012, 2.97213205e-08, 1.88447302e-08, -2.97213205e-08, 0.999999821, -1.86264515e-09, 1.88447302e-08, 1.86264515e-09, -0.999999881), Vector3.new(371.852844, 5.56997252, 53.5832138)) 
      createWall(CFrame.new(-1529.57568, 28.8269882, 2325.34424, -1.00000012, 2.97213205e-08, 1.88447302e-08, -2.97213205e-08, 0.999999821, -1.86264515e-09, 1.88447302e-08, 1.86264515e-09, -0.999999881), Vector3.new(31.7297535, 5.16327238, 53.5832138)) 
      createWall(CFrame.new(-1528.28796, 28.558382, 2325.34424, -1.00000012, 2.97213205e-08, 1.88447302e-08, -2.97213205e-08, 0.999999821, -1.86264515e-09, 1.88447302e-08, 1.86264515e-09, -0.999999881), Vector3.new(31.3896217, 4.62606096, 53.5832138)) 
      createWall(CFrame.new(-1527.79773, 28.3058643, 2325.34424, -1.00000012, 2.97213205e-08, 1.88447302e-08, -2.97213205e-08, 0.999999821, -1.86264515e-09, 1.88447302e-08, 1.86264515e-09, -0.999999881), Vector3.new(32.3699989, 4.12102604, 53.5832138)) 
      createWall(CFrame.new(-1527.37683, 28.102354, 2325.34424, -1.00000012, 2.97213205e-08, 1.88447302e-08, -2.97213205e-08, 0.999999821, -1.86264515e-09, 1.88447302e-08, 1.86264515e-09, -0.999999881), Vector3.new(33.211895, 3.71400523, 53.5832138)) 
      createWall(CFrame.new(-1526.84424, 27.9374313, 2325.34424, -1.00000012, 2.97213205e-08, 1.88447302e-08, -2.97213205e-08, 0.999999821, -1.86264515e-09, 1.88447302e-08, 1.86264515e-09, -0.999999881), Vector3.new(34.2771111, 3.38415861, 53.5832138)) 
      createWall(CFrame.new(-1855.52856, 37.2675323, 2286.03491, -1.00000024, -8.24050039e-06, 3.51449016e-05, 4.88978958e-06, 0.932308853, 0.36166212, -3.57189347e-05, 0.36166209, -0.932308912), Vector3.new(44.2060127, 6.02838516, 49.6322327)) 
      createWall(CFrame.new(-1858.3186, 46.4191093, 2232.7439, -1.00000048, 1.18888238e-07, 7.53789209e-08, -1.18888238e-07, 0.999999285, 0, 7.53789209e-08, 0, -0.999999404), Vector3.new(56.2976837, 5.61337185, 63.1329041)) 
      createWall(CFrame.new(-1938.64209, 59.3698273, 2253.55371, -0.975066185, 0.221918508, 1.4699873e-07, 0.221918583, 0.975063741, -3.34559616e-08, 1.50757813e-07, -8.96166618e-15, -0.999998748), Vector3.new(141.891571, 6.28999996, 63.1329041)) 
      createWall(CFrame.new(-2031.08984, 76.6613846, 2259.55518, -1.00000191, 4.61935997e-07, 3.01515627e-07, -4.61935997e-07, 0.999997079, 5.15942202e-14, 3.01515627e-07, -5.15942202e-14, -0.999997497), Vector3.new(48.2068825, 3.13832617, 97.6713715)) 
      createWall(CFrame.new(-2037.69958, 90.5315781, 2323.69995, -1.00000381, -4.73108639e-06, -5.01252653e-05, 4.97483006e-06, 0.975067258, -0.221883357, 5.15119791e-05, -0.221883178, -0.975068092), Vector3.new(48.2068825, 4.05999994, 133.019562)) 
      createWall(CFrame.new(-2035.52686, 103.249794, 2413.302, -1, 1.79664345e-14, 1.13686838e-13, -1.79664345e-14, 1, -8.8817842e-16, 1.13686838e-13, 8.8817842e-16, -1), Vector3.new(48.8988571, 8.13232899, 50.8320503)) 
      createWall(CFrame.new(-1952.27319, 116.819923, 2413.41699, -0.97507298, -0.221884459, 5.84738664e-05, -0.221884459, 0.97507298, 7.50656818e-06, -5.86818787e-05, -5.65499067e-06, -1), Vector3.new(144.940002, 7.03901482, 40.3282356)) 
      createWall(CFrame.new(-1857.91382, 134.10907, 2348.59229, -0.99999994, 3.59328656e-14, 2.27373662e-13, -3.5932869e-14, 1, -1.77635684e-15, 2.27373675e-13, 1.77635684e-15, -1), Vector3.new(56.4390755, 4.47680473, 177.607712)) 
      createWall(CFrame.new(-1873.65051, 136.331314, 2318.76172, -0.855346203, 0.518056273, 7.74251973e-13, 0.518056035, 0.85534656, -4.77246931e-13, 9.09494539e-13, 7.10542736e-15, -1), Vector3.new(6.69999218, 0.0500000007, 150.532593)) 
      createWall(CFrame.new(-1946.55249, 137.231415, 2319.61206, -0.999999166, 2.98023224e-08, 1.81898875e-12, -2.98023224e-08, 1, -1.42108547e-14, 1.81898875e-12, 1.42108547e-14, -1), Vector3.new(137.636246, 3.40450764, 150.532593)) 
      createWall(CFrame.new(-1945.93896, 137.022552, 2319.61206, -0.999999166, 2.98023224e-08, 1.81898875e-12, -2.98023224e-08, 1, -1.42108547e-14, 1.81898875e-12, 1.42108547e-14, -1), Vector3.new(138.863373, 2.98677969, 150.532593)) 
      createWall(CFrame.new(-2190.23413, 136.711761, 2325.40161, -0.999999166, 2.98023224e-08, 1.81898875e-12, -2.98023224e-08, 1, -1.42108547e-14, 1.81898875e-12, 1.42108547e-14, -1), Vector3.new(366.358093, 2.36521196, 39.7483025))
      createWall(CFrame.new(-2674.35205, 192.732971, 2320.76904, -1, 0, 0, 0, 1, 0, 0, 0, -1), Vector3.new(279.199799, 6.58692169, 290.013947)) 
      createWall(CFrame.new(-2672.68774, 192.732971, 2320.76904, -1, 0, 0, 0, 1, 0, 0, 0, -1), Vector3.new(282.528381, 6.58692169, 290.013947)) 
      createWall(CFrame.new(-2398.11328, 162.203232, 2325.17139, 0.970287263, 0.241955817, 0, -0.241955817, 0.970287263, 0, 0, 0, 1.00000012), Vector3.new(274.739532, 0.558954656, 51.0499992)) 
      local t = waitForExist(workspace, "borders")
      t:Destroy()
      if _G.destroy_map then
        workspace.Terrain:Clear()
        for i,v in pairs(workspace:GetChildren()) do
          if v.Name ~= "lastBossSafeZones" and v.Name ~="Terrain" and (v.ClassName == "Model" or v:IsA("BasePart")) and v ~= game.Players.LocalPlayer.Character and v.Name ~= regionPartName then
            v:Destroy()
          end
        end
      end
        while true do
          local s = game:GetService("Workspace").dungeon.room3.enemyFolder
          if #s:GetChildren() == 41 then
            forceObjectiveExists = true
            thePart.CFrame = CFrame.new(-1240.337, 7.648, 2246.159)
            while wait() do
              local _,_,_,root = getPlayer()
              if root then
                if root.Position.Y < 21 then break end
              end
            end
            forceObjectiveExists = false
            break
          end
          wait(1)
        end          
        while true do
          local s = game:GetService("Workspace").dungeon.room5.enemyFolder
          if #s:GetChildren() == 16 then
            forceObjectiveExists = true
            thePart.CFrame = CFrame.new(-1858.319, 46.419, 2232.744)
            while wait() do
              local _,_,_,root = getPlayer()
              if root then
                if root.Position.Y < 38 then break end
              end
            end
            forceObjectiveExists = false
            break
          end
          wait(1)
        end          
      --[[spawn(function()
          while true do
            local s = game:GetService("Workspace").dungeon.room6.enemyFolder
            if s:FindFirstChild("Ancient Temple Protector") then
              local g = s:FindFirstChild("Ancient Temple Protector")
              local ts = game:GetService("TweenService")
              g:WaitForChild("HumanoidRootPart")
              while g ~= nil and g.Parent ~= nil and g:FindFirstChild("Humanoid") and g.Humanoid.Health > 0 do
                local s = g.Humanoid:GetPlayingAnimationTracks()
                bossRange = 15
                for i,v in pairs(s) do
                  if v.Animation.AnimationId == "rbxassetid://6106580202" then
                    -- doing stupid ass attack
                    forceObjectiveExists = true
                    walkspeed = 32
                    thePart.CFrame = g.HumanoidRootPart.CFrame * CFrame.new(0,-(g.HumanoidRootPart.Size.Y*.4),10)
                    local _,_,_,root = getPlayer()
                    if root ~= nil then
                      dist = (thePart.Position-root.Position).magnitude
                      ts:Create(root,  TweenInfo.new(dist/30), {CFrame = g.HumanoidRootPart.CFrame * CFrame.new(0,-(g.HumanoidRootPart.Size.Y*.4),10)}):Play()
                      warn(dist/30)
                      break
                    end
                  else
                    walkspeed = 24
                    forceObjectiveExists = false
                  end
                end
                wait()
              end
              forceObjectiveExists = false
              bossRange = 15
              break
            end
            wait(1)
          end
        end)]]
    end
    function volcanicFix()
      createWall(CFrame.new(-1233.02295, 2.79844761, 705.183167, -0.999982297, -6.14493274e-08, -0.00593414903, -6.1298465e-08, 1, -2.56039989e-08, 0.00593414903, -2.52398049e-08, -0.999982297), Vector3.new(148.029877, 17.849968, 161.050003))
      createWall(CFrame.new(-1127.02625, -2.89132118, 699.554077, -0.981609523, 0.190805554, -0.00593414763, 0.190808892, 0.981627166, -2.57277861e-08, 0.0058251163, -0.00113231386, -0.999982119), Vector3.new(69.5298767, 18.849968, 35.0500031))
      createWall(CFrame.new(-793.540466, -8.58208942, 699.325134, -0.999981225, -4.8950298e-08, -0.00593414297, -5.41017471e-08, 0.999999881, -2.59606168e-08, 0.00593414484, -2.53785402e-08, -0.999981582), Vector3.new(606.529907, 18.849968, 38.5500031))
      createWall(CFrame.new(-417.026733, -7.0820694, 700.590942, -0.999981225, -4.8950298e-08, -0.00593414297, -5.41017471e-08, 0.999999881, -2.59606168e-08, 0.00593414484, -2.53785402e-08, -0.999981582), Vector3.new(157.529907, 18.849968, 158.550003))
      createWall(CFrame.new(-498.050507, 0.667925298, 696.821716, -0.999981225, -4.8950298e-08, -0.00593414297, -5.41017471e-08, 0.999999881, -2.59606168e-08, 0.00593414484, -2.53785402e-08, -0.999981582), Vector3.new(5.52990723, 2.34996796, 37.0500031))
      createWall(CFrame.new(-498.800507, 0.417925298, 696.826172, -0.999981225, -4.8950298e-08, -0.00593414297, -5.41017471e-08, 0.999999881, -2.59606168e-08, 0.00593414484, -2.53785402e-08, -0.999981582), Vector3.new(7.02990723, 1.84996796, 37.0500031))
      createWall(CFrame.new(135.459915, -8.58203983, 696.812256, -0.999981225, -4.8950298e-08, -0.00593414297, -5.41017471e-08, 0.999999881, -2.59606168e-08, 0.00593414484, -2.53785402e-08, -0.999981582), Vector3.new(280.529907, 18.849968, 44.5500031))
      createWall(CFrame.new(273.457336, -8.0820322, 695.993347, -0.999981225, -4.8950298e-08, -0.00593414297, -5.41017471e-08, 0.999999881, -2.59606168e-08, 0.00593414484, -2.53785402e-08, -0.999981582), Vector3.new(4.52990723, 19.849968, 44.5500031))
      createWall(CFrame.new(276.957275, -7.5820322, 695.972595, -0.999981225, -4.8950298e-08, -0.00593414297, -5.41017471e-08, 0.999999881, -2.59606168e-08, 0.00593414484, -2.53785402e-08, -0.999981582), Vector3.new(9.52990723, 20.849968, 44.5500031))
      createWall(CFrame.new(289.707031, -6.58203173, 695.896912, -0.999981225, -4.8950298e-08, -0.00593414297, -5.41017471e-08, 0.999999881, -2.59606168e-08, 0.00593414484, -2.53785402e-08, -0.999981582), Vector3.new(21.0299072, 22.849968, 44.5500031))
      createWall(CFrame.new(-12.0373135, -8.08204746, 697.687561, -0.999981225, -4.8950298e-08, -0.00593414297, -5.41017471e-08, 0.999999881, -2.59606168e-08, 0.00593414484, -2.53785402e-08, -0.999981582), Vector3.new(44.5299072, 19.849968, 44.5500031))
      createWall(CFrame.new(-14.5372658, -7.58204746, 697.702393, -0.999981225, -4.8950298e-08, -0.00593414297, -5.41017471e-08, 0.999999881, -2.59606168e-08, 0.00593414484, -2.53785402e-08, -0.999981582), Vector3.new(39.5299072, 20.849968, 44.5500031))
      createWall(CFrame.new(-16.5372276, -7.08204746, 697.714233, -0.999981225, -4.8950298e-08, -0.00593414297, -5.41017471e-08, 0.999999881, -2.59606168e-08, 0.00593414484, -2.53785402e-08, -0.999981582), Vector3.new(35.5299072, 21.849968, 44.5500031))
      createWall(CFrame.new(-19.0371799, -6.58204746, 697.729065, -0.999981225, -4.8950298e-08, -0.00593414297, -5.41017471e-08, 0.999999881, -2.59606168e-08, 0.00593414484, -2.53785402e-08, -0.999981582), Vector3.new(30.5299072, 22.849968, 44.5500031))
      createWall(CFrame.new(-24.2870808, -6.08204794, 697.760193, -0.999981225, -4.8950298e-08, -0.00593414297, -5.41017471e-08, 0.999999881, -2.59606168e-08, 0.00593414484, -2.53785402e-08, -0.999981582), Vector3.new(20.0299072, 23.849968, 44.5500031))
      createWall(CFrame.new(-40.2867775, -5.83204842, 697.855164, -0.999981225, -4.8950298e-08, -0.00593414297, -5.41017471e-08, 0.999999881, -2.59606168e-08, 0.00593414484, -2.53785402e-08, -0.999981582), Vector3.new(39.0299072, 24.349968, 44.5500031))
      createWall(CFrame.new(-44.036705, -6.58204842, 697.877441, -0.999981225, -4.8950298e-08, -0.00593414297, -5.41017471e-08, 0.999999881, -2.59606168e-08, 0.00593414484, -2.53785402e-08, -0.999981582), Vector3.new(46.5299072, 22.849968, 44.5500031))
      createWall(CFrame.new(-48.0366287, -7.08204889, 697.901123, -0.999981225, -4.8950298e-08, -0.00593414297, -5.41017471e-08, 0.999999881, -2.59606168e-08, 0.00593414484, -2.53785402e-08, -0.999981582), Vector3.new(54.5299072, 21.849968, 44.5500031))
      createWall(CFrame.new(-65.2863083, -7.33204985, 698.003479, -0.999981225, -4.8950298e-08, -0.00593414297, -5.41017471e-08, 0.999999881, -2.59606168e-08, 0.00593414484, -2.53785402e-08, -0.999981582), Vector3.new(89.0299072, 21.349968, 44.5500031))
      createWall(CFrame.new(-80.536026, -7.58205032, 698.093994, -0.999981225, -4.8950298e-08, -0.00593414297, -5.41017471e-08, 0.999999881, -2.59606168e-08, 0.00593414484, -2.53785402e-08, -0.999981582), Vector3.new(119.529907, 20.849968, 44.5500031))
      createWall(CFrame.new(-88.5358734, -8.08205032, 698.141479, -0.999981225, -4.8950298e-08, -0.00593414297, -5.41017471e-08, 0.999999881, -2.59606168e-08, 0.00593414484, -2.53785402e-08, -0.999981582), Vector3.new(135.529907, 19.849968, 44.5500031))
      createWall(CFrame.new(-113.535408, -8.58205223, 698.289856, -0.999981225, -4.8950298e-08, -0.00593414297, -5.41017471e-08, 0.999999881, -2.59606168e-08, 0.00593414484, -2.53785402e-08, -0.999981582), Vector3.new(185.529907, 18.849968, 44.5500031))
      createWall(CFrame.new(-215.033478, -8.08205795, 698.89209, -0.999981225, -4.8950298e-08, -0.00593414297, -5.41017471e-08, 0.999999881, -2.59606168e-08, 0.00593414484, -2.53785402e-08, -0.999981582), Vector3.new(26.5299072, 19.849968, 44.5500031))
      createWall(CFrame.new(-243.282944, -7.83205986, 699.059753, -0.999981225, -4.8950298e-08, -0.00593414297, -5.41017471e-08, 0.999999881, -2.59606168e-08, 0.00593414484, -2.53785402e-08, -0.999981582), Vector3.new(32.0299072, 20.349968, 44.5500031))
      createWall(CFrame.new(-270.78241, -7.33206129, 699.222961, -0.999981225, -4.8950298e-08, -0.00593414297, -5.41017471e-08, 0.999999881, -2.59606168e-08, 0.00593414484, -2.53785402e-08, -0.999981582), Vector3.new(49.0299072, 21.349968, 44.5500031))
      createWall(CFrame.new(-309.781677, -7.0820632, 699.454407, -0.999981225, -4.8950298e-08, -0.00593414297, -5.41017471e-08, 0.999999881, -2.59606168e-08, 0.00593414484, -2.53785402e-08, -0.999981582), Vector3.new(53.0299072, 21.849968, 44.5500031))
      createWall(CFrame.new(-313.281616, -6.5820632, 699.475159, -0.999981225, -4.8950298e-08, -0.00593414297, -5.41017471e-08, 0.999999881, -2.59606168e-08, 0.00593414484, -2.53785402e-08, -0.999981582), Vector3.new(46.0299072, 22.849968, 44.5500031))
      createWall(CFrame.new(-314.781586, -6.3320632, 699.48407, -0.999981225, -4.8950298e-08, -0.00593414297, -5.41017471e-08, 0.999999881, -2.59606168e-08, 0.00593414484, -2.53785402e-08, -0.999981582), Vector3.new(43.0299072, 23.349968, 44.5500031))
      createWall(CFrame.new(-317.031555, -5.8320632, 699.497437, -0.999981225, -4.8950298e-08, -0.00593414297, -5.41017471e-08, 0.999999881, -2.59606168e-08, 0.00593414484, -2.53785402e-08, -0.999981582), Vector3.new(38.5299072, 24.349968, 44.5500031))
      createWall(CFrame.new(-319.531494, -5.5820632, 699.512268, -0.999981225, -4.8950298e-08, -0.00593414297, -5.41017471e-08, 0.999999881, -2.59606168e-08, 0.00593414484, -2.53785402e-08, -0.999981582), Vector3.new(33.5299072, 24.849968, 44.5500031))
      createWall(CFrame.new(-320.531464, -6.0820632, 699.518188, -0.999981225, -4.8950298e-08, -0.00593414297, -5.41017471e-08, 0.999999881, -2.59606168e-08, 0.00593414484, -2.53785402e-08, -0.999981582), Vector3.new(35.5299072, 23.849968, 44.5500031))
      createWall(CFrame.new(-323.031403, -6.5820632, 699.53302, -0.999981225, -4.8950298e-08, -0.00593414297, -5.41017471e-08, 0.999999881, -2.59606168e-08, 0.00593414484, -2.53785402e-08, -0.999981582), Vector3.new(40.5299072, 22.849968, 44.5500031))
      createWall(CFrame.new(-326.776886, -6.5820632, 700.305298, -0.999981225, -4.8950298e-08, -0.00593414297, -5.41017471e-08, 0.999999881, -2.59606168e-08, 0.00593414484, -2.53785402e-08, -0.999981582), Vector3.new(48.0299072, 22.849968, 76.0500031))
      createWall(CFrame.new(-330.281281, -7.0820632, 699.57605, -0.999981225, -4.8950298e-08, -0.00593414297, -5.41017471e-08, 0.999999881, -2.59606168e-08, 0.00593414484, -2.53785402e-08, -0.999981582), Vector3.new(55.0299072, 21.849968, 90.5500031))
      createWall(CFrame.new(-2341.5, 9.19974613, 695.25, 1, 0, 0, 0, 1, 0, 0, 0, 1), Vector3.new(197, 3, 194.5))
      createWall(CFrame.new(-2244.75, 10.1997461, 695.25, 1, 0, 0, 0, 1, 0, 0, 0, 1), Vector3.new(10.5, 1, 194.5))
      createWall(CFrame.new(-46.5366592, -6.33204842, 697.892273, -0.999981225, -4.8950298e-08, -0.00593414297, -5.41017471e-08, 0.999999881, -2.59606168e-08, 0.00593414484, -2.53785402e-08, -0.999981582), Vector3.new(34.5299072, 23.349968, 44.5500031))
      createWall(CFrame.new(278.207245, -7.0820322, 695.965149, -0.999981225, -4.8950298e-08, -0.00593414297, -5.41017471e-08, 0.999999881, -2.59606168e-08, 0.00593414484, -2.53785402e-08, -0.999981582), Vector3.new(7.02990723, 21.849968, 44.5500031))
      createWall(CFrame.new(-2093.75, 9.94974613, 696.75, 1, 0, 0, 0, 1, 0, 0, 0, 1), Vector3.new(692.5, 0.5, 37.5))
      createWall(CFrame.new(-1725.44324, 10.6997461, 694.778015, 0.694658399, 0, 0.719339788, 0, 1, 0, -0.719339788, 0, 0.694658399), Vector3.new(48, 2, 45))
      createWall(CFrame.new(-1339.51733, 4.49533796, 698.180054, 0.99026829, -0.13917312, 0, 0.13917312, 0.99026829, 0, 0, 0, 1), Vector3.new(67.5, 4, 37))
      createWall(CFrame.new(-1363.59412, 1.11156046, 708.326904, 0.820969999, -0.13917318, 0.553750992, 0.115379818, 0.990268767, 0.0778246224, -0.559193194, 0, 0.829037607), Vector3.new(34, 4, 49))
      createWall(CFrame.new(-1371.4259, -0.998918772, 723.160156, 0.930549145, -0.139173374, -0.338692099, 0.13078016, 0.990270197, -0.047600057, 0.34202072, -7.4505806e-09, 0.939693034), Vector3.new(38.5, 4, 48))
      createWall(CFrame.new(-1393.78589, -4.70867538, 741.874329, 0.525701582, -0.11796616, -0.842453718, 0.0624936409, 0.993020117, -0.100052938, 0.848372996, -4.99562702e-05, 0.529402494), Vector3.new(57, 4, 48))
      createWall(CFrame.new(-1426.87244, -9.64694118, 727.73645, -0.0525785685, -0.117965765, -0.991624653, -0.00619550375, 0.993017733, -0.117802992, 0.998597682, -5.02976873e-05, -0.0529423133), Vector3.new(43, 4, 49))
      createWall(CFrame.new(-1542.79834, -24.1414528, 693.151733, 0.151433259, -0.117894612, -0.981410801, 0.0179410838, 0.993028104, -0.116522513, 0.988308668, 3.75595118e-05, 0.152491033), Vector3.new(16.5, 4, 24.5))
      createWall(CFrame.new(-1525.43823, -22.3317413, 680.852295, 0.711567044, -0.117893316, -0.692656934, 0.0844521746, 0.993026376, -0.0822597519, 0.697524667, 3.69343543e-05, 0.716561079), Vector3.new(16.5, 3.5, 31))
      createWall(CFrame.new(-1512.83789, -21.387928, 669.898132, 0.0859401673, -0.117966108, -0.989292026, 0.010259347, 0.993018389, -0.117519177, 0.996249139, -4.99039452e-05, 0.086550802), Vector3.new(16.5, 3.5, 26))
      createWall(CFrame.new(-1502.39136, -20.650486, 668.989319, 0.0859401673, -0.117966108, -0.989292026, 0.010259347, 0.993018389, -0.117519177, 0.996249139, -4.99039452e-05, 0.086550802), Vector3.new(16.5, 3.5, 26))
      createWall(CFrame.new(-1481.26001, -18.1399117, 673.785461, -0.526738107, -0.117966197, -0.841804624, -0.0625315532, 0.993019879, -0.100029439, 0.847729981, -4.99358321e-05, -0.530434847), Vector3.new(16.5, 3.5, 26))
      createWall(CFrame.new(-1468.12195, -15.5714817, 686.85675, -0.526738107, -0.117966197, -0.841804624, -0.0625315532, 0.993019879, -0.100029439, 0.847729981, -4.99358321e-05, -0.530434847), Vector3.new(24.5, 3.5, 34.5))
      createWall(CFrame.new(-1726.15015, 10.4497461, 694.790344, 0.694658399, 0, 0.719339788, 0, 1, 0, -0.719339788, 0, 0.694658399), Vector3.new(49, 1.5, 46))
      createWall(CFrame.new(-1727.22302, 10.1997461, 694.101868, 0.694658399, 0, 0.719339788, 0, 1, 0, -0.719339788, 0, 0.694658399), Vector3.new(49.5, 1, 48.5))
      createWall(CFrame.new(-1594.52539, -24.3682365, 695.275208, 1, 0, 0, 0, 1, 0, 0, 0, 1), Vector3.new(88.5, 2.5, 96))
      createWall(CFrame.new(-1677.15637, -15.417098, 623.046021, 0.984657705, 0.0171872638, -0.173648149, -0.0174524058, 0.99984771, 0, 0.173621729, 0.00303057837, 0.98480767), Vector3.new(80.5, 8, 85.5))
      createWall(CFrame.new(-1450.97681, -13.2820768, 704.461609, -0.526738107, -0.117966197, -0.841804624, -0.0625315532, 0.993019879, -0.100029439, 0.847729981, -4.99358321e-05, -0.530434847), Vector3.new(36, 4, 32.5))
      createWall(CFrame.new(-1635.84265, -139.839996, 622.938721, 0.178292945, 0, 0.98397553, 0, 1, 0, -0.983975589, 0, 0.178293034), Vector3.new(14, 255, 4.35629797))
      createWall(CFrame.new(-1631.328, -140.839996, 623.947815, 0.2464917, 0, 0.969143093, 0, 1, 0, -0.969143093, 0, 0.24649176), Vector3.new(14, 255, 5.8792901))
      createWall(CFrame.new(-1608.31348, -147.839996, 639.822876, 0.866703033, 0, 0.498820961, 0, 1, 0, -0.498820961, 0, 0.866703033), Vector3.new(14, 255, 5.13447332))
      createWall(CFrame.new(-1606.00684, -148.839996, 644.197998, 0.899387717, 0, 0.437147677, 0, 1, 0, -0.437147677, 0, 0.899387717), Vector3.new(14, 255, 5.74125433))
      createWall(CFrame.new(-1626.75098, -141.839996, 625.260925, 0.313491344, 0, 0.949589133, 0, 1, 0, -0.949589133, 0, 0.313491404), Vector3.new(14, 255, 4.62769413))
      createWall(CFrame.new(-1623.35046, -142.839996, 626.612061, 0.426887631, 0, 0.904302716, 0, 1, 0, -0.904302716, 0, 0.426887691), Vector3.new(14, 255, 4.41635466))
      createWall(CFrame.new(-1610.32239, -146.839996, 636.802979, 0.78356123, 0, 0.621311903, 0, 1, 0, -0.621311784, 0, 0.783561289), Vector3.new(14, 255, 4.21742392))
      createWall(CFrame.new(-1619.98938, -143.839996, 628.473572, 0.532674611, 0, 0.846318007, 0, 1, 0, -0.846318007, 0, 0.53267467), Vector3.new(14, 255, 4.97442102))
      createWall(CFrame.new(-1616.38782, -144.839996, 630.914368, 0.590408921, 0, 0.807102084, 0, 1, 0, -0.807102084, 0, 0.59040904), Vector3.new(14, 255, 4.71004725))
      createWall(CFrame.new(-1613.16479, -145.839996, 633.713562, 0.701997042, 0, 0.712177455, 0, 1, 0, -0.712177455, 0, 0.701997101), Vector3.new(14, 255, 5.9066267))
      createWall(CFrame.new(-1604.04761, -149.839996, 648.575867, 0.927696943, 0, 0.373347104, 0, 1, 0, -0.373347104, 0, 0.927697003), Vector3.new(14, 255, 4.8348875))
      createWall(CFrame.new(-1712.18823, -137.559921, 611.531189, -0.0305747688, -3.8556589e-08, 0.999530673, -1.6698479e-07, 1, 3.34666268e-08, -0.999530613, -1.6588379e-07, -0.030574739), Vector3.new(14, 255, 5.74125433))
      createWall(CFrame.new(-1717.12427, -136.559921, 611.844177, -0.100224018, -3.8556589e-08, 0.994963169, -1.6891255e-07, 1, 2.17368452e-08, -0.994963109, -1.6588379e-07, -0.100223958), Vector3.new(14, 255, 5.13447332))
      createWall(CFrame.new(-1720.7019, -135.559921, 612.44043, -0.246018708, -3.8556589e-08, 0.969263375, -1.7027071e-07, 1, -3.43903395e-09, -0.969263315, -1.6588379e-07, -0.246018708), Vector3.new(14, 255, 4.21742392))
      createWall(CFrame.new(-1724.68433, -134.559921, 613.768799, -0.362314641, -3.8556589e-08, 0.932054043, -1.68582289e-07, 1, -2.41653098e-08, -0.932054043, -1.6588379e-07, -0.362314641), Vector3.new(14, 255, 5.9066267))
      createWall(CFrame.new(-1728.55774, -133.559921, 615.56311, -0.494606912, -3.8556589e-08, 0.869114876, -1.63242419e-07, 1, -4.85371636e-08, -0.869114757, -1.6588379e-07, -0.494606853), Vector3.new(14, 255, 4.71004725))
      createWall(CFrame.new(-1732.25928, -132.559921, 617.849548, -0.554024041, -3.8556589e-08, 0.83249861, -1.5945929e-07, 1, -5.9805302e-08, -0.83249855, -1.6588379e-07, -0.554023981), Vector3.new(14, 255, 4.97442102))
      createWall(CFrame.new(-1735.33374, -131.559921, 620.153809, -0.650239468, -3.8556589e-08, 0.759727001, -1.5109741e-07, 1, -7.8571702e-08, -0.759726942, -1.6588379e-07, -0.650239348), Vector3.new(14, 255, 4.41635466))
      createWall(CFrame.new(-1737.95874, -130.559921, 622.703003, -0.737985492, -3.8556589e-08, 0.674813986, -1.40394903e-07, 1, -9.64013083e-08, -0.674813926, -1.6588379e-07, -0.737985432), Vector3.new(14, 255, 4.62769413))
      createWall(CFrame.new(-1741.03076, -129.559921, 626.341125, -0.783257902, -3.8556589e-08, 0.621694207, -1.33328726e-07, 1, -1.0595938e-07, -0.621694148, -1.6588379e-07, -0.783257842), Vector3.new(14, 255, 5.8792901))
      createWall(CFrame.new(-1743.79993, -128.559921, 630.046875, -0.824713767, -3.8556589e-08, 0.565547168, -1.25613255e-07, 1, -1.15001065e-07, -0.565547168, -1.6588379e-07, -0.824713647), Vector3.new(14, 255, 4.35629797))
      createWall(CFrame.new(-1745.77539, -127.560036, 633.337646, -0.879498184, -8.67711378e-08, 0.475898564, -1.12849136e-07, 1, -2.62235904e-08, -0.475898594, -7.67686217e-08, -0.879498243), Vector3.new(14, 255, 4.99258232))
      createWall(CFrame.new(-1747.48596, -126.560036, 637.008545, -0.930946112, -8.67711378e-08, 0.365169674, -1.08812841e-07, 1, -3.97812556e-08, -0.365169674, -7.67686217e-08, -0.930946112), Vector3.new(14, 255, 4.8348875))
      createWall(CFrame.new(-1749.06567, -125.560036, 641.53717, -0.954145014, -8.67711378e-08, 0.299338609, -1.05772067e-07, 1, -4.72744333e-08, -0.299338609, -7.67686217e-08, -0.954145014), Vector3.new(14, 255, 5.74125433))
      createWall(CFrame.new(-1750.39087, -124.560036, 646.302246, -0.972701669, -8.67711378e-08, 0.2320517, -1.02216717e-07, 1, -5.45375691e-08, -0.2320517, -7.67686217e-08, -0.972701669), Vector3.new(14, 255, 5.13447332))
      createWall(CFrame.new(-1751.00244, -123.560036, 649.877319, -0.99630177, -8.67711378e-08, 0.0859023929, -9.30448607e-08, 1, -6.90308681e-08, -0.0859024227, -7.67686217e-08, -0.996301889), Vector3.new(14, 255, 4.21742392))
      createWall(CFrame.new(-1751.05554, -122.560036, 654.075134, -0.99934417, -8.67711378e-08, -0.0361632407, -8.39380334e-08, 1, -7.98561928e-08, 0.0361632407, -7.67686217e-08, -0.99934417), Vector3.new(14, 255, 5.9066267))
      createWall(CFrame.new(-1750.63257, -121.560036, 658.322998, -0.983336091, -8.67711378e-08, -0.181787133, -7.13696551e-08, 1, -9.12632245e-08, 0.181787133, -7.67686217e-08, -0.983336091), Vector3.new(14, 255, 4.71004725))
      createWall(CFrame.new(-1749.68848, -120.560036, 662.570007, -0.968261242, -8.67711378e-08, -0.249933213, -6.4830104e-08, 1, -9.60190647e-08, 0.249933243, -7.67686217e-08, -0.968261242), Vector3.new(14, 255, 4.97442102))
      createWall(CFrame.new(-1741.95715, -116.560036, 677.476013, -0.80499965, -8.67711378e-08, -0.59327215, -2.43060558e-08, 1, -1.13277608e-07, 0.59327215, -7.67686217e-08, -0.80499959), Vector3.new(14, 255, 4.35629797))
      createWall(CFrame.new(-1744.5481, -117.560036, 673.643494, -0.844420195, -8.67711378e-08, -0.535677969, -3.21480513e-08, 1, -1.11306363e-07, 0.535678029, -7.67686217e-08, -0.844420195), Vector3.new(14, 255, 5.8792901))
      createWall(CFrame.new(-1746.97571, -118.560036, 669.54718, -0.879728258, -8.67711378e-08, -0.475472927, -3.98336297e-08, 1, -1.08792854e-07, 0.475472957, -7.67686217e-08, -0.879728317), Vector3.new(14, 255, 4.62769413))
      createWall(CFrame.new(-1748.52148, -119.560036, 666.230652, -0.931119382, -8.67711378e-08, -0.364709496, -5.27960502e-08, 1, -1.03127007e-07, 0.364709556, -7.67686217e-08, -0.931119382), Vector3.new(14, 255, 4.41635466))
      createWall(CFrame.new(-1740.73279, 50.4497452, 720.327759, 0.694658399, 0, 0.719339788, 0, 1, 0, -0.719339788, 0, 0.694658399), Vector3.new(8, 81.5, 31.5))
      createWall(CFrame.new(-1994.25, 10.4497461, 709.5, 1, 0, 0, 0, 1, 0, 0, 0, 1), Vector3.new(492.5, 0.5, 5))
      createWall(CFrame.new(-1994.25, 10.4497461, 681.5, 1, 0, 0, 0, 1, 0, 0, 0, 1), Vector3.new(492.5, 0.5, 4))
      wait(.1)
      local t = waitForExist(workspace, "borders")
      for i,v in pairs(t:GetChildren()) do
        cs:AddTag(v, "RayWhitelist")
        v.Transparency = _G.wall_transparency
      end
      if _G.destroy_map then
        workspace.map:Destroy()
      else
        for j, k in pairs(workspace.map:GetChildren()) do
          if k:FindFirstChild("Meshes/Forgers Mark2_Circle.001") then
            k:Destroy()
          end
        end
      end

    end

    function fixOrbital()
      createWall(CFrame.new(2.05055237, 6.13212585, 144.456467, 1, 0, 0, 0, 1, 0, 0, 0, 1), Vector3.new(184, 1.5, 81))
      createWall(CFrame.new(-27.9494476, 18.8821259, 183.206467, 1, 0, 0, 0, 1, 0, 0, 0, 1), Vector3.new(130, 27, 3.5))
      createWall(CFrame.new(65.8005524, 18.8821259, 182.206467, 1, 0, 0, 0, 1, 0, 0, 0, 1), Vector3.new(60.5, 27, 5.5))
      createWall(CFrame.new(80.5505524, 18.8821259, 176.206467, 1, 0, 0, 0, 1, 0, 0, 0, 1), Vector3.new(31, 27, 17.5))
      createWall(CFrame.new(91.5505524, 18.8821259, 162.206467, 1, 0, 0, 0, 1, 0, 0, 0, 1), Vector3.new(9, 27, 45.5))
      createWall(CFrame.new(71.8005524, 20.3821259, 101.206467, 1, 0, 0, 0, 1, 0, 0, 0, 1), Vector3.new(72.5, 30, 3.5))
      createWall(CFrame.new(86.5673981, 5.77369833, 120.956467, 0.98480767, -0.173648179, 0, 0.173648179, 0.98480767, 0, 0, 0, 1), Vector3.new(40, 7, 38))
      createWall(CFrame.new(122.800552, 8.88212585, 116.456467, 1, 0, 0, 0, 1, 0, 0, 0, 1), Vector3.new(35.5, 7, 35))
      createWall(CFrame.new(136.300552, 16.8821259, 132.706467, 1, 0, 0, 0, 1, 0, 0, 0, 1), Vector3.new(60.5, 23, 10.5))
      createWall(CFrame.new(123.300552, 16.8821259, 103.206467, 1, 0, 0, 0, 1, 0, 0, 0, 1), Vector3.new(34.5, 23, 0.5))
      createWall(CFrame.new(130.692398, 10.4759054, 116.456467, 0.98480773, -0.173648179, 0, 0.173648179, 0.98480773, 0, 0, 0, 1), Vector3.new(24, 7, 35))
      createWall(CFrame.new(225.300552, 10.8821259, 83.7064667, 1, 0, 0, 0, 1, 0, 0, 0, 1), Vector3.new(172.5, 11, 149.5))
      createWall(CFrame.new(139.050552, 16.6321259, 84.4564667, 1, 0, 0, 0, 1, 0, 0, 0, 1), Vector3.new(11, 22.5, 47))
      createWall(CFrame.new(151.469864, 16.6321259, 61.0406761, 0.91354543, 0, -0.406736642, 0, 1, 0, 0.406736642, 0, 0.91354543), Vector3.new(3, 22.5, 94))
      createWall(CFrame.new(169.348312, 16.6321259, 42.4514313, 0.694658279, 0, -0.719339728, 0, 1, 0, 0.719339728, 0, 0.694658279), Vector3.new(4, 22.5, 94))
      createWall(CFrame.new(207.741302, 16.6321259, 22.175375, 0.358367801, 0, -0.93358016, 0, 1, 0, 0.93358016, 0, 0.358367801), Vector3.new(3.5, 22.5, 94))
      createWall(CFrame.new(200.99971, 16.6321259, 23.0883999, 0.0174523592, 0, -0.999846816, 0, 1, 0, 0.999846816, 0, 0.0174523592), Vector3.new(2, 22.5, 94))
      createWall(CFrame.new(251.564911, 16.6321259, 18.5538025, 0.766042292, 0, -0.642785966, 0, 1, 0, 0.642785966, 0, 0.766042292), Vector3.new(2, 22.5, 13.5))
      createWall(CFrame.new(255.064896, 16.6321259, 9.05387974, 0.999991894, 0, -1.78813934e-07, 0, 1, 0, 1.78813934e-07, 0, 0.999991894), Vector3.new(5, 22.5, 13.5))
      createWall(CFrame.new(170.300552, 16.8821259, 128.706467, 1, 0, 0, 0, 1, 0, 0, 0, 1), Vector3.new(9.5, 23, 18.5))
      createWall(CFrame.new(174.550552, 16.8821259, 109.206467, 1, 0, 0, 0, 1, 0, 0, 0, 1), Vector3.new(1, 23, 21.5))
      createWall(CFrame.new(178.440842, 16.8821259, 87.8495941, 0.906307757, 0, -0.42261827, 0, 1, 0, 0.42261827, 0, 0.906307757), Vector3.new(3, 23, 26.5))
      createWall(CFrame.new(192.023926, 16.8821259, 70.1889038, 0.629320323, 0, -0.777145863, 0, 1, 0, 0.777145863, 0, 0.629320323), Vector3.new(4, 23, 21))
      createWall(CFrame.new(207.625092, 16.8821259, 62.0181961, 0.258818924, 0, -0.965925455, 0, 1, 0, 0.965925455, 0, 0.258818924), Vector3.new(5.5, 23, 21.5))
      createWall(CFrame.new(235.841599, 16.8821259, 62.0727882, -0.0174523555, 0, -0.999844193, 0, 1, 0, 0.999844193, 0, -0.0174523555), Vector3.new(9, 23, 42))
      createWall(CFrame.new(268.73175, 16.8821259, 68.6477737, -0.0174523555, 0, -0.999844193, 0, 1, 0, 0.999844193, 0, -0.0174523555), Vector3.new(6, 23, 49))
      createWall(CFrame.new(295.005676, 16.8821259, 38.8518867, -0.0174523555, 0, -0.999844193, 0, 1, 0, 0.999844193, 0, -0.0174523555), Vector3.new(66.5, 23, 5.5))
      createWall(CFrame.new(290.775604, 16.8821259, 9.02362251, -0.0174523555, 0, -0.999844193, 0, 1, 0, 0.999844193, 0, -0.0174523555), Vector3.new(13, 23, 15))
      createWall(CFrame.new(237.565033, 20.8821259, -8.44598103, 0.999991894, 0, -1.78813934e-07, 0, 1, 0, 1.78813934e-07, 0, 0.999991894), Vector3.new(31, 31, 48.5))
      createWall(CFrame.new(216.315201, 20.8821259, -32.4457855, 0.999991894, 0, -1.78813934e-07, 0, 1, 0, 1.78813934e-07, 0, 0.999991894), Vector3.new(21.5, 31, 96.5))
      createWall(CFrame.new(335.789215, 20.8821259, -32.4457664, 0.999991894, 0, -1.78813934e-07, 0, 1, 0, 1.78813934e-07, 0, 0.999991894), Vector3.new(44.5500183, 31, 96.5))
      createWall(CFrame.new(306.28949, 20.8821259, -8.19596863, 0.999991894, 0, -1.78813934e-07, 0, 1, 0, 1.78813934e-07, 0, 0.999991894), Vector3.new(19.5500164, 31, 48))
      createWall(CFrame.new(274.800537, 11.3821259, -97.7935333, 1, 0, 0, 0, 1, 0, 0, 0, 1), Vector3.new(146.5, 12, 225.5))
      createWall(CFrame.new(204.550537, 22.3821259, -144.543533, 1, 0, 0, 0, 1, 0, 0, 0, 1), Vector3.new(6, 34, 132))
      createWall(CFrame.new(346.550537, 22.3821259, -144.543533, 1, 0, 0, 0, 1, 0, 0, 0, 1), Vector3.new(3, 34, 132))
      createWall(CFrame.new(253.300537, 22.3821259, -206.043533, 1, 0, 0, 0, 1, 0, 0, 0, 1), Vector3.new(103.5, 34, 5))
      createWall(CFrame.new(334.550537, 22.3821259, -206.043533, 1, 0, 0, 0, 1, 0, 0, 0, 1), Vector3.new(19, 34, 5))
      createWall(CFrame.new(339.300537, 22.3821259, -242.043533, 1, 0, 0, 0, 1, 0, 0, 0, 1), Vector3.new(9.5, 34, 77))
      createWall(CFrame.new(260.300537, 22.3821259, -219.293533, 1, 0, 0, 0, 1, 0, 0, 0, 1), Vector3.new(54.5, 34, 31.5))
      createWall(CFrame.new(312.050537, 11.3821259, -110.543533, 1, 0, 0, 0, 1, 0, 0, 0, 1), Vector3.new(72, 12, 251))
      createWall(CFrame.new(314.800537, 22.3821259, -277.293518, 1, 0, 0, 0, 1, 0, 0, 0, 1), Vector3.new(58.5, 34, 9.5))
      createWall(CFrame.new(221.550537, 23.8821259, -421.543518, 1, 0, 0, 0, 1, 0, 0, 0, 1), Vector3.new(14, 42, 8))
      createWall(CFrame.new(221.300537, 23.8821259, -497.293518, 1, 0, 0, 0, 1, 0, 0, 0, 1), Vector3.new(14.5, 42, 32.5))
      createWall(CFrame.new(319.965942, 16.5022373, -230.817398, 0.950360954, 4.37113883e-08, -0.311149508, -2.79408212e-08, 1, 5.51423724e-08, 0.311149508, -4.37113883e-08, 0.950360954), Vector3.new(69, 1.5, 85))
      createWall(CFrame.new(289.800537, 9.63212585, -304.293518, 1, 0, 0, 0, 1, 0, 0, 0, 1), Vector3.new(116.5, 8.5, 138.5))
      createWall(CFrame.new(233.300537, 21.6321259, -252.543518, 1, 0, 0, 0, 1, 0, 0, 0, 1), Vector3.new(3.5, 34.5, 35))
      createWall(CFrame.new(234.925537, 22.1321259, -319.043518, 1, 0, 0, 0, 1, 0, 0, 0, 1), Vector3.new(21.25, 33.5, 100))
      createWall(CFrame.new(313.300537, 22.1321259, -304.043518, 1, 0, 0, 0, 1, 0, 0, 0, 1), Vector3.new(37.5, 33.5, 57))
      createWall(CFrame.new(352.550537, 22.1321259, -322.793518, 1, 0, 0, 0, 1, 0, 0, 0, 1), Vector3.new(55, 33.5, 94.5))
      createWall(CFrame.new(268.550537, 22.1321259, -366.043518, 1, 0, 0, 0, 1, 0, 0, 0, 1), Vector3.new(66, 33.5, 6))
      createWall(CFrame.new(302.300537, 9.63212585, -375.543518, 1, 0, 0, 0, 1, 0, 0, 0, 1), Vector3.new(154.5, 8.5, 281))
      createWall(CFrame.new(377.550537, 25.1321259, -440.043518, 1, 0, 0, 0, 1, 0, 0, 0, 1), Vector3.new(4, 39.5, 147))
      createWall(CFrame.new(302.800537, 25.1321259, -512.293518, 1, 0, 0, 0, 1, 0, 0, 0, 1), Vector3.new(153.5, 39.5, 2.5))
      createWall(CFrame.new(227.050537, 25.1321259, -492.793518, 1, 0, 0, 0, 1, 0, 0, 0, 1), Vector3.new(10, 39.5, 41.5))
      createWall(CFrame.new(227.300537, 25.1321259, -400.043518, 1, 0, 0, 0, 1, 0, 0, 0, 1), Vector3.new(10.5, 39.5, 68))
      createWall(CFrame.new(149.300537, 23.8821259, -501.293518, 1, 0, 0, 0, 1, 0, 0, 0, 1), Vector3.new(158.5, 42, 24.5))
      createWall(CFrame.new(72.3005371, 23.8821259, -414.543518, 1, 0, 0, 0, 1, 0, 0, 0, 1), Vector3.new(4.5, 42, 16))
      createWall(CFrame.new(165.300537, 23.3821259, -412.793518, 1, 0, 0, 0, 1, 0, 0, 0, 1), Vector3.new(123.5, 41, 14.5))
      createWall(CFrame.new(143.550537, 10.1321259, -427.793518, 1, 0, 0, 0, 1, 0, 0, 0, 1), Vector3.new(178, 9.5, 176.5))
      createWall(CFrame.new(170.300537, 23.8821259, -387.293518, 1, 0, 0, 0, 1, 0, 0, 0, 1), Vector3.new(4.5, 42, 60.5))
      createWall(CFrame.new(159.175537, 23.8821259, -335.043518, 1, 0, 0, 0, 1, 0, 0, 0, 1), Vector3.new(25.25, 42, 59))
      createWall(CFrame.new(92.8005371, 23.8821259, -360.793518, 1, 0, 0, 0, 1, 0, 0, 0, 1), Vector3.new(47.5, 42, 7.5))
      createWall(CFrame.new(69.8005371, 23.8821259, -424.543518, 1, 0, 0, 0, 1, 0, 0, 0, 1), Vector3.new(1.5, 42, 135))
      createWall(CFrame.new(84.3005371, 22.6321259, -303.543518, 1, 0, 0, 0, 1, 0, 0, 0, 1), Vector3.new(133.5, 44.5, 6))
      createWall(CFrame.new(67.0505371, 22.6321259, -351.293518, 1, 0, 0, 0, 1, 0, 0, 0, 1), Vector3.new(54, 44.5, 26.5))
      createWall(CFrame.new(89.0505371, 22.6321259, -344.543518, 1, 0, 0, 0, 1, 0, 0, 0, 1), Vector3.new(17, 44.5, 25))
      createWall(CFrame.new(122.300537, 10.8821259, -333.793518, 1, 0, 0, 0, 1, 0, 0, 0, 1), Vector3.new(51.5, 11, 54.5))
      createWall(CFrame.new(64.4733582, -4.418859, -333.793518, 0.906307757, -0.42261827, 0, 0.42261827, 0.906307757, 0, 0, 0, 1), Vector3.new(75.5, 11, 54.5))
      createWall(CFrame.new(20.3005371, -3.61787415, -356.293518, 1, 0, 0, 0, 1, 0, 0, 0, 1), Vector3.new(95.5, 11, 99.5))
      createWall(CFrame.new(39.9685135, 6.63212585, -380.228729, 0.913545489, 0, 0.406736732, 0, 1, 0, -0.406736732, 0, 0.913545489), Vector3.new(14.5, 31.5, 46.5))
      createWall(CFrame.new(18.114563, 6.63212585, -403.113617, 0.0174522102, 0, 0.999847889, 0, 1, 0, -0.999847889, 0, 0.0174522102), Vector3.new(14.5, 31.5, 91))
      createWall(CFrame.new(-26.2788792, 6.63212585, -366.632813, 0.0174522102, 0, 0.999847889, 0, 1, 0, -0.999847889, 0, 0.0174522102), Vector3.new(89, 31.5, 3.5))
      createWall(CFrame.new(-36.5266075, 17.3821259, -309.552948, 0.0174522102, 0, 0.999847889, 0, 1, 0, -0.999847889, 0, 0.0174522102), Vector3.new(26.5, 53, 57))
      createWall(CFrame.new(5.80053711, 4.07662964, -309.267822, 1, 0, 0, 0, -0.656059086, 0.754709542, 0, -0.754709542, -0.656059086), Vector3.new(31.5, 24, 15.5))
      createWall(CFrame.new(19.5505371, 19.3427505, -291.517181, 1, 0, 0, 0, 0.0174524486, 0.99984777, 0, -0.99984777, 0.0174524486), Vector3.new(5, 62, 50.5))
      createWall(CFrame.new(-102.175552, 17.3821259, -272.943085, 0.0174522102, 0, 0.999847889, 0, 1, 0, -0.999847889, 0, 0.0174522102), Vector3.new(102, 53, 90))
      createWall(CFrame.new(4.05209827, 17.3821259, -242.084457, 0.0174522102, 0, 0.999847889, 0, 1, 0, -0.999847889, 0, 0.0174522102), Vector3.new(40, 53, 74.5))
      createWall(CFrame.new(38.5662766, 17.3821259, -170.971268, 0.0174522102, 0, 0.999847889, 0, 1, 0, -0.999847889, 0, 0.0174522102), Vector3.new(181, 53, 3))
      createWall(CFrame.new(-47.4959297, 17.3821259, -82.2097092, 0.0174522102, 0, 0.999847889, 0, 1, 0, -0.999847889, 0, 0.0174522102), Vector3.new(0.499998093, 53, 172))
      createWall(CFrame.new(-130.682892, 17.3821259, -158.17308, 0.0174522102, 0, 0.999847889, 0, 1, 0, -0.999847889, 0, 0.0174522102), Vector3.new(149.5, 53, 3))
      createWall(CFrame.new(-40.7920074, 4.38212585, -194.109756, 0.0174522102, 0, 0.999847889, 0, 1, 0, -0.999847889, 0, 0.0174522102), Vector3.new(224.5, 27, 181.5))
      createWall(CFrame.new(-25.6994476, 18.8821259, 117.706467, 1, 0, 0, 0, 1, 0, 0, 0, 1), Vector3.new(125.5, 27, 36.5))
      createWall(CFrame.new(-89.1994476, 18.8821259, 154.206467, 1, 0, 0, 0, 1, 0, 0, 0, 1), Vector3.new(7.5, 27, 61.5))
      createWall(CFrame.new(282.050537, 22.1321259, -316.793518, 1, 0, 0, 0, 1, 0, 0, 0, 1), Vector3.new(28, 33.5, 5.5))
      createWall(CFrame.new(226.777496, 14.4964676, -453.289978, 0.99999994, -8.74227766e-08, -2.84238873e-16, 8.74227695e-08, 1, 8.74227766e-08, -7.35850217e-15, -8.74227766e-08, 1), Vector3.new(8, 1, 45.5))
      createWall(CFrame.new(226.277496, 14.9964676, -453.289978, 0.99999994, -8.74227766e-08, -2.84238873e-16, 8.74227695e-08, 1, 8.74227766e-08, -7.35850217e-15, -8.74227766e-08, 1), Vector3.new(7, 2, 43.5))
      createWall(CFrame.new(225.777496, 15.4964676, -453.289978, 0.99999994, -8.74227766e-08, -2.84238873e-16, 8.74227695e-08, 1, 8.74227766e-08, -7.35850217e-15, -8.74227766e-08, 1), Vector3.new(6, 3, 41.5))
      createWall(CFrame.new(210.777496, 15.9964666, -456.539978, 0.99999994, -8.74227766e-08, -2.84238873e-16, 8.74227695e-08, 1, 8.74227766e-08, -7.35850217e-15, -8.74227766e-08, 1), Vector3.new(31, 4, 77))
      createWall(CFrame.new(210.027496, 14.9964666, -456.539978, 0.99999994, -8.74227766e-08, -2.84238873e-16, 8.74227695e-08, 1, 8.74227766e-08, -7.35850217e-15, -8.74227766e-08, 1), Vector3.new(32.5, 4, 77))
      createWall(CFrame.new(209.527496, 14.4964666, -456.539978, 0.99999994, -8.74227766e-08, -2.84238873e-16, 8.74227695e-08, 1, 8.74227766e-08, -7.35850217e-15, -8.74227766e-08, 1), Vector3.new(33.5, 3, 77))
      createWall(CFrame.new(-3.77072525, 17.3821259, -202.161972, -0.731354296, 0, 0.681998551, 0, 1, 0, -0.681998551, 0, -0.731354296), Vector3.new(29.5, 53, 29.5))
      createWall(CFrame.new(21.5335732, 17.3821259, -189.938141, -0.99026978, 0, 0.13917309, 0, 1, 0, -0.13917309, 0, -0.99026978), Vector3.new(45, 53, 24.5))
      createWall(CFrame.new(-11.1203985, 17.3821259, -219.985062, -0.190809608, 0, 0.981628776, 0, 1, 0, -0.981628776, 0, -0.190809608), Vector3.new(29.5, 53, 29.5))
      createWall(CFrame.new(21.5335732, 17.3821259, -189.938141, -0.99026978, 0, 0.13917309, 0, 1, 0, -0.13917309, 0, -0.99026978), Vector3.new(45, 53, 24.5))
      createWall(CFrame.new(201.004074, 16.6321259, 23.3383617, 0.0174523592, 0, -0.999846816, 0, 1, 0, 0.999846816, 0, 0.0174523592), Vector3.new(2.5, 22.5, 94))
      createWall(CFrame.new(291.03064, 16.8821259, 66.0365601, -0.0174523555, 0, -0.999844193, 0, 1, 0, 0.999844193, 0, -0.0174523555), Vector3.new(12, 23, 12.5))
      createWall(CFrame.new(292.446808, 16.8821259, 13.5534649, -0.0174523555, 0, -0.999844193, 0, 1, 0, 0.999844193, 0, -0.0174523555), Vector3.new(16, 23, 11.5))
      createWall(CFrame.new(241.550537, 22.1321259, -316.793518, 1, 0, 0, 0, 1, 0, 0, 0, 1), Vector3.new(12, 33.5, 5.5))
      createWall(CFrame.new(198.585739, 15.9964609, -495.978149, 0.69465822, -8.74227766e-08, 0.719339728, -2.15772644e-09, 1, 1.23615649e-07, -0.719339669, -8.74227837e-08, 0.694658399), Vector3.new(31, 4, 24.5))
      createWall(CFrame.new(197.891083, 14.9964609, -495.25882, 0.69465822, -8.74227766e-08, 0.719339728, -2.15772644e-09, 1, 1.23615649e-07, -0.719339669, -8.74227837e-08, 0.694658399), Vector3.new(31, 4, 24.5))
      createWall(CFrame.new(196.849091, 13.9964609, -494.17981, 0.69465822, -8.74227766e-08, 0.719339728, -2.15772644e-09, 1, 1.23615649e-07, -0.719339669, -8.74227837e-08, 0.694658399), Vector3.new(31, 4, 24.5))
      createWall(CFrame.new(200.608017, 15.9964695, -413.158813, 0.707106352, -8.74227979e-08, -0.70710659, 1.23634393e-07, 1, 2.44249065e-14, 0.707106471, -8.74227837e-08, 0.707106888), Vector3.new(31, 4, 21))
      createWall(CFrame.new(199.900909, 14.9964695, -413.865906, 0.707106352, -8.74227979e-08, -0.70710659, 1.23634393e-07, 1, 2.44249065e-14, 0.707106471, -8.74227837e-08, 0.707106888), Vector3.new(31, 4, 21))
      createWall(CFrame.new(199.193802, 13.9964695, -414.572998, 0.707106352, -8.74227979e-08, -0.70710659, 1.23634393e-07, 1, 2.44249065e-14, 0.707106471, -8.74227837e-08, 0.707106888), Vector3.new(31, 4, 21))
      createWall(CFrame.new(82.0505371, 23.8821259, -496.543518, 1, 0, 0, 0, 1, 0, 0, 0, 1), Vector3.new(24, 42, 34))
      createWall(CFrame.new(319.015594, 15.5022373, -231.12854, 0.950360954, 4.37113883e-08, -0.311149508, -2.79408212e-08, 1, 5.51423724e-08, 0.311149508, -4.37113883e-08, 0.950360954), Vector3.new(69, 1.5, 85))
      createWall(CFrame.new(318.065247, 14.5022373, -231.439682, 0.950360954, 4.37113883e-08, -0.311149508, -2.79408212e-08, 1, 5.51423724e-08, 0.311149508, -4.37113883e-08, 0.950360954), Vector3.new(69, 1.5, 85))
      createWall(CFrame.new(317.114899, 13.5022373, -231.750824, 0.950360954, 4.37113883e-08, -0.311149508, -2.79408212e-08, 1, 5.51423724e-08, 0.311149508, -4.37113883e-08, 0.950360954), Vector3.new(69, 1.5, 85))
      createWall(CFrame.new(241.800537, 22.1321259, -317.043518, 1, 0, 0, 0, 1, 0, 0, 0, 1), Vector3.new(12.5, 33.5, 6))
      createWall(CFrame.new(122.300537, 9.88212585, -334.293518, 1, 0, 0, 0, 1, 0, 0, 0, 1), Vector3.new(51.5, 11.5, 55.5))
      wait(.1)
      if _G.destroy_map then
        workspace.Terrain:Clear()
        workspace.Map:Destroy()
      end
    end

    function canalsFix()
      createWall(CFrame.new(155.957275, 32.8910141, -46.5320663, 1, 0, 0, 0, 1, 0, 0, 0, 1), Vector3.new(11.7300148, 87.4399948, 105.580002))
      createWall(CFrame.new(-138.143799, 32.8910141, 163.496231, -4.37113883e-08, 0, 1, 0, 1, 0, -1, 0, -4.37113883e-08), Vector3.new(97.5299759, 87.4399948, 22.3999958))
      createWall(CFrame.new(-34.8195114, 32.8910141, -67.9616165, -1, -8.74227766e-08, 0, -8.74227766e-08, 1, -8.74227766e-08, 7.64274186e-15, -8.74227766e-08, -1), Vector3.new(83.9499435, 87.4399948, 46.5899925))
      createWall(CFrame.new(-103.979477, 32.8910141, -224.424011, -4.37113883e-08, 0, -1, 0, 1, 0, 1, 0, -4.37113883e-08), Vector3.new(6.84993505, 87.4399948, 235.629959))
      createWall(CFrame.new(-186.825027, 62.1460152, 73.4007111, 1, 0, 0, 0, 1, 0, 0, 0, 1), Vector3.new(84.4299774, 145.949997, 5.42000008))
      createWall(CFrame.new(-241.964264, 32.8910141, -94.9756775, -0.766044438, -6.69697329e-08, -0.642787576, -3.12285025e-08, 1, -6.69697329e-08, 0.642787576, -3.12285025e-08, -0.766044438), Vector3.new(66.1999207, 87.4399948, 5.42000008))
      createWall(CFrame.new(-55.4694901, 32.8910141, -157.089325, -1, -8.74227766e-08, 0, -8.74227766e-08, 1, -8.74227766e-08, 7.64274186e-15, -8.74227766e-08, -1), Vector3.new(6.84993505, 87.4399948, 138.609985))
      createWall(CFrame.new(-145.703644, 32.8910141, 28.710371, -1, -8.74227766e-08, 0, -8.74227766e-08, 1, -8.74227766e-08, 7.64274186e-15, -8.74227766e-08, -1), Vector3.new(84.4299774, 87.4399948, 5.42000008))
      createWall(CFrame.new(71.0828094, 32.8910141, 50.8468018, -4.37113883e-08, 0, -1, 0, 1, 0, 1, 0, -4.37113883e-08), Vector3.new(49.6700058, 87.4399948, 93.9099808))
      createWall(CFrame.new(135.878815, 32.8910141, 15.5871773, 0.719339788, 0, -0.694658399, 0, 1, 0, 0.694658399, 0, 0.719339788), Vector3.new(11.7300148, 87.4399948, 58.2199783))
      createWall(CFrame.new(225.497131, 36.9860115, -59.8648605, 1, 0, 0, 0, 1, 0, 0, 0, 1), Vector3.new(150.809937, 95.6299896, 52.0899887))
      createWall(CFrame.new(-242.781433, 32.8910141, -16.9685707, -0.121869326, -1.06541549e-08, 0.992546141, -1.74193914e-07, 1, -1.06541549e-08, -0.992546141, -1.74193914e-07, -0.121869326), Vector3.new(80.8499374, 87.4399948, 5.42000008))
      createWall(CFrame.new(-224.062851, 32.8910141, -75.7806473, -0.766044438, -6.69697329e-08, -0.642787576, -3.12285025e-08, 1, -6.69697329e-08, 0.642787576, -3.12285025e-08, -0.766044438), Vector3.new(63.4499245, 87.4399948, 5.92000008))
      createWall(CFrame.new(-145.703644, 62.2310066, 113.641754, -4.37113883e-08, 0, 1, 0, 1, 0, -1, 0, -4.37113883e-08), Vector3.new(84.4299774, 146.11998, 5.42000008))
      createWall(CFrame.new(-294.795288, 32.8910141, -76.0985794, -0.99862951, -8.73029649e-08, -0.0523359589, -8.28474214e-08, 1, -8.73029649e-08, 0.0523359589, -8.28474214e-08, -0.99862951), Vector3.new(63.6999283, 87.4399948, 5.42000008))
      createWall(CFrame.new(-123.277046, 32.8910141, 120.19175, -4.37113883e-08, 0, 1, 0, 1, 0, -1, 0, -4.37113883e-08), Vector3.new(97.5299759, 87.4399948, 15.5299997))
      createWall(CFrame.new(397.023865, 36.9860115, -58.8248749, 1, 0, 0, 0, 1, 0, 0, 0, 1), Vector3.new(150.809937, 95.6299896, 54.1699905))
      createWall(CFrame.new(416.749054, 36.9860115, -96.7398682, 1, 0, 0, 0, 1, 0, 0, 0, 1), Vector3.new(111.359848, 95.6299896, 117.999992))
      createWall(CFrame.new(425.636475, 36.9860115, 1.16940498, 1, 0, 0, 0, 1, 0, 0, 0, 1), Vector3.new(106.859848, 95.6299896, 82.909996))
      createWall(CFrame.new(-121.666016, 32.8910141, 279.982574, -4.37113883e-08, 0, 1, 0, 1, 0, -1, 0, -4.37113883e-08), Vector3.new(97.5299759, 87.4399948, 11.550005))
      createWall(CFrame.new(-98.9495239, 59.7010269, -44.2266006, -1, -8.74227766e-08, 0, -8.74227766e-08, 1, -8.74227766e-08, 7.64274186e-15, -8.74227766e-08, -1), Vector3.new(58.7299576, 33.8199959, 24.7199955))
      createWall(CFrame.new(-98.8532333, 32.8910141, 51.1067657, -4.37113883e-08, 0, -1, 0, 1, 0, 1, 0, -4.37113883e-08), Vector3.new(50.0699921, 87.4399948, 41.260006))
      createWall(CFrame.new(371.486694, 36.9860115, 44.0894165, 1, 0, 0, 0, 1, 0, 0, 0, 1), Vector3.new(215.159775, 95.6299896, 16.9300041))
      createWall(CFrame.new(189.412186, 36.9860115, 17.0006351, 1, 0, 0, 0, 1, 0, 0, 0, 1), Vector3.new(16.339817, 95.6299896, 52.0800133))
      createWall(CFrame.new(196.772171, 36.9860115, -85.2920761, 1, 0, 0, 0, 1, 0, 0, 0, 1), Vector3.new(93.3599701, 95.6299896, 28.0600014))
      createWall(CFrame.new(155.065796, 36.9860115, 67.287796, 1, 0, 0, 0, 1, 0, 0, 0, 1), Vector3.new(20.3698311, 95.6299896, 17.1600227))
      createWall(CFrame.new(124.959198, 36.9860115, 134.113754, 1, 0, 0, 0, 1, 0, 0, 0, 1), Vector3.new(41.2598, 95.6299896, 74.7600098))
      createWall(CFrame.new(-162.458191, 32.8910141, -68.6916199, -1, -8.74227766e-08, 0, -8.74227766e-08, 1, -8.74227766e-08, 7.64274186e-15, -8.74227766e-08, -1), Vector3.new(83.9499435, 87.4399948, 45.1299858))
      createWall(CFrame.new(-111.588234, 32.8910141, 50.9817734, -4.37113883e-08, 0, -1, 0, 1, 0, 1, 0, -4.37113883e-08), Vector3.new(49.939991, 87.4399948, 15.7900009))
      createWall(CFrame.new(-25.9021072, 32.8910141, 50.9817734, -4.37113883e-08, 0, -1, 0, 1, 0, 1, 0, -4.37113883e-08), Vector3.new(49.939991, 87.4399948, 114.280014))
      createWall(CFrame.new(-223.311798, 32.8910141, -168.529022, 1, 0, 0, 0, 1, 0, 0, 0, 1), Vector3.new(6.84993505, 87.4399948, 116.899963))
      createWall(CFrame.new(-136.288849, 32.8910141, 301.444031, -4.37113883e-08, 0, 1, 0, 1, 0, -1, 0, -4.37113883e-08), Vector3.new(32.1999626, 87.4399948, 18.6900043))
      createWall(CFrame.new(-232.190765, 32.8910141, 48.9222374, -0.224951044, -1.96658441e-08, 0.974370062, -1.72604913e-07, 1, -1.96658441e-08, -0.974370062, -1.72604913e-07, -0.224951044), Vector3.new(54.5299835, 87.4399948, 5.42000008))
      createWall(CFrame.new(-170.796127, 32.8910141, 24.3202763, -4.37113883e-08, 0, -1, 0, 1, 0, 1, 0, -4.37113883e-08), Vector3.new(84.4299774, 87.4399948, 5.42000008))
      createWall(CFrame.new(186.772171, 36.9860115, -167.385376, 1, 0, 0, 0, 1, 0, 0, 0, 1), Vector3.new(113.35997, 95.6299896, 15.4500008))
      createWall(CFrame.new(-132.073868, 32.8910141, 268.779114, -4.37113883e-08, 0, 1, 0, 1, 0, -1, 0, -4.37113883e-08), Vector3.new(97.5299759, 87.4399948, 10.260006))
      createWall(CFrame.new(175.484131, 36.9860115, 53.6146545, -0.707106769, -6.18172393e-08, 0.707106769, -1.49240009e-07, 1, -6.18172393e-08, -0.707106769, -1.49240009e-07, -0.707106769), Vector3.new(16.339817, 95.6299896, 46.5600052))
      createWall(CFrame.new(124.959198, 36.9860115, 71.5675964, 1, 0, 0, 0, 1, 0, 0, 0, 1), Vector3.new(41.2598, 95.6299896, 17.1600227))
      createWall(CFrame.new(117.913742, 77.9372025, 156.825684, 1, 0, 0, 0, 1, 0, 0, 0, 1), Vector3.new(167.879807, 17.2299976, 14.8899794))
      createWall(CFrame.new(-207.538849, 32.8910141, 296.944031, -4.37113883e-08, 0, 1, 0, 1, 0, -1, 0, -4.37113883e-08), Vector3.new(41.1999626, 87.4399948, 2.19000244))
      createWall(CFrame.new(-187.778656, 27.8627968, 362.189514, -4.37113883e-08, 0, 1, 0, 1, 0, -1, 0, -4.37113883e-08), Vector3.new(125.759773, 117.039948, 42.3200684))
      createWall(CFrame.new(-47.6979599, 48.4710083, 120.507584, 1, 0, 0, 0, 1, 0, 0, 0, 1), Vector3.new(68.4998016, 72.6599579, 42.0500107))
      createWall(CFrame.new(-330.275391, 43.1127968, 387.889862, 1, 0, 0, 0, 1, 0, 0, 0, 1), Vector3.new(245.559784, 86.5399475, 41.8200684))
      createWall(CFrame.new(267.329956, 44.1549873, 47.4600601, 1, 0, -4.37113883e-08, 0, 1, 0, 4.37113883e-08, 0, 1), Vector3.new(83.4698105, 65.7099991, 33.4500122))
      createWall(CFrame.new(-281.293365, 65.0105286, 53.0568275, -0.241921902, -2.11494839e-08, 0.970295727, -1.72248718e-07, 1, -2.11494839e-08, -0.970295727, -1.72248718e-07, -0.241921902), Vector3.new(145.519989, 89.8999939, 14.3299999))
      createWall(CFrame.new(-463.079102, 43.6127968, 295.492493, -4.37113883e-08, 0, 1, 0, 1, 0, -1, 0, -4.37113883e-08), Vector3.new(245.559784, 85.5399475, 41.8200684))
      createWall(CFrame.new(46.2713356, 50.5749092, -60.2988358, -4.37113883e-08, 0, -1, 0, 1, 0, 1, 0, -4.37113883e-08), Vector3.new(102.98999, 76.6199799, 150.919952))
      createWall(CFrame.new(-51.3865967, 44.7459869, 279.715424, 1, 0, 0, 0, 1, 0, 0, 0, 1), Vector3.new(140.999802, 54.1599617, 44.3200684))
      createWall(CFrame.new(-304.962646, 44.8627968, 155.790512, -1, -8.74227766e-08, 0, -8.74227766e-08, 1, -8.74227766e-08, 7.64274186e-15, -8.74227766e-08, -1), Vector3.new(245.559784, 83.0399475, 41.8200684))
      createWall(CFrame.new(-33.8865967, 44.7459869, 164.972504, 1, 0, 0, 0, 1, 0, 0, 0, 1), Vector3.new(101.999802, 54.1599617, 52.3200684))
      createWall(CFrame.new(-303.172791, 48.7665901, -37.5034637, -0.10452842, -9.13816489e-09, 0.994521916, -1.74366647e-07, 1, -9.13816489e-09, -0.994521916, -1.74366647e-07, -0.10452842), Vector3.new(48.9499397, 19.0299969, 20.3599987))
      createWall(CFrame.new(13.9149284, 36.9860115, 136.112579, 1, 0, 0, 0, 1, 0, 0, 0, 1), Vector3.new(57.2598, 95.6299896, 76.2600098))
      createWall(CFrame.new(-219.415039, 70.8955231, 110.323151, 1, 0, 0, 0, 1, 0, 0, 0, 1), Vector3.new(83.8099518, 122.169983, 13.8299999))
      createWall(CFrame.new(-165.575058, 61.5059929, 108.555695, 1, 0, 0, 0, 1, 0, 0, 0, 1), Vector3.new(41.9299812, 144.669952, 23.8700027))
      createWall(CFrame.new(-198.054108, 47.3627968, 299.961273, -0.809017003, -7.07265144e-08, 0.587785244, -1.38808588e-07, 1, -7.07265144e-08, -0.587785244, -1.38808588e-07, -0.809017003), Vector3.new(21.0899963, 78.0399475, 6.30006504))
      createWall(CFrame.new(17.4978638, 32.8910141, 45.4267883, -4.37113883e-08, 0, -1, 0, 1, 0, 1, 0, -4.37113883e-08), Vector3.new(38.8299904, 87.4399948, 201.079956))
      createWall(CFrame.new(-304.545441, 64.4899902, 21.4497986, -0.104528427, 1.77635684e-15, 0.994521916, 0, 1, 0, -0.994521916, 1.42108547e-14, -0.104528427), Vector3.new(190.769989, 98.3999939, 10.8299999))
      createWall(CFrame.new(-112.038849, 4.6410141, 169.694031, -4.37113883e-08, 0, 1, 0, 1, 0, -1, 0, -4.37113883e-08), Vector3.new(17.6999512, 30.9399948, 41.1900024))
      createWall(CFrame.new(-249.993698, 65.0105209, 98.5818253, -0.681998253, -2.1149468e-08, 0.731353581, -1.4039864e-07, 1, -1.02005565e-07, -0.731353581, -1.72248718e-07, -0.681998253), Vector3.new(214.269989, 89.8999939, 3.57999992))
      createWall(CFrame.new(-248.899078, 32.8910065, -55.5102959, -0.121869326, -1.06541549e-08, 0.992546141, -1.74193914e-07, 1, -1.06541549e-08, -0.992546141, -1.74193914e-07, -0.121869326), Vector3.new(4.34993744, 87.4399948, 8.17000008))
      createWall(CFrame.new(-273.835968, 17.4611702, 40.0727425, 0, -8.74227695e-08, 1, -8.74227837e-08, 1, 8.74227837e-08, -1, -8.74227837e-08, 0), Vector3.new(230.769989, 4.8999939, 88.3300018))
      createWall(CFrame.new(-251.195892, 7.01116419, 91.0399628, -1, -8.74227766e-08, 0, -8.74227766e-08, 1, -8.74227766e-08, 7.64274186e-15, -8.74227766e-08, -1), Vector3.new(47.0499802, 24, 33.1999054))
      createWall(CFrame.new(-249.195892, 6.01116419, 91.5399628, -1, -8.74227766e-08, 0, -8.74227766e-08, 1, -8.74227766e-08, 7.64274186e-15, -8.74227766e-08, -1), Vector3.new(47.0499802, 24, 41.1999054))
      createWall(CFrame.new(-247.195892, 5.01116419, 93.2899628, -1, -8.74227766e-08, 0, -8.74227766e-08, 1, -8.74227766e-08, 7.64274186e-15, -8.74227766e-08, -1), Vector3.new(47.0499802, 24, 45.6999054))
      createWall(CFrame.new(-245.195892, 4.01116419, 89.2899628, -1, -8.74227766e-08, 0, -8.74227766e-08, 1, -8.74227766e-08, 7.64274186e-15, -8.74227766e-08, -1), Vector3.new(47.0499802, 24, 50.6999054))
      createWall(CFrame.new(-243.195892, 3.01116443, 92.0399628, -1, -8.74227766e-08, 0, -8.74227766e-08, 1, -8.74227766e-08, 7.64274186e-15, -8.74227766e-08, -1), Vector3.new(47.0499802, 24, 46.1999054))
      createWall(CFrame.new(-241.195892, 2.01116443, 92.2899628, -1, -8.74227766e-08, 0, -8.74227766e-08, 1, -8.74227766e-08, 7.64274186e-15, -8.74227766e-08, -1), Vector3.new(47.0499802, 24, 47.6999054))
      createWall(CFrame.new(-239.195892, 1.01116467, 95.2899628, -1, -8.74227766e-08, 0, -8.74227766e-08, 1, -8.74227766e-08, 7.64274186e-15, -8.74227766e-08, -1), Vector3.new(47.0499802, 24, 45.6999054))
      createWall(CFrame.new(-181.175049, 11.859992, 89.4149475, -2.80912309e-16, -8.74227624e-08, 1, -8.74227766e-08, 1, 8.74227908e-08, -1, -8.74227766e-08, 7.36183101e-15), Vector3.new(33.769989, 0.899993896, 68.8300018))
      createWall(CFrame.new(-38.9890747, 11.6300173, -100.624664, -1, -8.74227766e-08, 7.70258813e-15, -8.74227766e-08, 1, -8.74227766e-08, -5.98462659e-17, -8.74227766e-08, -1), Vector3.new(388.849945, 2.43999481, 252.609985))
      createWall(CFrame.new(-79.9495239, 44.2010269, -44.2266006, -1, -8.74227766e-08, 0, -8.74227766e-08, 1, -8.74227766e-08, 7.64274186e-15, -8.74227766e-08, -1), Vector3.new(20.7299576, 64.8199921, 24.7199955))
      createWall(CFrame.new(-114.449524, 44.2010269, -44.2266006, -1, -8.74227766e-08, 0, -8.74227766e-08, 1, -8.74227766e-08, 7.64274186e-15, -8.74227766e-08, -1), Vector3.new(21.7299576, 64.8199921, 24.7199955))
      createWall(CFrame.new(-146.699524, 44.2010269, -23.4766006, -1, -8.74227766e-08, 0, -8.74227766e-08, 1, -8.74227766e-08, 7.64274186e-15, -8.74227766e-08, -1), Vector3.new(56.2299576, 64.8199921, 66.2199936))
      createWall(CFrame.new(-47.6995239, 44.2010345, -30.7266006, -1, -8.74227766e-08, 0, -8.74227766e-08, 1, -8.74227766e-08, 7.64274186e-15, -8.74227766e-08, -1), Vector3.new(41.22995, 64.8199921, 51.7199936))
      createWall(CFrame.new(121.772171, 36.9860115, -141.885376, 1, 0, 0, 0, 1, 0, 0, 0, 1), Vector3.new(21.3599701, 95.6299896, 66.4499969))
      createWall(CFrame.new(305.272156, 36.9860115, -162.635376, 1, 0, 0, 0, 1, 0, 0, 0, 1), Vector3.new(125.35997, 95.6299896, 24.9500008))
      createWall(CFrame.new(207.30394, 36.9860153, 63.8677101, -0.707106769, -6.18172393e-08, 0.707106769, -1.49240009e-07, 1, -6.18172393e-08, -0.707106769, -1.49240009e-07, -0.707106769), Vector3.new(6.83981705, 95.6299896, 61.0600052))
      createWall(CFrame.new(182.976639, 30.7049866, 90.3965759, -0.887010872, -3.55271368e-15, 0.46174866, 0, 1, -7.10542736e-15, -0.46174866, 0, -0.887010872), Vector3.new(5.33981705, 95.6299896, 14.0600052))
      createWall(CFrame.new(178.860107, 32.4249954, 129.819794, -1.00000012, -3.15129545e-15, -2.98023224e-08, 3.15129566e-15, 1, -8.74588793e-15, 2.98023224e-08, 8.74588793e-15, -1.00000012), Vector3.new(4.33981705, 95.6299896, 69.0600052))
      createWall(CFrame.new(160.610107, 32.4249954, 163.569794, -1.00000012, -3.15129545e-15, -2.98023224e-08, 3.15129566e-15, 1, -8.74588793e-15, 2.98023224e-08, 8.74588793e-15, -1.00000012), Vector3.new(40.839817, 95.6299896, 1.56000519))
      createWall(CFrame.new(88.459198, 36.9860115, 166.613754, 1, 0, 0, 0, 1, 0, 0, 0, 1), Vector3.new(114.259796, 95.6299896, 9.76000977))
      createWall(CFrame.new(311.260925, 24.7869816, -58.2802277, -1, -8.74098589e-08, -1.52582125e-09, -8.74224142e-08, 0.99984777, 0.0174522698, 3.52690052e-14, 0.0174522698, -0.99984777), Vector3.new(23.3499451, 39.9399948, 24.6099854))
      createWall(CFrame.new(17.1134033, 44.7459869, 243.465424, 1, 0, 0, 0, 1, 0, 0, 0, 1), Vector3.new(3.99980164, 54.1599617, 116.820068))
      createWall(CFrame.new(-166.538849, 32.8910141, 307.694031, -4.37113883e-08, 0, 1, 0, 1, 0, -1, 0, -4.37113883e-08), Vector3.new(19.6999626, 87.4399948, 79.1900024))
      createWall(CFrame.new(-207.538849, 32.8910141, 217.694031, -4.37113883e-08, 0, 1, 0, 1, 0, -1, 0, -4.37113883e-08), Vector3.new(82.6999664, 87.4399948, 2.19000244))
      createWall(CFrame.new(-427.212646, 47.3627853, 175.540512, -1, -8.74227766e-08, 0, -8.74227766e-08, 1, -8.74227766e-08, 7.64274186e-15, -8.74227766e-08, -1), Vector3.new(31.0597839, 78.0399475, 81.3200684))
      createWall(CFrame.new(-176.288849, 32.8910141, 211.694031, -4.37113883e-08, 0, 1, 0, 1, 0, -1, 0, -4.37113883e-08), Vector3.new(42.6999664, 87.4399948, 59.6900024))
      createWall(CFrame.new(75.8479004, 0.891014099, -2.7682178, -4.37113883e-08, 0, -1, 0, 1, 0, 1, 0, -4.37113883e-08), Vector3.new(391.440002, 23.4399948, 462.780029))
      createWall(CFrame.new(-49.6365967, 18.9959869, 200.222504, 1, 0, 0, 0, 1, 0, 0, 0, 1), Vector3.new(133.499802, 2.6599617, 121.820068))
      createWall(CFrame.new(-290.788849, 0.641014099, 262.194031, -4.37113883e-08, 0, 1, 0, 1, 0, -1, 0, -4.37113883e-08), Vector3.new(241.699966, 22.9399948, 369.690002))
      createWall(CFrame.new(-109.038849, 1.3910141, 264.194031, -4.37113883e-08, 0, 1, 0, 1, 0, -1, 0, -4.37113883e-08), Vector3.new(237.699951, 24.4399948, 35.1900024))
      createWall(CFrame.new(239.912186, 36.9860115, -22.4993649, 1, 0, 0, 0, 1, 0, 0, 0, 1), Vector3.new(117.339813, 95.6299896, 48.0800133))
      createWall(CFrame.new(178.260925, 23.3800297, -162.874664, -1, -8.74227766e-08, 7.70258813e-15, -8.74227766e-08, 1, -8.74227766e-08, -5.98462659e-17, -8.74227766e-08, -1), Vector3.new(121.349945, 25.9399948, 128.109985))
      createWall(CFrame.new(307.760925, 23.380043, -136.374664, -1, -8.74227766e-08, 7.70258813e-15, -8.74227766e-08, 1, -8.74227766e-08, -5.98462659e-17, -8.74227766e-08, -1), Vector3.new(137.349945, 25.9399948, 181.109985))
      createWall(CFrame.new(-99.9021072, -12.9436626, 113.714745, -3.53632537e-08, 2.56929074e-08, -1, 0.587785184, 0.809016943, -4.4408921e-16, 0.809016943, -0.587785184, -4.37113918e-08), Vector3.new(79.9400024, 23.4399948, 56.2800293))
      createWall(CFrame.new(42.959198, 36.9860115, 134.363754, 1, 0, 0, 0, 1, 0, 0, 0, 1), Vector3.new(23.2597961, 95.6299896, 74.2600098))
      createWall(CFrame.new(-121.288857, 0.756968558, 202.870163, -4.20180761e-08, 1.20484973e-08, 1, 0.275637388, 0.961261809, 3.33066907e-15, -0.961261809, 0.275637388, -4.37113918e-08), Vector3.new(59.1999512, 23.9399948, 10.6900024))
      createWall(CFrame.new(310.510925, 23.1539402, -49.8755417, -1, -7.33189793e-08, -4.76138418e-08, -8.7422741e-08, 0.838670671, 0.544638932, -1.30358269e-14, 0.544638932, -0.838670671), Vector3.new(24.8499451, 39.9399948, 16.6099854))
      createWall(CFrame.new(310.510925, 21.0615959, -71.9470215, -1, -7.78942706e-08, 3.96891195e-08, -8.74227766e-08, 0.89100647, -0.453990608, -5.3323414e-17, -0.453990608, -0.89100647), Vector3.new(24.8499451, 39.9399948, 24.6099854))
      createWall(CFrame.new(137.010925, 20.868412, -68.4826736, -1, -8.04731002e-08, -3.41587914e-08, -8.74227695e-08, 0.920504868, 0.390731037, -5.14420645e-17, 0.390731037, -0.920504868), Vector3.new(38.8499451, 4.43999481, 68.1099854))
      createWall(CFrame.new(256.935089, 9.34212494, 30.1253357, -0.920504808, -0.390731215, 3.55271368e-15, -0.390731215, 0.920504808, -8.74227837e-08, 3.41587985e-08, -8.04730931e-08, -1), Vector3.new(66.8499451, 24.4399948, 66.1099854))
      createWall(CFrame.new(337.760925, 22.6300564, 12.8753357, -1, -8.74227766e-08, 7.70258813e-15, -8.74227766e-08, 1, -8.74227766e-08, -5.98462659e-17, -8.74227766e-08, -1), Vector3.new(77.3499451, 24.4399948, 100.609985))
      createWall(CFrame.new(337.010925, 22.1300583, 30.1253357, -1, -8.74227766e-08, 7.70258813e-15, -8.74227766e-08, 1, -8.74227766e-08, -5.98462659e-17, -8.74227766e-08, -1), Vector3.new(78.8499451, 23.4399948, 66.1099854))
      createWall(CFrame.new(329.510925, 21.1300583, 30.1253357, -1, -8.74227766e-08, 7.70258813e-15, -8.74227766e-08, 1, -8.74227766e-08, -5.98462659e-17, -8.74227766e-08, -1), Vector3.new(93.8499451, 24.4399948, 66.1099854))
      createWall(CFrame.new(-110.288849, 1.1410141, 231.444031, -4.37113883e-08, 0, 1, 0, 1, 0, -1, 0, -4.37113883e-08), Vector3.new(51.1999512, 23.9399948, 37.6900024))
      createWall(CFrame.new(-112.038849, 0.891014099, 231.444031, -4.37113883e-08, 0, 1, 0, 1, 0, -1, 0, -4.37113883e-08), Vector3.new(51.1999512, 23.4399948, 41.1900024))
      createWall(CFrame.new(-245.053238, 24.6439991, -76.1922913, 0.131052777, 0.743242264, 0.656061411, -0.984807491, 0.173650265, -3.70293856e-06, -0.113928005, -0.646093667, 0.754707873), Vector3.new(4.34993744, 13.9399948, 22.9200001))
      createWall(CFrame.new(-219.118988, 16.1449757, -98.7366257, -0.342632473, 0.672451258, 0.656058371, -0.891007841, -0.453988045, -5.27128577e-06, 0.297839075, -0.58455497, 0.754710317), Vector3.new(4.34993744, 33.9399948, 22.9200001))
      createWall(CFrame.new(-235.20369, 24.6545467, -84.7544098, -0.118063509, 0.745420098, 0.656065226, -0.987691581, -0.156433806, -3.13296914e-06, 0.102626264, -0.647989988, 0.754713774), Vector3.new(4.59993744, 13.9399948, 22.9200001))
      createWall(CFrame.new(-254.772614, 20.8520355, -67.7679214, 0.335811794, 0.688516259, 0.642787576, -0.898794055, 0.438371211, -1.86264515e-09, -0.281779528, -0.577733696, 0.766044378), Vector3.new(3.09993744, 14.6899948, 22.9200001))
      if _G.destroy_map then
        workspace.Terrain:Clear()
        for i,v in pairs(workspace:GetChildren()) do
          if v.ClassName == "Model" or v.ClassName == "Part" or v.ClassName == "UnionOperation" or v.ClassName == "WedgePart" or v.Name == "MeshPart" then
            if v ~= game.Players.LocalPlayer.Character and v.Name ~= regionPartName and v.Name ~= "secondBossSafeSpots" and v.Name ~= "finalBossObjectSpawns" then
              v:Destroy()
            end
          end
        end
      end
    end

    function steamFix()
      createWall(CFrame.new(1598.42798, -10.4780731, -429.198364, 1, 0, 0, 0, 1, 0, 0, 0, 1), Vector3.new(2.5, 59, 146.5))
      createWall(CFrame.new(1487.67798, -10.4780731, -502.198364, 1, 0, 0, 0, 1, 0, 0, 0, 1), Vector3.new(224, 59, 0.5))
      createWall(CFrame.new(1488.92798, -10.4780731, -357.448364, 1, 0, 0, 0, 1, 0, 0, 0, 1), Vector3.new(221.5, 59, 7))
      createWall(CFrame.new(1388.92798, -40.2280731, -429.448364, 1, 0, 0, 0, 1, 0, 0, 0, 1), Vector3.new(44.5, 29.5, 151))
      createWall(CFrame.new(1431.1106, -53.0152588, -431.698364, 0.882947683, 0.469471514, 0, -0.469471514, 0.882947683, 0, 0, 0, 1), Vector3.new(62.5, 29.5, 31.5))
      createWall(CFrame.new(1326.0979, -27.7056007, -431.698364, 0.965927362, 0.258819342, 0, -0.258819342, 0.965927362, 0, 0, 0, 1), Vector3.new(155, 29.5, 31.5))
      createWall(CFrame.new(1316.12097, -7.95021439, -416.198364, 0.965927362, 0.258819342, 0, -0.258819342, 0.965927362, 0, 0, 0, 1), Vector3.new(125.5, 62.5, 0.5))
      createWall(CFrame.new(1316.84546, -8.14432907, -447.948364, 0.965927362, 0.258819342, 0, -0.258819342, 0.965927362, 0, 0, 0, 1), Vector3.new(127, 62.5, 3))
      createWall(CFrame.new(1171.92798, -8.22807312, -429.448364, 1, 0, 0, 0, 1, 0, 0, 0, 1), Vector3.new(165.5, 29.5, 151))
      createWall(CFrame.new(1171.92798, 9.52192688, -481.448364, 1, 0, 0, 0, 1, 0, 0, 0, 1), Vector3.new(165.5, 65, 47))
      createWall(CFrame.new(1171.92798, 9.52192688, -397.198364, 1, 0, 0, 0, 1, 0, 0, 0, 1), Vector3.new(165.5, 65, 10.5))
      createWall(CFrame.new(1088.17798, 9.52192688, -408.698364, 1, 0, 0, 0, 1, 0, 0, 0, 1), Vector3.new(5, 65, 33.5))
      createWall(CFrame.new(1088.92798, 9.52192688, -447.698364, 1, 0, 0, 0, 1, 0, 0, 0, 1), Vector3.new(3.5, 65, 22.5))
      createWall(CFrame.new(1059.92798, -3.47807312, -429.698364, 1, 0, 0, 0, 1, 0, 0, 0, 1), Vector3.new(61.5, 39, 58.5))
      createWall(CFrame.new(1034.92798, -7.47807312, -429.698364, 1, 0, 0, 0, 1, 0, 0, 0, 1), Vector3.new(111.5, 31, 94.5))
      createWall(CFrame.new(1019.40039, -7.82135487, -430.448364, 0.866025388, -0.5, 0, 0.5, 0.866025388, 0, 0, 0, 1), Vector3.new(40.5, 31.5, 28))
      createWall(CFrame.new(978.677979, 0.27192688, -429.698364, 1, 0, 0, 0, 1, 0, 0, 0, 1), Vector3.new(2, 14.5, 94.5))
      createWall(CFrame.new(977.927979, 0.0219268799, -429.698364, 1, 0, 0, 0, 1, 0, 0, 0, 1), Vector3.new(2.5, 14, 94.5))
      createWall(CFrame.new(977.427979, -0.22807312, -429.698364, 1, 0, 0, 0, 1, 0, 0, 0, 1), Vector3.new(3.5, 13.5, 94.5))
      createWall(CFrame.new(960.427979, -13.4780731, -437.698364, 1, 0, 0, 0, 1, 0, 0, 0, 1), Vector3.new(37.5, 39, 161.5))
      createWall(CFrame.new(937.427979, -13.4780731, -481.198364, 1, 0, 0, 0, 1, 0, 0, 0, 1), Vector3.new(83.5, 39, 74.5))
      createWall(CFrame.new(937.427979, 8.27192688, -510.698364, 1, 0, 0, 0, 1, 0, 0, 0, 1), Vector3.new(83.5, 82.5, 15.5))
      createWall(CFrame.new(976.177979, 8.27192688, -489.198364, 1, 0, 0, 0, 1, 0, 0, 0, 1), Vector3.new(9, 82.5, 56.5))
      createWall(CFrame.new(975.927979, 8.27192688, -379.448364, 1, 0, 0, 0, 1, 0, 0, 0, 1), Vector3.new(8.5, 82.5, 39))
      createWall(CFrame.new(811.927979, -33.4780731, -435.948364, 1, 0, 0, 0, 1, 0, 0, 0, 1), Vector3.new(334.5, 2, 165))
      createWall(CFrame.new(947.677979, -27.1234665, -424.020416, 1, 0, 0, 0, 0.777145922, -0.629320383, 0, 0.629320383, 0.777145922), Vector3.new(63, 27, 72.5))
      createWall(CFrame.new(680.177979, -8.72807312, -364.198364, 1, 0, 0, 0, 1, 0, 0, 0, 1), Vector3.new(71, 51.5, 32.5))
      createWall(CFrame.new(679.927979, -9.72807312, -493.948364, 1, 0, 0, 0, 1, 0, 0, 0, 1), Vector3.new(70.5, 49.5, 31))
      createWall(CFrame.new(644.177979, -16.4780731, -461.448364, 1, 0, 0, 0, 1, 0, 0, 0, 1), Vector3.new(4, 36, 35))
      createWall(CFrame.new(644.177979, -16.4780731, -395.948364, 1, 0, 0, 0, 1, 0, 0, 0, 1), Vector3.new(4, 36, 38))
      createWall(CFrame.new(597.093445, -20.3076077, -428.198364, 0.965925813, 0.258819044, 0, -0.258819044, 0.965925813, 0, 0, 0, 1), Vector3.new(129, 2, 35.5))
      createWall(CFrame.new(398.177979, -18.7280731, -428.198364, 1, 0, 0, 0, 1, 0, 0, 0, 1), Vector3.new(277, 31.5, 103.5))
      createWall(CFrame.new(496.177979, 1.77192688, -377.948364, 1, 0, 0, 0, 1, 0, 0, 0, 1), Vector3.new(81, 72.5, 3))
      createWall(CFrame.new(496.177979, 1.77192688, -480.698364, 1, 0, 0, 0, 1, 0, 0, 0, 1), Vector3.new(81, 72.5, 3.5))
      createWall(CFrame.new(467.177979, 1.77192688, -459.948364, 1, 0, 0, 0, 1, 0, 0, 0, 1), Vector3.new(5, 72.5, 45))
      createWall(CFrame.new(467.177979, 1.77192688, -399.948364, 1, 0, 0, 0, 1, 0, 0, 0, 1), Vector3.new(5, 72.5, 39))
      createWall(CFrame.new(589.427979, 1.77192688, -397.448364, 1, 0, 0, 0, 1, 0, 0, 0, 1), Vector3.new(111.5, 72.5, 34))
      createWall(CFrame.new(589.427979, 1.77192688, -466.948364, 1, 0, 0, 0, 1, 0, 0, 0, 1), Vector3.new(111.5, 72.5, 46))
      createWall(CFrame.new(351.927979, -3.47807312, -464.948364, 1, 0, 0, 0, 1, 0, 0, 0, 1), Vector3.new(221.5, 62, 30))
      createWall(CFrame.new(260.677979, -18.4780731, -428.198364, 1, 0, 0, 0, 1, 0, 0, 0, 1), Vector3.new(2, 32, 103.5))
      createWall(CFrame.new(249.677979, -17.9780731, -428.198364, 1, 0, 0, 0, 1, 0, 0, 0, 1), Vector3.new(21, 33, 103.5))
      createWall(CFrame.new(249.677979, -7.97807312, -428.198364, 1, 0, 0, 0, 1, 0, 0, 0, 1), Vector3.new(19, 15, 103.5))
      createWall(CFrame.new(249.677979, -7.47807312, -438.698364, 1, 0, 0, 0, 1, 0, 0, 0, 1), Vector3.new(16, 16, 82.5))
      createWall(CFrame.new(234.190384, -24.4961605, -428.198364, 0.848048091, -0.529919267, 0, 0.529919267, 0.848048091, 0, 0, 0, 1), Vector3.new(33, 33, 103.5))
      createWall(CFrame.new(115.927979, -27.2280731, -296.698364, 1, 0, 0, 0, 1, 0, 0, 0, 1), Vector3.new(292.5, 38.5, 396.5))
      createWall(CFrame.new(41.9279785, -22.7280731, -25.4483643, 1, 0, 0, 0, 1, 0, 0, 0, 1), Vector3.new(56.5, 47.5, 147))
      createWall(CFrame.new(69.1779785, 11.0219269, 10.3016357, 1, 0, 0, 0, 1, 0, 0, 0, 1), Vector3.new(2, 54, 75.5))
      createWall(CFrame.new(18.4279785, 11.0219269, 10.0516357, 1, 0, 0, 0, 1, 0, 0, 0, 1), Vector3.new(0.5, 54, 76))
      createWall(CFrame.new(44.1779785, 11.0219269, 43.3016357, 1, 0, 0, 0, 1, 0, 0, 0, 1), Vector3.new(52, 54, 9.5))
      createWall(CFrame.new(43.1779785, -8.81507015, -108.920464, 1, 0, 0, 0, 0.906307936, 0.4226183, 0, -0.4226183, 0.906307936), Vector3.new(33, 9, 29))
      createWall(CFrame.new(915.927979, -13.4780731, -419.948364, 1, 0, 0, 0, 1, 0, 0, 0, 1), Vector3.new(1.5, 39, 50))
      createWall(CFrame.new(1105.50012, 1.51558495, -430.948364, 0.838670552, 0.544639051, 0, -0.544639051, 0.838670552, 0, 0, 0, 1), Vector3.new(40.5, 8.5, 12))
      createWall(CFrame.new(1258.92798, 9.52192688, -475.698364, 1, 0, 0, 0, 1, 0, 0, 0, 1), Vector3.new(13.5, 65, 58.5))
      createWall(CFrame.new(1259.17798, 9.52192688, -409.448364, 1, 0, 0, 0, 1, 0, 0, 0, 1), Vector3.new(14, 65, 14))
      createWall(CFrame.new(1421.67798, -37.7280731, -416.198364, 1, 0, 0, 0, 1, 0, 0, 0, 1), Vector3.new(31, 34.5, 0.5))
      createWall(CFrame.new(1421.67798, -38.4780731, -447.698364, 1, 0, 0, 0, 1, 0, 0, 0, 1), Vector3.new(31, 33, 0.5))
      createWall(CFrame.new(942.427979, 25.0219269, -440.073364, 1, 0, 0, 0, 1, 0, 0, 0, 1), Vector3.new(1.5, 39, 10.75))
      createWall(CFrame.new(1370.17798, -24.7280731, -383.448364, 1, 0, 0, 0, 1, 0, 0, 0, 1), Vector3.new(7, 60.5, 59))
      createWall(CFrame.new(1371.92798, -24.7280731, -475.948364, 1, 0, 0, 0, 1, 0, 0, 0, 1), Vector3.new(10.5, 60.5, 60))
      createWall(CFrame.new(1059.42798, 3.02192688, -401.698364, 1, 0, 0, 0, 1, 0, 0, 0, 1), Vector3.new(99.5, 52, 47.5))
      createWall(CFrame.new(1059.17798, 3.02192688, -449.948364, 1, 0, 0, 0, 1, 0, 0, 0, 1), Vector3.new(99, 52, 26))
      wait(.1)
      if _G.destroy_map then
        local t = waitForExist(workspace, "borders")
        for i,v in pairs(t:GetChildren()) do
          cs:AddTag(v, "RayWhitelist")
        end
        workspace.Terrain:Clear()
        for i,v in pairs(workspace:GetChildren()) do
          if v.ClassName == "Model" or v.ClassName == "Part" or v.ClassName == "UnionOperation" or v.ClassName == "WedgePart" or v.Name == "MeshPart" then
            if v ~= game.Players.LocalPlayer.Character and v.Name ~= regionPartName then
              v:Destroy()
            end
          end
        end
      end
    end

    function ghastlyFix()
      _G.smallTeleportVal = 100
      _G.smallTeleports = true 
      _G.teleportDuringBossOnly = false
      createWall(CFrame.new(314.997986, 164.955307, 141.573303, 0.969875216, 0, 0.243605107, 0, 1.00000072, 0, -0.243605226, 0, 0.96987462), Vector3.new(47.75, 1.75, 32.25))
      createWall(CFrame.new(330.773529, 164.955322, 178.724518, 0.847127557, 0, 0.531389952, 0, 1.00000024, 0, -0.531390011, 0, 0.847127378), Vector3.new(35.25, 1.75, 66.5))
      createWall(CFrame.new(291.867157, 164.455322, 192.210632, 0.847127557, 0, 0.531389952, 0, 1.00000024, 0, -0.531390011, 0, 0.847127378), Vector3.new(45.5, 0.75, 28.5))
      createWall(CFrame.new(314.526306, 166.267242, 122.420898, 0.999228716, 0.0203912593, 0.0335599519, 8.98155777e-05, 0.853422642, -0.521219611, -0.0392691493, 0.520820618, 0.852762461), Vector3.new(31.25, 5.75, 11))
      createWall(CFrame.new(309.891113, 205.179276, -100.146835, 0.995393157, 1.86264515e-09, 0.0958794728, 0, 1.00000012, -2.98023224e-08, -0.0958794951, 0, 0.995392919), Vector3.new(44, 6, 43.25))
      createWall(CFrame.new(310.046906, 204.929276, -98.5293198, 0.995393157, 1.86264515e-09, 0.0958794728, 0, 1.00000012, -2.98023224e-08, -0.0958794951, 0, 0.995392919), Vector3.new(44, 5.5, 46.5))
      createWall(CFrame.new(312.679291, 209.306335, -100.399132, 0.95375818, 0.156644791, 0.256531715, 2.63154507e-05, 0.853422999, -0.521219373, -0.300576419, 0.497123897, 0.813954473), Vector3.new(60.25, 2, 15))
      createWall(CFrame.new(288.865051, 212.591721, -123.438225, 0.948331475, 9.31322575e-10, 0.317283809, -1.49011612e-08, 1.00000048, -2.98023224e-08, -0.317284107, 0, 0.948330641), Vector3.new(71.25, 2.75, 46.5))
      createWall(CFrame.new(271.416656, 208.042877, -149.974716, 0.963662565, -0.133397385, 0.231429577, -2.28088975e-05, 0.866338432, 0.499457479, -0.267122626, -0.481313825, 0.834854841), Vector3.new(44.25, 2.5, 18.75))
      createWall(CFrame.new(317.858276, 226.091736, -141.969772, 0.902594805, -1.11274026e-07, 0.430492133, -6.26038599e-08, 1.00000179, -1.56817535e-07, -0.430491447, -1.11401803e-07, 0.902596354), Vector3.new(14.5, 26.75, 20.25))
      createWall(CFrame.new(327.610962, 226.091751, -128.030334, 0.713265777, -3.46563553e-07, 0.700896978, -2.28876587e-07, 1.00000536, -4.53092753e-07, -0.700894475, -3.37397211e-07, 0.713270009), Vector3.new(14.5, 26.75, 20.25))
      createWall(CFrame.new(299.221466, 219.653625, -171.897232, 0.999782085, -1.21432961e-07, 0.0208872557, -1.15081804e-07, 1.00000358, -3.05271271e-07, -0.0208872557, -3.02800913e-07, 0.999785483), Vector3.new(22.25, 41.75, 50.249836))
      createWall(CFrame.new(302.612976, 218.403732, -206.136353, 0.914973915, 3.57694532e-08, -0.403517187, -2.30164034e-07, 1.00000715, -6.10544703e-07, 0.403514266, -6.51506639e-07, 0.914980114), Vector3.new(18, 41, 29.249836))
      createWall(CFrame.new(326.326263, 224.250214, -238.250687, 0.697180986, 1.19631932e-06, -0.716895223, -4.60329346e-07, 1, 1.22108031e-06, 0.716895163, -5.21306106e-07, 0.697180986), Vector3.new(15.5, 41, 52.499836))
      createWall(CFrame.new(273.453644, 206.549149, -171.125031, 0.999962032, 0, 0.00871858001, -1.49011612e-08, 1.00000012, -8.94069672e-08, -0.00871856511, -2.98023224e-08, 0.999962091), Vector3.new(43.5, 1.5, 45.25))
      createWall(CFrame.new(276.836884, 203.299271, -199.41629, 0.999660194, -0.0130174877, 0.0225868188, -3.66615131e-06, 0.866337717, 0.499459028, -0.026069466, -0.499289542, 0.866043389), Vector3.new(48.75, 0.75, 14))
      createWall(CFrame.new(278.942017, 199.432602, -215.061096, 0.917066813, 7.4505806e-08, -0.398734063, -2.79396772e-08, 1.00000048, -2.38418579e-07, 0.398733914, -2.38418579e-07, 0.917067349), Vector3.new(39, 2.75, 44.25))
      createWall(CFrame.new(289.955353, 198.776428, -221.000946, 0.771579385, -0.317793787, -0.551065564, 0.000133678317, 0.866355062, -0.499431521, 0.636133432, 0.385276377, 0.668504), Vector3.new(52, 0.749944925, 32.75))
      createWall(CFrame.new(310.594818, 206.462585, -252.894989, 0.675608575, 6.66826963e-07, -0.737262726, -1.34110451e-07, 1.00000179, -1.01327896e-06, 0.737261295, -8.04662704e-07, 0.675610304), Vector3.new(52, 1.24994493, 49))
      createWall(CFrame.new(69.4087906, 144.00502, -171.119354, 0.99996233, -5.89203459e-08, 0.00871866941, -5.46784662e-08, 1.00000095, -4.86772592e-07, -0.0087184906, -4.86277315e-07, 0.999963284), Vector3.new(43.75, 3.75, 49))
      createWall(CFrame.new(52.5376968, 153.755035, -170.597244, 0.99996233, -5.89203459e-08, 0.00871866941, -5.46784662e-08, 1.00000095, -4.86772592e-07, -0.0087184906, -4.86277315e-07, 0.999963284), Vector3.new(10, 23.25, 48.25))
      createWall(CFrame.new(64.1473999, 141.698074, -201.493713, 0.999660909, -0.0130176228, 0.022584945, -2.62307003e-06, 0.86633873, 0.499459445, -0.0260674842, -0.499291092, 0.866045833), Vector3.new(29.5, 1.24981689, 14.25))
      createWall(CFrame.new(62.3234749, 137.645157, -210.031967, 0.837708116, -1.23679638e-06, 0.546123624, -2.17929482e-07, 1.00000381, -1.90734863e-06, -0.546121001, -1.4603138e-06, 0.837710857), Vector3.new(38.25, 3.49981689, 32.5))
      createWall(CFrame.new(-166.044968, 37.7829933, 287.729126, 0.0175017715, -2.39997362e-23, 0.999847293, 2.16954798e-23, 1, -2.43831762e-23, -0.999847054, -2.21189041e-23, 0.0175016522), Vector3.new(119.25, 16.2497978, 131.25))
      createWall(CFrame.new(26.7727909, 131.330139, -229.596436, 0.498491108, -1.49011612e-08, 0.866894901, 0, 1, -2.98023224e-08, -0.86689496, -2.98023224e-08, 0.498491049), Vector3.new(49.75, 3.74981594, 60.25))
      createWall(CFrame.new(52.0516853, 155.705139, -223.206177, 0.828062892, -2.11616907e-07, 0.560636103, 4.75783892e-08, 1, -2.57120234e-07, -0.560636997, -1.33975519e-07, 0.828062534), Vector3.new(38.25, 44.9998169, 3.75))
      createWall(CFrame.new(104.046776, 139.162552, -171.938599, 0.986322045, -0.164742291, 0.00536258006, 0.164738536, 0.986336589, 0.00113770308, -0.00547673693, -0.000238718087, 0.99998498), Vector3.new(32.0000076, 16.1000004, 19.6999855))
      createWall(CFrame.new(181.243668, 158.680099, -172.372742, 0.942704737, -0.333585948, 0.0053159981, 0.333584517, 0.94271946, 0.00117557438, -0.00540364953, 0.00066511496, 0.999985158), Vector3.new(27.6000061, 18.1999969, 19.6999855))
      createWall(CFrame.new(131.853058, 145.830246, -172.094543, 0.976343989, -0.216156989, 0.0053403331, 0.216153711, 0.976358593, 0.00119193445, -0.00547172502, -9.40531027e-06, 0.999985039), Vector3.new(25.4000072, 14.2999983, 19.6999855))
      createWall(CFrame.new(318.447052, 163.461685, 37.7652664, 0.999982238, 0.000530938152, 0.0059381309, 1.35496957e-05, 0.995821595, -0.0913198441, -0.00596180419, 0.0913182944, 0.995803893), Vector3.new(16.2999992, 19.3199978, 41.7999878))
      createWall(CFrame.new(318.052277, 174.400818, -28.883812, 0.999982417, 0.00173310237, 0.00567422993, 2.61646928e-05, 0.955086589, -0.296326905, -0.00593294576, 0.296321839, 0.955069721), Vector3.new(16.2999992, 26.0899982, 41.7999878))
      createWall(CFrame.new(226.274368, 183.300385, -172.641464, 0.870467842, -0.492196739, 0.00530316494, 0.492197692, 0.870482564, 0.00121696084, -0.00521529652, 0.00155088026, 0.999985218), Vector3.new(25.4000072, 11.5999985, 19.6999855))
      createWall(CFrame.new(152.616531, 158.295456, -172.219894, 0.958893836, -0.283715218, 0.005320244, 0.283712894, 0.958908498, 0.00120666309, -0.0054439758, 0.000352359959, 0.999985099), Vector3.new(170.769989, 20.6599998, 19.6999855))
      createWall(CFrame.new(318.252289, 167.785767, 4.91963005, 0.999982595, 0.00117594865, 0.00578253064, -2.67500873e-05, 0.980835259, -0.194838986, -0.00590083003, 0.194835439, 0.980818212), Vector3.new(16.2999992, 21.3699989, 41.7999878))
      createWall(CFrame.new(244.598236, 195.088745, -172.753021, 0.824243903, -0.566209912, 0.00532178301, 0.566212296, 0.824258626, 0.00119986106, -0.00506589841, 0.00202428014, 0.999985099), Vector3.new(25.4000072, 11.2999992, 19.6999855))
      createWall(CFrame.new(203.613464, 171.606827, -172.507065, 0.917157352, -0.398489952, 0.00530689815, 0.398489475, 0.917172134, 0.00119122909, -0.00534203229, 0.00102219847, 0.999985218), Vector3.new(25.4000072, 11.8999987, 19.6999855))
      createWall(CFrame.new(317.851074, 185.098953, -62.7725983, 0.999982536, 0.00234849169, 0.00542167015, -1.89922284e-05, 0.918884039, -0.394527793, -0.00590843149, 0.394520819, 0.918868005), Vector3.new(16.2999992, 29.8699989, 41.7999878))
      createWall(CFrame.new(313.591675, 164.848785, 87.4919815, 0.999982238, 1.23396703e-05, 0.00595618133, 1.23396703e-05, 0.999991417, -0.00414342992, -0.00595618133, 0.00414342992, 0.999973655), Vector3.new(26.6000271, 12.3999996, 63.6499863))
      createWall(CFrame.new(313.780762, 164.967224, 119.242188, 0.999982238, 1.23396703e-05, 0.00595618133, 1.23396703e-05, 0.999991417, -0.00414342992, -0.00595618133, 0.00414342992, 0.999973655), Vector3.new(26.6000271, 12.8999996, 1.64998627))
      createWall(CFrame.new(360.600037, 217.278778, 183.034668, -0.66911006, 0, 0.743163466, 0, 1, 0, -0.743163466, 0, -0.66911006), Vector3.new(77.5999832, 140.259995, 5.57999849))
      createWall(CFrame.new(329.736298, 201.704147, 121.851646, 0.990270376, 0, 0.13915664, 0, 1, 0, -0.13915664, 0, 0.990270376), Vector3.new(8.30997372, 92.3699722, 7.27999878))
      createWall(CFrame.new(336.563782, 201.704147, 98.0409088, 0.961273968, -0, -0.275594592, 0, 1, -0, 0.275594592, 0, 0.961273968), Vector3.new(8.30997372, 92.3699722, 49.2699966))
      createWall(CFrame.new(336.604401, 225.51413, 1.04374969, 1, 0, 0, 0, 1, 0, 0, 0, 1), Vector3.new(22.5599785, 139.98996, 158.379974))
      createWall(CFrame.new(291.936859, 201.704147, 117.422958, 1, 0, 0, 0, 1, 0, 0, 0, 1), Vector3.new(22.5599785, 92.3699722, 85.6899643))
      createWall(CFrame.new(325.460632, 217.398804, 205.506134, 0.601813793, -0, -0.798636556, 0, 1, -0, 0.798636556, 0, 0.601813793), Vector3.new(31.1900005, 140.5, 5.57999849))
      createWall(CFrame.new(356.861755, 217.278778, 201.473495, 0.79861635, 0, 0.601840496, 0, 1, 0, -0.601840496, 0, 0.79861635), Vector3.new(52.8799973, 140.259995, 5.57999849))
      createWall(CFrame.new(332.964478, 201.704147, 137.253326, 0.139203906, -0, -0.99026376, 0, 1, -0, 0.99026376, 0, 0.139203906), Vector3.new(37.4799767, 92.3699722, 5.57999849))
      createWall(CFrame.new(299.712402, 225.474121, 0.448717952, 1, 0, 0, 0, 1, 0, 0, 0, 1), Vector3.new(22.5599785, 139.909927, 154.210022))
      createWall(CFrame.new(268.070129, 201.704147, 200.553894, 0.829036474, 0, 0.559194624, 0, 1, 0, -0.559194624, 0, 0.829036474), Vector3.new(4.10997677, 92.3699722, 43.399971))
      createWall(CFrame.new(-3.77216744, 81.1528473, -397.064117, 0.987685978, 0, 0.156449571, 0, 1, 0, -0.156449571, 0, 0.987685978), Vector3.new(26.0000801, 131.969925, 144.389969))
      createWall(CFrame.new(-417.882141, 71.6578674, -111.429916, 0.956294656, 0, 0.292404652, 0, 1, 0, -0.292404652, 0, 0.956294656), Vector3.new(12.0600824, 112.979919, 155.639954))
      createWall(CFrame.new(89.2471313, 201.152954, -201.564957, 0, 0, -1, 0, 1, 0, 1, 0, 0), Vector3.new(12.8600912, 155.529922, 27.2199631))
      createWall(CFrame.new(-322.662384, 71.6578674, -175.193466, 0.970287263, 0, 0.241955817, 0, 1, 0, -0.241955817, 0, 0.970287263), Vector3.new(52.1000938, 112.979919, 26.0899544))
      createWall(CFrame.new(-125.327179, 150.609619, 448.347321, 0, 1, 0, 1, 0, 0, 0, 0, -1), Vector3.new(110.670059, 16.2098866, 21.2899628))
      createWall(CFrame.new(278.299347, 240.282928, -82.8367004, -0.965929747, 0, -0.258804798, 0, 1, 0, 0.258804798, 0, -0.965929747), Vector3.new(26.6800213, 77.2699661, 29.6099987))
      createWall(CFrame.new(268.070129, 201.704147, 200.553894, 0.829036474, 0, 0.559194624, 0, 1, 0, -0.559194624, 0, 0.829036474), Vector3.new(4.10997677, 92.3699722, 43.399971))
      createWall(CFrame.new(321.441681, 258.039154, -126.414459, -0.406715393, 0, 0.913554907, 0, 1, 0, -0.913554907, 0, -0.406715393), Vector3.new(129.209961, 9.13999081, 34.7499962))
      createWall(CFrame.new(136.824524, 71.6578674, -210.560226, 0.788016856, -0, -0.615653694, 0, 1, -0, 0.615653694, 0, 0.788016856), Vector3.new(23.9600925, 112.979919, 112.829971))
      createWall(CFrame.new(280.31485, 201.704147, 174.340118, 0.829036474, 0, 0.559194624, 0, 1, 0, -0.559194624, 0, 0.829036474), Vector3.new(53.7299843, 92.3699722, 13.6299658))
      createWall(CFrame.new(-42.6308556, 83.3778839, -423.266296, 0.987685978, 0, 0.156449571, 0, 1, 0, -0.156449571, 0, 0.987685978), Vector3.new(55.3900757, 136.419937, 3.29997849))
      createWall(CFrame.new(253.593842, 201.152954, -198.05365, -0.999848366, 0, 0.017436387, 0, 1, 0, -0.017436387, 0, -0.999848366), Vector3.new(7.96000004, 155.529922, 9.87997532))
      createWall(CFrame.new(80.389328, 130.517944, -178.993362, 0.587748766, -0, -0.809043527, 0, 1, -0, 0.809043527, 0, 0.587748766), Vector3.new(84.3001022, 14.2599249, 27.2500114))
      createWall(CFrame.new(-56.7383423, 82.0228577, -388.675171, 0.987685978, 0, 0.156449571, 0, 1, 0, -0.156449571, 0, 0.987685978), Vector3.new(16.700079, 133.709915, 144.389969))
      createWall(CFrame.new(-90.3630447, 71.6578674, -322.139832, 0.999847949, -0, -0.017436387, 0, 1, -0, 0.017436387, 0, 0.999847949), Vector3.new(76.3400879, 112.979919, 10.0999537))
      createWall(CFrame.new(-269.883667, 71.6578674, -211.016266, 0.933587551, 0, 0.358349502, 0, 1, 0, -0.358349502, 0, 0.933587551), Vector3.new(28.4701061, 112.979919, 26.0899544))
      createWall(CFrame.new(66.7276688, 201.152954, -145.322754, -1, 0, 0, 0, 1, 0, 0, 0, -1), Vector3.new(65.3700638, 155.529922, 7.01998234))
      createWall(CFrame.new(147.480667, 71.6578674, -481.844696, 0.981621504, -0, -0.190838262, 0, 1, -0, 0.190838262, 0, 0.981621504), Vector3.new(84.450058, 112.979919, 15.2799673))
      createWall(CFrame.new(171.137604, 201.152954, -190.154861, -1, 0, 0, 0, 1, 0, 0, 0, -1), Vector3.new(161.15007, 155.529922, 20.5299816))
      createWall(CFrame.new(289.106201, 199.204453, -237.240112, -0.681973696, 0, 0.731376648, 0, 1, 0, -0.731376648, 0, -0.681973696), Vector3.new(46.5600014, 1.63998556, 20.0499992))
      createWall(CFrame.new(46.1648331, 170.712921, -244.133514, 0.933587551, -0, -0.358349502, 0, 1, -0, 0.358349502, 0, 0.933587551), Vector3.new(48.9500923, 94.6499176, 9.41996288))
      createWall(CFrame.new(32.8624992, 71.6578674, -504.092804, 0.981621504, -0, -0.190838262, 0, 1, -0, 0.190838262, 0, 0.981621504), Vector3.new(84.450058, 112.979919, 15.2799673))
      createWall(CFrame.new(171.137604, 201.152954, -154.059052, -1, 0, 0, 0, 1, 0, 0, 0, -1), Vector3.new(161.15007, 155.529922, 20.5299816))
      createWall(CFrame.new(56.9643517, 128.217972, -214.544128, 0.587748766, -0, -0.809043527, 0, 1, -0, 0.809043527, 0, 0.587748766), Vector3.new(21.7401257, 9.65992451, 31.1400127))
      createWall(CFrame.new(78.888588, 201.152954, -216.94101, 0.544665456, -0, -0.838653445, 0, 1, -0, 0.838653445, 0, 0.544665456), Vector3.new(23.9600925, 155.529922, 9.41996288))
      createWall(CFrame.new(201.904037, 81.967865, -316.362091, 0.788016856, -0, -0.615653694, 0, 1, -0, 0.615653694, 0, 0.788016856), Vector3.new(51.6700859, 133.59993, 141.20993))
      createWall(CFrame.new(-151.983612, 71.6578674, -307.082306, 0.829036474, 0, 0.559194624, 0, 1, 0, -0.559194624, 0, 0.829036474), Vector3.new(100.530083, 112.979919, 10.0999537))
      createWall(CFrame.new(-211.735306, 71.6578674, -241.287537, 0.469467044, 0, 0.882950008, 0, 1, 0, -0.882950008, 0, 0.469467044), Vector3.new(89.0900803, 112.979919, 10.0999537))
      createWall(CFrame.new(10.404254, 71.6578674, -235.046997, 0.984812498, 0, 0.173621148, 0, 1, 0, -0.173621148, 0, 0.984812498), Vector3.new(39.1400681, 112.979919, 31.4799538))
      createWall(CFrame.new(299.215668, 201.704147, 210.820496, 0.829036474, 0, 0.559194624, 0, 1, 0, -0.559194624, 0, 0.829036474), Vector3.new(53.7299843, 92.3699722, 13.6299658))
      createWall(CFrame.new(302.519348, 248.124329, -170.130829, 0.0175017118, 0, 0.999846935, 0, 1, 0, -0.999846935, 0, 0.0175017118), Vector3.new(53.5899887, 22.2499924, 36.8600044))
      createWall(CFrame.new(-72.5408325, 92.6578674, -226.426178, 0.999847949, 0, 0.017436387, 0, 1, 0, -0.017436387, 0, 0.999847949), Vector3.new(130.620087, 154.979904, 36.8499527))
      createWall(CFrame.new(37.5846519, 71.6578674, -237.363373, 0.999847949, -0, -0.017436387, 0, 1, -0, 0.017436387, 0, 0.999847949), Vector3.new(21.0300751, 112.979919, 29.3599606))
      createWall(CFrame.new(-239.524338, 71.6578674, -200.243027, 0.933587551, 0, 0.358349502, 0, 1, 0, -0.358349502, 0, 0.933587551), Vector3.new(28.4701061, 112.979919, 26.0899544))
      createWall(CFrame.new(-286.944824, 71.6578674, -186.516891, 0.90629667, 0, 0.422642082, 0, 1, 0, -0.422642082, 0, 0.90629667), Vector3.new(28.4701061, 112.979919, 26.0899544))
      createWall(CFrame.new(-390.022064, 71.6578674, -175.793915, 0.956294656, 0, 0.292404652, 0, 1, 0, -0.292404652, 0, 0.956294656), Vector3.new(86.9200897, 112.979919, 26.0899544))
      createWall(CFrame.new(296.471771, 209.142975, -107.708954, -0.951068401, 0, -0.308980465, 0, 1, 0, 0.308980465, 0, -0.951068401), Vector3.new(68.9400024, 8.52998447, 9.06999397))
      createWall(CFrame.new(27.5196838, 170.712921, -245.540726, 0.999847949, 0, 0.017436387, 0, 1, 0, -0.017436387, 0, 0.999847949), Vector3.new(48.9500923, 94.6499176, 9.41996288))
      createWall(CFrame.new(285.192871, 209.142975, -142.421982, -0.951068401, 0, -0.308980465, 0, 1, 0, 0.308980465, 0, -0.951068401), Vector3.new(68.9400024, 8.52998447, 9.06999397))
      createWall(CFrame.new(304.893066, 229.299469, -222.380829, -0.766061664, 0, 0.642767608, 0, 1, 0, -0.642767608, 0, -0.766061664), Vector3.new(6.65000296, 61.8299904, 10.8399925))
      createWall(CFrame.new(39.5098419, 201.152954, -171.609802, 0, 0, -1, 0, 1, 0, 1, 0, 0), Vector3.new(66.7700806, 155.529922, 28.3999786))
      createWall(CFrame.new(102.651863, 81.8628693, -404.385468, 0.981621504, -0, -0.190838262, 0, 1, -0, 0.190838262, 0, 0.981621504), Vector3.new(26.0000801, 133.389938, 184.459961))
      createWall(CFrame.new(334.250702, 259.569092, -104.673012, -0.173624277, 0, 0.984811902, 0, 1, 0, -0.984811902, 0, -0.173624277), Vector3.new(80.2499771, 208.099976, 9.06999397))
      createWall(CFrame.new(257.434692, 240.282928, -114.319412, -0.951068401, 0, -0.308980465, 0, 1, 0, 0.308980465, 0, -0.951068401), Vector3.new(7.70001984, 77.2699661, 45.7699966))
      createWall(CFrame.new(331.207611, 201.152954, -268.791962, -0.74314785, 0, -0.669127226, 0, 1, 0, 0.669127226, 0, -0.74314785), Vector3.new(7.96000004, 155.529922, 50.1699715))
      createWall(CFrame.new(259.305756, 201.152954, -219.461853, -0.906296611, 0, 0.422642082, 0, 1, 0, -0.422642082, 0, -0.906296611), Vector3.new(7.96000004, 155.529922, 52.3299637))
      createWall(CFrame.new(285.489746, 202.64946, -249.168152, -0.681973696, 0, 0.731376648, 0, 1, 0, -0.731376648, 0, -0.681973696), Vector3.new(68.9400024, 8.52998447, 9.06999397))
      createWall(CFrame.new(271.153839, 202.64946, -189.05751, -1, 0, 0, 0, 1, 0, 0, 0, -1), Vector3.new(68.9400024, 8.52998447, 9.06999397))
      createWall(CFrame.new(26.5978699, 178.708435, -202.503372, 0.469467044, 0, 0.882950008, 0, 1, 0, -0.882950008, 0, 0.469467044), Vector3.new(87.330101, 11.7599154, 70.6699524))
      createWall(CFrame.new(146.12854, 82.1978836, -359.938873, 0.788016856, -0, -0.615653694, 0, 1, -0, 0.615653694, 0, 0.788016856), Vector3.new(26.0000801, 134.059937, 141.20993))
      createWall(CFrame.new(296.637207, 201.152954, -266.805756, -0.66911006, 0, 0.743163466, 0, 1, 0, -0.743163466, 0, -0.66911006), Vector3.new(7.96000004, 155.529922, 50.1699715))
      createWall(CFrame.new(99.3139725, 71.6578674, -192.906723, 0.788016856, -0, -0.615653694, 0, 1, -0, 0.615653694, 0, 0.788016856), Vector3.new(61.3401108, 112.979919, 38.8199997))
      createWall(CFrame.new(275.48941, 201.152954, -246.046173, -0.731384635, 0, 0.681965172, 0, 1, 0, -0.681965172, 0, -0.731384635), Vector3.new(7.96000004, 155.529922, 10.8099756))
      createWall(CFrame.new(191.84343, 71.6578674, -519.669495, 0.981621504, 0, -0.190838262, 0, 1, 0, 0.190838262, 0, 0.981621504), Vector3.new(11.7900572, 112.979919, 106.469978))
      createWall(CFrame.new(8.56675243, 176.11792, -233.824677, 0.469467044, 0, 0.882950008, 0, 1, 0, -0.882950008, 0, 0.469467044), Vector3.new(48.9500923, 105.459915, 9.41996288))
      createWall(CFrame.new(4.76045275, 71.6578674, -554.318726, 0.981621504, 0, -0.190838262, 0, 1, 0, 0.190838262, 0, 0.981621504), Vector3.new(11.7900572, 112.979919, 103.099976))
      createWall(CFrame.new(336.604401, 238.509155, -76.2662277, 1, 0, 0, 0, 1, 0, 0, 0, 1), Vector3.new(22.5599785, 165.97998, 3.75999427))
      createWall(CFrame.new(103.385704, 71.6578674, -584.13147, 0.981621504, 0, -0.190838262, 0, 1, 0, 0.190838262, 0, 0.981621504), Vector3.new(192.360016, 112.979919, 6.27996731))
      createWall(CFrame.new(45.7099876, 82.1828537, -415.45401, 0.981621504, -0, -0.190838262, 0, 1, -0, 0.190838262, 0, 0.981621504), Vector3.new(26.0000801, 134.029907, 184.459961))
      createWall(CFrame.new(192.358246, 82.1778717, -374.678314, 0.788016856, -0, -0.615653694, 0, 1, -0, 0.615653694, 0, 0.788016856), Vector3.new(39.2300949, 134.019928, 6.05993652))
      createWall(CFrame.new(-353.975555, 71.6578674, -63.2335167, 0.956294656, 0, 0.292404652, 0, 1, 0, -0.292404652, 0, 0.956294656), Vector3.new(86.1100769, 112.979919, 26.0899544))
      createWall(CFrame.new(251.776321, 240.282928, -140.439316, -0.951068401, 0, -0.308980465, 0, 1, 0, 0.308980465, 0, -0.951068401), Vector3.new(13.0800266, 77.2699661, 10.5299988))
      createWall(CFrame.new(22.8892059, 108.482849, 344.445435, 0.515037358, -0, -0.857167721, 0, 1, -0, 0.857167721, 0, 0.515037358), Vector3.new(7.17007732, 196.649918, 88.9599533))
      createWall(CFrame.new(-189.411392, 115.27285, 512.67157, -0.74314785, 0, -0.669127226, 0, 1, 0, 0.669127226, 0, -0.74314785), Vector3.new(7.17007732, 210.229919, 107.459976))
      createWall(CFrame.new(3.59355736, 115.27285, 400.595734, 0.79861635, 0, 0.601840496, 0, 1, 0, -0.601840496, 0, 0.79861635), Vector3.new(20.2200737, 210.229919, 83.4799728))
      createWall(CFrame.new(-48.4561577, 115.27285, 524.388855, 0.994518042, -0, -0.104565002, 0, 1, -0, 0.104565002, 0, 0.994518042), Vector3.new(29.3600597, 210.229919, 38.3299599))
      createWall(CFrame.new(-217.117432, 108.482849, 331.702698, 0.788016856, 0, 0.615653694, 0, 1, 0, -0.615653694, 0, 0.788016856), Vector3.new(7.17007732, 196.649918, 65.809967))
      createWall(CFrame.new(-132.738174, 115.27285, 485.842224, -0.656062722, 0, -0.754706323, 0, 1, 0, 0.754706323, 0, -0.656062722), Vector3.new(15.610075, 210.229919, 80.2799683))
      createWall(CFrame.new(-114.245438, 115.27285, 502.964417, -0.656062722, 0, -0.754706323, 0, 1, 0, 0.754706323, 0, -0.656062722), Vector3.new(23.2500763, 210.229919, 18.7399883))
      createWall(CFrame.new(-181.212082, 108.482849, 455.194031, -0.978144407, 0, -0.207926437, 0, 1, 0, 0.207926437, 0, -0.978144407), Vector3.new(7.17007732, 196.649918, 28.6599598))
      createWall(CFrame.new(-171.409775, 108.482849, 480.494568, -0.866007447, 0, -0.500031412, 0, 1, 0, 0.500031412, 0, -0.866007447), Vector3.new(7.17007732, 196.649918, 28.6599598))
      createWall(CFrame.new(-153.358505, 108.482849, 499.273956, -0.529884458, 0, -0.848069847, 0, 1, 0, 0.848069847, 0, -0.529884458), Vector3.new(7.17007732, 196.649918, 28.6599598))
      createWall(CFrame.new(2.28053975, 191.96788, 412.527252, 0.965929627, 0, 0.258804798, 0, 1, 0, -0.258804798, 0, 0.965929627), Vector3.new(46.6800728, 51.1199303, 30.3899784))
      createWall(CFrame.new(-11.8301239, 69.1528625, -32.3248634, -0.190845728, 0, 0.981620014, 0, 1, 0, -0.981620014, 0, -0.190845728), Vector3.new(33.9601364, 117.989929, 43.3399582))
      createWall(CFrame.new(-5.22509098, 115.27285, 490.063293, 0.484826028, -0, -0.874610603, 0, 1, -0, 0.874610603, 0, 0.484826028), Vector3.new(20.2200737, 210.229919, 83.4799728))
      createWall(CFrame.new(-127.205185, 108.482849, 510.990234, -0.275688529, 0, -0.961247265, 0, 1, 0, 0.961247265, 0, -0.275688529), Vector3.new(8.14007759, 196.649918, 33.0399551))
      createWall(CFrame.new(-159.152649, 108.482849, 380.508484, -0.719358206, 0, 0.694639385, 0, 1, 0, -0.694639385, 0, -0.719358206), Vector3.new(7.17007732, 196.649918, 28.6599598))
      createWall(CFrame.new(-308.969879, 71.6578674, -94.8810577, 0.961249948, 0, 0.275678426, 0, 1, 0, -0.275678426, 0, 0.961249948), Vector3.new(27.9000931, 112.979919, 25.8499527))
      createWall(CFrame.new(-196.633072, 71.6578674, 20.2068882, -0.29242146, 0, 0.95628953, 0, 1, 0, -0.95628953, 0, -0.29242146), Vector3.new(3.35009265, 112.979919, 193.439865))
      createWall(CFrame.new(-64.1702118, 108.482849, 196.430222, 0.808997452, 0, 0.587812185, 0, 1, 0, -0.587812185, 0, 0.808997452), Vector3.new(7.17007732, 196.649918, 19.1599712))
      createWall(CFrame.new(21.93013, 115.27285, 434.743622, 0.965929627, 0, 0.258804798, 0, 1, 0, -0.258804798, 0, 0.965929627), Vector3.new(20.2200737, 210.229919, 83.4799728))
      createWall(CFrame.new(-33.0243149, 115.27285, 372.81546, 0.258864343, 0, 0.965913713, 0, 1, 0, -0.965913713, 0, 0.258864343), Vector3.new(20.2200737, 210.229919, 83.4799728))
      createWall(CFrame.new(-153.190704, 115.27285, 421.939972, -0.913549781, 0, 0.406727046, 0, 1, 0, -0.406727046, 0, -0.913549781), Vector3.new(20.2200737, 210.229919, 83.4799728))
      createWall(CFrame.new(-186.537735, 71.6578674, 55.9972839, -0.29242146, 0, 0.95628953, 0, 1, 0, -0.95628953, 0, -0.29242146), Vector3.new(6.85009241, 112.979919, 191.819916))
      createWall(CFrame.new(-102.091415, 108.482849, 351.480042, -0.374604106, 0, 0.92718488, 0, 1, 0, -0.92718488, 0, -0.374604106), Vector3.new(7.17007732, 196.649918, 105.239922))
      createWall(CFrame.new(-150.674164, 108.482849, 227.823898, 0.0175017118, 0, 0.999846935, 0, 1, 0, -0.999846935, 0, 0.0175017118), Vector3.new(1.08007801, 196.649918, 27.1100006))
      createWall(CFrame.new(2.66658545, 112.507874, 74.4540482, 0.0697871447, 0, 0.997561872, 0, 1, 0, -0.997561872, 0, 0.0697871447), Vector3.new(121.150146, 204.699951, 38.2499657))
      createWall(CFrame.new(-95.8713608, 108.482849, 212.595322, -0.642763734, 0, 0.766064942, 0, 1, 0, -0.766064942, 0, -0.642763734), Vector3.new(2.72007704, 196.649918, 74.0400085))
      createWall(CFrame.new(3.05939007, 111.247864, 1.23464596, -0.342042685, 0, 0.939684391, 0, 1, 0, -0.939684391, 0, -0.342042685), Vector3.new(106.420143, 202.179932, 38.2499657))
      createWall(CFrame.new(-296.766571, 71.6578674, -104.887527, 0.951068401, 0, 0.308980465, 0, 1, 0, -0.308980465, 0, 0.951068401), Vector3.new(21.460104, 112.979919, 5.02994967))
      createWall(CFrame.new(-136.902573, 115.27285, 400.373932, -0.587748766, 0, 0.809043527, 0, 1, 0, -0.809043527, 0, -0.587748766), Vector3.new(20.2200737, 210.229919, 83.4799728))
      createWall(CFrame.new(-126.523605, 71.6578674, -35.9618187, -0.515037298, 0, 0.857167721, 0, 1, 0, -0.857167721, 0, -0.515037298), Vector3.new(69.3901215, 112.979919, 10.0999537))
      createWall(CFrame.new(-107.43457, 108.482849, 200.957001, -0.642763734, 0, 0.766064942, 0, 1, 0, -0.766064942, 0, -0.642763734), Vector3.new(2.72007704, 196.649918, 81.4400024))
      createWall(CFrame.new(-156.125748, 115.27285, 447.67746, -0.961273909, 0, -0.275594592, 0, 1, 0, 0.275594592, 0, -0.961273909), Vector3.new(20.2200737, 210.229919, 83.4799728))
      createWall(CFrame.new(-84.8648453, 108.482849, 167.946167, 0.808997452, 0, 0.587812185, 0, 1, 0, -0.587812185, 0, 0.808997452), Vector3.new(7.17007732, 196.649918, 22.8599682))
      createWall(CFrame.new(-28.1472721, 112.442856, -60.752491, -0.573599219, 0, 0.81913656, 0, 1, 0, -0.81913656, 0, -0.573599219), Vector3.new(63.9601364, 204.569916, 38.2499657))
      createWall(CFrame.new(-75.1926804, 108.482849, 332.591461, -0.74314785, 0, 0.669127226, 0, 1, 0, -0.669127226, 0, -0.74314785), Vector3.new(8.96007824, 196.649918, 53.559948))
      createWall(CFrame.new(-275.843719, 71.6578674, 63.9708595, -0.29242146, 0, 0.95628953, 0, 1, 0, -0.95628953, 0, -0.29242146), Vector3.new(43.8200836, 112.979919, 32.2699165))
      createWall(CFrame.new(-90.2726288, 108.482849, 117.84272, 0.999391913, -0, -0.0348687991, 0, 1, -0, 0.0348687991, 0, 0.999391913), Vector3.new(7.17007732, 196.649918, 88.6899643))
      createWall(CFrame.new(-188.159439, 108.482849, 236.08194, -0.342042685, 0, 0.939684391, 0, 1, 0, -0.939684391, 0, -0.342042685), Vector3.new(7.17007732, 196.649918, 65.809967))
      createWall(CFrame.new(8.69923592, 108.482849, 164.62558, 0.0175017118, 0, 0.999846935, 0, 1, 0, -0.999846935, 0, 0.0175017118), Vector3.new(105.130081, 196.649918, 21.1499653))
      createWall(CFrame.new(-217.38678, 71.6578674, -120.78791, 0.981621504, 0, 0.190838262, 0, 1, 0, -0.190838262, 0, 0.981621504), Vector3.new(28.2900963, 112.979919, 25.8499527))
      createWall(CFrame.new(-177.051682, 71.6578674, -95.5953293, -0.731384635, 0, 0.681965172, 0, 1, 0, -0.681965172, 0, -0.731384635), Vector3.new(92.0400925, 112.979919, 10.0999537))
      createWall(CFrame.new(-91.2905579, 98.7878723, -180.786469, -0.642763734, 0, 0.766064942, 0, 1, 0, -0.766064942, 0, -0.642763734), Vector3.new(100.200134, 167.239929, 34.0199585))
      createWall(CFrame.new(-60.8750038, 104.102882, -118.505707, -0.970287442, 0, 0.241955817, 0, 1, 0, -0.241955817, 0, -0.970287442), Vector3.new(14.3101358, 177.869934, 52.2899513))
      createWall(CFrame.new(-81.9202881, 115.27285, 376.216888, -0.190845728, 0, 0.981620014, 0, 1, 0, -0.981620014, 0, -0.190845728), Vector3.new(20.2200737, 210.229919, 83.4799728))
      createWall(CFrame.new(14.3495579, 115.27285, 466.507202, 0.866007268, -0, -0.500031412, 0, 1, -0, 0.500031412, 0, 0.866007268), Vector3.new(20.2200737, 210.229919, 83.4799728))
      createWall(CFrame.new(16.8177929, 177.457901, 466.780548, 0.965929627, 0, 0.258804798, 0, 1, 0, -0.258804798, 0, 0.965929627), Vector3.new(46.6800728, 22.099926, 30.3899784))
      createWall(CFrame.new(-236.081604, 71.6578674, -107.771599, 0.951068401, 0, 0.308980465, 0, 1, 0, -0.308980465, 0, 0.951068401), Vector3.new(21.460104, 112.979919, 5.02994967))
      createWall(CFrame.new(-51.8448524, 113.727875, -79.1300812, -0.906296611, 0, 0.422642082, 0, 1, 0, -0.422642082, 0, -0.906296611), Vector3.new(63.9601364, 207.139954, 38.2499657))
      createWall(CFrame.new(11.4648485, 108.482849, 293.321198, -0.642763734, 0, -0.766064942, 0, 1, 0, 0.766064942, 0, -0.642763734), Vector3.new(7.17007732, 196.649918, 119.499962))
      createWall(CFrame.new(-37.7696838, 115.27285, 507.855652, 0.241953552, -0, -0.970287859, 0, 1, -0, 0.970287859, 0, 0.241953552), Vector3.new(26.7200642, 210.229919, 20.9799595))
      createWall(CFrame.new(-182.646271, 108.482849, 427.893585, -0.992540598, 0, 0.121917672, 0, 1, 0, -0.121917672, 0, -0.992540598), Vector3.new(7.17007732, 196.649918, 28.6599598))
      createWall(CFrame.new(-212.57103, 108.482849, 383.047607, -0.890994906, 0, 0.454013437, 0, 1, 0, -0.454013437, 0, -0.890994906), Vector3.new(7.17007732, 196.649918, 65.809967))
      createWall(CFrame.new(-219.156174, 115.27285, 442.736725, -0.997561932, 0, -0.0697919354, 0, 1, 0, 0.0697919354, 0, -0.997561932), Vector3.new(7.17007732, 210.229919, 84.3099747))
      createWall(CFrame.new(-47.2210999, 115.27285, 512.638611, 0.5592103, -0, -0.829025805, 0, 1, -0, 0.829025805, 0, 0.5592103), Vector3.new(29.3600597, 210.229919, 13.2199593))
      createWall(CFrame.new(-175.036667, 108.482849, 402.054779, -0.890994906, 0, 0.454013437, 0, 1, 0, -0.454013437, 0, -0.890994906), Vector3.new(7.17007732, 196.649918, 28.6599598))
      createWall(CFrame.new(-34.2681313, 108.482849, 220.731842, 0.601813793, 0, 0.798636556, 0, 1, 0, -0.798636556, 0, 0.601813793), Vector3.new(7.17007732, 196.649918, 65.809967))
      createWall(CFrame.new(-267.718323, 71.6578674, -106.124031, 0.933587551, 0, 0.358349502, 0, 1, 0, -0.358349502, 0, 0.933587551), Vector3.new(47.0600929, 112.979919, 25.8499527))
      createWall(CFrame.new(-79.1659088, 108.482849, 247.456345, 0.224959731, 0, 0.974368095, 0, 1, 0, -0.974368095, 0, 0.224959731), Vector3.new(2.72007704, 196.649918, 93.0200272))
      createWall(CFrame.new(-24.5546627, 153.542862, 346.573395, 0.309060872, 0, 0.951042235, 0, 1, 0, -0.951042235, 0, 0.309060872), Vector3.new(48.760067, 106.5299, 82.7499619))
      createWall(CFrame.new(-130.157043, 115.27285, 543.391418, -0.241953492, 0, -0.970287859, 0, 1, 0, 0.970287859, 0, -0.241953492), Vector3.new(7.17007732, 210.229919, 107.459976))
      createWall(CFrame.new(-62.0073128, 115.27285, 535.006409, 0.587748766, -0, -0.809043527, 0, 1, -0, 0.809043527, 0, 0.587748766), Vector3.new(13.5600739, 210.229919, 78.2199707))
      createWall(CFrame.new(1.19643378, 108.482849, 210.773438, 0.601813793, 0, 0.798636556, 0, 1, 0, -0.798636556, 0, 0.601813793), Vector3.new(55.8600845, 196.649918, 21.1499653))
      createWall(CFrame.new(-226.246323, 108.482849, 280.09845, 0.981621504, -0, -0.190838262, 0, 1, -0, 0.190838262, 0, 0.981621504), Vector3.new(7.17007732, 196.649918, 65.809967))
      createWall(CFrame.new(-93.2036362, 108.482849, 50.1853981, 0.984812498, 0, 0.173621148, 0, 1, 0, -0.173621148, 0, 0.984812498), Vector3.new(7.17007732, 196.649918, 49.9200096))
      createWall(CFrame.new(-99.4887619, 26.6458683, 204.488251, -0.642771602, -0.172286958, 0.74643296, 3.49506736e-05, 0.974375129, 0.224929258, -0.766058028, 0.144604191, -0.626294613), Vector3.new(17.6900787, 52.3899765, 81.5899811))
      createWall(CFrame.new(-90.5216141, 92.6578674, -212.284851, 0.999847949, 0, 0.017436387, 0, 1, 0, -0.017436387, 0, 0.999847949), Vector3.new(20.6700878, 154.979904, 64.4999695))
      createWall(CFrame.new(-69.007225, 150.609619, 414.444153, 0, 1, 0, 1, 0, 0, 0, 0, -1), Vector3.new(110.670059, 54.7698822, 46.6099701))
      createWall(CFrame.new(-17.0605316, 150.609619, 455.940033, 0, 1, 0, 1, 0, 0, 0, 0, -1), Vector3.new(110.670059, 16.2098866, 21.2899628))
      createWall(CFrame.new(44.4533386, 150.080139, -209.457306, 0.828062892, -2.11616907e-07, 0.560636103, 4.75783892e-08, 1, -2.57120234e-07, -0.560636997, -1.33975519e-07, 0.828062534), Vector3.new(10.25, 33.7498169, 18))
      createWall(CFrame.new(90.6520691, 55.3309364, -253.047241, 0.615655065, -8.31751947e-07, 0.788017154, -1.05084027e-07, 1, -9.73401143e-07, -0.78802079, -5.16469811e-07, 0.615655005), Vector3.new(112, 5.24979782, 111))
      createWall(CFrame.new(72.5854263, 90.4559326, -213.070435, 0.615655065, -8.31751947e-07, 0.788017154, -1.05084027e-07, 1, -9.73401143e-07, -0.78802079, -5.16469811e-07, 0.615655005), Vector3.new(26.75, 75.4998016, 90.25))
      createWall(CFrame.new(129.757416, 61.8308907, -222.495361, 0.615655065, -8.31751947e-07, 0.788017154, -1.05084027e-07, 1, -9.73401143e-07, -0.78802079, -5.16469811e-07, 0.615655005), Vector3.new(112, 18.2497978, 11.75))
      createWall(CFrame.new(151.133179, 61.8308983, -266.707794, 0.615655065, -8.31751947e-07, 0.788017154, -1.05084027e-07, 1, -9.73401143e-07, -0.78802079, -5.16469811e-07, 0.615655005), Vector3.new(16, 18.2497978, 32.5))
      createWall(CFrame.new(102.768631, 61.8309555, -304.493622, 0.615655065, -8.31751947e-07, 0.788017154, -1.05084027e-07, 1, -9.73401143e-07, -0.78802079, -5.16469811e-07, 0.615655005), Vector3.new(16, 18.2497978, 26.75))
      createWall(CFrame.new(85.0030518, 61.5809021, -314.366455, 0.190837413, -1.95113194e-06, 0.981623232, -2.10167372e-07, 1, -1.9468032e-06, -0.981629729, -1.65219262e-07, 0.190840572), Vector3.new(16.25, 19.2497978, 25.5))
      createWall(CFrame.new(27.7007961, 61.5810165, -325.506775, 0.190837413, -1.95113194e-06, 0.981623232, -2.10167372e-07, 1, -1.9468032e-06, -0.981629729, -1.65219262e-07, 0.190840572), Vector3.new(16.25, 19.2497978, 26.75))
      createWall(CFrame.new(7.84294891, 61.5429382, -322.138489, -0.156453863, -3.91142521e-06, 0.987685323, -4.20325563e-07, 1, 3.8936123e-06, -0.987685263, 1.94021311e-07, -0.156453878), Vector3.new(7.75, 19.2497978, 25.5))
      createWall(CFrame.new(-43.5881577, 67.4179993, -313.486664, -0.156449482, -3.69780161e-12, 0.987686753, 5.42860245e-13, 1, -3.65791512e-12, -0.9876858, 3.61038239e-14, -0.15644975), Vector3.new(8.25, 19.9997978, 14.25))
      createWall(CFrame.new(-87.1848373, 67.0428085, -313.408112, 0.0174364448, -7.29579678e-12, 0.999851346, 1.08572136e-12, 1, -7.31584064e-12, -0.999849319, -1.21311815e-12, 0.017436415), Vector3.new(7.25, 20.7497978, 75.5))
      createWall(CFrame.new(-156.584213, 67.3979263, -293.36441, -0.559194386, -6.6722218e-12, 0.829037786, 1.08572027e-12, 1, -7.31583284e-12, -0.829036236, 3.19087291e-12, -0.559195638), Vector3.new(7.5, 19.9997978, 71))
      createWall(CFrame.new(-203.402084, 67.4178085, -238.748154, -0.882949471, -8.786364e-12, 0.469468504, 2.17144011e-12, 1, -1.46316795e-11, -0.469466925, 1.18996219e-11, -0.882953048), Vector3.new(7, 19.9997978, 79.75))
      createWall(CFrame.new(-221.330124, 67.1680069, -201.287247, -0.358348906, -2.88762209e-11, 0.93359375, 4.34287719e-12, 1, -2.92634077e-11, -0.933586717, 6.43207146e-12, -0.358352125), Vector3.new(15, 19.9997978, 6.25))
      createWall(CFrame.new(-198.021118, 65.8308716, -124.031624, -0.309060812, -1.50344096e-17, 0.951042354, -1.75127433e-18, 1, -1.63774614e-17, -0.951042652, 6.72716669e-18, -0.309060782), Vector3.new(28, 27.7497978, 11.5))
      createWall(CFrame.new(-166.487717, 67.7930069, -97.6062241, -0.731385112, -1.97760074e-17, 0.681965232, -3.50254989e-18, 1, -3.27549229e-17, -0.681965768, 2.63450672e-17, -0.731384754), Vector3.new(82.75, 27.7497978, 7.25))
      createWall(CFrame.new(-119.565308, 67.7930069, -39.0402756, -0.515038013, -5.25450404e-17, 0.85716784, -7.00510723e-18, 1, -6.55098524e-17, -0.857169032, 3.97445693e-17, -0.515037596), Vector3.new(72, 27.7497978, 9.5))
      createWall(CFrame.new(-87.4858704, 62.2829895, 49.0097618, -0.173621446, -1.26597385e-16, 0.984812856, -1.40102294e-17, 1, -1.31019718e-16, -0.984815359, 3.65452431e-17, -0.173621505), Vector3.new(51.25, 27.7497978, 10))
      createWall(CFrame.new(-83.2823715, 63.5329895, 120.683098, 0.0348694921, -2.62857167e-16, 0.999392748, -2.80205249e-17, 1, -2.62039489e-16, -0.999397576, 1.88664826e-17, 0.0348683298), Vector3.new(96, 25.2497978, 7))
      createWall(CFrame.new(-78.467865, 63.5329933, 166.610886, -0.587812185, -1.65436123e-23, 0.808997571, 6.6174449e-24, 1, -1.4889251e-23, -0.808997512, -6.6174449e-24, -0.587812304), Vector3.new(18.5, 25.2497978, 4.75))
      createWall(CFrame.new(-60.2567482, 64.4079895, 191.676926, -0.587812245, -3.24787982e-23, 0.80899781, 2.16954798e-23, 1, -2.43831762e-23, -0.808997631, -3.21885739e-24, -0.587812483), Vector3.new(16.25, 24.4997978, 4.75))
      createWall(CFrame.new(-37.4936447, 64.6579895, 210.83847, -0.798636854, -6.40018756e-23, 0.60181427, 4.33909659e-23, 1, -4.87663651e-23, -0.601814091, 1.28333249e-23, -0.79863739), Vector3.new(43.75, 23.9997978, 4.75))
      createWall(CFrame.new(-313.654449, 46.2073135, -131.273331, -0.275637358, 0, 0.96126169, 0, 1, 0, -0.96126169, 0, -0.275637358), Vector3.new(110, 14.7497978, 208))
      createWall(CFrame.new(-165.12883, 54.2137146, 31.6172218, -0.294678897, 0, 0.955596387, 0, 1, 0, -0.955596209, 0, -0.294678926), Vector3.new(40.5, 2.24979782, 249.25))
      createWall(CFrame.new(-73.2428131, 56.4560051, -257.687622, 1, 0, 0, 0, 1, 0, 0, 0, 1), Vector3.new(290.25, 2.99979782, 126))
      createWall(CFrame.new(-112.780289, 56.830883, -107.574318, 0.857371926, 0, 0.514697373, 0, 1, 0, -0.514697313, 0, 0.857372046), Vector3.new(93, 2.24979782, 263.25))
      createWall(CFrame.new(-187.362808, 55.7058716, -134.105606, 0.95104146, 0, 0.309061378, 0, 1, 0, -0.309060663, 0, 0.951044798), Vector3.new(31.5, 4.49979782, 93.75))
      createWall(CFrame.new(-34.3526993, 56.1579857, 102.725609, 0.984812677, 1.29029866e-16, 0.173621446, -1.31019705e-16, 1.00000048, -3.97046694e-23, -0.173621535, -2.27477779e-17, 0.984813035), Vector3.new(110, 3.49979782, 231))
      createWall(CFrame.new(-69.5363007, 58.0819054, 176.25325, 0.788472474, 0.182033852, 0.587515831, -0.224951565, 0.974369884, -3.37541366e-07, -0.57245779, -0.132162333, 0.809212744), Vector3.new(16, 3.24977589, 25.75))
      createWall(CFrame.new(-97.6610107, 59.0887032, 8.19114017, 0.955596149, 6.10016286e-08, 0.294679552, 8.05594027e-08, 0.999999285, -1.49011612e-08, -0.294679046, -4.09781933e-08, 0.95559752), Vector3.new(16.5, 1.99977589, 36))
      createWall(CFrame.new(-97.7346802, 58.7137032, 7.95224094, 0.955596149, 6.10016286e-08, 0.294679552, 8.05594027e-08, 0.999999285, -1.49011612e-08, -0.294679046, -4.09781933e-08, 0.95559752), Vector3.new(20, 1.24977589, 40.5))
      createWall(CFrame.new(-97.6341782, 58.2137032, 7.00558901, 0.955596149, 6.10016286e-08, 0.294679552, 8.05594027e-08, 0.999999285, -1.49011612e-08, -0.294679046, -4.09781933e-08, 0.95559752), Vector3.new(24.25, 1.24977589, 43.75))
      createWall(CFrame.new(-113.563217, 56.2356071, 13.2257681, 0.89212507, -0.342453569, 0.294681668, 0.358367622, 0.933576107, -1.11758709e-07, -0.275106102, 0.10560298, 0.955603957), Vector3.new(11, 1.24977589, 43.75))
      createWall(CFrame.new(-223.621185, 51.8409386, -176.644882, 0.842409015, -0.48570472, 0.233319089, 0.499448329, 0.866343617, 0.000202953815, -0.202233106, 0.116359845, 0.972400308), Vector3.new(20.75, 6.74979782, 89))
      createWall(CFrame.new(-212.42215, 57.5808716, -169.559814, 0.951042056, 3.16649675e-08, 0.309060723, 1.11758709e-08, 0.99999994, -7.4505806e-09, -0.309060752, -1.49011612e-08, 0.951042473), Vector3.new(7.75, 4.24979782, 117))
      createWall(CFrame.new(-224.997284, 52.5610962, -177.975052, 0.811471164, -0.467886627, 0.350137621, 0.499437302, 0.866349936, 0.000212810439, -0.303441286, 0.174699053, 0.936698556), Vector3.new(17.75, 6.74979782, 32))
      createWall(CFrame.new(-210.638947, 57.2058716, -170.139297, 0.951042056, 3.16649675e-08, 0.309060723, 1.11758709e-08, 0.99999994, -7.4505806e-09, -0.309060752, -1.49011612e-08, 0.951042473), Vector3.new(7, 3.49979782, 117))
      createWall(CFrame.new(86.809967, 54.2058792, -434.137939, 0.188369185, 1.58486137e-12, 0.982098579, 4.9803499e-13, 1, 1.51822587e-12, -0.98209846, -2.03132501e-13, 0.188369095), Vector3.new(301, 3.49979782, 287.25))
      createWall(CFrame.new(52.8619156, 58.8309174, -320.487793, 0.190833777, -3.74184447e-06, 0.981622398, -4.20325563e-07, 1, 3.8936123e-06, -0.981622398, -1.15563375e-06, 0.190833792), Vector3.new(17, 1.74979782, 44))
      createWall(CFrame.new(54.4297676, 58.455925, -320.692352, 0.190833777, -3.74184447e-06, 0.981622398, -4.20325563e-07, 1, 3.8936123e-06, -0.981622398, -1.15563375e-06, 0.190833792), Vector3.new(22, 0.999797821, 47))
      createWall(CFrame.new(54.7160225, 57.205925, -322.164795, 0.190833777, -3.74184447e-06, 0.981622398, -4.20325563e-07, 1, 3.8936123e-06, -0.981622398, -1.15563375e-06, 0.190833792), Vector3.new(25, 1.49979782, 47))
      createWall(CFrame.new(55.0022812, 55.580925, -323.637238, 0.190833777, -3.74184447e-06, 0.981622398, -4.20325563e-07, 1, 3.8936123e-06, -0.981622398, -1.15563375e-06, 0.190833792), Vector3.new(28, 2.24979782, 47))
      createWall(CFrame.new(127.154045, 57.9558754, -280.683319, 0.615653574, 2.27373675e-13, 0.788017035, 1.13686838e-13, 1, 7.10542736e-14, -0.788017035, -2.27373675e-13, 0.615653574), Vector3.new(9, 3.99979782, 44))
      createWall(CFrame.new(129.044098, 56.8308754, -282.696472, 0.615653574, 2.27373675e-13, 0.788017035, 1.13686838e-13, 1, 7.10542736e-14, -0.788017035, -2.27373675e-13, 0.615653574), Vector3.new(20, 4.24979782, 50.5))
      createWall(CFrame.new(130.540146, 55.4558754, -285.017426, 0.615653574, 2.27373675e-13, 0.788017035, 1.13686838e-13, 1, 7.10542736e-14, -0.788017035, -2.27373675e-13, 0.615653574), Vector3.new(20, 4.49979782, 44))
      createWall(CFrame.new(132.079285, 54.8308754, -286.987457, 0.615653574, 2.27373675e-13, 0.788017035, 1.13686838e-13, 1, 7.10542736e-14, -0.788017035, -2.27373675e-13, 0.615653574), Vector3.new(25, 3.24979782, 44))
      createWall(CFrame.new(-20.4398537, 57.3308754, -317.710022, 0.984812856, 4.45411665e-13, 0.17362076, 4.3284457e-13, 1, 1.10245187e-13, -0.17362076, 3.34200441e-14, 0.984812677), Vector3.new(35.5, 4.74979782, 7.25))
      createWall(CFrame.new(-20.6999245, 56.9558754, -321.345093, 0.984812856, 4.45411665e-13, 0.17362076, 4.3284457e-13, 1, 1.10245187e-13, -0.17362076, 3.34200441e-14, 0.984812677), Vector3.new(53.75, 3.99979782, 20.5))
      createWall(CFrame.new(-21.2862549, 55.5808754, -322.510986, 0.984812856, 4.45411665e-13, 0.17362076, 4.3284457e-13, 1, 1.10245187e-13, -0.17362076, 3.34200441e-14, 0.984812677), Vector3.new(35.5, 4.74979782, 23))
      createWall(CFrame.new(-21.6769009, 55.0808754, -324.726807, 0.984812856, 4.45411665e-13, 0.17362076, 4.3284457e-13, 1, 1.10245187e-13, -0.17362076, 3.34200441e-14, 0.984812677), Vector3.new(35.5, 3.74979782, 27.5))
      spawn(function()
          while not workspace:FindFirstChild("playerPickupCannonballRing") do
            wait()
          end
          workspace.playerPickupCannonballRing.Changed:Connect(function(prop)
              if prop == "Transparency" then
                objectiveExists = not objectiveExists
                objectiveObject = workspace.playerPickupCannonballRing
              end
            end)
        end)
      if _G.destroy_map then
        workspace.borders:Destroy()
        workspace.borderFix:Destroy()
        for i,v in pairs(workspace:GetChildren()) do
          if v.ClassName == "Model" and v.Name ~= "corruptCannons" and v.Name ~= "playerFireCannon"  then
            if v ~= game.Players.LocalPlayer.Character and v.Name ~= regionPartName then
              v:Destroy()
            end
          end
        end
      end
      wait(2)
      while not game:GetService("Workspace").dungeon.room3.enemyFolder:FindFirstChildOfClass("Model") do
        wait(1)
      end
      -- get to bottom layer
      forceObjectiveExists = true
      thePart.CFrame = CFrame.new(58.451, 140.645, -221.236)
      local _,_,_,root = getPlayer()
      while true do
        if root ~= nil then
          if getMag(root.Position, thePart.Position) < 5 then
            break
          end
        end
        wait()
      end
      thePart.CFrame = CFrame.new(77.782, 140.645, -233.241)
      while root.Position.Y > 135 do
        wait()
      end
      forceObjectiveExists = false

      while not game:GetService("Workspace").dungeon.room4.enemyFolder:FindFirstChild("The Kraken") do
        wait(1)
      end
      while not game:GetService("Workspace").dungeon.room4.enemyFolder:FindFirstChild("The Kraken"):FindFirstChild("HumanoidRootPart") do
        wait(1)
      end
      while game:GetService("Workspace").dungeon.room4.enemyFolder:FindFirstChild("The Kraken"):FindFirstChild("HumanoidRootPart").Position.Y < -20 do
        forceObjectiveExists = true
        thePart.CFrame = CFrame.new(100.95, 58.9558, -524.832)
        wait()
      end
      forceObjectiveExists = false
      game:GetService("Players").LocalPlayer.Character.LowerTorso.Root:Remove()
      game:GetService("Players").LocalPlayer.Character.LowerTorso.Anchored = true
      spawn(function()
          while true do
            local s = game:GetService("Workspace").dungeon.bossRoom.enemyFolder
            if s:FindFirstChild("Sea Serpent") then
              local g = s:FindFirstChild("Sea Serpent")
              while g ~= nil and g.Parent ~= nil and g:FindFirstChild("Humanoid") and g.Humanoid.Health > 0 do
                if game.Players.LocalPlayer.Character:FindFirstChild("HumanoidRootPart") and game.Players.LocalPlayer.Character:FindFirstChild("Humanoid") then
                  game.Players.LocalPlayer.Character.HumanoidRootPart.CFrame = g.PrimaryPart.CFrame * CFrame.new(0,0,10)
                  game.Players.LocalPlayer.Character.Humanoid:ChangeState(11)
                end
                game:GetService("RunService").RenderStepped:wait()
              end
              game.Players.LocalPlayer.Character.HumanoidRootPart.CFrame = game.Players.LocalPlayer.Character.HumanoidRootPart.CFrame * CFrame.new(0,220,0)
            end
            wait(1)
          end
        end)
    end

    function samuraiFix()
      createWall(CFrame.new(-79.3490448, 17.7415733, -86.7040176, 0.7313537, 0, -0.681998372, 0, 1, 0, 0.681998372, 0, 0.7313537), Vector3.new(73.0999832, 120, 5))
      createWall(CFrame.new(-121.829887, 46.2415581, -115.202858, 0.974370062, 0, -0.224951044, 0, 1, 0, 0.224951044, 0, 0.974370062), Vector3.new(34.9499969, 176.999969, 5))
      createWall(CFrame.new(-144.170593, 49.5415764, -131.804932, 0.57357645, 0, -0.819152057, 0, 1, 0, 0.819152057, 0, 0.57357645), Vector3.new(34.9499969, 183.600006, 5))
      createWall(CFrame.new(-148.874176, 40.8565865, -154.876312, 0.0174523834, 0, -0.99984771, 0, 1, 0, 0.99984771, 0, 0.0174523834), Vector3.new(34.9499969, 166.230026, 5))
      createWall(CFrame.new(-145.585724, 36.8465843, -173.163925, -0.559192896, -4.88861964e-08, -0.829037547, -1.49460107e-08, 1, -4.88861964e-08, 0.829037547, -1.49460107e-08, -0.559192896), Vector3.new(34.9499969, 158.210022, 5))
      createWall(CFrame.new(-128.299927, 38.8115654, -190.066727, -0.838670552, -7.33189083e-08, -0.544639051, -3.98089171e-08, 1, -7.33189083e-08, 0.544639051, -3.98089171e-08, -0.838670552), Vector3.new(34.9499969, 162.139984, 5))
      createWall(CFrame.new(-114.954521, 38.4115791, -193.36969, -0.99862951, -8.73029649e-08, -0.0523359589, -8.28474214e-08, 1, -8.73029649e-08, 0.0523359589, -8.28474214e-08, -0.99862951), Vector3.new(34.9499969, 161.340012, 5))
      createWall(CFrame.new(-94.6667786, 41.6165733, -187.850113, -0.906307757, -7.92319383e-08, 0.42261827, -1.24369237e-07, 1, -7.92319383e-08, -0.42261827, -1.24369237e-07, -0.906307757), Vector3.new(34.9499969, 167.75, 5))
      createWall(CFrame.new(-76.6514664, 42.5215492, -173.739227, -0.484809577, -4.23833981e-08, 0.874619722, -1.63884465e-07, 1, -4.23833981e-08, -0.874619722, -1.63884465e-07, -0.484809577), Vector3.new(34.9499969, 169.559952, 5))
      createWall(CFrame.new(-71.1062622, 38.1915855, -159.090225, 0.0174523834, 0, 0.99984771, 0, 1, 0, -0.99984771, 0, 0.0174523834), Vector3.new(34.9499969, 160.900024, 5))
      createWall(CFrame.new(-70.8261185, 31.206562, -149.575394, 0.49999997, 0, 0.866025448, 0, 1, 0, -0.866025448, 0, 0.49999997), Vector3.new(34.9499969, 146.929977, 5))
      createWall(CFrame.new(-53.192379, 17.7415733, -112.487228, -0.719339788, -6.28866843e-08, 0.694658399, -1.48151742e-07, 1, -6.28866843e-08, -0.694658399, -1.48151742e-07, -0.719339788), Vector3.new(71.1999741, 120, 5))
      createWall(CFrame.new(-16.0917797, 17.7415733, -84.8617783, -0.927183867, -8.10569887e-08, 0.37460658, -1.20171919e-07, 1, -8.10569887e-08, -0.37460658, -1.20171919e-07, -0.927183867), Vector3.new(28.6499805, 120, 5))
      createWall(CFrame.new(18.1154346, 17.7415733, -80.3057556, -1, -8.74227766e-08, 0, -8.74227766e-08, 1, -8.74227766e-08, 7.64274186e-15, -8.74227766e-08, -1), Vector3.new(44.1499825, 120, 5))
      createWall(CFrame.new(44.4154396, 17.7415733, -77.3612747, -0.866025388, -7.57103464e-08, 0.5, -1.31134158e-07, 1, -7.57103464e-08, -0.5, -1.31134158e-07, -0.866025388), Vector3.new(44.1499825, 120, 5))
      createWall(CFrame.new(86.6246567, 17.7415733, -47.5756416, -0.777145922, -6.79402561e-08, 0.629320383, -1.42439717e-07, 1, -6.79402561e-08, -0.629320383, -1.42439717e-07, -0.777145922), Vector3.new(82.649971, 120, 5))
      createWall(CFrame.new(-52.7619934, 17.7415733, 44.2467651, -0.0174523834, -1.52573587e-09, 0.99984771, -1.74832238e-07, 1, -1.52573587e-09, -0.99984771, -1.74832238e-07, -0.0174523834), Vector3.new(210.749954, 120, 5))
      createWall(CFrame.new(113.934662, 17.7415733, 5.35666466, -0.0174523834, -1.52573587e-09, 0.99984771, -1.74832238e-07, 1, -1.52573587e-09, -0.99984771, -1.74832238e-07, -0.0174523834), Vector3.new(68.5999527, 120, 5))
      createWall(CFrame.new(105.848, 17.7415733, 100.737358, -0.0174523834, -1.52573587e-09, 0.99984771, -1.74832238e-07, 1, -1.52573587e-09, -0.99984771, -1.74832238e-07, -0.0174523834), Vector3.new(96.9499588, 120, 5))
      createWall(CFrame.new(76.6631012, 75.4415894, 148.297241, -1, -8.74227766e-08, 0, -8.74227766e-08, 1, -8.74227766e-08, 7.64274186e-15, -8.74227766e-08, -1), Vector3.new(68.8998871, 129, 18.5))
      createWall(CFrame.new(22.9380455, 76.1915817, 312.697144, -1, -8.74227766e-08, 0, -8.74227766e-08, 1, -8.74227766e-08, 7.64274186e-15, -8.74227766e-08, -1), Vector3.new(141.350006, 127.5, 10))
      createWall(CFrame.new(101.938057, 75.9415817, 232.997162, -4.37113883e-08, 0, -1, 0, 1, 0, 1, 0, -4.37113883e-08), Vector3.new(162.44989, 128, 8.5))
      createWall(CFrame.new(-132.212021, 79.9415817, 180.147202, -1, -8.74227766e-08, 0, -8.74227766e-08, 1, -8.74227766e-08, 7.64274186e-15, -8.74227766e-08, -1), Vector3.new(168.149887, 120, 72))
      createWall(CFrame.new(-123.587051, 79.9415817, 287.997192, -1, -8.74227766e-08, 0, -8.74227766e-08, 1, -8.74227766e-08, 7.64274186e-15, -8.74227766e-08, -1), Vector3.new(150.899948, 120, 72.5))
      createWall(CFrame.new(-229.801941, 79.9415817, 220.263245, -0.906307757, -7.92319383e-08, -0.42261827, -5.04763129e-08, 1, -7.92319383e-08, 0.42261827, -5.04763129e-08, -0.906307757), Vector3.new(55.5999222, 120, 5))
      createWall(CFrame.new(-241.71637, 79.9415817, 221.566833, -0.342020154, -2.99003524e-08, -0.939692616, -5.27224131e-09, 1, -2.99003524e-08, 0.939692616, -5.27224131e-09, -0.342020154), Vector3.new(55.5999222, 120, 5))
      createWall(CFrame.new(-276.772064, 79.9415817, 273.57489, -0.681998372, -5.96221881e-08, -0.7313537, -2.34858035e-08, 1, -5.96221881e-08, 0.7313537, -2.34858035e-08, -0.681998372), Vector3.new(73.2999039, 120, 5))
      createWall(CFrame.new(-247.87471, 79.9415817, 294.94928, -0.7313537, -6.3936973e-08, -0.681998372, -2.78005885e-08, 1, -6.3936973e-08, 0.681998372, -2.78005885e-08, -0.7313537), Vector3.new(65.2999191, 120, 5))
      createWall(CFrame.new(-217.981018, 79.9415817, 272.917114, -0.997564077, -8.72098198e-08, -0.0697564706, -8.13244725e-08, 1, -8.72098198e-08, 0.0697564706, -8.13244725e-08, -0.997564077), Vector3.new(17.0999241, 120, 5))
      createWall(CFrame.new(-204.486954, 79.9415817, 264.958984, -0.484809577, -4.23833981e-08, -0.874619722, -1.09610951e-08, 1, -4.23833981e-08, 0.874619722, -1.09610951e-08, -0.484809577), Vector3.new(27.4999256, 120, 5))
      createWall(CFrame.new(-307.982819, 79.9415817, 295.596252, 0.866025388, 0, -0.5, 0, 1, 0, 0.5, 0, 0.866025388), Vector3.new(20.2499027, 120, 5))
      createWall(CFrame.new(-324.856873, 79.9415817, 291.09314, 0.999390841, 0, 0.0348994955, 0, 1, 0, -0.0348994955, 0, 0.999390841), Vector3.new(20.2499027, 120, 5))
      createWall(CFrame.new(-334.888336, 79.9415817, 294.865021, 0.838670552, 0, 0.544639051, 0, 1, 0, -0.544639051, 0, 0.838670552), Vector3.new(25.0999069, 120, 5))
      createWall(CFrame.new(-344.876831, 79.9415817, 303.412811, 0.544639051, 0, 0.838670552, 0, 1, 0, -0.838670552, 0, 0.544639051), Vector3.new(25.0999069, 120, 5))
      createWall(CFrame.new(-353.138275, 79.9415817, 319.06076, 0.309016973, 0, 0.95105654, 0, 1, 0, -0.95105654, 0, 0.309016973), Vector3.new(25.0999069, 120, 5))
      createWall(CFrame.new(-355.918182, 79.9415817, 338.616058, -0.156434491, -1.36759377e-08, 0.987688363, -1.73769237e-07, 1, -1.36759377e-08, -0.987688363, -1.73769237e-07, -0.156434491), Vector3.new(25.0999069, 120, 5))
      createWall(CFrame.new(-338.64389, 79.9415817, 361.615967, -0.719339788, -6.28866843e-08, 0.694658399, -1.48151742e-07, 1, -6.28866843e-08, -0.694658399, -1.48151742e-07, -0.719339788), Vector3.new(50.5999031, 120, 5))
      createWall(CFrame.new(-340.175018, 79.9415817, 406.1138, -0.642787635, -5.61942812e-08, -0.766044438, -2.04530437e-08, 1, -5.61942812e-08, 0.766044438, -2.04530437e-08, -0.642787635), Vector3.new(68.14991, 120, 5))
      createWall(CFrame.new(-345.91333, 79.9415817, 462.58136, 0.42261824, 0, -0.906307817, 0, 1, 0, 0.906307817, 0, 0.42261824), Vector3.new(103.199928, 120, 5))
      createWall(CFrame.new(-308.45636, 79.9415817, 507.855316, 0.987688363, 0, -0.156434476, 0, 1, 0, 0.156434476, 0, 0.987688363), Vector3.new(47.6499405, 120, 5))
      createWall(CFrame.new(-276.312256, 79.9415817, 511.668976, 0.99984771, 0, 0.0174524058, 0, 1, 0, -0.0174524058, 0, 0.99984771), Vector3.new(47.6499405, 120, 5))
      createWall(CFrame.new(-241.047165, 79.9415817, 538.805542, -0.453990519, -3.96891124e-08, 0.891006529, -1.65317033e-07, 1, -3.96891124e-08, -0.891006529, -1.65317033e-07, -0.453990519), Vector3.new(65.5499344, 120, 5))
      createWall(CFrame.new(-220.261414, 79.9415817, 575.792419, -0.559192896, -4.88861964e-08, 0.829037547, -1.59899542e-07, 1, -4.88861964e-08, -0.829037547, -1.59899542e-07, -0.559192896), Vector3.new(47.3499336, 120, 5))
      createWall(CFrame.new(-186.82869, 79.9415817, 601.801575, -0.882947564, -7.71897248e-08, 0.469471574, -1.28465288e-07, 1, -7.71897248e-08, -0.469471574, -1.28465288e-07, -0.882947564), Vector3.new(76.9499283, 120, 5))
      createWall(CFrame.new(-273.247772, 79.9415817, 323.264557, -0.42261824, -3.69464601e-08, -0.906307817, -8.19083112e-09, 1, -3.69464601e-08, 0.906307817, -8.19083112e-09, -0.42261824), Vector3.new(17.9499207, 120, 5))
      createWall(CFrame.new(-278.552307, 79.9415817, 339.3573, -0.207911655, -1.81762143e-08, -0.978147626, -1.91039362e-09, 1, -1.81762143e-08, 0.978147626, -1.91039362e-09, -0.207911655), Vector3.new(17.9499207, 120, 5))
      createWall(CFrame.new(-283.670166, 79.9415817, 356.718292, -0.35836798, -3.13295239e-08, -0.933580399, -5.80658366e-09, 1, -3.13295239e-08, 0.933580399, -5.80658366e-09, -0.35836798), Vector3.new(20.6499119, 120, 5))
      createWall(CFrame.new(-268.345642, 79.9415817, 364.530884, 0.999390841, 0, 0.0348994955, 0, 1, 0, -0.0348994955, 0, 0.999390841), Vector3.new(40.7998962, 120, 5))
      createWall(CFrame.new(-232.930862, 79.9415817, 367.778046, 0.974370062, 0, -0.224951044, 0, 1, 0, 0.224951044, 0, 0.974370062), Vector3.new(40.7998962, 120, 5))
      createWall(CFrame.new(-198.301727, 79.9415817, 406.548157, -0.438371152, -3.83236234e-08, 0.898794055, -1.65997847e-07, 1, -3.83236234e-08, -0.898794055, -1.65997847e-07, -0.438371152), Vector3.new(85.8499603, 120, 5))
      createWall(CFrame.new(-191.77713, 79.9415817, 455.941559, -0.515038073, -4.50260593e-08, -0.857167304, -1.24868293e-08, 1, -4.50260593e-08, 0.857167304, -1.24868293e-08, -0.515038073), Vector3.new(42.049984, 120, 5))
      createWall(CFrame.new(-208.300247, 79.9415817, 479.683472, -0.629320443, -5.50169403e-08, -0.777145922, -1.94825205e-08, 1, -5.50169403e-08, 0.777145922, -1.94825205e-08, -0.629320443), Vector3.new(42.049984, 120, 5))
      createWall(CFrame.new(-209.384109, 79.9415817, 507.477234, 0.642787635, 0, -0.766044438, 0, 1, 0, 0.766044438, 0, 0.642787635), Vector3.new(36.9999733, 120, 5))
      createWall(CFrame.new(-180.930634, 79.9415817, 525.294922, 0.974370062, 0, -0.224951044, 0, 1, 0, 0.224951044, 0, 0.974370062), Vector3.new(36.9999733, 120, 5))
      createWall(CFrame.new(-145.599655, 79.9415817, 528.387268, 0.997564077, 0, 0.0697564706, 0, 1, 0, -0.0697564706, 0, 0.997564077), Vector3.new(36.9999733, 120, 5))
      createWall(CFrame.new(-132.102982, 79.9415817, 531.453186, -0.0697565079, -6.09830764e-09, 0.997564077, -1.74632589e-07, 1, -6.09830764e-09, -0.997564077, -1.74632589e-07, -0.0697565079), Vector3.new(35.899971, 120, 17.3999958))
      createWall(CFrame.new(-153.191727, 79.9415817, 603.870667, 0.49999997, 0, 0.866025448, 0, 1, 0, -0.866025448, 0, 0.49999997), Vector3.new(36.1999664, 120, 9.19999409))
      createWall(CFrame.new(92.1630783, 79.9415817, 575.945129, 0.99984771, 0, -0.0174524058, 0, 1, 0, 0.0174524058, 0, 0.99984771), Vector3.new(129.549896, 120, 14.0500021))
      createWall(CFrame.new(85.5814362, 79.9415817, 623.537842, 0.99984771, 0, -0.0174524058, 0, 1, 0, 0.0174524058, 0, 0.99984771), Vector3.new(118.049873, 120, 14.0500021))
      createWall(CFrame.new(155.319351, 79.9415817, 644.592834, 0.438371152, 0, -0.898794055, 0, 1, 0, 0.898794055, 0, 0.438371152), Vector3.new(58.5498695, 120, 4.65000153))
      createWall(CFrame.new(150.972641, 79.9415817, 733.93103, 0.275637388, 0, 0.96126169, 0, 1, 0, -0.96126169, 0, 0.275637388), Vector3.new(134.699875, 120, 4.65000153))
      createWall(CFrame.new(113.599823, 79.9415817, 834.299438, 0.469471604, 0, 0.882947564, 0, 1, 0, -0.882947564, 0, 0.469471604), Vector3.new(82.6498489, 120, 4.65000153))
      createWall(CFrame.new(83.7891617, 79.9415817, 886.715393, 0.544639051, 0, 0.838670552, 0, 1, 0, -0.838670552, 0, 0.544639051), Vector3.new(40.299839, 120, 4.65000153))
      createWall(CFrame.new(57.0700951, 79.9415817, 912.924072, 0.857167304, 0, 0.515038073, 0, 1, 0, -0.515038073, 0, 0.857167304), Vector3.new(40.299839, 120, 4.65000153))
      createWall(CFrame.new(-16.656601, 79.9415817, 934.313538, 0.981627166, 0, 0.190808997, 0, 1, 0, -0.190808997, 0, 0.981627166), Vector3.new(116.849838, 120, 4.65000153))
      createWall(CFrame.new(-14.7186928, 79.9415817, 1032.85339, 0.981627166, 0, 0.190808997, 0, 1, 0, -0.190808997, 0, 0.981627166), Vector3.new(150.649872, 120, 4.65000153))
      createWall(CFrame.new(100.627106, 79.9415817, 999.678406, 0.91354543, 0, 0.406736642, 0, 1, 0, -0.406736642, 0, 0.91354543), Vector3.new(96.7998657, 120, 4.65000153))
      createWall(CFrame.new(-82.9455414, 79.9415817, 944.657593, 0.99984771, 0, -0.0174524058, 0, 1, 0, 0.0174524058, 0, 0.99984771), Vector3.new(37.8998451, 120, 4.65000153))
      createWall(CFrame.new(-131.292542, 79.9415817, 922.620178, 0.798635542, 0, -0.601814985, 0, 1, 0, 0.601814985, 0, 0.798635542), Vector3.new(75.9498596, 120, 4.65000153))
      createWall(CFrame.new(-232.84433, 79.9415817, 900.761597, 0.99862951, 0, -0.0523359589, 0, 1, 0, 0.0523359589, 0, 0.99862951), Vector3.new(160.549911, 120, 4.65000153))
      createWall(CFrame.new(-99.3179703, 79.9415817, 1066.7688, 0.515038073, 0, 0.857167304, 0, 1, 0, -0.857167304, 0, 0.515038073), Vector3.new(47.8498611, 120, 4.65000153))
      createWall(CFrame.new(191.109024, 79.9415817, 590.424316, 0.96126169, 0, -0.275637358, 0, 1, 0, 0.275637358, 0, 0.96126169), Vector3.new(129.549896, 120, 14.0500021))
      createWall(CFrame.new(116.764015, 79.9415817, 982.981506, 0.587785304, 0, 0.809017003, 0, 1, 0, -0.809017003, 0, 0.587785304), Vector3.new(44.3998642, 120, 4.65000153))
      createWall(CFrame.new(147.403961, 79.9415817, 956.020203, 0.866025388, 0, 0.5, 0, 1, 0, -0.5, 0, 0.866025388), Vector3.new(44.3998642, 120, 4.65000153))
      createWall(CFrame.new(187.493103, 79.9415817, 912.867615, 0.669130564, 0, 0.74314487, 0, 1, 0, -0.74314487, 0, 0.669130564), Vector3.new(115.299873, 120, 4.65000153))
      createWall(CFrame.new(199.873352, 79.9415817, 869.370178, -0.0348994955, -3.05101078e-09, 0.999390841, -1.74792291e-07, 1, -3.05101078e-09, -0.999390841, -1.74792291e-07, -0.0348994955), Vector3.new(120.999878, 120, 4.65000153))
      createWall(CFrame.new(203.445938, 79.9415817, 792.87146, 0.309016973, 0, 0.95105654, 0, 1, 0, -0.95105654, 0, 0.309016973), Vector3.new(36.849865, 120, 4.65000153))
      createWall(CFrame.new(207.590225, 79.9415817, 760.274048, 0.0348994955, 0, -0.999390841, 0, 1, 0, 0.999390841, 0, 0.0348994955), Vector3.new(52.099865, 120, 4.65000153))
      createWall(CFrame.new(220.461777, 79.9415817, 663.820862, -0.258819073, -2.26266827e-08, -0.965925813, -2.97885805e-09, 1, -2.26266827e-08, 0.965925813, -2.97885805e-09, -0.258819073), Vector3.new(145.199936, 120, 14.2000027))
      createWall(CFrame.new(-312.379059, 79.9415817, 901.517517, 0.642787635, 0, 0.766044438, 0, 1, 0, -0.766044438, 0, 0.642787635), Vector3.new(55.4000015, 120, 4.65000153))
      createWall(CFrame.new(-325.956299, 79.9415817, 988.109619, -4.37113883e-08, 0, 1, 0, 1, 0, -1, 0, -4.37113883e-08), Vector3.new(173.950043, 120, 4.65000153))
      createWall(CFrame.new(-198.956482, 79.9415817, 1094.80957, -1, -8.74227766e-08, 0, -8.74227766e-08, 1, -8.74227766e-08, 7.64274186e-15, -8.74227766e-08, -1), Vector3.new(188.15004, 120, 4.65000153))
      createWall(CFrame.new(46.1631012, 77.6916199, 283.547241, -1, -8.74227766e-08, 0, -8.74227766e-08, 1, -8.74227766e-08, 7.64274186e-15, -8.74227766e-08, -1), Vector3.new(71.8998871, 17.5, 4))
      createWall(CFrame.new(-153.191727, 79.9415817, 603.870667, 0.49999997, 0, 0.866025448, 0, 1, 0, -0.866025448, 0, 0.49999997), Vector3.new(36.1999664, 120, 9.19999409))
      createWall(CFrame.new(-218.836899, 66.4415817, 262.047241, -1, -8.74227766e-08, 0, -8.74227766e-08, 1, -8.74227766e-08, 7.64274186e-15, -8.74227766e-08, -1), Vector3.new(84.8998871, 1, 108))
      createWall(CFrame.new(-35.8530579, 63.9391098, 607.062622, -1.00000024, 6.68149738e-22, 0, -6.68149738e-22, 1, 0, 0, 0, -0.999999881), Vector3.new(207.399887, 1.5, 166))
      createWall(CFrame.new(78.6687851, 17.7415791, 47.7285957, -0.0174523834, -1.52573587e-09, 0.99984771, -1.74832238e-07, 1, -1.52573587e-09, -0.99984771, -1.74832238e-07, -0.0174523834), Vector3.new(46.0999527, 120, 77))
      createWall(CFrame.new(-14.8169785, 17.7415791, 49.3603935, -0.0174523834, -1.52573587e-09, 0.99984771, -1.74832238e-07, 1, -1.52573587e-09, -0.99984771, -1.74832238e-07, -0.0174523834), Vector3.new(46.0999527, 120, 78))
      createWall(CFrame.new(32.8341637, 5.29244184, 34.5653267, -3.7252903e-09, 4.65661287e-10, 1, -0.244939968, 0.969538212, 1.25146471e-09, -0.969538152, -0.244939908, 3.7252903e-09), Vector3.new(51.5999527, 5, 20.5))
      createWall(CFrame.new(25.6630993, 93.6915894, 151.797241, -1, -8.74227766e-08, 0, -8.74227766e-08, 1, -8.74227766e-08, 7.64274186e-15, -8.74227766e-08, -1), Vector3.new(135.899887, 92.5, 9.5))
      createWall(CFrame.new(-21.0868988, 73.9415894, 149.297241, -1, -8.74227766e-08, 0, -8.74227766e-08, 1, -8.74227766e-08, 7.64274186e-15, -8.74227766e-08, -1), Vector3.new(69.3998871, 132, 14.5))
      createWall(CFrame.new(-50.836895, 37.691597, 220.797241, -1, -8.74227766e-08, 0, -8.74227766e-08, 1, -8.74227766e-08, 7.64274186e-15, -8.74227766e-08, -1), Vector3.new(9.89988708, 59.5, 157.5))
      createWall(CFrame.new(56.413105, 38.6916161, 283.547241, -1, -8.74227766e-08, 0, -8.74227766e-08, 1, -8.74227766e-08, 7.64274186e-15, -8.74227766e-08, -1), Vector3.new(92.3998871, 61.5, 4))
      createWall(CFrame.new(-32.086895, 38.6916046, 283.547241, -1, -8.74227766e-08, 0, -8.74227766e-08, 1, -8.74227766e-08, 7.64274186e-15, -8.74227766e-08, -1), Vector3.new(28.3998871, 61.5, 4))
      createWall(CFrame.new(30.4380493, 67.9415741, 211.697144, -1, -8.74227766e-08, 0, -8.74227766e-08, 1, -8.74227766e-08, 7.64274186e-15, -8.74227766e-08, -1), Vector3.new(156.350006, 4, 146))
      createWall(CFrame.new(29.5450134, 2.84688377, 217.2388, 1, 0, 0, 0, 1, 0, 0, 0, 1), Vector3.new(165.91008, 22.4399872, 132.789948))
      createWall(CFrame.new(87.6880493, 67.1915817, 224.947144, -1, -8.74227766e-08, 0, -8.74227766e-08, 1, -8.74227766e-08, 7.64274186e-15, -8.74227766e-08, -1), Vector3.new(24.8500061, 4.5, 172.5))
      createWall(CFrame.new(48.4890289, 38.7647934, 298.738983, -0.707106829, -0.707106769, 4.37113883e-08, -0.707106829, 0.707106769, -4.37113847e-08, 0, -6.18172393e-08, -1), Vector3.new(81.3500061, 5.5, 26))
      createWall(CFrame.new(-8.87301826, 14.249526, 296.988922, -1.00000012, -8.94069672e-08, 9.40053089e-15, -8.94069672e-08, 0.99999994, -8.74227695e-08, 1.77635684e-15, -8.74227766e-08, -1), Vector3.new(59.3500061, 0.5, 26.5))
      createWall(CFrame.new(-28.1230221, 37.4995232, 296.988922, -1.00000012, -8.94069672e-08, 9.40053089e-15, -8.94069672e-08, 0.99999994, -8.74227695e-08, 1.77635684e-15, -8.74227766e-08, -1), Vector3.new(20.8500061, 47, 26.5))
      createWall(CFrame.new(28.0450134, 2.59688377, 106.488808, 1, 0, 0, 0, 1, 0, 0, 0, 1), Vector3.new(158.91008, 21.9399872, 94.2899399))
      createWall(CFrame.new(-124.586899, 67.1915894, 236.797241, -1, -8.74227766e-08, 0, -8.74227766e-08, 1, -8.74227766e-08, 7.64274186e-15, -8.74227766e-08, -1), Vector3.new(157.399887, 0.5, 57.5))
      createWall(CFrame.new(-254.643875, 66.3116455, 432.286926, -0.912263155, 0, -0.409604788, -6.68149738e-22, 1, 0, 0.409604847, 0, -0.912263036), Vector3.new(207.399887, 2.5, 151))
      createWall(CFrame.new(-125.181572, 64.4391098, 589.670898, -0.945519269, 2.00444967e-21, 0.325568169, -2.04085147e-21, 1, -2.17528256e-22, -0.325568289, 5.04870979e-29, -0.945518196), Vector3.new(17.3998871, 2.5, 166))
      createWall(CFrame.new(-137.709702, 64.9391098, 585.357117, -0.945519269, 2.00444967e-21, 0.325568169, -2.04085147e-21, 1, -2.17528256e-22, -0.325568289, 5.04870979e-29, -0.945518196), Vector3.new(22.8998871, 3.5, 166))
      createWall(CFrame.new(19.0190639, 64.4391098, 609.972961, -0.990270078, 5.86774583e-21, 0.139173076, -5.88725364e-21, 1, 5.91148532e-22, -0.139173225, 8.70114437e-22, -0.990266919), Vector3.new(23.8998871, 2.5, 111.5))
      createWall(CFrame.new(105.727264, 64.9391098, 804.053894, -0.990270078, 5.86774583e-21, 0.139173076, -5.88725364e-21, 1, 5.91148532e-22, -0.139173225, 8.70114437e-22, -0.990266919), Vector3.new(214.149902, 3.5, 514.25))
      createWall(CFrame.new(-224.200012, 65.5, 1001.75006, -1.00000405, 1.1819003e-20, 2.98023224e-07, -1.1819003e-20, 1, 5.46135296e-22, 2.98023224e-07, -5.46135296e-22, -0.999997675), Vector3.new(181.399902, 4, 138.5))
      createWall(CFrame.new(-146.199707, 66, 1001.75006, -1.00000405, 1.1819003e-20, 2.98023224e-07, -1.1819003e-20, 1, 5.46135296e-22, 2.98023224e-07, -5.46135296e-22, -0.999997675), Vector3.new(25.3999023, 5, 138.5))
      createWall(CFrame.new(-174.199951, 66, 1047.75, -0.62932831, 3.54571487e-20, 0.777146101, -4.02626932e-20, 1, -7.34422647e-21, -0.777149975, -1.63841185e-21, -0.629315674), Vector3.new(25.3999023, 5, 138.5))
      createWall(CFrame.new(-237.197769, 66, 1060.49756, 0.173636138, 1.16034402e-19, 0.984809875, -1.30376718e-19, 1, -9.48368712e-20, -0.984809875, -1.11929169e-19, 0.173636138), Vector3.new(25.3999023, 5, 138.5))
      createWall(CFrame.new(-283.1716, 66, 1015.58191, 0.906302631, 1.16034402e-19, 0.422629356, -1.52466835e-19, 1, 5.24021665e-20, -0.422629356, -1.11929169e-19, 0.906302631), Vector3.new(25.3999023, 5, 138.5))
      createWall(CFrame.new(-261.013458, 66, 946.482361, 0.77715373, 1.16034389e-19, -0.629310906, -1.97383098e-20, 1, 1.60007905e-19, 0.629310906, -1.11929182e-19, 0.77715373), Vector3.new(25.3999023, 5, 138.5))
      createWall(CFrame.new(-210.805298, 66, 933.739136, -0.190796942, 1.16034389e-19, -0.981629729, 1.32012016e-19, 1, 9.25470866e-20, 0.981629729, -1.11929182e-19, -0.190796942), Vector3.new(25.3999023, 5, 138.5))
      createWall(CFrame.new(-162.697159, 66, 955.924011, -0.707098544, 1.16034363e-19, -0.707116008, 1.61194651e-19, 1, 2.90485394e-21, 0.707116008, -1.11929195e-19, -0.707098544), Vector3.new(25.3999023, 5, 138.5))
      createWall(CFrame.new(-160.222321, 66.5, 953.449097, -0.707098544, 1.16034363e-19, -0.707116008, 1.61194651e-19, 1, 2.90485394e-21, 0.707116008, -1.11929195e-19, -0.707098544), Vector3.new(25.3999023, 5, 138.5))
      createWall(CFrame.new(-157.040375, 67, 950.26709, -0.707098544, 1.16034363e-19, -0.707116008, 1.61194651e-19, 1, 2.90485394e-21, 0.707116008, -1.11929195e-19, -0.707098544), Vector3.new(25.3999023, 5, 138.5))
      createWall(CFrame.new(-155.272629, 67.5, 948.499329, -0.707098544, 1.16034363e-19, -0.707116008, 1.61194651e-19, 1, 2.90485394e-21, 0.707116008, -1.11929195e-19, -0.707098544), Vector3.new(25.3999023, 5, 138.5))
      createWall(CFrame.new(-152.797791, 68, 946.024414, -0.707098544, 1.16034363e-19, -0.707116008, 1.61194651e-19, 1, 2.90485394e-21, 0.707116008, -1.11929195e-19, -0.707098544), Vector3.new(25.3999023, 5, 138.5))
      createWall(CFrame.new(-150.676498, 68.5, 943.903076, -0.707098544, 1.16034363e-19, -0.707116008, 1.61194651e-19, 1, 2.90485394e-21, 0.707116008, -1.11929195e-19, -0.707098544), Vector3.new(25.3999023, 5, 138.5))
      createWall(CFrame.new(-144.199692, 66.5, 1001.75006, -1.00000405, 1.1819003e-20, 2.98023224e-07, -1.1819003e-20, 1, 5.46135296e-22, 2.98023224e-07, -5.46135296e-22, -0.999997675), Vector3.new(25.3999023, 5, 138.5))
      createWall(CFrame.new(-141.199677, 67, 1001.75006, -1.00000405, 1.1819003e-20, 2.98023224e-07, -1.1819003e-20, 1, 5.46135296e-22, 2.98023224e-07, -5.46135296e-22, -0.999997675), Vector3.new(25.3999023, 5, 138.5))
      createWall(CFrame.new(-140.199661, 67.5, 1001.75006, -1.00000405, 1.1819003e-20, 2.98023224e-07, -1.1819003e-20, 1, 5.46135296e-22, 2.98023224e-07, -5.46135296e-22, -0.999997675), Vector3.new(25.3999023, 5, 138.5))
      createWall(CFrame.new(-139.199661, 68, 1001.75006, -1.00000405, 1.1819003e-20, 2.98023224e-07, -1.1819003e-20, 1, 5.46135296e-22, 2.98023224e-07, -5.46135296e-22, -0.999997675), Vector3.new(25.3999023, 5, 138.5))
      createWall(CFrame.new(-116.44957, 68.5, 1001.75006, -1.00000405, 1.1819003e-20, 2.98023224e-07, -1.1819003e-20, 1, 5.46135296e-22, 2.98023224e-07, -5.46135296e-22, -0.999997675), Vector3.new(67.8999023, 5, 138.5))
      createWall(CFrame.new(-112.699554, 68, 1001.75006, -1.00000405, 1.1819003e-20, 2.98023224e-07, -1.1819003e-20, 1, 5.46135296e-22, 2.98023224e-07, -5.46135296e-22, -0.999997675), Vector3.new(75.3999023, 4, 138.5))
      createWall(CFrame.new(-107.699532, 67.5, 1001.75006, -1.00000405, 1.1819003e-20, 2.98023224e-07, -1.1819003e-20, 1, 5.46135296e-22, 2.98023224e-07, -5.46135296e-22, -0.999997675), Vector3.new(85.3999023, 3, 138.5))
      createWall(CFrame.new(-103.949516, 67, 1001.75006, -1.00000405, 1.1819003e-20, 2.98023224e-07, -1.1819003e-20, 1, 5.46135296e-22, 2.98023224e-07, -5.46135296e-22, -0.999997675), Vector3.new(92.8999023, 2, 138.5))
      createWall(CFrame.new(-100.199501, 66.75, 1001.75006, -1.00000405, 1.1819003e-20, 2.98023224e-07, -1.1819003e-20, 1, 5.46135296e-22, 2.98023224e-07, -5.46135296e-22, -0.999997675), Vector3.new(100.399902, 1.5, 138.5))
      createWall(CFrame.new(-173.570618, 66.5, 1048.5271, -0.62932831, 3.54571487e-20, 0.777146101, -4.02626932e-20, 1, -7.34422647e-21, -0.777149975, -1.63841185e-21, -0.629315674), Vector3.new(25.3999023, 5, 138.5))
      createWall(CFrame.new(-172.626633, 67, 1049.69287, -0.62932831, 3.54571487e-20, 0.777146101, -4.02626932e-20, 1, -7.34422647e-21, -0.777149975, -1.63841185e-21, -0.629315674), Vector3.new(25.3999023, 5, 138.5))
      createWall(CFrame.new(-171.367981, 67.5, 1051.24719, -0.62932831, 3.54571487e-20, 0.777146101, -4.02626932e-20, 1, -7.34422647e-21, -0.777149975, -1.63841185e-21, -0.629315674), Vector3.new(25.3999023, 5, 138.5))
      createWall(CFrame.new(-168.536011, 68, 1054.74438, -0.62932831, 3.54571487e-20, 0.777146101, -4.02626932e-20, 1, -7.34422647e-21, -0.777149975, -1.63841185e-21, -0.629315674), Vector3.new(25.3999023, 5, 138.5))
      createWall(CFrame.new(-166.962692, 68.5, 1056.68726, -0.62932831, 3.54571487e-20, 0.777146101, -4.02626932e-20, 1, -7.34422647e-21, -0.777149975, -1.63841185e-21, -0.629315674), Vector3.new(25.3999023, 5, 138.5))
      createWall(CFrame.new(-166.018707, 69, 1057.85303, -0.62932831, 3.54571487e-20, 0.777146101, -4.02626932e-20, 1, -7.34422647e-21, -0.777149975, -1.63841185e-21, -0.629315674), Vector3.new(25.3999023, 5, 138.5))
      createWall(CFrame.new(-238.239594, 66.5, 1066.40637, 0.173636138, 1.16034402e-19, 0.984809875, -1.30376718e-19, 1, -9.48368712e-20, -0.984809875, -1.11929169e-19, 0.173636138), Vector3.new(25.3999023, 5, 138.5))
      createWall(CFrame.new(-238.673691, 67, 1068.86841, 0.173636138, 1.16034402e-19, 0.984809875, -1.30376718e-19, 1, -9.48368712e-20, -0.984809875, -1.11929169e-19, 0.173636138), Vector3.new(25.3999023, 5, 138.5))
      createWall(CFrame.new(-239.020966, 67.5, 1070.83801, 0.173636138, 1.16034402e-19, 0.984809875, -1.30376718e-19, 1, -9.48368712e-20, -0.984809875, -1.11929169e-19, 0.173636138), Vector3.new(25.3999023, 5, 138.5))
      createWall(CFrame.new(-239.54187, 68, 1073.79248, 0.173636138, 1.16034402e-19, 0.984809875, -1.30376718e-19, 1, -9.48368712e-20, -0.984809875, -1.11929169e-19, 0.173636138), Vector3.new(25.3999023, 5, 138.5))
      createWall(CFrame.new(-240.062775, 68.5, 1076.74695, 0.173636138, 1.16034402e-19, 0.984809875, -1.30376718e-19, 1, -9.48368712e-20, -0.984809875, -1.11929169e-19, 0.173636138), Vector3.new(25.3999023, 5, 138.5))
      createWall(CFrame.new(-286.343658, 66.5, 1017.0611, 0.906302631, 1.16034402e-19, 0.422629356, -1.52466835e-19, 1, 5.24021665e-20, -0.422629356, -1.11929169e-19, 0.906302631), Vector3.new(25.3999023, 5, 138.5))
      createWall(CFrame.new(-289.515717, 67, 1018.54028, 0.906302631, 1.16034402e-19, 0.422629356, -1.52466835e-19, 1, 5.24021665e-20, -0.422629356, -1.11929169e-19, 0.906302631), Vector3.new(25.3999023, 5, 138.5))
      createWall(CFrame.new(-291.781464, 67.5, 1019.59686, 0.906302631, 1.16034402e-19, 0.422629356, -1.52466835e-19, 1, 5.24021665e-20, -0.422629356, -1.11929169e-19, 0.906302631), Vector3.new(25.3999023, 5, 138.5))
      createWall(CFrame.new(-294.500366, 68, 1020.86475, 0.906302631, 1.16034402e-19, 0.422629356, -1.52466835e-19, 1, 5.24021665e-20, -0.422629356, -1.11929169e-19, 0.906302631), Vector3.new(25.3999023, 5, 138.5))
      createWall(CFrame.new(-298.12558, 68.5, 1022.55524, 0.906302631, 1.16034402e-19, 0.422629356, -1.52466835e-19, 1, 5.24021665e-20, -0.422629356, -1.11929169e-19, 0.906302631), Vector3.new(25.3999023, 5, 138.5))
      createWall(CFrame.new(-262.179199, 66.5, 945.538391, 0.77715373, 1.16034389e-19, -0.629310906, -1.97383098e-20, 1, 1.60007905e-19, 0.629310906, -1.11929182e-19, 0.77715373), Vector3.new(25.3999023, 5, 138.5))
      createWall(CFrame.new(-263.34494, 67, 944.594421, 0.77715373, 1.16034389e-19, -0.629310906, -1.97383098e-20, 1, 1.60007905e-19, 0.629310906, -1.11929182e-19, 0.77715373), Vector3.new(25.3999023, 5, 138.5))
      createWall(CFrame.new(-264.899261, 67.5, 943.335815, 0.77715373, 1.16034389e-19, -0.629310906, -1.97383098e-20, 1, 1.60007905e-19, 0.629310906, -1.11929182e-19, 0.77715373), Vector3.new(25.3999023, 5, 138.5))
      createWall(CFrame.new(-266.065002, 68, 942.391846, 0.77715373, 1.16034389e-19, -0.629310906, -1.97383098e-20, 1, 1.60007905e-19, 0.629310906, -1.11929182e-19, 0.77715373), Vector3.new(25.3999023, 5, 138.5))
      createWall(CFrame.new(-266.842163, 68.5, 941.762512, 0.77715373, 1.16034389e-19, -0.629310906, -1.97383098e-20, 1, 1.60007905e-19, 0.629310906, -1.11929182e-19, 0.77715373), Vector3.new(25.3999023, 5, 138.5))
      createWall(CFrame.new(-210.137512, 66.5, 930.303406, -0.190796942, 1.16034389e-19, -0.981629729, 1.32012016e-19, 1, 9.25470866e-20, 0.981629729, -1.11929182e-19, -0.190796942), Vector3.new(25.3999023, 5, 138.5))
      createWall(CFrame.new(-209.660522, 67, 927.849304, -0.190796942, 1.16034389e-19, -0.981629729, 1.32012016e-19, 1, 9.25470866e-20, 0.981629729, -1.11929182e-19, -0.190796942), Vector3.new(25.3999023, 5, 138.5))
      createWall(CFrame.new(-208.992737, 67.5, 924.413635, -0.190796942, 1.16034389e-19, -0.981629729, 1.32012016e-19, 1, 9.25470866e-20, 0.981629729, -1.11929182e-19, -0.190796942), Vector3.new(25.3999023, 5, 138.5))
      createWall(CFrame.new(-208.706543, 68, 922.941162, -0.190796942, 1.16034389e-19, -0.981629729, 1.32012016e-19, 1, 9.25470866e-20, 0.981629729, -1.11929182e-19, -0.190796942), Vector3.new(25.3999023, 5, 138.5))
      createWall(CFrame.new(-208.420349, 68.5, 921.468689, -0.190796942, 1.16034389e-19, -0.981629729, 1.32012016e-19, 1, 9.25470866e-20, 0.981629729, -1.11929182e-19, -0.190796942), Vector3.new(25.3999023, 5, 138.5))
      createWall(CFrame.new(42.9820786, 0.3806144, 36.3547974, -0.000348969304, 0, 0.99999994, 0, 1, 0, -0.99999994, 0, -0.000348969304), Vector3.new(49.7200928, 29.8699951, 3.82001257))
      createWall(CFrame.new(21.461998, -1.51294553, 36.6358871, -0.000348969304, 0, 0.99999994, 0, 1, 0, -0.99999994, 0, -0.000348969304), Vector3.new(48.7200928, 36.8699951, 3.82001257))
      createWall(CFrame.new(28.1880493, 67.1915741, 230.697144, -1, -8.74227766e-08, 0, -8.74227766e-08, 1, -8.74227766e-08, 7.64274186e-15, -8.74227766e-08, -1), Vector3.new(160.850006, 2.5, 61))
      createWall(CFrame.new(29.4380493, 67.6915741, 234.197144, -1, -8.74227766e-08, 0, -8.74227766e-08, 1, -8.74227766e-08, 7.64274186e-15, -8.74227766e-08, -1), Vector3.new(158.350006, 3.5, 61))
      createWall(CFrame.new(28.6880493, 67.4415741, 230.697144, -1, -8.74227766e-08, 0, -8.74227766e-08, 1, -8.74227766e-08, 7.64274186e-15, -8.74227766e-08, -1), Vector3.new(159.850006, 3, 62))
      createWall(CFrame.new(27.4380493, 66.9415741, 234.947144, -1, -8.74227766e-08, 0, -8.74227766e-08, 1, -8.74227766e-08, 7.64274186e-15, -8.74227766e-08, -1), Vector3.new(162.350006, 2, 48.5))
      createWall(CFrame.new(56.7784882, 64.9391098, 983.48761, -0.990270078, 5.86774583e-21, 0.139173076, -5.88725364e-21, 1, 5.91148532e-22, -0.139173225, 8.70114437e-22, -0.990266919), Vector3.new(261.149902, 3.5, 145.25))
      wait(.1)
      if _G.destroy_map then
        for i,v in pairs(workspace:GetChildren()) do
          if v.ClassName == "Model" or v.ClassName == "Part" or v.ClassName == "UnionOperation" or v.ClassName == "WedgePart" then
            if v ~= game.Players.LocalPlayer.Character and v.Name ~= regionPartName then
              v:Destroy()
            end
          end
        end

        game:GetService("Workspace").fence:Destroy()
        game:GetService("Workspace").borders:Destroy()
      end
      workspace:WaitForChild("eliteSwordsman")
      local s = game:GetService("Workspace").eliteSwordsman
      s.ChildAdded:Connect(function(instance) -- all future folders, if mob spawned, give hitbox
          if instance.ClassName == "Model" and instance.Name == "Ultimate Swordsman" then
            instance:WaitForChild("HumanoidRootPart")
            --cs:AddTag(instance, "Enemy")
            addHitBox(instance, 30, "square")
          end
        end)

      while not game:GetService("Workspace").dungeon.room4.enemyFolder:FindFirstChild("Sanada Yukimura") do
        wait(1)
      end
      while not game:GetService("Workspace").dungeon.room4.enemyFolder:FindFirstChild("Sanada Yukimura"):FindFirstChild("HumanoidRootPart") do
        wait(1)
      end
      -- cant path to second boss, paths to second boss area until hes in position
      forceObjectiveExists = true
      thePart.CFrame = CFrame.new(88.5511551, 72.7995224, 276.368042)
      local _,_,_,root = getPlayer()
      while root.Position.Y < 69.999526977539 do
        wait()
      end
      forceObjectiveExists = false

    end
    function underworldFix()
      createWall(CFrame.new(487, 65.1197205, 416.394165, 1, 0, 0, 0, 0.89100647, 0.4539904, 0, -0.4539904, 0.89100647), Vector3.new(68, 1, 83.5))
      createWall(CFrame.new(487, 61.8143387, 275.542908, 1, 0, 0, 0, 0.89100647, 0.4539904, 0, -0.4539904, 0.89100647), Vector3.new(68, 1, 17.5))
      --[[
      while not game:GetService("Workspace").dungeon.room8.enemyFolder:FindFirstChild("Kolvumar") do
        wait(1)
      end
      while not game:GetService("Workspace").dungeon.room8.enemyFolder:FindFirstChild("Kolvumar"):FindFirstChild("HumanoidRootPart") do
        wait(1)
      end]]
    end

    function pirateFix()
      createWall(CFrame.new(-68.2813721, 189.801392, 430.691193, 0.997564077, 0, -0.0697564706, 0, 1, 0, 0.0697564706, 0, 0.997564077), Vector3.new(115.020088, 173.349854, 90.7301254))
      createWall(CFrame.new(-248.68956, 189.686432, 446.980225, 1, 0, 0, 0, 1, 0, 0, 0, 1), Vector3.new(145.240143, 173.119949, 132.979874))
      createWall(CFrame.new(-156.12616, 190.301392, 468.405304, 0.997564077, 0, -0.0697564706, 0, 1, 0, 0.0697564706, 0, 0.997564077), Vector3.new(59.0200806, 174.349854, 3.23012543))
      createWall(CFrame.new(-0.124966383, 263.126404, 237.607864, 0.948323667, 0, -0.317304641, 0, 1, 0, 0.317304641, 0, 0.948323667), Vector3.new(17.7299881, 319.999939, 105.929977))
      createWall(CFrame.new(-13.9006824, 263.126404, 334.261169, 0.998134792, 0, 0.0610485412, 0, 1, 0, -0.0610485412, 0, 0.998134792), Vector3.new(16.7299881, 319.999939, 102.700035))
      createWall(CFrame.new(12.5065136, 263.126404, 193.714981, 0.997564077, 0, 0.0697564706, 0, 1, 0, -0.0697564706, 0, 0.997564077), Vector3.new(10.2299871, 319.999939, 105.929977))
      createWall(CFrame.new(-23.2540989, 263.126404, 130.036514, -0.0958457589, -8.37910274e-09, -0.995396197, -4.02479827e-10, 1, -8.37910274e-09, 0.995396197, -4.02479827e-10, -0.0958457589), Vector3.new(10.2299871, 319.999939, 108.449997))
      createWall(CFrame.new(-182.51709, 263.126404, 105.839249, 0.113203242, 0, -0.993571877, 0, 1, 0, 0.993571877, 0, 0.113203242), Vector3.new(93.6899948, 319.999939, 94.2900009))
      createWall(CFrame.new(-210.425171, 225.446411, 136.269073, 0.688354611, 0, -0.725374341, 0, 1, 0, 0.725374341, 0, 0.688354611), Vector3.new(37.7000008, 244.639954, 70.2799683))
      createWall(CFrame.new(-240.888153, 225.446411, 204.484818, -1, -8.74227766e-08, 0, -8.74227766e-08, 1, -8.74227766e-08, 7.64274186e-15, -8.74227766e-08, -1), Vector3.new(37.7000008, 244.639954, 125.269974))
      createWall(CFrame.new(-242.00853, 223.686432, 287.601959, -0.99984771, -8.7409461e-08, 0.0174524058, -8.89485108e-08, 1, -8.7409461e-08, -0.0174524058, -8.89485108e-08, -0.99984771), Vector3.new(84.8199768, 241.119949, 65.279953))
      createWall(CFrame.new(-266.261414, 223.686432, 329.667603, -0.737277329, -6.44548308e-08, 0.675590158, -1.46484751e-07, 1, -6.44548308e-08, -0.675590158, -1.46484751e-07, -0.737277329), Vector3.new(84.2599869, 241.119949, 103.149963))
      createWall(CFrame.new(-171.303024, 263.126404, 7.99746418, 0.999961913, 0, -0.00872653536, 0, 1, 0, 0.00872653536, 0, 0.999961913), Vector3.new(18.7299881, 319.999939, 135.039978))
      createWall(CFrame.new(-186.983673, 308.136475, -85.8008804, 0.878817141, 0, 0.477158755, 0, 1, 0, -0.477158755, 0, 0.878817141), Vector3.new(15.7299871, 229.979904, 62.4799805))
      createWall(CFrame.new(-228.494202, 263.126404, -183.719955, 0.999961913, 0, -0.00872653536, 0, 1, 0, 0.00872653536, 0, 0.999961913), Vector3.new(10.2299871, 319.999939, 135.039978))
      createWall(CFrame.new(-216.488495, 308.136475, -116.623718, 0.507538378, 0, 0.861629128, 0, 1, 0, -0.861629128, 0, 0.507538378), Vector3.new(14.2299871, 229.979904, 31.0399818))
      createWall(CFrame.new(-180.638794, 263.126404, -276.830627, 0.995396197, 0, 0.0958457515, 0, 1, 0, -0.0958457515, 0, 0.995396197), Vector3.new(113.549988, 319.999939, 97.3899994))
      createWall(CFrame.new(-54.6073608, 263.126404, 74.6437073, 0.891006529, 0, -0.453990489, 0, 1, 0, 0.453990489, 0, 0.891006529), Vector3.new(14.7299871, 319.999939, 115.449997))
      createWall(CFrame.new(-37.863369, 263.126404, -4.13345909, 0.999961913, 0, -0.00872653536, 0, 1, 0, 0.00872653536, 0, 0.999961913), Vector3.new(10.2299871, 319.999939, 108.449997))
      createWall(CFrame.new(-31.8706627, 263.126404, -72.4572144, 0.945518553, 0, -0.32556814, 0, 1, 0, 0.32556814, 0, 0.945518553), Vector3.new(10.2299871, 319.999939, 35.8099937))
      createWall(CFrame.new(-7.3540988, 263.126404, -107.615921, 0.713250458, 0, -0.700909257, 0, 1, 0, 0.700909257, 0, 0.713250458), Vector3.new(10.2299871, 319.999939, 58.8699951))
      createWall(CFrame.new(5.32070923, 263.126404, -181.679382, 0.999961913, 0, -0.00872653536, 0, 1, 0, 0.00872653536, 0, 0.999961913), Vector3.new(10.2299871, 319.999939, 135.039978))
      createWall(CFrame.new(-23.2827835, 263.126404, -230.279099, 0.32556814, 0, 0.945518553, 0, 1, 0, -0.945518553, 0, 0.32556814), Vector3.new(29.2299881, 319.999939, 142.539978))
      createWall(CFrame.new(-115.024994, 241.249969, -414.445007, 1, 0, 0, 0, 1, 0, 0, 0, 1), Vector3.new(190.049988, 2.49993896, 169.889999))
      createWall(CFrame.new(-209.274994, 249.999969, -366.445007, 1, 0, 0, 0, 1, 0, 0, 0, 1), Vector3.new(3.54998779, 19.999939, 20.8899994))
      createWall(CFrame.new(-109.024994, 252.035263, -308.551788, 1, 0, 0, 0, 0.906307757, 0.42261827, 0, -0.42261827, 0.906307757), Vector3.new(48.0499878, 1.99993896, 61.8899994))
      createWall(CFrame.new(-109.024994, 268.374207, -263.68924, 1, 0, 0, 0, 0.974370062, 0.224951088, 0, -0.224951088, 0.974370062), Vector3.new(48.0499878, 2.49993896, 36.8899994))
      createWall(CFrame.new(-109.024994, 270.498352, -240.767548, 1, 0, 0, 0, 0.9510566, -0.309016943, 0, 0.309016943, 0.9510566), Vector3.new(48.0499878, 2.49993896, 11.8899994))
      createWall(CFrame.new(-114.774994, 255.249969, -85.0700073, 1, 0, 0, 0, 1, 0, 0, 0, 1), Vector3.new(232.549988, 30.499939, 309.140015))
      createWall(CFrame.new(-53.2749939, 255.999969, -24.6950073, 1, 0, 0, 0, 1, 0, 0, 0, 1), Vector3.new(109.549988, 31.999939, 59.3900146))
      createWall(CFrame.new(-28.5249939, 273.499969, 15.3049927, 1, 0, 0, 0, 1, 0, 0, 0, 1), Vector3.new(60.0499878, 66.999939, 139.390015))
      createWall(CFrame.new(-80.7749939, 267.999969, 54.8049927, 1, 0, 0, 0, 1, 0, 0, 0, 1), Vector3.new(164.549988, 6.99993896, 23.3900146))
      createWall(CFrame.new(-154.774994, 279.999969, 52.0549927, 1, 0, 0, 0, 1, 0, 0, 0, 1), Vector3.new(16.5499878, 30.999939, 28.8900146))
      createWall(CFrame.new(-137.024994, 267.999969, 14.5549927, 1, 0, 0, 0, 1, 0, 0, 0, 1), Vector3.new(39.0499878, 6.99993896, 29.8900146))
      createWall(CFrame.new(-167.024994, 267.749969, -113.406532, 0.866025388, 0, 0.5, 0, 1, 0, -0.5, 0, 0.866025388), Vector3.new(39.0499878, 6.49993896, 103.890015))
      createWall(CFrame.new(-170.580597, 271.249969, -111.065025, 0.866025388, 0, 0.5, 0, 1, 0, -0.5, 0, 0.866025388), Vector3.new(24.5499878, 1.49993896, 92.3900146))
      createWall(CFrame.new(-176.571625, 271.749969, -119.441788, 0.866025388, 0, 0.5, 0, 1, 0, -0.5, 0, 0.866025388), Vector3.new(15.5499878, 2.49993896, 63.8900146))
      createWall(CFrame.new(-155.324982, 270.499908, -185.195007, 1, 0, 0, 0, 1, 0, 0, 0, 0.99999994), Vector3.new(35.5499878, 1.99993896, 36.3900146))
      createWall(CFrame.new(-158.574982, 270.999908, -193.195007, 1, 0, 0, 0, 1, 0, 0, 0, 0.99999994), Vector3.new(21.0499878, 2.99993896, 16.3900146))
      createWall(CFrame.new(-160.074982, 271.249908, -193.695007, 1, 0, 0, 0, 1, 0, 0, 0, 0.99999994), Vector3.new(10.0499878, 3.49993896, 7.39001465))
      createWall(CFrame.new(-47.5749817, 270.499908, -162.195007, 1, 0, 0, 0, 1, 0, 0, 0, 0.99999994), Vector3.new(70.0499878, 1.99993896, 118.390015))
      createWall(CFrame.new(-49.8249817, 270.999908, -181.695007, 1, 0, 0, 0, 1, 0, 0, 0, 0.99999994), Vector3.new(52.5499878, 2.99993896, 55.3900146))
      createWall(CFrame.new(-141.574982, 287.499908, -233.195007, 1, 0, 0, 0, 1, 0, 0, 0, 0.99999994), Vector3.new(55.0499878, 35.999939, 15.3900146))
      createWall(CFrame.new(-7.88667679, 275.376404, -116.717194, 0.999961913, 0, -0.0087265335, 0, 1, 0, 0.00872653536, 0, 0.999961793), Vector3.new(15.0499878, 22.499939, 30.8900146))
      createWall(CFrame.new(-216.351822, 277.376404, -126.646851, 0.999961913, 0, -0.00872653257, 0, 1, 0, 0.0087265363, 0, 0.999961674), Vector3.new(15.0499878, 16.499939, 19.8900146))
      createWall(CFrame.new(-220.909836, 275.376404, -219.818344, 0.995396256, 0, 0.0958457068, 0, 1, 0, -0.0958457515, 0, 0.99539578), Vector3.new(16.5499878, 13.499939, 8.39001465))
      createWall(CFrame.new(-103.524994, 251.527222, 104.294586, 1, 0, 0, 0, 0.906307757, -0.42261827, 0, 0.42261827, 0.906307757), Vector3.new(99.0499878, 5.99993896, 78.8900146))
      createWall(CFrame.new(-108.024994, 236.249969, 298.054993, 1, 0, 0, 0, 0.99999994, 0, 0, 0, 0.99999994), Vector3.new(245.049988, 4.49993896, 338.890015))
      createWall(CFrame.new(-115.274994, 236.749969, 332.554993, 1, 0, 0, 0, 0.99999994, 0, 0, 0, 0.99999994), Vector3.new(39.5499878, 5.49993896, 40.8900146))
      createWall(CFrame.new(-114.524994, 237.249969, 331.554993, 1, 0, 0, 0, 0.99999994, 0, 0, 0, 0.99999994), Vector3.new(24.0499878, 6.49993896, 21.8900146))
      createWall(CFrame.new(-201.774994, 236.749969, 305.804993, 1, 0, 0, 0, 0.99999994, 0, 0, 0, 0.99999994), Vector3.new(59.5499878, 5.49993896, 149.390015))
      createWall(CFrame.new(-206.274994, 259.249969, 305.054993, 1, 0, 0, 0, 0.99999994, 0, 0, 0, 0.99999994), Vector3.new(50.5499878, 50.499939, 148.890015))
      createWall(CFrame.new(-195.774994, 236.749969, 253.054993, 1, 0, 0, 0, 0.99999994, 0, 0, 0, 0.99999994), Vector3.new(71.5499878, 5.49993896, 36.8900146))
      createWall(CFrame.new(-201.024994, 237.249969, 251.054993, 1, 0, 0, 0, 0.99999994, 0, 0, 0, 0.99999994), Vector3.new(61.0499878, 6.49993896, 24.8900146))
      createWall(CFrame.new(-60.7749939, 236.749969, 330.554993, 1, 0, 0, 0, 0.99999994, 0, 0, 0, 0.99999994), Vector3.new(47.5499878, 5.49993896, 44.8900146))
      createWall(CFrame.new(-61.5249939, 237.249969, 331.554993, 1, 0, 0, 0, 0.99999994, 0, 0, 0, 0.99999994), Vector3.new(20.0499878, 6.49993896, 17.8900146))
      createWall(CFrame.new(-29.0249939, 236.749969, 293.554993, 1, 0, 0, 0, 0.99999994, 0, 0, 0, 0.99999994), Vector3.new(30.0499878, 5.49993896, 32.8900146))
      createWall(CFrame.new(-26.0249939, 237.249969, 293.804993, 1, 0, 0, 0, 0.99999994, 0, 0, 0, 0.99999994), Vector3.new(11.0499878, 6.49993896, 23.3900146))
      createWall(CFrame.new(-16.2749939, 236.749969, 210.804993, 1, 0, 0, 0, 0.99999994, 0, 0, 0, 0.99999994), Vector3.new(35.5499878, 5.49993896, 34.3900146))
      createWall(CFrame.new(-69.3916397, 236.499969, 184.50386, 0.96126169, 0, 0.275637299, 0, 0.999999821, 0, -0.275637329, 0, 0.961261511), Vector3.new(84.0499878, 4.99993896, 38.8900146))
      createWall(CFrame.new(-66.1986313, 236.749969, 183.848358, 0.96126169, 0, 0.275637299, 0, 0.999999821, 0, -0.275637329, 0, 0.961261511), Vector3.new(57.5499878, 5.49993896, 30.3900146))
      createWall(CFrame.new(-62.4224892, 236.999969, 182.505493, 0.96126169, 0, 0.275637299, 0, 0.999999821, 0, -0.275637329, 0, 0.961261511), Vector3.new(49.5499878, 5.99993896, 24.8900146))
      createWall(CFrame.new(-63.9332924, 237.249969, 182.678635, 0.96126169, 0, 0.275637299, 0, 0.999999821, 0, -0.275637329, 0, 0.961261511), Vector3.new(29.5499878, 6.49993896, 19.3900146))
      createWall(CFrame.new(-62.1821709, 237.499969, 182.436569, 0.96126169, 0, 0.275637299, 0, 0.999999821, 0, -0.275637329, 0, 0.961261511), Vector3.new(19.0499878, 6.99993896, 13.8900146))
      createWall(CFrame.new(-103.524994, 238.727341, 132.97348, 1, 0, 0, 0, 0.965925813, -0.258819044, 0, 0.258819044, 0.965925813), Vector3.new(99.0499878, 9.49993896, 32.3900146))
      createWall(CFrame.new(-130.324982, 238.999908, 150.914978, 1, 0, 0, 0, 0.999999881, -1.49011612e-08, 0, 0, 0.999999821), Vector3.new(45.5499878, 0.999940872, 19.3900146))
      createWall(CFrame.new(-131.824982, 239.499908, 147.914978, 1, 0, 0, 0, 0.999999881, -1.49011612e-08, 0, 0, 0.999999821), Vector3.new(34.5499878, 1.99994087, 13.3900146))
      createWall(CFrame.new(-134.824982, 239.749908, 145.914978, 1, 0, 0, 0, 0.999999881, -1.49011612e-08, 0, 0, 0.999999821), Vector3.new(22.5499878, 2.49994087, 9.39001465))
      createWall(CFrame.new(-2.22501421, 269.749908, 145.414978, 0.999999881, 0, 2.98023224e-08, 0, 0.999999583, 0, 2.98023224e-08, 0, 0.999999583), Vector3.new(18.5499878, 62.499939, 21.3900146))
      createWall(CFrame.new(-216.172623, 238.749939, 167.096695, 0.788009822, 0, -0.615660012, 0, 0.999997318, 0, 0.615660667, 0, 0.788008869), Vector3.new(18.5499878, 0.499946952, 55.3900146))
      createWall(CFrame.new(-217.157623, 238.999939, 166.327118, 0.788009822, 0, -0.615660012, 0, 0.999997318, 0, 0.615660667, 0, 0.788008869), Vector3.new(16.0499878, 0.999946952, 55.3900146))
      createWall(CFrame.new(-217.748642, 239.249939, 165.865372, 0.788009822, 0, -0.615660012, 0, 0.999997318, 0, 0.615660667, 0, 0.788008869), Vector3.new(14.5499878, 1.49994695, 55.3900146))
      createWall(CFrame.new(-205.281525, 241.749939, 149.908188, 0.788009822, 0, -0.615660012, 0, 0.999997318, 0, 0.615660667, 0, 0.788008869), Vector3.new(14.5499878, 6.49994707, 14.8900146))
      createWall(CFrame.new(-176.024994, 236.499969, 425.554993, 1, 0, 0, 0, 0.99999994, 0, 0, 0, 0.99999994), Vector3.new(26.0499878, 4.99993896, 46.8900146))
      createWall(CFrame.new(-177.524994, 236.749969, 425.054993, 1, 0, 0, 0, 0.99999994, 0, 0, 0, 0.99999994), Vector3.new(23.0499878, 5.49993896, 43.8900146))
      createWall(CFrame.new(-178.774994, 237.249969, 425.804993, 1, 0, 0, 0, 0.99999994, 0, 0, 0, 0.99999994), Vector3.new(20.5499878, 6.49993896, 38.3900146))
      createWall(CFrame.new(-180.774994, 237.499969, 429.054993, 1, 0, 0, 0, 0.99999994, 0, 0, 0, 0.99999994), Vector3.new(16.5499878, 6.99993896, 24.8900146))
      createWall(CFrame.new(-181.774994, 237.999969, 430.304993, 1, 0, 0, 0, 0.99999994, 0, 0, 0, 0.99999994), Vector3.new(14.5499878, 7.99993896, 18.3900146))
      createWall(CFrame.new(-124.774994, 236.499969, 415.804993, 1, 0, 0, 0, 0.99999994, 0, 0, 0, 0.99999994), Vector3.new(15.5499878, 4.99993896, 38.3900146))
      createWall(CFrame.new(-123.524994, 236.749969, 416.554993, 1, 0, 0, 0, 0.99999994, 0, 0, 0, 0.99999994), Vector3.new(13.0499878, 5.49993896, 25.8900146))
      createWall(CFrame.new(-121.774994, 236.999969, 416.304993, 1, 0, 0, 0, 0.99999994, 0, 0, 0, 0.99999994), Vector3.new(9.54998779, 5.99993896, 19.3900146))
      createWall(CFrame.new(-89.5749817, 280.749908, -237.695007, 1, 0, 0, 0, 1, 0, 0, 0, 0.99999994), Vector3.new(7.04998779, 22.499939, 6.39001465))
      createWall(CFrame.new(-50.7568512, 263.126404, -284.197937, 1, 0, 0, 0, 1, 0, 0, 0, 1), Vector3.new(82.5499878, 319.999939, 92.3899994))
      createWall(CFrame.new(-84.7568512, 263.126404, -250.447937, 1, 0, 0, 0, 1, 0, 0, 0, 1), Vector3.new(21.5499878, 319.999939, 24.8899994))
      createWall(CFrame.new(-20.2568512, 263.126404, -418.197937, 1, 0, 0, 0, 1, 0, 0, 0, 1), Vector3.new(4.54998779, 319.999939, 181.389999))
      createWall(CFrame.new(-212.506851, 263.126404, -418.197937, 1, 0, 0, 0, 1, 0, 0, 0, 1), Vector3.new(13.0499878, 319.999939, 181.389999))
      createWall(CFrame.new(-168.256851, 263.126404, -328.947937, 1, 0, 0, 0, 1, 0, 0, 0, 1), Vector3.new(79.5499878, 319.999939, 2.88999939))
      createWall(CFrame.new(-163.006851, 263.126404, -572.947937, 1, 0, 0, 0, 1, 0, 0, 0, 1), Vector3.new(90.0499878, 319.999939, 150.889999))
      createWall(CFrame.new(-53.5068512, 263.126404, -534.947937, 1, 0, 0, 0, 1, 0, 0, 0, 1), Vector3.new(71.0499878, 319.999939, 74.8899994))
      createWall(CFrame.new(-75.8494415, 263.126404, -590.692261, -0.258819044, 0, -0.965925753, 0, 1, 0, 0.965925753, 0, -0.258819044), Vector3.new(50.5499878, 319.999939, 10.3899994))
      createWall(CFrame.new(-47.9917145, 263.126404, -617.715088, -0.898792207, 0, -0.43836987, 0, 1, 0, 0.43836987, 0, -0.898792207), Vector3.new(50.5499878, 319.999939, 10.3899994))
      createWall(CFrame.new(-5.61179876, 263.126404, -643.846008, -0.798630357, 0, -0.601810753, 0, 1, 0, 0.601810753, 0, -0.798630357), Vector3.new(50.5499878, 319.999939, 10.3899994))
      createWall(CFrame.new(21.596756, 263.126404, -678.58075, -0.390731424, 0, -0.920504749, 0, 1, 0, 0.920504749, 0, -0.390731424), Vector3.new(48.5499878, 319.999939, 12.3899994))
      createWall(CFrame.new(32.232254, 263.126404, -711.717529, -0.224951372, 0, -0.974370062, 0, 1, 0, 0.974370062, 0, -0.224951372), Vector3.new(33.5499878, 319.999939, 17.8899994))
      createWall(CFrame.new(-91.2977295, 250.376404, -663.801025, 0.882947803, 0, 0.469471604, 0, 1, 0, -0.469471604, 0, 0.882947803), Vector3.new(121.049988, 76.499939, 17.8899994))
      createWall(CFrame.new(-35.862896, 250.376404, -706.077393, 0.374607325, 0, 0.927185595, 0, 1, 0, -0.927185595, 0, 0.374607325), Vector3.new(38.5499878, 76.499939, 17.8899994))
      createWall(CFrame.new(-36.112896, 250.376404, -724.327393, 1, 0, 0, 0, 1, 0, 0, 0, 1), Vector3.new(24.0499878, 76.499939, 7.38999939))
      createWall(CFrame.new(46.887104, 250.376404, -749.077393, 1, 0, 0, 0, 1, 0, 0, 0, 1), Vector3.new(5.04998779, 76.499939, 56.8899994))
      createWall(CFrame.new(35.387104, 250.376404, -795.827393, 1, 0, 0, 0, 1, 0, 0, 0, 1), Vector3.new(28.0499878, 76.499939, 47.3899994))
      createWall(CFrame.new(-37.862896, 250.376404, -787.827393, 1, 0, 0, 0, 1, 0, 0, 0, 1), Vector3.new(27.5499878, 76.499939, 38.3899994))
      createWall(CFrame.new(-48.362896, 250.376404, -748.077393, 1, 0, 0, 0, 1, 0, 0, 0, 1), Vector3.new(6.54998779, 76.499939, 42.8899994))
      createWall(CFrame.new(-38.4214478, 250.376404, -825.885254, 0.882947505, 0, 0.469471455, 0, 1, 0, -0.469471455, 0, 0.882947505), Vector3.new(6.04998779, 76.499939, 47.8899994))
      createWall(CFrame.new(1.74190998, 250.376404, -838.746277, 0.882947505, 0, 0.469471455, 0, 1, 0, -0.469471455, 0, 0.882947505), Vector3.new(14.0499878, 76.499939, 120.889999))
      createWall(CFrame.new(-78.6714478, 250.376404, -824.135254, 1, 0, 0, 0, 1, 0, 0, 0, 1), Vector3.new(58.5499878, 76.499939, 44.3899994))
      createWall(CFrame.new(-180.171448, 250.376404, -824.135254, 1, 0, 0, 0, 1, 0, 0, 0, 1), Vector3.new(120.549988, 76.499939, 44.3899994))
      createWall(CFrame.new(-187.421448, 250.376404, -892.635254, 1, 0, 0, 0, 1, 0, 0, 0, 1), Vector3.new(95.0499878, 76.499939, 13.3899994))
      createWall(CFrame.new(-114.421448, 250.376404, -892.635254, 1, 0, 0, 0, 1, 0, 0, 0, 1), Vector3.new(25.0499878, 76.499939, 13.3899994))
      createWall(CFrame.new(-58.4214478, 250.376404, -892.635254, 1, 0, 0, 0, 1, 0, 0, 0, 1), Vector3.new(55.0499878, 76.499939, 13.3899994))
      createWall(CFrame.new(-32.5747032, 250.376404, -881.752502, 0.866025448, 0, -0.5, 0, 1, 0, 0.5, 0, 0.866025448), Vector3.new(48.5499878, 76.499939, 13.3899994))
      createWall(CFrame.new(-123.171448, 250.376404, -901.135254, 1, 0, 0, 0, 1, 0, 0, 0, 1), Vector3.new(80.5499878, 76.499939, 0.38999939))
      createWall(CFrame.new(-140.421448, 250.376404, -897.885254, 1, 0, 0, 0, 1, 0, 0, 0, 1), Vector3.new(46.0499878, 76.499939, 6.88999939))
      createWall(CFrame.new(-116.171448, 250.376404, -828.635254, 1, 0, 0, 0, 1, 0, 0, 0, 1), Vector3.new(28.5499878, 76.499939, 10.3899994))
      createWall(CFrame.new(-530.105103, 279.979858, -1092.07043, 0.999390841, 0, -0.0348994955, 0, 1, 0, 0.0348994955, 0, 0.999390841), Vector3.new(66.3700256, 165.859863, 74.1800003))
      createWall(CFrame.new(-434.260559, 279.979858, -1090.26013, 0.999390841, 0, -0.0348994955, 0, 1, 0, 0.0348994955, 0, 0.999390841), Vector3.new(66.3700256, 165.859863, 75.3499756))
      createWall(CFrame.new(-623.851563, 279.979858, -1429.71814, -0.719339788, -6.28866843e-08, 0.694658399, -1.48151742e-07, 1, -6.28866843e-08, -0.694658399, -1.48151742e-07, -0.719339788), Vector3.new(159.419998, 165.859863, 17.4799919))
      createWall(CFrame.new(-587.972534, 279.979858, -1466.33179, -0.719339788, -6.28866843e-08, 0.694658399, -1.48151742e-07, 1, -6.28866843e-08, -0.694658399, -1.48151742e-07, -0.719339788), Vector3.new(160.169998, 165.859863, 44.1299934))
      createWall(CFrame.new(-510.793091, 279.979858, -1412.05334, -0.91354543, -7.98646766e-08, 0.406736642, -1.22980822e-07, 1, -7.98646766e-08, -0.406736642, -1.22980822e-07, -0.91354543), Vector3.new(149.439972, 165.859863, 22.9799919))
      createWall(CFrame.new(-471.971405, 279.979858, -1355.68689, -0.0174523834, -1.52573587e-09, 0.99984771, -1.74832238e-07, 1, -1.52573587e-09, -0.99984771, -1.74832238e-07, -0.0174523834), Vector3.new(145.919983, 165.859863, 19.7599926))
      createWall(CFrame.new(-585.297424, 279.979858, -1324.81335, -0.182235524, -1.59315352e-08, 0.98325491, -1.7338165e-07, 1, -1.59315352e-08, -0.98325491, -1.7338165e-07, -0.182235524), Vector3.new(128.960007, 165.859863, 42.9799919))
      createWall(CFrame.new(-588.963806, 279.979858, -1300.72192, 0.999390841, 0, -0.0348994955, 0, 1, 0, 0.0348994955, 0, 0.999390841), Vector3.new(142.960007, 165.859863, 17.4799919))
      createWall(CFrame.new(-703.672302, 279.979858, -1446.30786, -0.669130564, -5.84972533e-08, -0.74314487, -2.24549908e-08, 1, -5.84972533e-08, 0.74314487, -2.24549908e-08, -0.669130564), Vector3.new(69.8000183, 165.859863, 17.4799919))
      createWall(CFrame.new(-756.852478, 279.979858, -1402.3075, -0.870355666, -7.60889094e-08, -0.492423564, -4.4373742e-08, 1, -7.60889094e-08, 0.492423564, -4.4373742e-08, -0.870355666), Vector3.new(69.8000183, 165.859863, 17.4799919))
      createWall(CFrame.new(-797.608215, 279.979858, -1387.88354, -0.996917307, -8.71532819e-08, -0.0784590989, -8.0563666e-08, 1, -8.71532819e-08, 0.0784590989, -8.0563666e-08, -0.996917307), Vector3.new(55.3900223, 165.859863, 17.4799919))
      createWall(CFrame.new(-820.038269, 279.979858, -1385.85034, -0.662620068, -5.79280872e-08, 0.748955727, -1.52898565e-07, 1, -5.79280872e-08, -0.748955727, -1.52898565e-07, -0.662620068), Vector3.new(82.0700302, 165.859863, 17.4799919))
      createWall(CFrame.new(-841.949463, 279.979858, -1427.98669, 0.078459084, 0, -0.996917307, 0, 1, 0, 0.996917307, 0, 0.078459084), Vector3.new(55.3900223, 165.859863, 17.4799919))
      createWall(CFrame.new(-834.237122, 279.979858, -1469.92981, -0.42261824, -3.69464601e-08, -0.906307817, -8.19083112e-09, 1, -3.69464601e-08, 0.906307817, -8.19083112e-09, -0.42261824), Vector3.new(86.6100311, 165.859863, 17.4799919))
      createWall(CFrame.new(-767.177551, 279.979858, -1564.18726, -0.656059027, -5.73545016e-08, -0.754709542, -2.14439737e-08, 1, -5.73545016e-08, 0.754709542, -2.14439737e-08, -0.656059027), Vector3.new(160.029999, 165.859863, 17.4799919))
      createWall(CFrame.new(-720.77832, 279.979858, -1597.55005, -0.656059027, -5.73545016e-08, -0.754709542, -2.14439737e-08, 1, -5.73545016e-08, 0.754709542, -2.14439737e-08, -0.656059027), Vector3.new(57.8500061, 165.859863, 43.7400017))
      createWall(CFrame.new(-650.672546, 279.979858, -1540.46497, -0.656059027, -5.73545016e-08, -0.754709542, -2.14439737e-08, 1, -5.73545016e-08, 0.754709542, -2.14439737e-08, -0.656059027), Vector3.new(57.8500061, 165.859863, 43.7400017))
      createWall(CFrame.new(-686.894653, 279.979858, -1577.92639, -0.656059027, -5.73545016e-08, -0.754709542, -2.14439737e-08, 1, -5.73545016e-08, 0.754709542, -2.14439737e-08, -0.656059027), Vector3.new(57.8500061, 165.859863, 63.2200089))
      createWall(CFrame.new(-773.282104, 285.979858, -1474.0929, -0.669130683, 0, -0.74314481, 0, 1, 0, 0.74314481, 0, -0.669130683), Vector3.new(214.029999, 2.85986328, 126.479996))
      createWall(CFrame.new(-613.74707, 269.706024, -1446.57446, -0.694678783, 0.11874482, -0.709454238, -4.41642478e-05, 0.986274898, 0.165120974, 0.71931982, 0.114737399, -0.685142875), Vector3.new(22.5299988, 5.10986328, 165.479996))
      createWall(CFrame.new(-527.871521, 279.979858, -1234.82935, 0.999390841, 0, -0.0348994955, 0, 1, 0, 0.0348994955, 0, 0.999390841), Vector3.new(60.8700256, 165.859863, 61.6799927))
      createWall(CFrame.new(-558.849976, 279.979858, -1109.59131, 1, 0, 0, 0, 1, 0, 0, 0, 1), Vector3.new(1.87002563, 165.859863, 191.179993))
      createWall(CFrame.new(-417.599976, 279.979858, -1110.34131, 1, 0, 0, 0, 1, 0, 0, 0, 1), Vector3.new(1.37002563, 165.859863, 189.679993))
      createWall(CFrame.new(-431.140198, 279.979858, -1251.24927, 0.999390841, 0, -0.0348994955, 0, 1, 0, 0.0348994955, 0, 0.999390841), Vector3.new(71.3700256, 165.859863, 93.3499756))
      createWall(CFrame.new(-494.599976, 243.729858, -1086.84131, 1, 0, 0, 0, 1, 0, 0, 0, 1), Vector3.new(161.370026, 29.3598633, 664.679993))
      createWall(CFrame.new(-439.099976, 279.979858, -970.341309, 1, 0, 0, 0, 1, 0, 0, 0, 1), Vector3.new(50.3700256, 165.859863, 95.6799927))
      createWall(CFrame.new(-536.349976, 279.979858, -973.341309, 1, 0, 0, 0, 1, 0, 0, 0, 1), Vector3.new(68.8700256, 165.859863, 89.6799927))
      createWall(CFrame.new(-528.849976, 305.979858, -872.341309, 1, 0, 0, 0, 1, 0, 0, 0, 1), Vector3.new(83.8700256, 113.859863, 132.679993))
      createWall(CFrame.new(-522.703003, 305.979858, -802.900574, 0.965925813, 0, 0.258819044, 0, 1, 0, -0.258819044, 0, 0.965925813), Vector3.new(83.8700256, 113.859863, 87.1799927))
      createWall(CFrame.new(-510.382385, 305.979858, -783.183533, 0.848048031, 0, 0.529919267, 0, 1, 0, -0.529919267, 0, 0.848048031), Vector3.new(83.8700256, 113.859863, 133.679993))
      createWall(CFrame.new(-498.169495, 305.979858, -768.628662, 0.766044259, 0, 0.642787516, 0, 1, 0, -0.642787516, 0, 0.766044259), Vector3.new(83.8700256, 113.859863, 171.679993))
      createWall(CFrame.new(-483.661346, 305.979858, -758.842712, 0.559192538, 0, 0.82903707, 0, 1, 0, -0.82903707, 0, 0.559192538), Vector3.new(83.8700256, 113.859863, 206.679993))
      createWall(CFrame.new(-364.621796, 305.979858, -708.448608, 0.0174524225, 0, 0.99984771, 0, 1, 0, -0.99984771, 0, 0.0174524225), Vector3.new(83.8700256, 113.859863, 116.679993))
      createWall(CFrame.new(-340.879913, 305.979858, -765.881897, -0.453990519, 0, 0.891006529, 0, 1, 0, -0.891006529, 0, -0.453990519), Vector3.new(8.37002563, 113.859863, 168.179993))
      createWall(CFrame.new(-329.829071, 295.979858, -781.740417, -0.766044497, 0, 0.642787576, 0, 1, 0, -0.642787576, 0, -0.766044497), Vector3.new(7.37002563, 133.859863, 194.179993))
      createWall(CFrame.new(-474.099976, 244.229858, -797.341309, 1, 0, 0, 0, 1, 0, 0, 0, 1), Vector3.new(257.370026, 30.3598633, 85.6799927))
      createWall(CFrame.new(-523.349976, 305.979858, -827.341309, 1, 0, 0, 0, 1, 0, 0, 0, 1), Vector3.new(94.8700256, 113.859863, 42.6799927))
      createWall(CFrame.new(-475.599976, 244.729858, -791.841309, 1, 0, 0, 0, 1, 0, 0, 0, 1), Vector3.new(254.370026, 31.3598633, 74.6799927))
      createWall(CFrame.new(-477.599976, 245.229858, -787.341309, 1, 0, 0, 0, 1, 0, 0, 0, 1), Vector3.new(250.370026, 32.3598633, 65.6799927))
      createWall(CFrame.new(-478.599976, 245.479858, -784.341309, 1, 0, 0, 0, 1, 0, 0, 0, 1), Vector3.new(248.370026, 32.8598633, 59.6799927))
      createWall(CFrame.new(-478.599976, 245.729858, -781.841309, 1, 0, 0, 0, 1, 0, 0, 0, 1), Vector3.new(248.370026, 33.3598633, 54.6799927))
      createWall(CFrame.new(-439.849976, 272.229858, -883.341309, 1, 0, 0, 0, 1, 0, 0, 0, 1), Vector3.new(51.8700256, 86.3598633, 123.679993))
      createWall(CFrame.new(-379.849976, 272.229858, -832.841309, 1, 0, 0, 0, 1, 0, 0, 0, 1), Vector3.new(68.8700256, 86.3598633, 19.6799927))
      createWall(CFrame.new(-325.158051, 241.062012, -822.414978, 0.789027095, 0.334922045, 0.515037596, -0.390731275, 0.920504749, 4.84287739e-08, -0.474095762, -0.201241508, 0.857167423), Vector3.new(9.37002563, 14.8598633, 8.17999268))
      createWall(CFrame.new(-345.652191, 245.233566, -781.809937, 0.850778162, 0.104462422, 0.515038013, -0.121869348, 0.992546141, 0, -0.511199117, -0.0627673566, 0.857167304), Vector3.new(31.3700256, 33.3598633, 54.6799927))
      createWall(CFrame.new(-345.599976, 272.229858, -831.341309, 1, 0, 0, 0, 1, 0, 0, 0, 1), Vector3.new(0.370025635, 86.3598633, 22.6799927))
      createWall(CFrame.new(-341.921783, 249.663269, -835.159546, 0.848048091, 0, 0.529919267, 0, 1, 0, -0.529919267, 0, 0.848048091), Vector3.new(29.3700256, 76.8598633, 32.1799927))
      createWall(CFrame.new(-320.835754, 230.047226, -824.571289, 0.776302516, 0.0652871206, 0.626969218, -0.284233958, 0.92402339, 0.255714566, -0.562643945, -0.37671876, 0.735880792), Vector3.new(52.3700256, 31.3598633, 95.6799927))
      createWall(CFrame.new(-289.109406, 220.88858, -848.419983, 0.778962135, 0.0109720025, 0.626974881, -0.219083488, 0.941601098, 0.255714387, -0.587554574, -0.336551666, 0.735875428), Vector3.new(50.8700256, 30.8598633, 95.6799927))
      createWall(CFrame.new(-89.6850128, 249.173721, -513.710205, 1, 0, 0, 0, 0.994521797, 0.104528457, 0, -0.104528457, 0.994521797), Vector3.new(5.37002563, 16.8598633, 30.6799927))
      createWall(CFrame.new(-510.848236, 279.979858, -1284.52026, 0.798635483, 0, 0.601814926, 0, 1, 0, -0.601814926, 0, 0.798635483), Vector3.new(12.8700256, 165.859863, 39.6799927))
      createWall(CFrame.new(-510.486816, 279.979858, -1279.47107, 0.798635483, 0, 0.601814926, 0, 1, 0, -0.601814926, 0, 0.798635483), Vector3.new(7.37002563, 165.859863, 42.1799927))
      createWall(CFrame.new(-512.099976, 273.589722, -1203.34131, 1, 0, 0, 0, 1, 0, 0, 0, 1), Vector3.new(15.3700256, 30.3598633, 9.67999268))
      createWall(CFrame.new(-450.099976, 273.589722, -1203.34131, 1, 0, 0, 0, 1, 0, 0, 0, 1), Vector3.new(20.3700256, 30.3598633, 9.67999268))
      createWall(CFrame.new(-294.008087, 223.338501, -850.775452, 1, 0, 0, 0, 1, 0, 0, 0, 1), Vector3.new(25.3700256, 23.8598633, 15.1799927))
      createWall(CFrame.new(-328.758087, 223.338501, -860.025452, 1, 0, 0, 0, 1, 0, 0, 0, 1), Vector3.new(18.8700256, 23.8598633, 7.67999268))
      createWall(CFrame.new(-33.4668579, 239.946518, -446.482941, 1, 0, 0, 0, 0.999999762, 0, 0, 0, 0.999999762), Vector3.new(21.8700256, 7.35986328, 26.1799927))
      createWall(CFrame.new(-24.9668579, 249.946518, -446.232941, 1, 0, 0, 0, 0.999999762, 0, 0, 0, 0.999999762), Vector3.new(4.87002563, 27.3598633, 20.6799927))
      createWall(CFrame.new(-327.824738, 237.437775, -801.812622, 0.762220681, 0.371759921, 0.529919147, -0.438371092, 0.898793995, 1.49011612e-08, -0.476288557, -0.232301384, 0.84804821), Vector3.new(27.8700256, 31.8598633, 64.6799927))
      createWall(CFrame.new(-336.758087, 222.838501, -903.525452, 1, 0, 0, 0, 1, 0, 0, 0, 1), Vector3.new(159.870026, 22.8598633, 147.679993))
      createWall(CFrame.new(-339.008087, 269.588501, -954.775452, 1, 0, 0, 0, 1, 0, 0, 0, 1), Vector3.new(164.370026, 116.359863, 45.1799927))
      createWall(CFrame.new(-271.008087, 243.088501, -925.025452, 1, 0, 0, 0, 1, 0, 0, 0, 1), Vector3.new(28.3700256, 63.3598633, 104.679993))
      createWall(CFrame.new(-399.008087, 223.338501, -934.775452, 1, 0, 0, 0, 1, 0, 0, 0, 1), Vector3.new(35.3700256, 23.8598633, 85.1799927))
      createWall(CFrame.new(-165.758087, 222.838501, -867.025452, 1, 0, 0, 0, 1, 0, 0, 0, 1), Vector3.new(197.870026, 22.8598633, 69.6799927))
      createWall(CFrame.new(-253.171448, 250.376404, -830.885254, 1, 0, 0, 0, 1, 0, 0, 0, 1), Vector3.new(38.5499878, 76.499939, 57.8899994))
      createWall(CFrame.new(-253.171448, 250.376404, -883.635254, 1, 0, 0, 0, 1, 0, 0, 0, 1), Vector3.new(38.5499878, 76.499939, 21.3899994))
      createWall(CFrame.new(-483.418579, 267.041748, -1068.15332, -0.999052703, -0.0155198928, 0.040654961, 5.86081296e-06, 0.934192657, 0.356768906, -0.04351658, 0.356431216, -0.933307588), Vector3.new(31.6913509, 2.7721417, 4.24422979))
      createWall(CFrame.new(-483.981842, 260.92804, -1055.25232, -0.999047458, -0.0207527075, 0.0383878089, 9.14558768e-07, 0.879672229, 0.475580454, -0.0436382741, 0.475127459, -0.878834188), Vector3.new(31.6913509, 2.74081826, 18.896841))
      createWall(CFrame.new(-483.538757, 266.034851, -1065.40332, -0.999046981, -0.0144734327, 0.0411781222, 2.83131376e-05, 0.943206012, 0.332208306, -0.0436476469, 0.331892908, -0.942306757), Vector3.new(31.6913509, 2.76432514, 4.3225441))
      createWall(CFrame.new(-481.38623, 266.034943, -1114.70557, 0.999046981, 0.0144734401, -0.0411781222, 2.83066183e-05, 0.943206012, 0.332208335, 0.0436476506, -0.331892937, 0.942306757), Vector3.new(31.6913509, 2.76432514, 4.3225441))
      createWall(CFrame.new(-480.943359, 260.928314, -1124.85657, 0.999047458, 0.0207526181, -0.0383878089, 9.90927219e-07, 0.879672289, 0.475580454, 0.0436382294, -0.475127459, 0.878834248), Vector3.new(31.6913509, 2.74081826, 18.896841))
      createWall(CFrame.new(-482.463654, 268.856995, -1090.03271, 0.999048233, 0, -0.0436193869, 0, 1, 0, 0.0436193869, 0, 0.999048233), Vector3.new(31.6913509, 2.74081826, 23.9508228))
      createWall(CFrame.new(-481.854034, 268.718964, -1104.005, 0.999045253, 0.00244113314, -0.0436193869, -7.33807683e-05, 0.99853003, 0.0542014502, 0.0436875783, -0.0541465022, 0.997576892), Vector3.new(31.6913509, 2.74081826, 4.3225441))
      createWall(CFrame.new(-483.248901, 268.208527, -1072.04712, -0.999044776, -0.00906737149, 0.0427475348, 9.39015299e-05, 0.977787733, 0.209597498, -0.043698512, 0.209401295, -0.976852834), Vector3.new(31.6913509, 2.74081826, 4.3225441))
      createWall(CFrame.new(-481.506134, 267.04184, -1111.95569, 0.999052703, 0.0155199626, -0.040654961, 5.79282641e-06, 0.934192657, 0.356768847, 0.0435166061, -0.356431156, 0.933307588), Vector3.new(31.6913509, 2.7721417, 4.24422979))
      createWall(CFrame.new(-481.676361, 268.208527, -1108.06177, 0.999044776, 0.00906729046, -0.0427475348, 9.39778984e-05, 0.977787733, 0.209597453, 0.0436984971, -0.20940125, 0.976852894), Vector3.new(31.6913509, 2.74081826, 4.3225441))
      createWall(CFrame.new(-483.071716, 268.719055, -1076.10388, -0.999045253, -0.00244113663, 0.0436193869, -7.33849593e-05, 0.99853003, 0.0542014316, -0.0436875783, 0.0541464835, -0.997576892), Vector3.new(31.6913509, 2.74081826, 4.3225441))
      createWall(CFrame.new(-483.349976, 244.229858, -1089.84131, 1, 0, 0, 0, 1, 0, 0, 0, 1), Vector3.new(39.8700256, 30.3598633, 91.6799927))
      createWall(CFrame.new(-367.75824, 249.663269, -845.841492, 0.848048091, 0, 0.529919267, 0, 1, 0, -0.529919267, 0, 0.848048091), Vector3.new(34.8700256, 76.8598633, 13.6799927))
      createWall(CFrame.new(-43.2580872, 223.338501, -867.025452, 1, 0, 0, 0, 1, 0, 0, 0, 1), Vector3.new(50.8700256, 23.8598633, 69.6799927))
      createWall(CFrame.new(-40.5080872, 223.838501, -867.025452, 1, 0, 0, 0, 1, 0, 0, 0, 1), Vector3.new(47.3700256, 24.8598633, 69.6799927))
      createWall(CFrame.new(4.49191284, 224.838501, -762.025452, 1, 0, 0, 0, 1, 0, 0, 0, 1), Vector3.new(99.3700256, 26.8598633, 124.679993))
      createWall(CFrame.new(-25.2580872, 224.338501, -852.025452, 1, 0, 0, 0, 1, 0, 0, 0, 1), Vector3.new(36.8700256, 25.8598633, 55.6799927))
      createWall(CFrame.new(-37.7580872, 237.588501, -825.775452, 1, 0, 0, 0, 1, 0, 0, 0, 1), Vector3.new(11.8700256, 52.3598633, 22.1799927))
      createWall(CFrame.new(10.7419128, 224.838501, -837.275452, 1, 0, 0, 0, 1, 0, 0, 0, 1), Vector3.new(86.8700256, 26.8598633, 50.1799927))
      createWall(CFrame.new(4.49191284, 224.338501, -703.525452, 1, 0, 0, 0, 1, 0, 0, 0, 1), Vector3.new(99.3700256, 25.8598633, 15.6799927))
      createWall(CFrame.new(4.49191284, 223.838501, -701.525452, 1, 0, 0, 0, 1, 0, 0, 0, 1), Vector3.new(99.3700256, 24.8598633, 19.6799927))
      createWall(CFrame.new(8.24191284, 223.338501, -667.775452, 1, 0, 0, 0, 1, 0, 0, 0, 1), Vector3.new(91.8700256, 23.8598633, 87.1799927))
      createWall(CFrame.new(-32.2580872, 223.088501, -637.275452, 1, 0, 0, 0, 1, 0, 0, 0, 1), Vector3.new(172.870026, 23.3598633, 148.179993))
      createWall(CFrame.new(-115.024994, 237.18399, -535.179443, 1, 0, 0, 0, 0.994521797, 0.104528457, 0, -0.104528457, 0.994521797), Vector3.new(190.049988, 2.49993896, 75.8899994))
      createWall(CFrame.new(-110.508087, 223.338501, -580.775452, 1, 0, 0, 0, 1, 0, 0, 0, 1), Vector3.new(16.3700256, 23.8598633, 35.1799927))
      createWall(CFrame.new(14.4349861, 247.448364, -670.319519, 0.874619722, 0, -0.484809607, 0, 1, 0, 0.484809607, 0, 0.874619722), Vector3.new(16.8700256, 24.3598633, 64.1799927))
      createWall(CFrame.new(-114.508087, 246.948364, -651.275452, 1, 0, 0, 0, 1, 0, 0, 0, 1), Vector3.new(13.3700256, 24.3598633, 42.1799927))
      createWall(CFrame.new(-327.09436, 240.060562, -797.918823, 0.789027095, 0.334922045, 0.515037596, -0.390731275, 0.920504749, 4.84287739e-08, -0.474095762, -0.201241508, 0.857167423), Vector3.new(29.8700256, 28.8598633, 63.1799927))
      createWall(CFrame.new(-664.139648, 282.215668, -1495.0968, -0.691134691, 0.299709588, -0.657652676, 0, 0.909961283, 0.414693236, 0.722725987, 0.286608875, -0.628905833), Vector3.new(25.5299988, 5.60986328, 12.4799957))
      wait(.1)
      game:GetService("Workspace").dungeon.room5["barrier"]:Destroy()
      if _G.destroy_map then
        --workspace.Terrain:Clear()
        for i,v in pairs(workspace:GetChildren()) do
          if v.ClassName == "Model" or v.ClassName == "Part" or v.ClassName == "UnionOperation" or v.ClassName == "WedgePart" then
            if v ~= game.Players.LocalPlayer.Character and v.Name ~= regionPartName then
              v:Destroy()
            end
          end
        end
      end

      while not game:GetService("Workspace").dungeon.room5.enemyFolder:FindFirstChild("Spider Queen") do -- wait for spider boss to spawn
        wait(1)
      end
      while not game:GetService("Workspace").dungeon.room5.enemyFolder:FindFirstChild("Spider Queen"):FindFirstChild("HumanoidRootPart") do
        wait(1)
      end
      local objPart = createWall(CFrame.new(-198.633, 235.589, -866.15), Vector3.new(3.62, 2.86, 4.93))
      objPart.CanCollide = false
      objectiveExists = true
      objectiveObject = objPart
      while wait(1) do
        local _,_,_,root = getPlayer()
        if getMag(root.Position, objPart.Position) < 5 then break end
      end
      objectiveExists = false
      objectiveObject = nil
    end

    function kingFix()
      createWall(CFrame.new(-265.670135, 39.9012566, 821.916565, 0.267238349, 0, 0.963630438, 0, 1, 0, -0.963630438, 0, 0.267238349), Vector3.new(205.490036, 121.409996, 83.2699738))
      createWall(CFrame.new(-84.1567535, 39.9012566, 206.857864, -4.37113883e-08, 0, -1, 0, 1, 0, 1, 0, -4.37113883e-08), Vector3.new(7.70991707, 121.409996, 20.2999802))
      createWall(CFrame.new(-87.2210388, 39.9012566, 185.695068, 1, 0, 0, 0, 1, 0, 0, 0, 1), Vector3.new(7.70991707, 121.409996, 38.0599823))
      createWall(CFrame.new(30.827137, 50.6512566, 315.457825, -4.37113883e-08, 0, -1, 0, 1, 0, 1, 0, -4.37113883e-08), Vector3.new(224.909897, 99.909996, 40.819973))
      createWall(CFrame.new(-201.965851, 39.9012566, 538.666504, 0.999657333, 0, 0.02617695, 0, 1, 0, -0.02617695, 0, 0.999657333), Vector3.new(182.820007, 121.409996, 128.269974))
      createWall(CFrame.new(-241.969254, 39.9012566, 610.253235, -0.0261769947, -2.28846564e-09, 0.999657333, -1.74815597e-07, 1, -2.28846564e-09, -0.999657333, -1.74815597e-07, -0.0261769947), Vector3.new(251.470016, 121.409996, 81.7699738))
      createWall(CFrame.new(-13.5106697, 61.6240005, -82.0305099, 0.0261769947, 0, -0.999657333, 0, 1, 0, 0.999657333, 0, 0.0261769947), Vector3.new(60.3699608, 70.859993, 81.8800201))
      createWall(CFrame.new(59.8843384, 39.9012566, 206.815186, 1, 0, 0, 0, 1, 0, 0, 0, 1), Vector3.new(29.4499016, 121.409996, 7.64001656))
      createWall(CFrame.new(-52.9094086, 39.9012566, 315.457825, -4.37113883e-08, 0, -1, 0, 1, 0, 1, 0, -4.37113883e-08), Vector3.new(224.909897, 121.409996, 40.819973))
      createWall(CFrame.new(74.1219025, 39.9012527, 575.307129, -0.999390841, -8.73695214e-08, -0.0348994955, -8.43717629e-08, 1, -8.73695214e-08, 0.0348994955, -8.43717629e-08, -0.999390841), Vector3.new(125.539993, 121.409996, 237.639999))
      createWall(CFrame.new(37.6457291, 39.9012566, 151.17514, 1, 0, 0, 0, 1, 0, 0, 0, 1), Vector3.new(62.3399086, 121.409996, 43.2400017))
      createWall(CFrame.new(0.196162999, 65.1762543, 441.391022, 0.0261769947, 0, -0.999657333, 0, 1, 0, 0.999657333, 0, 0.0261769947), Vector3.new(62.0499763, 70.859993, 81.8800201))
      createWall(CFrame.new(-55.767437, 39.9012566, 12.0568619, -4.37113883e-08, 0, 1, 0, 1, 0, -1, 0, -4.37113883e-08), Vector3.new(242.48996, 121.409996, 43.2400017))
      createWall(CFrame.new(31.8941364, 39.9012566, 16.1985588, 0.0174523834, 0, 0.99984771, 0, 1, 0, -0.99984771, 0, 0.0174523834), Vector3.new(234.210022, 121.409996, 43.2400017))
      createWall(CFrame.new(-7.2978816, 63.2866745, 155.216705, 0.0261769947, 0, -0.999657333, 0, 1, 0, 0.999657333, 0, 0.0261769947), Vector3.new(62.0499763, 68.6600037, 81.8800201))
      createWall(CFrame.new(66.2143402, 39.9012566, 170.095139, 1, 0, 0, 0, 1, 0, 0, 0, 1), Vector3.new(16.7899017, 121.409996, 81.0800095))
      createWall(CFrame.new(-108.321632, 39.9012566, 444.232849, 0.0261769947, 0, -0.999657333, 0, 1, 0, 0.999657333, 0, 0.0261769947), Vector3.new(62.0499763, 121.409996, 155.169968))
      createWall(CFrame.new(84.8040543, 39.9012566, 451.600067, 0.0348994955, 0, -0.999390841, 0, 1, 0, 0.999390841, 0, 0.0348994955), Vector3.new(62.0499763, 121.409996, 155.169968))
      createWall(CFrame.new(97.8463821, 39.9012566, 665.138977, -0.0348994955, -3.05101078e-09, 0.999390841, -1.74792291e-07, 1, -3.05101078e-09, -0.999390841, -1.74792291e-07, -0.0348994955), Vector3.new(19.5399895, 121.409996, 56.4300117))
      createWall(CFrame.new(46.9567528, 39.9012566, 674.57135, -0.366501212, -3.20405533e-08, 0.930417597, -1.68762469e-07, 1, -3.20405533e-08, -0.930417597, -1.68762469e-07, -0.366501212), Vector3.new(19.5399895, 121.409996, 56.4300117))
      createWall(CFrame.new(-34.3111458, 39.9012566, 725.983276, -0.719339788, -6.28866843e-08, 0.694658399, -1.48151742e-07, 1, -6.28866843e-08, -0.694658399, -1.48151742e-07, -0.719339788), Vector3.new(42.0399895, 121.409996, 197.409988))
      createWall(CFrame.new(-112.350136, 39.9012566, 837.091858, -0.965925813, -8.44439185e-08, 0.258819044, -1.10049456e-07, 1, -8.44439185e-08, -0.258819044, -1.10049456e-07, -0.965925813), Vector3.new(40.0399895, 121.409996, 103.629967))
      createWall(CFrame.new(-139.625366, 39.9012566, 961.8349, -0.968147635, -8.46381525e-08, 0.250380009, -1.09311692e-07, 1, -8.46381525e-08, -0.250380009, -1.09311692e-07, -0.968147635), Vector3.new(47.8199997, 121.409996, 187.62999))
      createWall(CFrame.new(-200.630081, 65.554451, 1018.6449, -2.18195708e-18, -8.74227837e-08, 1.00000024, -8.74227695e-08, 1, 8.74227837e-08, -1.00000024, -8.74227979e-08, 7.6405599e-15), Vector3.new(60.8199997, 121.409996, 125.489998))
      createWall(CFrame.new(-230.756363, 39.9012566, 1027.81616, 1, 0, 0, 0, 1, 0, 0, 0, 1), Vector3.new(40.8199997, 121.409996, 136.48999))
      createWall(CFrame.new(-253.298645, 39.9012566, 919.571655, 0.902585268, 0, 0.430511087, 0, 1, 0, -0.430511087, 0, 0.902585268), Vector3.new(43.3199997, 121.409996, 114.269997))
      createWall(CFrame.new(-59.9060516, 39.9012566, 151.17514, 1, 0, 0, 0, 1, 0, 0, 0, 1), Vector3.new(62.3399086, 121.409996, 43.2400017))
      createWall(CFrame.new(37.8478165, 16.8362617, -190.005951, -4.37113883e-08, 0, 1, 0, 1, 0, -1, 0, -4.37113883e-08), Vector3.new(16.16996, 75.2800064, 17.949995))
      createWall(CFrame.new(43.4540367, 16.8362617, -158.997726, -0.819152057, -7.1612547e-08, 0.57357645, -1.37566417e-07, 1, -7.1612547e-08, -0.57357645, -1.37566417e-07, -0.819152057), Vector3.new(28.7199612, 75.2800064, 21.4999905))
      createWall(CFrame.new(-78.8311462, 39.9012566, -291.1315, -4.37113883e-08, 0, 1, 0, 1, 0, -1, 0, -4.37113883e-08), Vector3.new(107.669968, 121.409996, 6.42999887))
      createWall(CFrame.new(-114.162926, 16.8362617, -234.379257, -4.37113883e-08, 0, 1, 0, 1, 0, -1, 0, -4.37113883e-08), Vector3.new(2.349967, 75.2800064, 3.74999881))
      createWall(CFrame.new(43.2896805, 16.8362617, -174.360001, -1, -8.74227766e-08, 0, -8.74227766e-08, 1, -8.74227766e-08, 7.64274186e-15, -8.74227766e-08, -1), Vector3.new(16.16996, 75.2800064, 17.949995))
      createWall(CFrame.new(-11.822731, 61.6240005, -17.5732212, 0.0261769947, 0, -0.999657333, 0, 1, 0, 0.999657333, 0, 0.0261769947), Vector3.new(3.48996258, 70.859993, 81.8800201))
      createWall(CFrame.new(-187.323776, 16.8362617, -240.981262, -4.37113883e-08, 0, 1, 0, 1, 0, -1, 0, -4.37113883e-08), Vector3.new(3.3399663, 75.2800064, 7.0199976))
      createWall(CFrame.new(-71.4555283, -9.84874344, 8.86862564, 0.0261769947, 0, -0.999657333, 0, 1, 0, 0.999657333, 0, 0.0261769947), Vector3.new(930.549988, 24.909996, 401.669983))
      createWall(CFrame.new(-141.047348, 39.9012566, -346.645721, -1, -8.74227766e-08, 0, -8.74227766e-08, 1, -8.74227766e-08, 7.64274186e-15, -8.74227766e-08, -1), Vector3.new(136.869934, 121.409996, 6.42999887))
      createWall(CFrame.new(36.2830582, 16.8362617, -147.050018, -0.819152057, -7.1612547e-08, 0.57357645, -1.37566417e-07, 1, -7.1612547e-08, -0.57357645, -1.37566417e-07, -0.819152057), Vector3.new(9.30995846, 75.2800064, 31.1199837))
      createWall(CFrame.new(-209.860611, 39.9012566, -292.526398, -4.37113883e-08, 0, 1, 0, 1, 0, -1, 0, -4.37113883e-08), Vector3.new(119.619957, 121.409996, 6.42999887))
      createWall(CFrame.new(17.7576237, -9.09874344, -452.124695, 0.0261769947, 0, -0.999657333, 0, 1, 0, 0.999657333, 0, 0.0261769947), Vector3.new(28.5499878, 25.409996, 231.169983))
      createWall(CFrame.new(-51.8212013, -8.75, -568.843323, 0.0261769947, 0, -0.999657333, 0, 1, 0, 0.999657333, 0, 0.0261769947), Vector3.new(216.549988, 26.409996, 364.169983))
      createWall(CFrame.new(-261.46759, -21.155468, -615.121277, -4.37113883e-08, -0.406736642, -0.91354543, 0, 0.91354543, -0.406736642, 1, -1.77790227e-08, -3.99323383e-08), Vector3.new(87.0499878, 26.409996, 69.1699829))
      createWall(CFrame.new(-250.886627, -11.7916269, -731.871277, -4.37113883e-08, 0, -1, 0, 1, 0, 1, 0, -4.37113883e-08), Vector3.new(146.550003, 46.909996, 39.6699829))
      createWall(CFrame.new(-250.886627, -11.7916269, -513.371277, -4.37113883e-08, 0, -1, 0, 1, 0, 1, 0, -4.37113883e-08), Vector3.new(116.550003, 46.909996, 39.6699829))
      createWall(CFrame.new(-413.386627, 24.458374, -464.371277, -4.37113883e-08, 0, -1, 0, 1, 0, 1, 0, -4.37113883e-08), Vector3.new(18.5500031, 119.409996, 364.669983))
      createWall(CFrame.new(-414.136627, 24.458374, -779.121277, -4.37113883e-08, 0, -1, 0, 1, 0, 1, 0, -4.37113883e-08), Vector3.new(18.0499878, 119.409996, 366.169983))
      createWall(CFrame.new(-464.386597, -19.291626, -617.371277, -4.37113883e-08, 0, -1, 0, 1, 0, 1, 0, -4.37113883e-08), Vector3.new(324.549988, 31.909996, 0.66998291))
      createWall(CFrame.new(-366.386597, -22.791626, -617.371277, -4.37113883e-08, 0, -1, 0, 1, 0, 1, 0, -4.37113883e-08), Vector3.new(324.549988, 24.909996, 197.669983))
      createWall(CFrame.new(-111.886597, 24.458374, -659.621277, -4.37113883e-08, 0, -1, 0, 1, 0, 1, 0, -4.37113883e-08), Vector3.new(25.0499878, 119.409996, 255.669983))
      createWall(CFrame.new(-110.386597, 24.458374, -560.871277, -4.37113883e-08, 0, -1, 0, 1, 0, 1, 0, -4.37113883e-08), Vector3.new(50.5499878, 119.409996, 258.669983))
      createWall(CFrame.new(79.3634033, 24.458374, -548.871277, -4.37113883e-08, 0, -1, 0, 1, 0, 1, 0, -4.37113883e-08), Vector3.new(164.549988, 119.409996, 63.1699829))
      createWall(CFrame.new(56.8634033, 24.458374, -641.121277, -4.37113883e-08, 0, -1, 0, 1, 0, 1, 0, -4.37113883e-08), Vector3.new(22.0499878, 119.409996, 108.169983))
      createWall(CFrame.new(11.1134005, 24.458374, -536.621277, -4.37113883e-08, 0, -1, 0, 1, 0, 1, 0, -4.37113883e-08), Vector3.new(136.049988, 119.409996, 16.6699829))
      createWall(CFrame.new(-13.6366024, 24.458374, -469.621277, -4.37113883e-08, 0, -1, 0, 1, 0, 1, 0, -4.37113883e-08), Vector3.new(2.05000305, 119.409996, 66.1699829))
      createWall(CFrame.new(-43.3866081, 24.458374, -390.371277, -4.37113883e-08, 0, -1, 0, 1, 0, 1, 0, -4.37113883e-08), Vector3.new(160.550003, 119.409996, 6.66998291))
      createWall(CFrame.new(111.363388, 24.458374, -390.371277, -4.37113883e-08, 0, -1, 0, 1, 0, 1, 0, -4.37113883e-08), Vector3.new(160.550003, 119.409996, 6.16998291))
      createWall(CFrame.new(77.6133881, 24.458374, -258.121277, -4.37113883e-08, 0, -1, 0, 1, 0, 1, 0, -4.37113883e-08), Vector3.new(128.050003, 119.409996, 73.6699829))
      createWall(CFrame.new(-22.8866119, 24.458374, -280.621277, -4.37113883e-08, 0, -1, 0, 1, 0, 1, 0, -4.37113883e-08), Vector3.new(83.0500031, 119.409996, 90.6699829))
      createWall(CFrame.new(-90.8866119, 24.458374, -216.621277, -4.37113883e-08, 0, -1, 0, 1, 0, 1, 0, -4.37113883e-08), Vector3.new(60.0500031, 119.409996, 49.6699829))
      createWall(CFrame.new(-105.136612, 24.458374, -148.621277, -4.37113883e-08, 0, -1, 0, 1, 0, 1, 0, -4.37113883e-08), Vector3.new(25.0500031, 119.409996, 78.1699829))
      createWall(CFrame.new(-177.886612, 24.458374, -184.871277, -4.37113883e-08, 0, -1, 0, 1, 0, 1, 0, -4.37113883e-08), Vector3.new(97.5500031, 119.409996, 73.6699829))
      createWall(CFrame.new(-43.8866119, 24.458374, -79.8712769, -4.37113883e-08, 0, -1, 0, 1, 0, 1, 0, -4.37113883e-08), Vector3.new(126.550003, 119.409996, 47.6699829))
      createWall(CFrame.new(21.6133881, 24.458374, -79.8712769, -4.37113883e-08, 0, -1, 0, 1, 0, 1, 0, -4.37113883e-08), Vector3.new(126.550003, 119.409996, 46.6699829))
      createWall(CFrame.new(-595.011597, 29.583374, -617.371277, -4.37113883e-08, 0, -1, 0, 1, 0, 1, 0, -4.37113883e-08), Vector3.new(324.549988, 129.660004, 5.91998291))
      createWall(CFrame.new(-528.511597, -4.16662598, -617.371277, -4.37113883e-08, 0, -1, 0, 1, 0, 1, 0, -4.37113883e-08), Vector3.new(324.549988, 1.15999603, 128.919983))
      createWall(CFrame.new(-542.636597, 9.45837402, -619.371277, -4.37113883e-08, 0, -1, 0, 1, 0, 1, 0, -4.37113883e-08), Vector3.new(36.5499878, 25.909996, 41.6699829))
      createWall(CFrame.new(-559.011597, 23.958374, -619.371277, -4.37113883e-08, 0, -1, 0, 1, 0, 1, 0, -4.37113883e-08), Vector3.new(36.5499878, 54.909996, 8.91998291))
      createWall(CFrame.new(-580.636597, 44.083374, -566.496277, -4.37113883e-08, 0, -1, 0, 1, 0, 1, 0, -4.37113883e-08), Vector3.new(42.2999878, 95.159996, 42.1699829))
      createWall(CFrame.new(-582.511597, 44.083374, -672.246277, -4.37113883e-08, 0, -1, 0, 1, 0, 1, 0, -4.37113883e-08), Vector3.new(41.2999878, 95.159996, 38.4199829))
      createWall(CFrame.new(-12.2616129, 24.458374, -255.746277, -4.37113883e-08, 0, -1, 0, 1, 0, 1, 0, -4.37113883e-08), Vector3.new(132.800003, 119.409996, 34.9199829))
      if _G.destroy_map then
        for i,v in pairs(workspace:GetChildren()) do
          if v.ClassName == "Model" or v.ClassName == "Part" or v.ClassName == "UnionOperation" or v.ClassName == "WedgePart" or v.ClassName == "MeshPart" then
            if v ~= game.Players.LocalPlayer.Character and v.Name ~= regionPartName then
              v:Destroy()
            end
          end
        end
      end
      wait(5)
      while not game:GetService("Workspace").dungeon.room3.enemyFolder:FindFirstChild("Beast Master") do
        wait(1)
      end
      while not game:GetService("Workspace").dungeon.room3.enemyFolder:FindFirstChild("Beast Master"):FindFirstChild("HumanoidRootPart") do
        wait(1)
      end
      -- cant path to second boss, paths to second boss area until hes in position
      forceObjectiveExists = true
      thePart.CFrame = CFrame.new(3.85899, 5.60531, 31.656)
      local t = game:GetService("Workspace").dungeon.room3.enemyFolder:FindFirstChild("Beast Master")
      while t.PrimaryPart.Position.Y > 35 do
        wait()
      end
      forceObjectiveExists = false
    end

    function winterFix()
      local dun = waitForExist(workspace, "dungeon")
      workspace.Terrain:Clear()
      createWall(CFrame.new(49.6182404, 44.75, 118.716324, 0.857167304, 0, -0.515038073, 0, 1, 0, 0.515038073, 0, 0.857167304), Vector3.new(82.5, 2.5, 32))
      createWall(CFrame.new(65.4887466, 54.5, 107.836174, 0.857167304, 0, -0.515038073, 0, 1, 0, 0.515038073, 0, 0.857167304), Vector3.new(63.5, 22, 5))
      createWall(CFrame.new(36.3633881, 54.5, 129.12648, 0.857167304, 0, -0.515038073, 0, 1, 0, 0.515038073, 0, 0.857167304), Vector3.new(92.5, 22, 1.5))
      createWall(CFrame.new(53.4067535, 58.25, -19.6698608, -0.342020094, 0, -0.939692616, 0, 1, 0, 0.939692616, 0, -0.342020094), Vector3.new(64, 29.5, 2))
      createWall(CFrame.new(6.28490734, 44.75, 78.9878387, 0.438371092, 0, -0.898794055, 0, 1, 0, 0.898794055, 0, 0.438371092), Vector3.new(54, 2.5, 46))
      createWall(CFrame.new(26.3271828, 54.5, 64.7621689, 0.438371092, 0, -0.898794055, 0, 1, 0, 0.898794055, 0, 0.438371092), Vector3.new(62, 22, 5.5))
      createWall(CFrame.new(-20.3219051, 54.5, 78.6136322, 0.438371092, 0, -0.898794055, 0, 1, 0, 0.898794055, 0, 0.438371092), Vector3.new(78, 22, 8.5))
      createWall(CFrame.new(2.55875301, 44.75, 71.3480911, 0.438371092, 0, -0.898794055, 0, 1, 0, 0.898794055, 0, 0.438371092), Vector3.new(71, 2.5, 46))
      createWall(CFrame.new(24.2970142, 44.75, -28.1365814, -0.342020094, 0, -0.939692616, 0, 1, 0, 0.939692616, 0, -0.342020094), Vector3.new(182, 2.5, 62.5))
      createWall(CFrame.new(47.7676086, 42.7324867, -1175.33252, 2.97297333e-08, -2.07890483e-09, -1, 0.0697564632, 0.997564077, 3.26544807e-16, 0.997564077, -0.0697564632, 2.98023295e-08), Vector3.new(41.5, 15.5, 167))
      createWall(CFrame.new(34.0146065, 58.25, 20.1416855, -0.798635483, 0, -0.601815045, 0, 1, 0, 0.601815045, 0, -0.798635483), Vector3.new(57, 29.5, 7))
      createWall(CFrame.new(59.3021507, 58.25, -66.8049469, -0.0697563887, 0, -0.997563958, 0, 1, 0, 0.997563958, 0, -0.0697563887), Vector3.new(80.5, 29.5, 2))
      createWall(CFrame.new(-9.12857437, 56, -32.0551186, -0.342020094, 0, -0.939692616, 0, 1, 0, 0.939692616, 0, -0.342020094), Vector3.new(173.5, 25, 7))
      createWall(CFrame.new(72.586441, 57.25, -108.386299, -0.0348994732, 0, -0.999390781, 0, 1, 0, 0.999390781, 0, -0.0348994732), Vector3.new(8.5, 27.5, 25))
      createWall(CFrame.new(32.1111145, 57.25, -109.799721, -0.0348994732, 0, -0.999390781, 0, 1, 0, 0.999390781, 0, -0.0348994732), Vector3.new(8.5, 27.5, 23))
      createWall(CFrame.new(41.0176544, 44.75, -213.190704, 2.98023224e-08, 0, -0.999999881, 0, 1, 0, 0.999999881, 0, 2.98023224e-08), Vector3.new(215, 2.5, 91.5))
      createWall(CFrame.new(3.76765871, 61.5, -213.940704, 2.98023224e-08, 0, -0.999999881, 0, 1, 0, 0.999999881, 0, 2.98023224e-08), Vector3.new(222.5, 36, 17))
      createWall(CFrame.new(12.5176563, 61.5, -235.440704, 2.98023224e-08, 0, -0.999999881, 0, 1, 0, 0.999999881, 0, 2.98023224e-08), Vector3.new(52.5, 36, 34.5))
      createWall(CFrame.new(11.7676601, 61.5, -132.190704, 2.98023224e-08, 0, -0.999999881, 0, 1, 0, 0.999999881, 0, 2.98023224e-08), Vector3.new(59, 36, 33))
      createWall(CFrame.new(81.2676544, 62, -213.440704, 2.98023224e-08, 0, -0.999999881, 0, 1, 0, 0.999999881, 0, 2.98023224e-08), Vector3.new(215.5, 37, 11))
      createWall(CFrame.new(74.2676544, 62, -228.690704, 2.98023224e-08, 0, -0.999999881, 0, 1, 0, 0.999999881, 0, 2.98023224e-08), Vector3.new(53, 37, 25))
      createWall(CFrame.new(74.2676544, 62, -122.190712, 2.98023224e-08, 0, -0.999999881, 0, 1, 0, 0.999999881, 0, 2.98023224e-08), Vector3.new(21, 37, 25))
      createWall(CFrame.new(15.2676544, 61.25, -322.940674, 2.98023224e-08, 0, -0.999999881, 0, 1, 0, 0.999999881, 0, 2.98023224e-08), Vector3.new(14.5, 35.5, 40))
      createWall(CFrame.new(71.0176468, 61.25, -322.940674, 2.98023224e-08, 0, -0.999999881, 0, 1, 0, 0.999999881, 0, 2.98023224e-08), Vector3.new(14.5, 35.5, 37.5))
      createWall(CFrame.new(51.7676086, 58, -1590.19067, 2.98023224e-08, 0, -0.999999881, 0, 1, 0, 0.999999881, 0, 2.98023224e-08), Vector3.new(60, 41, 172))
      createWall(CFrame.new(-2.48238373, 58, -1368.94067, 2.98023224e-08, 0, -0.999999881, 0, 1, 0, 0.999999881, 0, 2.98023224e-08), Vector3.new(10.5, 41, 74.5))
      createWall(CFrame.new(87.0176086, 58, -1368.94067, 2.98023224e-08, 0, -0.999999881, 0, 1, 0, 0.999999881, 0, 2.98023224e-08), Vector3.new(10.5, 41, 69.5))
      createWall(CFrame.new(41.5176239, 45.25, -964.440674, 2.98023224e-08, 0, -0.999999881, 0, 1, 0, 0.999999881, 0, 2.98023224e-08), Vector3.new(6.5, 15.5, 141.5))
      createWall(CFrame.new(113.517601, 58, -1261.19067, 2.98023224e-08, 0, -0.999999881, 0, 1, 0, 0.999999881, 0, 2.98023224e-08), Vector3.new(213, 41, 3.5))
      createWall(CFrame.new(47.767601, 44.25, -1501.44067, 2.98023224e-08, 0, -0.999999881, 0, 1, 0, 0.999999881, 0, 2.98023224e-08), Vector3.new(266.5, 13.5, 167))
      createWall(CFrame.new(84.6765747, 54.5, 139.489838, 0.857167304, 0, -0.515038073, 0, 1, 0, 0.515038073, 0, 0.857167304), Vector3.new(4, 22, 30.5))
      createWall(CFrame.new(43.5176506, 42.4555817, -310.699219, 2.80050312e-08, 1.01929967e-08, -1, -0.342020154, 0.939692736, 2.50114324e-16, 0.939692736, 0.342020154, 2.98023295e-08), Vector3.new(19.5, 9.5, 71.5))
      createWall(CFrame.new(44.2676468, 41.5, -394.940674, 2.98023224e-08, 0, -0.999999881, 0, 1, 0, 0.999999881, 0, 2.98023224e-08), Vector3.new(182.5, 8, 43))
      createWall(CFrame.new(62.5176468, 58.25, -407.940674, 2.98023224e-08, 0, -0.999999881, 0, 1, 0, 0.999999881, 0, 2.98023224e-08), Vector3.new(182.5, 41.5, 6.5))
      createWall(CFrame.new(16.2676506, 58.25, -407.690674, 2.98023224e-08, 0, -0.999999881, 0, 1, 0, 0.999999881, 0, 2.98023224e-08), Vector3.new(184, 41.5, 19))
      createWall(CFrame.new(44.2676353, 44.4752426, -493.355347, 2.76322254e-08, 1.11641461e-08, -0.999999642, -0.37460652, 0.927183867, 0, 0.927183509, 0.37460655, 2.98023153e-08), Vector3.new(15, 8.5, 57))
      createWall(CFrame.new(52.5176392, 43.75, -590.190674, 2.98023224e-08, 0, -0.999999881, 0, 1, 0, 0.999999881, 0, 2.98023224e-08), Vector3.new(183, 12.5, 94.5))
      createWall(CFrame.new(58.5176392, 56, -545.190674, 2.98023224e-08, 0, -0.999999881, 0, 1, 0, 0.999999881, 0, 2.98023224e-08), Vector3.new(93, 37, 14.5))
      createWall(CFrame.new(21.2676411, 56, -545.190674, 2.98023224e-08, 0, -0.999999881, 0, 1, 0, 0.999999881, 0, 2.98023224e-08), Vector3.new(93, 37, 24))
      createWall(CFrame.new(10.517643, 55.75, -635.190674, 2.98023224e-08, 0, -0.999999881, 0, 1, 0, 0.999999881, 0, 2.98023224e-08), Vector3.new(93, 36.5, 10.5))
      createWall(CFrame.new(96.0176392, 55.75, -635.190674, 2.98023224e-08, 0, -0.999999881, 0, 1, 0, 0.999999881, 0, 2.98023224e-08), Vector3.new(93, 36.5, 8.5))
      createWall(CFrame.new(83.7071075, 55.75, -593.931519, 0.587785304, 0, -0.809017003, 0, 1, 0, 0.809017062, 0, 0.587785304), Vector3.new(18.5, 36.5, 34))
      createWall(CFrame.new(44.2676506, 45.7468681, -322.680908, 2.98023224e-08, -3.63461795e-15, -1, 8.83349074e-08, 1, -1.00203257e-15, 1, -8.83349074e-08, 2.98023224e-08), Vector3.new(9, 9.5, 43))
      createWall(CFrame.new(68.7676315, 46.7623405, -677.575806, 1.44484531e-08, -2.60657025e-08, -1, 0.874619722, 0.484809637, -1.75880865e-15, 0.484809637, -0.874619722, 2.98023259e-08), Vector3.new(9, 16, 107))
      createWall(CFrame.new(50.2676353, 46, -716.690613, 2.98023259e-08, 0, -1, 0, 1, 0, 1, 0, 2.98023259e-08), Vector3.new(70, 17, 29))
      createWall(CFrame.new(6.26764297, 58.5, -711.440674, 2.98023224e-08, 0, -0.999999881, 0, 1, 0, 0.999999881, 0, 2.98023224e-08), Vector3.new(71.5, 42, 74))
      createWall(CFrame.new(89.2676392, 58.5, -711.440674, 2.98023224e-08, 0, -0.999999881, 0, 1, 0, 0.999999881, 0, 2.98023224e-08), Vector3.new(71.5, 42, 54))
      createWall(CFrame.new(41.5176277, 46, -853.940674, 2.98023224e-08, 0, -0.999999881, 0, 1, 0, 0.999999881, 0, 2.98023224e-08), Vector3.new(215.5, 17, 141.5))
      createWall(CFrame.new(-25.9823647, 59, -853.940674, 2.98023224e-08, 0, -0.999999881, 0, 1, 0, 0.999999881, 0, 2.98023224e-08), Vector3.new(215.5, 43, 6.5))
      createWall(CFrame.new(118.517624, 59, -853.940674, 2.98023224e-08, 0, -0.999999881, 0, 1, 0, 0.999999881, 0, 2.98023224e-08), Vector3.new(215.5, 43, 23.5))
      createWall(CFrame.new(111.267616, 59, -883.440796, 0.173648208, 0, -0.984807789, 0, 1, 0, 0.984807789, 0, 0.173648208), Vector3.new(154.5, 43, 38))
      createWall(CFrame.new(-5.48237181, 57.75, -964.190674, 2.98023224e-08, 0, -0.999999881, 0, 1, 0, 0.999999881, 0, 2.98023224e-08), Vector3.new(28, 40.5, 47.5))
      createWall(CFrame.new(100.517609, 57.75, -964.190674, 2.98023224e-08, 0, -0.999999881, 0, 1, 0, 0.999999881, 0, 2.98023224e-08), Vector3.new(28, 40.5, 70.5))
      createWall(CFrame.new(39.0176201, 44.5, -1058.19067, 2.98023259e-08, 0, -1, 0, 1, 0, 1, 0, 2.98023259e-08), Vector3.new(196, 15, 144.5))
      createWall(CFrame.new(3.799963, 56, -53.687912, -0.342020094, 0, -0.939692616, 0, 1, 0, 0.939692616, 0, -0.342020094), Vector3.new(40, 25, 16.5))
      createWall(CFrame.new(-24.2323837, 58, -1261.19067, 2.98023224e-08, 0, -0.999999881, 0, 1, 0, 0.999999881, 0, 2.98023224e-08), Vector3.new(213, 41, 23))
      createWall(CFrame.new(47.7676086, 44.25, -1262.69067, 2.98023224e-08, 0, -0.999999881, 0, 1, 0, 0.999999881, 0, 2.98023224e-08), Vector3.new(216, 13.5, 167))
      createWall(CFrame.new(-33.7323837, 58, -1491.94067, 2.98023224e-08, 0, -0.999999881, 0, 1, 0, 0.999999881, 0, 2.98023224e-08), Vector3.new(256.5, 41, 12))
      createWall(CFrame.new(120.767601, 58, -1491.94067, 2.98023224e-08, 0, -0.999999881, 0, 1, 0, 0.999999881, 0, 2.98023224e-08), Vector3.new(256.5, 41, 34))
      createWall(CFrame.new(-0.232380569, 60.75, -1165.44067, 2.98023224e-08, 0, -0.999999881, 0, 1, 0, 0.999999881, 0, 2.98023224e-08), Vector3.new(21.5, 46.5, 71))
      createWall(CFrame.new(85.5176086, 60.75, -1165.44067, 2.98023224e-08, 0, -0.999999881, 0, 1, 0, 0.999999881, 0, 2.98023224e-08), Vector3.new(21.5, 46.5, 66.5))
      createWall(CFrame.new(136.517609, 60.75, -1068.69067, 2.98023224e-08, 0, -0.999999881, 0, 1, 0, 0.999999881, 0, 2.98023224e-08), Vector3.new(215, 46.5, 30.5))
      createWall(CFrame.new(-36.9823761, 60.75, -1068.69067, 2.98023224e-08, 0, -0.999999881, 0, 1, 0, 0.999999881, 0, 2.98023224e-08), Vector3.new(215, 46.5, 20.5))
      createWall(CFrame.new(44.2676506, 42.8013573, -333.105347, 2.81786487e-08, -9.70269021e-09, -1, 0.325568229, 0.945518553, -1.09093672e-15, 0.945518553, -0.325568229, 2.98023224e-08), Vector3.new(19.5, 9.5, 43))
      createWall(CFrame.new(106.267624, 45.5, -1058.19067, 2.98023259e-08, 0, -1, 0, 1, 0, 1, 0, 2.98023259e-08), Vector3.new(196, 17, 33))
      createWall(CFrame.new(39.0176239, 45.5, -987.940674, 2.98023259e-08, 0, -1, 0, 1, 0, 1, 0, 2.98023259e-08), Vector3.new(55.5, 17, 144.5))
      createWall(CFrame.new(-19.482378, 45.5, -1058.94067, 2.98023259e-08, 0, -1, 0, 1, 0, 1, 0, 2.98023259e-08), Vector3.new(197.5, 17, 32.5))
      createWall(CFrame.new(39.7676201, 45.5, -1145.44067, 2.98023259e-08, 0, -1, 0, 1, 0, 1, 0, 2.98023259e-08), Vector3.new(24.5, 17, 146))
      createWall(CFrame.new(105.017624, 45, -1058.19067, 2.98023259e-08, 0, -1, 0, 1, 0, 1, 0, 2.98023259e-08), Vector3.new(196, 16, 35.5))
      createWall(CFrame.new(39.0176239, 45, -988.940674, 2.98023259e-08, 0, -1, 0, 1, 0, 1, 0, 2.98023259e-08), Vector3.new(57.5, 16, 144.5))
      createWall(CFrame.new(-18.482378, 45, -1058.94067, 2.98023259e-08, 0, -1, 0, 1, 0, 1, 0, 2.98023259e-08), Vector3.new(197.5, 16, 34.5))
      createWall(CFrame.new(39.7676201, 45, -1143.69067, 2.98023259e-08, 0, -1, 0, 1, 0, 1, 0, 2.98023259e-08), Vector3.new(28, 16, 146))
      createWall(CFrame.new(24.7676239, 46, -1016.19067, 2.98023259e-08, 0, -1, 0, 1, 0, 1, 0, 2.98023259e-08), Vector3.new(13, 18, 28))
      createWall(CFrame.new(2.2676239, 45.5, -1031.94067, 2.98023259e-08, 0, -1, 0, 1, 0, 1, 0, 2.98023259e-08), Vector3.new(44.5, 17, 28))
      createWall(CFrame.new(1.01762342, 46, -1041.44067, 2.98023259e-08, 0, -1, 0, 1, 0, 1, 0, 2.98023259e-08), Vector3.new(63.5, 18, 25.5))
      createWall(CFrame.new(4.76762342, 50, -1050.69067, 2.98023259e-08, 0, -1, 0, 1, 0, 1, 0, 2.98023259e-08), Vector3.new(44, 26, 23))
      createWall(CFrame.new(-1.98237896, 50, -1124.94067, 2.98023259e-08, 0, -1, 0, 1, 0, 1, 0, 2.98023259e-08), Vector3.new(28.5, 26, 19.5))
      createWall(CFrame.new(13.267621, 50, -1130.19067, 2.98023259e-08, 0, -1, 0, 1, 0, 1, 0, 2.98023259e-08), Vector3.new(18, 26, 50))
      createWall(CFrame.new(82.0176239, 50, -1130.19067, 2.98023259e-08, 0, -1, 0, 1, 0, 1, 0, 2.98023259e-08), Vector3.new(18, 26, 18.5))
      createWall(CFrame.new(84.2676239, 50, -1124.44067, 2.98023259e-08, 0, -1, 0, 1, 0, 1, 0, 2.98023259e-08), Vector3.new(29.5, 26, 14))
      createWall(CFrame.new(84.2676239, 50, -1028.19067, 2.98023259e-08, 0, -1, 0, 1, 0, 1, 0, 2.98023259e-08), Vector3.new(20, 26, 14))
      createWall(CFrame.new(75.5176239, 50, -1018.94067, 2.98023259e-08, 0, -1, 0, 1, 0, 1, 0, 2.98023259e-08), Vector3.new(9.5, 26, 31.5))
      createWall(CFrame.new(78.0176239, 45.25, -1024.19067, 2.98023259e-08, 0, -1, 0, 1, 0, 1, 0, 2.98023259e-08), Vector3.new(20, 16.5, 26.5))
      createWall(CFrame.new(50.1426544, 61.5, -157.565704, 2.98023224e-08, 0, -0.999999881, 0, 1, 0, 0.999999881, 0, 2.98023224e-08), Vector3.new(19.75, 36, 15.25))
      wait(.1)
      if _G.destroy_map then
        workspace.Terrain:Clear()
        for i,v in pairs(workspace:GetChildren()) do
          if v.ClassName == "Model" or v.ClassName == "Part" or v.ClassName == "UnionOperation" or v.ClassName == "WedgePart" then
            if v ~= game.Players.LocalPlayer.Character and v.Name ~= regionPartName then
              v:Destroy()
            end
          end
        end
        for i,room in pairs(workspace.dungeon:GetChildren()) do
          for j, v in pairs(room:GetChildren()) do
            if v.ClassName == "Model" or v.ClassName == "Part" or v.ClassName == "UnionOperation" or v.ClassName == "WedgePart" and not v:FindFirstChild("HumanoidRootPart") then
              if v ~= game.Players.LocalPlayer.Character and v.Name ~= regionPartName then
                v:Destroy()
              end
            end
          end
        end
      end
      while not game:GetService("Workspace").dungeon.bossRoom.enemyFolder:FindFirstChildOfClass("Model") do
        wait(1)
      end
      while not game:GetService("Workspace").dungeon.bossRoom.enemyFolder:FindFirstChildOfClass("Model"):FindFirstChild("HumanoidRootPart") do
        wait(1)
      end
      game.Players.LocalPlayer.Character.HumanoidRootPart.CFrame = game:GetService("Workspace").dungeon.bossRoom.enemyFolder:FindFirstChildOfClass("Model"):FindFirstChild("HumanoidRootPart").CFrame * CFrame.new(0,0,5)
    end

    function desertFix()
      local dun = waitForExist(workspace, "dungeon")
      for i,v in pairs(dun:GetChildren()) do
        for j, k in pairs(v:GetChildren()) do
          if k.ClassName == "Part" then
            if k.Name == "barrier" then
              k:Destroy()
            end
            local n = k.Orientation.X
            if n ~= math.floor(n) then
              k:Destroy()
            end
            local n = k.Orientation.Y
            if n ~= math.floor(n) then
              k:Destroy()
            end
            local n = k.Orientation.Z
            if n ~= math.floor(n) then
              k:Destroy()
            end
          elseif k.ClassName == "Model" or k.ClassName == "UnionOperation" or k.ClassName == "WedgePart" then
            k:Destroy() 
          end
        end
      end
    end

    function eggFix()
      game.ReplicatedStorage.remotes.equipSet:FireServer(_G.eggClass)
      local dun = waitForExist(workspace, "Map")
      for i,v in pairs(dun.Parts.Terrain:GetChildren()) do
        cs:AddTag(v, "RayWhitelist")
      end
      for i,v in pairs(dun.Parts.Misc:GetChildren()) do
        cs:AddTag(v, "RayWhitelist")
      end
      for i,v in pairs(dun.Barriers:GetChildren()) do
        cs:AddTag(v, "RayWhitelist")
      end
      for i,v in pairs(dun.Models:GetChildren()) do
        cs:AddTag(v, "RayWhitelist")
      end
      dun.Props:Destroy()
      wait(5)
      while not game:GetService("Workspace").dungeon.bossRoom.enemyFolder:FindFirstChild("Egg Mech") do
        wait(1)
      end
      while not game:GetService("Workspace").dungeon.bossRoom.enemyFolder:FindFirstChild("Egg Mech"):FindFirstChild("HumanoidRootPart") do
        wait(1)
      end
      -- cant path to second boss, paths to second boss area until hes in position
      forceObjectiveExists = true
      local _,_,_,root = getPlayer()
      thePart.CFrame = CFrame.new(570.516174, 124.525772, 5.6751118)
      while root.Position.Y > 120 do
        wait()
      end
      forceObjectiveExists = false
    end

    function fpsBoost()
      if _G.fpsBoost then
        local decalsyeeted = true -- Leaving this on makes games look shitty but the fps goes up by at least 20.
        local g = game
        local w = g.Workspace
        local l = g.Lighting
        local t = w.Terrain
        sethiddenproperty(l,"Technology",2)
        sethiddenproperty(t,"Decoration",false)
        t.WaterWaveSize = 0
        t.WaterWaveSpeed = 0
        t.WaterReflectance = 0
        t.WaterTransparency = 0
        l.GlobalShadows = false
        l.FogEnd = 9e9
        l.Brightness = 0
        settings().Rendering.QualityLevel = "Level01"
        for i, v in pairs(g:GetDescendants()) do
          if v:IsA("Part") or v:IsA("Union") or v:IsA("CornerWedgePart") or v:IsA("TrussPart") then
            v.Material = "Plastic"
            v.Reflectance = 0
          elseif v:IsA("Decal") or v:IsA("Texture") and decalsyeeted then
            v.Transparency = 1
          elseif v:IsA("ParticleEmitter") or v:IsA("Trail") then
            v.Lifetime = NumberRange.new(0)
          elseif v:IsA("Explosion") then
            v.BlastPressure = 1
            v.BlastRadius = 1
          elseif v:IsA("Fire") or v:IsA("SpotLight") or v:IsA("Smoke") or v:IsA("Sparkles") then
            v.Enabled = false
          elseif v:IsA("MeshPart") then
            v.Material = "Plastic"
            v.Reflectance = 0
            v.TextureID = 10385902758728957
          end
        end
        for i, e in pairs(l:GetChildren()) do
          if e:IsA("BlurEffect") or e:IsA("SunRaysEffect") or e:IsA("ColorCorrectionEffect") or e:IsA("BloomEffect") or e:IsA("DepthOfFieldEffect") then
            e.Enabled = false
          end
        end
      end
    end

    updatecheck = function()
      local places = {
        [5281215714] = { ['version'] = 46,   ['name'] = "Volcanic Chambers" },
        [4628698373] = { ['version'] = 39,   ['name'] = "Orbital Outpost"   },
        [4113459044] = { ['version'] = 68,   ['name'] = "Steampunk Sewers"  },
        [3737465474] = { ['version'] = 80,   ['name'] = "Ghastly Harbor"    },
        [3488584454] = { ['version'] = 93,   ['name'] = "The Canals"        },
        [3277965370] = { ['version'] = 110,  ['name'] = "Samurai Palace"    },
        [3119903031] = { ['version'] = 117,  ['name'] = "The Underworld"    },
        [3041739550] = { ['version'] = 134,  ['name'] = "King's Palace"     },
        [2988891534] = { ['version'] = 424,  ['name'] = "Pirate Island"     },
        [2743806150] = { ['version'] = 352,  ['name'] = "Winter Outpost"    },
        [2606294912] = { ['version'] = 473,  ['name'] = "Desert Temple"     },
        [4865331948] = { ['version'] = 473,  ['name'] = "Easter Event"      },
        [3220974599] = { ['version'] = 89,   ['name'] = "Wave Defense"      },
        [4286254333] = { ['version'] = 74,   ['name'] = "Boss Raid"         },
        [2414851778] = { ['version'] = 4360, ['name'] = "Lobby"             },
        [3220968688] = { ['version'] = 152, ['name'] = "Lobby2"             },
      }
      if places[game.PlaceId] ~= nil and places[game.PlaceId]['version'] ~= game.PlaceVersion then
        --failReport("Ban Prevention, DM MRob on discord", "PlaceId: "..tostring(game.PlaceId).." CurrentPlaceVersion: ".. tostring(places[game.PlaceId]['version']).." NewPlaceVersion: "..tostring(game.PlaceVersion) )
      end
    end
    spawn(updatecheck)
    if game.PlaceId == 6216785535 then
      webhookLocals.dungeonName = "Oceanic"
      spawn(oceanFix)
    elseif game.PlaceId == 5281215714 then -- volcanic
      webhookLocals.dungeonName = "Volcanic Chambers"
      spawn(volcanicFix)
    elseif game.PlaceId == 4628698373 then -- orbital
      webhookLocals.dungeonName = "Orbital Outpost"
      spawn(fixOrbital)
    elseif game.PlaceId == 4113459044 then -- steam
      webhookLocals.dungeonName = "Steampunk Sewers"
      spawn(steamFix)
    elseif game.PlaceId == 3737465474 then -- ghastly
      webhookLocals.dungeonName = "Ghastly Harbor"
      spawn(ghastlyFix)
    elseif game.PlaceId == 3488584454 then -- canals
      webhookLocals.dungeonName = "The Canals"
      spawn(canalsFix)
    elseif game.PlaceId == 3277965370 then -- samurai
      webhookLocals.dungeonName = "Samurai Palace"
      spawn(samuraiFix)
    elseif game.PlaceId == 3119903031 then -- underworld
      webhookLocals.dungeonName = "The Underworld"
      spawn(underworldFix)
    elseif game.PlaceId == 3041739550 then -- king
      webhookLocals.dungeonName = "Kings Palace"
      spawn(kingFix)
    elseif game.PlaceId == 2988891534 then -- pirate
      webhookLocals.dungeonName = "Pirate Island"
      spawn(pirateFix)
    elseif game.PlaceId == 2743806150 then -- winter
      webhookLocals.dungeonName = "Winter Outpost"
      spawn(winterFix)
    elseif game.PlaceId == 2606294912 then -- desert
      webhookLocals.dungeonName = "Desert Temple"
      spawn(desertFix)
    elseif game.PlaceId == 4286254333 then -- boss raid
      webhookLocals.dungeonName = "Boss Raid"
      normalDungeon = false
      bossRaid = true
    elseif workspace:FindFirstChild("currentWave") then -- wave defense
      webhookLocals.dungeonName = "Wave Defense"
      waveDefense = true
      normalDungeon = false
    elseif game.PlaceId == 4865331948 then -- easter egg event
      waveDefense = false
      normalDungeon = false  
      eggEvent = true
      spawn(eggFix)
    end
    if normalDungeon or waveDefense or eggEvent then -- same remote for wave defense and noraml dungeon
      game:GetService("ReplicatedStorage").remotes.changeStartValue:FireServer()
      if game.PlaceId == 2606294912 then
        wait(3)
      end
    elseif bossRaid then -- remote to start dungeon on boss raid
      workspace:WaitForChild("tier")
      game.ReplicatedStorage.remotes.readyUp:FireServer()
    end
    spawn(fpsBoost)

    function deleteFirstBarrier()
      if game:GetService("Workspace"):FindFirstChild("dungeon") then
        if  game:GetService("Workspace").dungeon.initialRoom:FindFirstChild("barrier") then
          game:GetService("Workspace").dungeon.initialRoom.barrier:Destroy()
        end
      end
    end

    game.Players.LocalPlayer.Character.Humanoid.AutoRotate = false

    if _G.hide_projectiles then
      spawn(function()
          if game.ReplicatedStorage:FindFirstChild("projectiles") then
            game.ReplicatedStorage.projectiles:Destroy()
          end
          if game.Players.LocalPlayer.PlayerGui:FindFirstChild("abilityLocal") then
            game.Players.LocalPlayer.PlayerGui.abilityLocal.Disabled = true 
            if game.Players.LocalPlayer.PlayerGui.abilityLocal:FindFirstChild("abilityLocal2") then
              game.Players.LocalPlayer.PlayerGui.abilityLocal.abilityLocal2.Disabled = true 
            end
          end
          if game.Players.LocalPlayer.PlayerScripts:FindFirstChild("MapSpecificLocals") then
            --game.Players.LocalPlayer.PlayerScripts.MapSpecificLocals.Disabled = true
          end
        end)
    end
  
    spawn(initHitBox)
    spawn(rayCollectionService)
    spawn(deleteFirstBarrier)
