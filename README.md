for i,v in pairs(getconnections(game.Players.LocalPlayer.Idled)) do
	v:Disable()
end
local tools = {}

for i,v in pairs(game.Players.LocalPlayer.Backpack:GetChildren()) do
	if v:IsA("Tool") then
		table.insert(tools, v.Name)
	end
end
local plr = game:GetService("Players").LocalPlayer

local Library = loadstring(game:HttpGet("https://raw.githubusercontent.com/Attrixx/FreeScripts/main/YTUILib1.lua"))():init("SeenHub-ADMIN-Version")
local Tab = Library:Tab("Main")
local Section = Tab:Section("Autofarm")
Section:Toggle("AutoFarm", false, function(state)
    getgenv().AutoFarm = state
end)

local quests = {
	"Bandit [Lv. 5]",
	"Monkey [Lv. 14]", 
	"Gorilla [Lv. 20]",
	"Pirate [Lv. 35]", 
	"Brute [Lv. 45]", 
	"Desert Bandit [Lv. 60]", 
	"Desert Officer [Lv. 70]", 
	"Snow Bandit [Lv. 90]", 
	"Snowman [Lv. 100]",
	"Chief Petty Officer [Lv. 120]" ,
	"Sky Bandit [Lv. 150]", 
	"Toga Warrior [Lv. 225]", 
	"Gladiator [Lv. 275]", 
	"Military Soldier [Lv. 300]", 
	"Military Spy [Lv. 330]", 
	"God's Guard [Lv. 450]",
	"Shanda [Lv. 475]", 
	"Galley Pirate [Lv. 625]"
}
local Section = Tab:Section("CommingSoon..")
local Section = Tab:Section("SelectCombat")
Section:Dropdown("Weapon", tools, "Select!", function(weapon)
	getgenv().CurrentWeapon = weapon
end)
Section:Toggle("Resetweapon", false, function(v)
    loadstring(game:HttpGet("https://pastebin.com/raw/L6XVEXLS"))()
end)
game.Players.LocalPlayer.Backpack.DescendantAdded:Connect(function(tool)
	local toolName = tool.Name
	if tool:IsA("Tool") then
		table.insert(tools, toolName)
		toolDropdown:Refresh(tools)
	end
end)
game.Players.LocalPlayer.Backpack.DescendantRemoving:Connect(function(tool)
	local toolName = tool.Name
	if tool:IsA("Tool") then
		for i,v in pairs(tools) do
			if v == toolName then
				table.remove(tools, i)
			end
		end	
	end
	toolDropdown:Refresh(tools)
end)

local Section = Tab:Section("SelectMob")
Section:Dropdown("SelectMob", quests, "Select!", "Input Something", function(chosenQuest)
    getgenv().CurrentQuest = chosenQuest
end)

function enemy()
    if game.Workspace.Enemies:FindFirstChild(getgenv().CurrentQuest) then
        local mobs = game.Workspace.Enemies:GetChildren()
        for i = 1, #mobs do local v = mobs[i]
            if v.Name == getgenv().CurrentQuest and v:IsA("Model") and v:FindFirstChild("Humanoid") and v.Humanoid.Health > 0 then
                return v
            end
        end
    end
    return game.ReplicatedStorage:FindFirstChild(getgenv().CurrentQuest)
end
game:GetService("RunService").Stepped:Connect(function()
    if getgenv().getgenv().Noclip then
        pcall(function()
            plr.Character.Humanoid:ChangeState(11)
        end)
    end
    if getgenv().AutoFarm or getgenv().Noclip then
        pcall(function()
            plr.Character.Humanoid:ChangeState(11)
	    local useTool = game.Players.LocalPlayer.Backpack[getgenv().CurrentWeapon]
            plr.Character.Humanoid:EquipTool(useTool)
        end)
    end
    if getgenv().SkillX then
        pcall(function()
            keypress(0x58)
            wait(1)
            keyrelease(0x58)
        end)
    end
    if getgenv().SkillC then
        pcall(function()
            keypress(0x43)
            wait(1)
            keyrelease(0x43)
        end)
    end
    if getgenv().SkillF then
        pcall(function()
            keypress(0x46)
            wait(1)
            keyrelease(0x46)
        end)
    end
    if getgenv().SkillZ then
        pcall(function()
            keypress(0x5A)
            wait(1)
            keyrelease(0x5A)
        end)
    end
end)
coroutine.wrap(function()
    while wait() do
        if getgenv().AutoFarm and not getgenv().FarmStopped then
            local v = enemy()
            local vuser = game:GetService("VirtualUser")
            vuser:CaptureController()
            vuser:ClickButton1(Vector2.new())
            pcall(function()
                plr.Character.HumanoidRootPart.CFrame = v.HumanoidRootPart.CFrame - v.HumanoidRootPart.CFrame.lookVector * 2
            end)
        end
    end
end)()
--teleport--
local Tab = Library:Tab("Teleport")
local Section = Tab:Section("Teleport")
Section:Toggle("Ctrl + Click = TP", false, function(va)
    local Plr = game:GetService("Players").LocalPlayer
local Mouse = Plr:GetMouse()
 
Mouse.Button1Down:connect(
    function()
        if not game:GetService("UserInputService"):IsKeyDown(Enum.KeyCode.LeftControl) then
            return
        end
        if not Mouse.Target then
            return
        end
        Plr.Character:MoveTo(Mouse.Hit.p)
    end)
end)
Section:Toggle("Starterland", false, function(va)
    game.Players.LocalPlayer.Character.HumanoidRootPart.CFrame = CFrame.new(946.396484, 16.5166149, 1428.54102, -0.0332927071, -4.42573764e-08, 0.999445617, -4.84113132e-11, 1, 4.42803092e-08, -0.999445617, 1.42582701e-09, -0.0332927071)
end)
Section:Toggle("MiddleTown", false, function(va)
    game.Players.LocalPlayer.Character.HumanoidRootPart.CFrame = CFrame.new(-698.071655, 7.85224533, 1559.16711, 0.971976697, 3.74573865e-08, 0.235077143, -4.1371532e-08, 1, 1.17186092e-08, -0.235077143, -2.11157172e-08, 0.971976697)
end)
Section:Toggle("Jungle", false, function(va)
    game.Players.LocalPlayer.Character.HumanoidRootPart.CFrame = CFrame.new(-1324.81079, 11.8530645, 492.504089, -0.950561523, 0, -0.310536355, 0, 1, 0, 0.310536355, 0, -0.950561523)
end)
Section:Toggle("Desert", false, function(va)
    game.Players.LocalPlayer.Character.HumanoidRootPart.CFrame = CFrame.new(909.186157, 6.5132513, 4380.58252, -0.979714632, -1.68406054e-08, 0.2003977, -9.15892709e-11, 1, 8.35881551e-08, -0.2003977, 8.18741839e-08, -0.979714632)
end)
Section:Toggle("SnowIsland", false, function(va)
    game.Players.LocalPlayer.Character.HumanoidRootPart.CFrame = CFrame.new(1390.01794, 87.272789, -1347.60876, -0.199600711, -3.93440693e-08, -0.979877293, 1.92018632e-08, 1, -4.40634516e-08, 0.979877293, -2.76105663e-08, -0.199600711)
end)
Section:Toggle("MarineIsland", false, function(va)
    game.Players.LocalPlayer.Character.HumanoidRootPart.CFrame = CFrame.new(-4818.64404, 20.6519604, 4371.78076, 0.853140891, 0, -0.521680713, 0, 1, 0, 0.521680713, 0, 0.853140891)
end)
Section:Toggle("Skypiea1", false, function(va)
    game.Players.LocalPlayer.Character.HumanoidRootPart.CFrame = CFrame.new(-4695.72168, 845.277161, -1849.30481, 0.942552745, 0, 0.33405903, 0, 1, 0, -0.33405903, 0, 0.942552745)
end)
Section:Toggle("Skypiea2", false, function(va)
    game.Players.LocalPlayer.Character.HumanoidRootPart.CFrame = CFrame.new(-7887.83545, 5545.49316, -380.958527, -0.000477724156, -6.86372985e-08, -0.999999881, 5.76642201e-08, 1, -6.86648534e-08, 0.999999881, -5.76970152e-08, -0.000477724156)
end)
Section:Toggle("Skypiea3", false, function(va)
    game.Players.LocalPlayer.Character.HumanoidRootPart.CFrame = CFrame.new(-7896.74023, 5635.96387, -1419.48267, -0.974992573, -6.90924438e-08, -0.222236812, -7.22519289e-08, 1, 6.08653838e-09, 0.222236812, 2.19913616e-08, -0.974992573)
end)
Section:Toggle("Prison", false, function(va)
    game.Players.LocalPlayer.Character.HumanoidRootPart.CFrame = CFrame.new(5009.61572, 3.65196347, 739.075989, -0.00479308004, 9.31296569e-08, 0.999988496, 5.43943734e-08, 1, -9.28700103e-08, -0.999988496, 5.39486145e-08, -0.00479308004)
end)
Section:Toggle("Colosseum", false, function(va)
    game.Players.LocalPlayer.Character.HumanoidRootPart.CFrame = CFrame.new(-1477.56165, 7.38933945, -2937.54102, 0.748681664, -4.16919406e-08, 0.662929654, -1.05962474e-08, 1, 7.4857347e-08, -0.662929654, -6.30688533e-08, 0.748681664)
end)
Section:Toggle("MagmaVillage", false, function(va)
    game.Players.LocalPlayer.Character.HumanoidRootPart.CFrame = CFrame.new(-5254.56592, 8.59067631, 8451.16797, -0.356155008, 7.88511798e-08, 0.934427261, 7.19219528e-08, 1, -5.69715759e-08, -0.934427261, 4.69150905e-08, -0.356155008)
end)
Section:Toggle("FishmanIsland", false, function(va)
    game.Players.LocalPlayer.Character.HumanoidRootPart.CFrame = CFrame.new(61352.3828, 18.8707905, 1502.90942, -0.999073625, 2.99610892e-09, -0.043031659, 3.08991832e-09, 1, -2.11348894e-09, 0.043031659, -2.24449526e-09, -0.999073625)
end)
Section:Toggle("FountainCity", false, function(va)
    game.Players.LocalPlayer.Character.HumanoidRootPart.CFrame = CFrame.new(5072.36914, 4.50129032, 4158.08545, 0.574859381, 0, 0.818252444, 0, 1, 0, -0.818252623, 0, 0.57485944)
end)
local Section = Tab:Section("TeleportWorld2")
Section:Toggle("First Spot", false, function(v)
    game.Players.LocalPlayer.Character.HumanoidRootPart.CFrame = CFrame.new(-12.0712032, 19.2767334, 2830.55103, 0.999991894, -9.70383311e-08, -0.0040255473, 9.6878793e-08, 1, -3.98273805e-08, 0.0040255473, 3.94370687e-08, 0.999991894)
end)
Section:Toggle("Kingdom of Rose", false, function(v)
    game.Players.LocalPlayer.Character.HumanoidRootPart.CFrame = CFrame.new(-389.280792, 123.159729, 1060.02148, 0.996645749, 5.8851569e-08, 0.0818369836, -5.40415108e-08, 1, -6.09910344e-08, -0.0818369836, 5.63638558e-08, 0.996645749)
end)
Section:Toggle("Dark Area", false, function(v)
    game.Players.LocalPlayer.Character.HumanoidRootPart.CFrame = CFrame.new(3621.16528, 13.3493481, -3302.7395, 0.778767526, 2.46919782e-08, -0.627312601, 1.19120687e-08, 1, 5.41495737e-08, 0.627312601, -4.96425194e-08, 0.778767526)
end)
Section:Toggle("Flamingo Mansion", false, function(v)
    game.Players.LocalPlayer.Character.HumanoidRootPart.CFrame = CFrame.new(-389.256256, 322.060638, 804.212036, 0.999959409, 2.65020912e-08, 0.00901245512, -2.67206168e-08, 1, 2.41266065e-08, -0.00901245512, -2.43664449e-08, 0.999959409)
end)
Section:Toggle("Flamingo Room", false, function(v)
    game.Players.LocalPlayer.Character.HumanoidRootPart.CFrame = CFrame.new(2285.01807, 15.1520376, 899.485596, 0.999968708, -6.92961066e-09, -0.00791095756, 6.41582387e-09, 1, -6.49716014e-08, 0.00791095756, 6.49188152e-08, 0.999968708)
end)
Section:Toggle("Green bit", false, function(v)
    game.Players.LocalPlayer.Character.HumanoidRootPart.CFrame = CFrame.new(-2250.07617, 73.2693329, -2679.00684, 0.91374141, -2.19674305e-08, 0.406296223, -6.10797457e-09, 1, 6.78040806e-08, -0.406296223, -6.44370459e-08, 0.91374141)
end)
Section:Toggle("Cafe", false, function(v)
    game.Players.LocalPlayer.Character.HumanoidRootPart.CFrame = CFrame.new(-385.250916, 73.0200958, 297.388397, 1, 0, 0, 0, 1, 0, 0, 0, 1)
end)
Section:Toggle("Factory", false, function(v)
    game.Players.LocalPlayer.Character.HumanoidRootPart.CFrame = CFrame.new(250.072113, 73.0679626, -250.566299, 0.709058344, -1.17480022e-05, -0.705149412, -3.07607564e-07, 1, -1.69696032e-05, 0.705149412, 1.22493602e-05, 0.709058344)
end)
Section:Toggle("Colosseum", false, function(v)
    game.Players.LocalPlayer.Character.HumanoidRootPart.CFrame = CFrame.new(-1829.7439, 45.7947121, 1365.79236, -0.0542050786, -4.29878817e-08, 0.998529673, 1.05718878e-09, 1, 4.31085674e-08, -0.998529673, 3.39233752e-09, -0.0542050786)
end)
Section:Toggle("Ghost Island", false, function(v)
    game.Players.LocalPlayer.Character.HumanoidRootPart.CFrame = CFrame.new(-5421.82031, 48.4801445, -716.68219, 0.172037855, -4.24350652e-08, 0.985090315, 2.80721419e-08, 1, 3.81747682e-08, -0.985090315, 2.10860893e-08, 0.172037855)
end)
Section:Toggle("Ghost Island2nd", false, function(v)
    game.Players.LocalPlayer.Character.HumanoidRootPart.CFrame = CFrame.new(-5831.49316, 4.41178799, -1095.0636, 0.772736669, 2.36010465e-08, 0.634726763, -2.5622688e-08, 1, -5.98912342e-09, -0.634726763, -1.16353904e-08, 0.772736669)
end)
Section:Toggle("Snow Mountain", false, function(v)
    game.Players.LocalPlayer.Character.HumanoidRootPart.CFrame = CFrame.new(762.678955, 409.101227, -5266.34814, 0.907148778, -2.98645695e-08, -0.420810103, 1.73319792e-09, 1, -6.72329463e-08, 0.420810103, 6.02609305e-08, 0.907148778)
end)
Section:Toggle("Hot and Cold", false, function(v)
    game.Players.LocalPlayer.Character.HumanoidRootPart.CFrame = CFrame.new(-5833.02832, 15.9517622, -4863.14209, 0.975660861, -4.19447694e-08, 0.219284937, 2.18369998e-08, 1, 9.41207432e-08, -0.219284937, -8.70413999e-08, 0.975660861)
end)
Section:Toggle("Magma Side", false, function(v)
    game.Players.LocalPlayer.Character.HumanoidRootPart.CFrame = CFrame.new(-5521.28516, 15.9513817, -5013.17236, 0.861727118, -2.95518046e-08, -0.507372081, 2.7988365e-09, 1, -5.34912594e-08, 0.507372081, 4.46748167e-08, 0.861727118)
end)
Section:Toggle("Cursed Ship", false, function(v)
    game.Players.LocalPlayer.Character.HumanoidRootPart.CFrame = CFrame.new(923.213074, 125.057129, 32852.832, -0.999960124, -4.50870052e-09, 0.0089182537, 2.86126522e-09, 1, 8.26388316e-07, -0.0089182537, 8.26381154e-07, -0.999960124)
end)
Section:Toggle("Frosted Island", false, function(v)
    game.Players.LocalPlayer.Character.HumanoidRootPart.CFrame = CFrame.new(5156.5459, 283.565033, -6531.28711, 0.417184055, -6.57488926e-08, -0.908822, 5.90824882e-08, 1, -4.52240556e-08, 0.908822, -3.48287124e-08, 0.417184055)
end)
Section:Toggle("Usoapp Island", false, function(v)
    game.Players.LocalPlayer.Character.HumanoidRootPart.CFrame = CFrame.new(4753.49365, 8.31866837, 2844.32739, -0.686578274, 5.83738391e-08, -0.727055907, -2.25612222e-08, 1, 1.0159313e-07, 0.727055907, 8.61549054e-08, -0.686578274)
end)
Section:Toggle("Raids Law", false, function(v)
    game.Players.LocalPlayer.Character.HumanoidRootPart.CFrame = CFrame.new(-6293.12012, 16.2000732, -4994.10205, -0.303607613, 1.02938024e-07, 0.952797174, 4.51372131e-08, 1, -9.36548048e-08, -0.952797174, 1.45723096e-08, -0.303607613)
end)
Section:Toggle("Forgotton Island", false, function(v)
    game.Players.LocalPlayer.Character.HumanoidRootPart.CFrame = CFrame.new(-3053.70313, 238.846237, -10213.8711, 0.997547388, 3.68009319e-06, -0.0699884221, -2.12733084e-07, 1, 4.95493987e-05, 0.0699884221, -4.94129854e-05, 0.997547388)
end)
--Players--
local Tab = Library:Tab("Players")
local Section = Tab:Section("Players")

players = {}
 
for i,v in pairs(game:GetService("Players"):GetChildren()) do
   table.insert(players,v.Name)
end
Section:Dropdown("Select Player", players, "Select", function(abc)
    Select = abc
end)
Section:Toggle("Refresh", false, function(v)
    loadstring(game:HttpGet("https://pastebin.com/raw/L6XVEXLS"))()
end)
Section:Toggle("Teleport", false, function(v)
    game.Players.LocalPlayer.Character.HumanoidRootPart.CFrame = game.Players[Select].Character.HumanoidRootPart.CFrame
end)
Section:Toggle("Kill", false, function(v)
     local on
local keybind=Enum.KeyCode.F5
local keybindEnd=Enum.KeyCode.F6
local UserInputService=game:GetService("UserInputService")
local RunService=game:GetService("RunService")
local plr=game:GetService("Players").LocalPlayer
local mouse=plr:GetMouse()

local sg=Instance.new("ScreenGui",plr.PlayerGui)
local f=Instance.new("TextLabel",sg)
f.Size=UDim2.new(0,25,0,10)
f.BackgroundColor3=Color3.fromRGB(180,50,50)
f.Visible=false
f.Text="On"
f.TextSize=11

local vu = game:GetService("VirtualUser")
local function CC()
vu:CaptureController();
end 
local function CB()
local v2 = Vector2.new();
vu:ClickButton1(v2);
end

function Start(a,b)
   if a.KeyCode==keybind then
       on=true
       a=RunService.Stepped:Connect(function()
           if on then
               CC();
               CB();
               f.Visible=true
               f.Position=UDim2.new(0,mouse.X-12.5,0,mouse.Y-15)
           else
               a:Disconnect()
           end
       end)
       f.Visible=false
   end
end

function Stop(a,b)
   if a.KeyCode==keybindEnd then
       on=false
       f.Visible=false
   end
end

UserInputService.InputBegan:connect(Start)
UserInputService.InputEnded:connect(Stop)
wait(1)
    game.Players.LocalPlayer.Character.HumanoidRootPart.CFrame = game.Players[Select].Character.HumanoidRootPart.CFrame
    wait()
    game.Players.LocalPlayer.Character.HumanoidRootPart.CFrame = game.Players[Select].Character.HumanoidRootPart.CFrame
wait()
    game.Players.LocalPlayer.Character.HumanoidRootPart.CFrame = game.Players[Select].Character.HumanoidRootPart.CFrame
wait()
    game.Players.LocalPlayer.Character.HumanoidRootPart.CFrame = game.Players[Select].Character.HumanoidRootPart.CFrame
wait()
    game.Players.LocalPlayer.Character.HumanoidRootPart.CFrame = game.Players[Select].Character.HumanoidRootPart.CFrame
wait()
    game.Players.LocalPlayer.Character.HumanoidRootPart.CFrame = game.Players[Select].Character.HumanoidRootPart.CFrame
wait()
    game.Players.LocalPlayer.Character.HumanoidRootPart.CFrame = game.Players[Select].Character.HumanoidRootPart.CFrame
wait()
    game.Players.LocalPlayer.Character.HumanoidRootPart.CFrame = game.Players[Select].Character.HumanoidRootPart.CFrame
wait()
    game.Players.LocalPlayer.Character.HumanoidRootPart.CFrame = game.Players[Select].Character.HumanoidRootPart.CFrame
wait()
    game.Players.LocalPlayer.Character.HumanoidRootPart.CFrame = game.Players[Select].Character.HumanoidRootPart.CFrame
wait()
    game.Players.LocalPlayer.Character.HumanoidRootPart.CFrame = game.Players[Select].Character.HumanoidRootPart.CFrame
wait()
    game.Players.LocalPlayer.Character.HumanoidRootPart.CFrame = game.Players[Select].Character.HumanoidRootPart.CFrame
wait()
    game.Players.LocalPlayer.Character.HumanoidRootPart.CFrame = game.Players[Select].Character.HumanoidRootPart.CFrame
wait()
    game.Players.LocalPlayer.Character.HumanoidRootPart.CFrame = game.Players[Select].Character.HumanoidRootPart.CFrame
wait()
    game.Players.LocalPlayer.Character.HumanoidRootPart.CFrame = game.Players[Select].Character.HumanoidRootPart.CFrame
wait()
    game.Players.LocalPlayer.Character.HumanoidRootPart.CFrame = game.Players[Select].Character.HumanoidRootPart.CFrame
wait()
    game.Players.LocalPlayer.Character.HumanoidRootPart.CFrame = game.Players[Select].Character.HumanoidRootPart.CFrame
wait()
    game.Players.LocalPlayer.Character.HumanoidRootPart.CFrame = game.Players[Select].Character.HumanoidRootPart.CFrame
wait()
    game.Players.LocalPlayer.Character.HumanoidRootPart.CFrame = game.Players[Select].Character.HumanoidRootPart.CFrame
wait()
    game.Players.LocalPlayer.Character.HumanoidRootPart.CFrame = game.Players[Select].Character.HumanoidRootPart.CFrame
wait()
    game.Players.LocalPlayer.Character.HumanoidRootPart.CFrame = game.Players[Select].Character.HumanoidRootPart.CFrame
wait()
    game.Players.LocalPlayer.Character.HumanoidRootPart.CFrame = game.Players[Select].Character.HumanoidRootPart.CFrame
wait()
    game.Players.LocalPlayer.Character.HumanoidRootPart.CFrame = game.Players[Select].Character.HumanoidRootPart.CFrame
wait()
    game.Players.LocalPlayer.Character.HumanoidRootPart.CFrame = game.Players[Select].Character.HumanoidRootPart.CFrame
wait()
    game.Players.LocalPlayer.Character.HumanoidRootPart.CFrame = game.Players[Select].Character.HumanoidRootPart.CFrame
wait()
    game.Players.LocalPlayer.Character.HumanoidRootPart.CFrame = game.Players[Select].Character.HumanoidRootPart.CFrame
wait()
    game.Players.LocalPlayer.Character.HumanoidRootPart.CFrame = game.Players[Select].Character.HumanoidRootPart.CFrame
wait()
    game.Players.LocalPlayer.Character.HumanoidRootPart.CFrame = game.Players[Select].Character.HumanoidRootPart.CFrame
wait()
    game.Players.LocalPlayer.Character.HumanoidRootPart.CFrame = game.Players[Select].Character.HumanoidRootPart.CFrame
wait()
    game.Players.LocalPlayer.Character.HumanoidRootPart.CFrame = game.Players[Select].Character.HumanoidRootPart.CFrame
wait()
    game.Players.LocalPlayer.Character.HumanoidRootPart.CFrame = game.Players[Select].Character.HumanoidRootPart.CFrame
wait()
    game.Players.LocalPlayer.Character.HumanoidRootPart.CFrame = game.Players[Select].Character.HumanoidRootPart.CFrame
wait()
    game.Players.LocalPlayer.Character.HumanoidRootPart.CFrame = game.Players[Select].Character.HumanoidRootPart.CFrame
wait()
    game.Players.LocalPlayer.Character.HumanoidRootPart.CFrame = game.Players[Select].Character.HumanoidRootPart.CFrame
wait()
    game.Players.LocalPlayer.Character.HumanoidRootPart.CFrame = game.Players[Select].Character.HumanoidRootPart.CFrame
wait()
    game.Players.LocalPlayer.Character.HumanoidRootPart.CFrame = game.Players[Select].Character.HumanoidRootPart.CFrame
wait()
    game.Players.LocalPlayer.Character.HumanoidRootPart.CFrame = game.Players[Select].Character.HumanoidRootPart.CFrame
wait()
    game.Players.LocalPlayer.Character.HumanoidRootPart.CFrame = game.Players[Select].Character.HumanoidRootPart.CFrame
game.Players.LocalPlayer.Character.HumanoidRootPart.CFrame = game.Players[Select].Character.HumanoidRootPart.CFrame
    wait()
    game.Players.LocalPlayer.Character.HumanoidRootPart.CFrame = game.Players[Select].Character.HumanoidRootPart.CFrame
wait()
    game.Players.LocalPlayer.Character.HumanoidRootPart.CFrame = game.Players[Select].Character.HumanoidRootPart.CFrame
wait()
    game.Players.LocalPlayer.Character.HumanoidRootPart.CFrame = game.Players[Select].Character.HumanoidRootPart.CFrame
wait()
    game.Players.LocalPlayer.Character.HumanoidRootPart.CFrame = game.Players[Select].Character.HumanoidRootPart.CFrame
wait()
    game.Players.LocalPlayer.Character.HumanoidRootPart.CFrame = game.Players[Select].Character.HumanoidRootPart.CFrame
wait()
    game.Players.LocalPlayer.Character.HumanoidRootPart.CFrame = game.Players[Select].Character.HumanoidRootPart.CFrame
wait()
    game.Players.LocalPlayer.Character.HumanoidRootPart.CFrame = game.Players[Select].Character.HumanoidRootPart.CFrame
wait()
    game.Players.LocalPlayer.Character.HumanoidRootPart.CFrame = game.Players[Select].Character.HumanoidRootPart.CFrame
wait()
    game.Players.LocalPlayer.Character.HumanoidRootPart.CFrame = game.Players[Select].Character.HumanoidRootPart.CFrame
wait()
    game.Players.LocalPlayer.Character.HumanoidRootPart.CFrame = game.Players[Select].Character.HumanoidRootPart.CFrame
wait()
    game.Players.LocalPlayer.Character.HumanoidRootPart.CFrame = game.Players[Select].Character.HumanoidRootPart.CFrame
wait()
    game.Players.LocalPlayer.Character.HumanoidRootPart.CFrame = game.Players[Select].Character.HumanoidRootPart.CFrame
wait()
    game.Players.LocalPlayer.Character.HumanoidRootPart.CFrame = game.Players[Select].Character.HumanoidRootPart.CFrame
wait()
    game.Players.LocalPlayer.Character.HumanoidRootPart.CFrame = game.Players[Select].Character.HumanoidRootPart.CFrame
wait()
    game.Players.LocalPlayer.Character.HumanoidRootPart.CFrame = game.Players[Select].Character.HumanoidRootPart.CFrame
wait()
    game.Players.LocalPlayer.Character.HumanoidRootPart.CFrame = game.Players[Select].Character.HumanoidRootPart.CFrame
wait()
    game.Players.LocalPlayer.Character.HumanoidRootPart.CFrame = game.Players[Select].Character.HumanoidRootPart.CFrame
wait()
    game.Players.LocalPlayer.Character.HumanoidRootPart.CFrame = game.Players[Select].Character.HumanoidRootPart.CFrame
wait()
    game.Players.LocalPlayer.Character.HumanoidRootPart.CFrame = game.Players[Select].Character.HumanoidRootPart.CFrame
wait()
    game.Players.LocalPlayer.Character.HumanoidRootPart.CFrame = game.Players[Select].Character.HumanoidRootPart.CFrame
wait()
    game.Players.LocalPlayer.Character.HumanoidRootPart.CFrame = game.Players[Select].Character.HumanoidRootPart.CFrame
wait()
    game.Players.LocalPlayer.Character.HumanoidRootPart.CFrame = game.Players[Select].Character.HumanoidRootPart.CFrame
wait()
    game.Players.LocalPlayer.Character.HumanoidRootPart.CFrame = game.Players[Select].Character.HumanoidRootPart.CFrame
wait()
    game.Players.LocalPlayer.Character.HumanoidRootPart.CFrame = game.Players[Select].Character.HumanoidRootPart.CFrame
wait()
    game.Players.LocalPlayer.Character.HumanoidRootPart.CFrame = game.Players[Select].Character.HumanoidRootPart.CFrame
wait()
    game.Players.LocalPlayer.Character.HumanoidRootPart.CFrame = game.Players[Select].Character.HumanoidRootPart.CFrame
wait()
    game.Players.LocalPlayer.Character.HumanoidRootPart.CFrame = game.Players[Select].Character.HumanoidRootPart.CFrame
wait()
    game.Players.LocalPlayer.Character.HumanoidRootPart.CFrame = game.Players[Select].Character.HumanoidRootPart.CFrame
wait()
    game.Players.LocalPlayer.Character.HumanoidRootPart.CFrame = game.Players[Select].Character.HumanoidRootPart.CFrame
wait()
    game.Players.LocalPlayer.Character.HumanoidRootPart.CFrame = game.Players[Select].Character.HumanoidRootPart.CFrame
wait()
    game.Players.LocalPlayer.Character.HumanoidRootPart.CFrame = game.Players[Select].Character.HumanoidRootPart.CFrame
wait()
    game.Players.LocalPlayer.Character.HumanoidRootPart.CFrame = game.Players[Select].Character.HumanoidRootPart.CFrame
wait()
    game.Players.LocalPlayer.Character.HumanoidRootPart.CFrame = game.Players[Select].Character.HumanoidRootPart.CFrame
wait()
    game.Players.LocalPlayer.Character.HumanoidRootPart.CFrame = game.Players[Select].Character.HumanoidRootPart.CFrame
wait()
    game.Players.LocalPlayer.Character.HumanoidRootPart.CFrame = game.Players[Select].Character.HumanoidRootPart.CFrame
wait()
    game.Players.LocalPlayer.Character.HumanoidRootPart.CFrame = game.Players[Select].Character.HumanoidRootPart.CFrame
wait()
    game.Players.LocalPlayer.Character.HumanoidRootPart.CFrame = game.Players[Select].Character.HumanoidRootPart.CFrame
game.Players.LocalPlayer.Character.HumanoidRootPart.CFrame = game.Players[Select].Character.HumanoidRootPart.CFrame
    wait()
    game.Players.LocalPlayer.Character.HumanoidRootPart.CFrame = game.Players[Select].Character.HumanoidRootPart.CFrame
wait()
    game.Players.LocalPlayer.Character.HumanoidRootPart.CFrame = game.Players[Select].Character.HumanoidRootPart.CFrame
wait()
    game.Players.LocalPlayer.Character.HumanoidRootPart.CFrame = game.Players[Select].Character.HumanoidRootPart.CFrame
wait()
    game.Players.LocalPlayer.Character.HumanoidRootPart.CFrame = game.Players[Select].Character.HumanoidRootPart.CFrame
wait()
    game.Players.LocalPlayer.Character.HumanoidRootPart.CFrame = game.Players[Select].Character.HumanoidRootPart.CFrame
wait()
    game.Players.LocalPlayer.Character.HumanoidRootPart.CFrame = game.Players[Select].Character.HumanoidRootPart.CFrame
wait()
    game.Players.LocalPlayer.Character.HumanoidRootPart.CFrame = game.Players[Select].Character.HumanoidRootPart.CFrame
wait()
    game.Players.LocalPlayer.Character.HumanoidRootPart.CFrame = game.Players[Select].Character.HumanoidRootPart.CFrame
wait()
    game.Players.LocalPlayer.Character.HumanoidRootPart.CFrame = game.Players[Select].Character.HumanoidRootPart.CFrame
wait()
    game.Players.LocalPlayer.Character.HumanoidRootPart.CFrame = game.Players[Select].Character.HumanoidRootPart.CFrame
wait()
    game.Players.LocalPlayer.Character.HumanoidRootPart.CFrame = game.Players[Select].Character.HumanoidRootPart.CFrame
wait()
    game.Players.LocalPlayer.Character.HumanoidRootPart.CFrame = game.Players[Select].Character.HumanoidRootPart.CFrame
wait()
    game.Players.LocalPlayer.Character.HumanoidRootPart.CFrame = game.Players[Select].Character.HumanoidRootPart.CFrame
wait()
    game.Players.LocalPlayer.Character.HumanoidRootPart.CFrame = game.Players[Select].Character.HumanoidRootPart.CFrame
wait()
    game.Players.LocalPlayer.Character.HumanoidRootPart.CFrame = game.Players[Select].Character.HumanoidRootPart.CFrame
wait()
    game.Players.LocalPlayer.Character.HumanoidRootPart.CFrame = game.Players[Select].Character.HumanoidRootPart.CFrame
wait()
    game.Players.LocalPlayer.Character.HumanoidRootPart.CFrame = game.Players[Select].Character.HumanoidRootPart.CFrame
wait()
    game.Players.LocalPlayer.Character.HumanoidRootPart.CFrame = game.Players[Select].Character.HumanoidRootPart.CFrame
wait()
    game.Players.LocalPlayer.Character.HumanoidRootPart.CFrame = game.Players[Select].Character.HumanoidRootPart.CFrame
wait()
    game.Players.LocalPlayer.Character.HumanoidRootPart.CFrame = game.Players[Select].Character.HumanoidRootPart.CFrame
wait()
    game.Players.LocalPlayer.Character.HumanoidRootPart.CFrame = game.Players[Select].Character.HumanoidRootPart.CFrame
wait()
    game.Players.LocalPlayer.Character.HumanoidRootPart.CFrame = game.Players[Select].Character.HumanoidRootPart.CFrame
wait()
    game.Players.LocalPlayer.Character.HumanoidRootPart.CFrame = game.Players[Select].Character.HumanoidRootPart.CFrame
wait()
    game.Players.LocalPlayer.Character.HumanoidRootPart.CFrame = game.Players[Select].Character.HumanoidRootPart.CFrame
wait()
    game.Players.LocalPlayer.Character.HumanoidRootPart.CFrame = game.Players[Select].Character.HumanoidRootPart.CFrame
wait()
    game.Players.LocalPlayer.Character.HumanoidRootPart.CFrame = game.Players[Select].Character.HumanoidRootPart.CFrame
wait()
    game.Players.LocalPlayer.Character.HumanoidRootPart.CFrame = game.Players[Select].Character.HumanoidRootPart.CFrame
wait()
    game.Players.LocalPlayer.Character.HumanoidRootPart.CFrame = game.Players[Select].Character.HumanoidRootPart.CFrame
wait()
    game.Players.LocalPlayer.Character.HumanoidRootPart.CFrame = game.Players[Select].Character.HumanoidRootPart.CFrame
wait()
    game.Players.LocalPlayer.Character.HumanoidRootPart.CFrame = game.Players[Select].Character.HumanoidRootPart.CFrame
wait()
    game.Players.LocalPlayer.Character.HumanoidRootPart.CFrame = game.Players[Select].Character.HumanoidRootPart.CFrame
wait()
    game.Players.LocalPlayer.Character.HumanoidRootPart.CFrame = game.Players[Select].Character.HumanoidRootPart.CFrame
wait()
    game.Players.LocalPlayer.Character.HumanoidRootPart.CFrame = game.Players[Select].Character.HumanoidRootPart.CFrame
wait()
    game.Players.LocalPlayer.Character.HumanoidRootPart.CFrame = game.Players[Select].Character.HumanoidRootPart.CFrame
wait()
    game.Players.LocalPlayer.Character.HumanoidRootPart.CFrame = game.Players[Select].Character.HumanoidRootPart.CFrame
wait()
    game.Players.LocalPlayer.Character.HumanoidRootPart.CFrame = game.Players[Select].Character.HumanoidRootPart.CFrame
wait()
    game.Players.LocalPlayer.Character.HumanoidRootPart.CFrame = game.Players[Select].Character.HumanoidRootPart.CFrame
game.Players.LocalPlayer.Character.HumanoidRootPart.CFrame = game.Players[Select].Character.HumanoidRootPart.CFrame
    wait()
    game.Players.LocalPlayer.Character.HumanoidRootPart.CFrame = game.Players[Select].Character.HumanoidRootPart.CFrame
wait()
    game.Players.LocalPlayer.Character.HumanoidRootPart.CFrame = game.Players[Select].Character.HumanoidRootPart.CFrame
wait()
    game.Players.LocalPlayer.Character.HumanoidRootPart.CFrame = game.Players[Select].Character.HumanoidRootPart.CFrame
wait()
    game.Players.LocalPlayer.Character.HumanoidRootPart.CFrame = game.Players[Select].Character.HumanoidRootPart.CFrame
wait()
    game.Players.LocalPlayer.Character.HumanoidRootPart.CFrame = game.Players[Select].Character.HumanoidRootPart.CFrame
wait()
    game.Players.LocalPlayer.Character.HumanoidRootPart.CFrame = game.Players[Select].Character.HumanoidRootPart.CFrame
wait()
    game.Players.LocalPlayer.Character.HumanoidRootPart.CFrame = game.Players[Select].Character.HumanoidRootPart.CFrame
wait()
    game.Players.LocalPlayer.Character.HumanoidRootPart.CFrame = game.Players[Select].Character.HumanoidRootPart.CFrame
wait()
    game.Players.LocalPlayer.Character.HumanoidRootPart.CFrame = game.Players[Select].Character.HumanoidRootPart.CFrame
wait()
    game.Players.LocalPlayer.Character.HumanoidRootPart.CFrame = game.Players[Select].Character.HumanoidRootPart.CFrame
wait()
    game.Players.LocalPlayer.Character.HumanoidRootPart.CFrame = game.Players[Select].Character.HumanoidRootPart.CFrame
wait()
    game.Players.LocalPlayer.Character.HumanoidRootPart.CFrame = game.Players[Select].Character.HumanoidRootPart.CFrame
wait()
    game.Players.LocalPlayer.Character.HumanoidRootPart.CFrame = game.Players[Select].Character.HumanoidRootPart.CFrame
wait()
    game.Players.LocalPlayer.Character.HumanoidRootPart.CFrame = game.Players[Select].Character.HumanoidRootPart.CFrame
wait()
    game.Players.LocalPlayer.Character.HumanoidRootPart.CFrame = game.Players[Select].Character.HumanoidRootPart.CFrame
wait()
    game.Players.LocalPlayer.Character.HumanoidRootPart.CFrame = game.Players[Select].Character.HumanoidRootPart.CFrame
wait()
    game.Players.LocalPlayer.Character.HumanoidRootPart.CFrame = game.Players[Select].Character.HumanoidRootPart.CFrame
wait()
    game.Players.LocalPlayer.Character.HumanoidRootPart.CFrame = game.Players[Select].Character.HumanoidRootPart.CFrame
wait()
    game.Players.LocalPlayer.Character.HumanoidRootPart.CFrame = game.Players[Select].Character.HumanoidRootPart.CFrame
wait()
    game.Players.LocalPlayer.Character.HumanoidRootPart.CFrame = game.Players[Select].Character.HumanoidRootPart.CFrame
wait()
    game.Players.LocalPlayer.Character.HumanoidRootPart.CFrame = game.Players[Select].Character.HumanoidRootPart.CFrame
wait()
    game.Players.LocalPlayer.Character.HumanoidRootPart.CFrame = game.Players[Select].Character.HumanoidRootPart.CFrame
wait()
    game.Players.LocalPlayer.Character.HumanoidRootPart.CFrame = game.Players[Select].Character.HumanoidRootPart.CFrame
wait()
    game.Players.LocalPlayer.Character.HumanoidRootPart.CFrame = game.Players[Select].Character.HumanoidRootPart.CFrame
wait()
    game.Players.LocalPlayer.Character.HumanoidRootPart.CFrame = game.Players[Select].Character.HumanoidRootPart.CFrame
wait()
    game.Players.LocalPlayer.Character.HumanoidRootPart.CFrame = game.Players[Select].Character.HumanoidRootPart.CFrame
wait()
    game.Players.LocalPlayer.Character.HumanoidRootPart.CFrame = game.Players[Select].Character.HumanoidRootPart.CFrame
wait()
    game.Players.LocalPlayer.Character.HumanoidRootPart.CFrame = game.Players[Select].Character.HumanoidRootPart.CFrame
wait()
    game.Players.LocalPlayer.Character.HumanoidRootPart.CFrame = game.Players[Select].Character.HumanoidRootPart.CFrame
wait()
    game.Players.LocalPlayer.Character.HumanoidRootPart.CFrame = game.Players[Select].Character.HumanoidRootPart.CFrame
wait()
    game.Players.LocalPlayer.Character.HumanoidRootPart.CFrame = game.Players[Select].Character.HumanoidRootPart.CFrame
wait()
    game.Players.LocalPlayer.Character.HumanoidRootPart.CFrame = game.Players[Select].Character.HumanoidRootPart.CFrame
wait()
    game.Players.LocalPlayer.Character.HumanoidRootPart.CFrame = game.Players[Select].Character.HumanoidRootPart.CFrame
wait()
    game.Players.LocalPlayer.Character.HumanoidRootPart.CFrame = game.Players[Select].Character.HumanoidRootPart.CFrame
wait()
    game.Players.LocalPlayer.Character.HumanoidRootPart.CFrame = game.Players[Select].Character.HumanoidRootPart.CFrame
wait()
    game.Players.LocalPlayer.Character.HumanoidRootPart.CFrame = game.Players[Select].Character.HumanoidRootPart.CFrame
wait()
    game.Players.LocalPlayer.Character.HumanoidRootPart.CFrame = game.Players[Select].Character.HumanoidRootPart.CFrame
game.Players.LocalPlayer.Character.HumanoidRootPart.CFrame = game.Players[Select].Character.HumanoidRootPart.CFrame
    wait()
    game.Players.LocalPlayer.Character.HumanoidRootPart.CFrame = game.Players[Select].Character.HumanoidRootPart.CFrame
wait()
    game.Players.LocalPlayer.Character.HumanoidRootPart.CFrame = game.Players[Select].Character.HumanoidRootPart.CFrame
wait()
    game.Players.LocalPlayer.Character.HumanoidRootPart.CFrame = game.Players[Select].Character.HumanoidRootPart.CFrame
wait()
    game.Players.LocalPlayer.Character.HumanoidRootPart.CFrame = game.Players[Select].Character.HumanoidRootPart.CFrame
wait()
    game.Players.LocalPlayer.Character.HumanoidRootPart.CFrame = game.Players[Select].Character.HumanoidRootPart.CFrame
wait()
    game.Players.LocalPlayer.Character.HumanoidRootPart.CFrame = game.Players[Select].Character.HumanoidRootPart.CFrame
wait()
    game.Players.LocalPlayer.Character.HumanoidRootPart.CFrame = game.Players[Select].Character.HumanoidRootPart.CFrame
wait()
    game.Players.LocalPlayer.Character.HumanoidRootPart.CFrame = game.Players[Select].Character.HumanoidRootPart.CFrame
wait()
    game.Players.LocalPlayer.Character.HumanoidRootPart.CFrame = game.Players[Select].Character.HumanoidRootPart.CFrame
wait()
    game.Players.LocalPlayer.Character.HumanoidRootPart.CFrame = game.Players[Select].Character.HumanoidRootPart.CFrame
wait()
    game.Players.LocalPlayer.Character.HumanoidRootPart.CFrame = game.Players[Select].Character.HumanoidRootPart.CFrame
wait()
    game.Players.LocalPlayer.Character.HumanoidRootPart.CFrame = game.Players[Select].Character.HumanoidRootPart.CFrame
wait()
    game.Players.LocalPlayer.Character.HumanoidRootPart.CFrame = game.Players[Select].Character.HumanoidRootPart.CFrame
wait()
    game.Players.LocalPlayer.Character.HumanoidRootPart.CFrame = game.Players[Select].Character.HumanoidRootPart.CFrame
wait()
    game.Players.LocalPlayer.Character.HumanoidRootPart.CFrame = game.Players[Select].Character.HumanoidRootPart.CFrame
wait()
    game.Players.LocalPlayer.Character.HumanoidRootPart.CFrame = game.Players[Select].Character.HumanoidRootPart.CFrame
wait()
    game.Players.LocalPlayer.Character.HumanoidRootPart.CFrame = game.Players[Select].Character.HumanoidRootPart.CFrame
wait()
    game.Players.LocalPlayer.Character.HumanoidRootPart.CFrame = game.Players[Select].Character.HumanoidRootPart.CFrame
wait()
    game.Players.LocalPlayer.Character.HumanoidRootPart.CFrame = game.Players[Select].Character.HumanoidRootPart.CFrame
wait()
    game.Players.LocalPlayer.Character.HumanoidRootPart.CFrame = game.Players[Select].Character.HumanoidRootPart.CFrame
wait()
    game.Players.LocalPlayer.Character.HumanoidRootPart.CFrame = game.Players[Select].Character.HumanoidRootPart.CFrame
wait()
    game.Players.LocalPlayer.Character.HumanoidRootPart.CFrame = game.Players[Select].Character.HumanoidRootPart.CFrame
wait()
    game.Players.LocalPlayer.Character.HumanoidRootPart.CFrame = game.Players[Select].Character.HumanoidRootPart.CFrame
wait()
    game.Players.LocalPlayer.Character.HumanoidRootPart.CFrame = game.Players[Select].Character.HumanoidRootPart.CFrame
wait()
    game.Players.LocalPlayer.Character.HumanoidRootPart.CFrame = game.Players[Select].Character.HumanoidRootPart.CFrame
wait()
    game.Players.LocalPlayer.Character.HumanoidRootPart.CFrame = game.Players[Select].Character.HumanoidRootPart.CFrame
wait()
    game.Players.LocalPlayer.Character.HumanoidRootPart.CFrame = game.Players[Select].Character.HumanoidRootPart.CFrame
wait()
    game.Players.LocalPlayer.Character.HumanoidRootPart.CFrame = game.Players[Select].Character.HumanoidRootPart.CFrame
wait()
    game.Players.LocalPlayer.Character.HumanoidRootPart.CFrame = game.Players[Select].Character.HumanoidRootPart.CFrame
wait()
    game.Players.LocalPlayer.Character.HumanoidRootPart.CFrame = game.Players[Select].Character.HumanoidRootPart.CFrame
wait()
    game.Players.LocalPlayer.Character.HumanoidRootPart.CFrame = game.Players[Select].Character.HumanoidRootPart.CFrame
wait()
    game.Players.LocalPlayer.Character.HumanoidRootPart.CFrame = game.Players[Select].Character.HumanoidRootPart.CFrame
wait()
    game.Players.LocalPlayer.Character.HumanoidRootPart.CFrame = game.Players[Select].Character.HumanoidRootPart.CFrame
wait()
    game.Players.LocalPlayer.Character.HumanoidRootPart.CFrame = game.Players[Select].Character.HumanoidRootPart.CFrame
wait()
    game.Players.LocalPlayer.Character.HumanoidRootPart.CFrame = game.Players[Select].Character.HumanoidRootPart.CFrame
wait()
    game.Players.LocalPlayer.Character.HumanoidRootPart.CFrame = game.Players[Select].Character.HumanoidRootPart.CFrame
wait()
    game.Players.LocalPlayer.Character.HumanoidRootPart.CFrame = game.Players[Select].Character.HumanoidRootPart.CFrame
game.Players.LocalPlayer.Character.HumanoidRootPart.CFrame = game.Players[Select].Character.HumanoidRootPart.CFrame
    wait()
    game.Players.LocalPlayer.Character.HumanoidRootPart.CFrame = game.Players[Select].Character.HumanoidRootPart.CFrame
wait()
    game.Players.LocalPlayer.Character.HumanoidRootPart.CFrame = game.Players[Select].Character.HumanoidRootPart.CFrame
wait()
    game.Players.LocalPlayer.Character.HumanoidRootPart.CFrame = game.Players[Select].Character.HumanoidRootPart.CFrame
wait()
    game.Players.LocalPlayer.Character.HumanoidRootPart.CFrame = game.Players[Select].Character.HumanoidRootPart.CFrame
wait()
    game.Players.LocalPlayer.Character.HumanoidRootPart.CFrame = game.Players[Select].Character.HumanoidRootPart.CFrame
wait()
    game.Players.LocalPlayer.Character.HumanoidRootPart.CFrame = game.Players[Select].Character.HumanoidRootPart.CFrame
wait()
    game.Players.LocalPlayer.Character.HumanoidRootPart.CFrame = game.Players[Select].Character.HumanoidRootPart.CFrame
wait()
    game.Players.LocalPlayer.Character.HumanoidRootPart.CFrame = game.Players[Select].Character.HumanoidRootPart.CFrame
wait()
    game.Players.LocalPlayer.Character.HumanoidRootPart.CFrame = game.Players[Select].Character.HumanoidRootPart.CFrame
wait()
    game.Players.LocalPlayer.Character.HumanoidRootPart.CFrame = game.Players[Select].Character.HumanoidRootPart.CFrame
wait()
    game.Players.LocalPlayer.Character.HumanoidRootPart.CFrame = game.Players[Select].Character.HumanoidRootPart.CFrame
wait()
    game.Players.LocalPlayer.Character.HumanoidRootPart.CFrame = game.Players[Select].Character.HumanoidRootPart.CFrame
wait()
    game.Players.LocalPlayer.Character.HumanoidRootPart.CFrame = game.Players[Select].Character.HumanoidRootPart.CFrame
wait()
    game.Players.LocalPlayer.Character.HumanoidRootPart.CFrame = game.Players[Select].Character.HumanoidRootPart.CFrame
wait()
    game.Players.LocalPlayer.Character.HumanoidRootPart.CFrame = game.Players[Select].Character.HumanoidRootPart.CFrame
wait()
    game.Players.LocalPlayer.Character.HumanoidRootPart.CFrame = game.Players[Select].Character.HumanoidRootPart.CFrame
wait()
    game.Players.LocalPlayer.Character.HumanoidRootPart.CFrame = game.Players[Select].Character.HumanoidRootPart.CFrame
wait()
    game.Players.LocalPlayer.Character.HumanoidRootPart.CFrame = game.Players[Select].Character.HumanoidRootPart.CFrame
wait()
    game.Players.LocalPlayer.Character.HumanoidRootPart.CFrame = game.Players[Select].Character.HumanoidRootPart.CFrame
wait()
    game.Players.LocalPlayer.Character.HumanoidRootPart.CFrame = game.Players[Select].Character.HumanoidRootPart.CFrame
wait()
    game.Players.LocalPlayer.Character.HumanoidRootPart.CFrame = game.Players[Select].Character.HumanoidRootPart.CFrame
wait()
    game.Players.LocalPlayer.Character.HumanoidRootPart.CFrame = game.Players[Select].Character.HumanoidRootPart.CFrame
wait()
    game.Players.LocalPlayer.Character.HumanoidRootPart.CFrame = game.Players[Select].Character.HumanoidRootPart.CFrame
wait()
    game.Players.LocalPlayer.Character.HumanoidRootPart.CFrame = game.Players[Select].Character.HumanoidRootPart.CFrame
wait()
    game.Players.LocalPlayer.Character.HumanoidRootPart.CFrame = game.Players[Select].Character.HumanoidRootPart.CFrame
wait()
    game.Players.LocalPlayer.Character.HumanoidRootPart.CFrame = game.Players[Select].Character.HumanoidRootPart.CFrame
wait()
    game.Players.LocalPlayer.Character.HumanoidRootPart.CFrame = game.Players[Select].Character.HumanoidRootPart.CFrame
wait()
    game.Players.LocalPlayer.Character.HumanoidRootPart.CFrame = game.Players[Select].Character.HumanoidRootPart.CFrame
wait()
    game.Players.LocalPlayer.Character.HumanoidRootPart.CFrame = game.Players[Select].Character.HumanoidRootPart.CFrame
wait()
    game.Players.LocalPlayer.Character.HumanoidRootPart.CFrame = game.Players[Select].Character.HumanoidRootPart.CFrame
wait()
    game.Players.LocalPlayer.Character.HumanoidRootPart.CFrame = game.Players[Select].Character.HumanoidRootPart.CFrame
wait()
    game.Players.LocalPlayer.Character.HumanoidRootPart.CFrame = game.Players[Select].Character.HumanoidRootPart.CFrame
wait()
    game.Players.LocalPlayer.Character.HumanoidRootPart.CFrame = game.Players[Select].Character.HumanoidRootPart.CFrame
wait()
    game.Players.LocalPlayer.Character.HumanoidRootPart.CFrame = game.Players[Select].Character.HumanoidRootPart.CFrame
wait()
    game.Players.LocalPlayer.Character.HumanoidRootPart.CFrame = game.Players[Select].Character.HumanoidRootPart.CFrame
wait()
    game.Players.LocalPlayer.Character.HumanoidRootPart.CFrame = game.Players[Select].Character.HumanoidRootPart.CFrame
wait()
    game.Players.LocalPlayer.Character.HumanoidRootPart.CFrame = game.Players[Select].Character.HumanoidRootPart.CFrame
game.Players.LocalPlayer.Character.HumanoidRootPart.CFrame = game.Players[Select].Character.HumanoidRootPart.CFrame
    wait()
    game.Players.LocalPlayer.Character.HumanoidRootPart.CFrame = game.Players[Select].Character.HumanoidRootPart.CFrame
wait()
    game.Players.LocalPlayer.Character.HumanoidRootPart.CFrame = game.Players[Select].Character.HumanoidRootPart.CFrame
wait()
    game.Players.LocalPlayer.Character.HumanoidRootPart.CFrame = game.Players[Select].Character.HumanoidRootPart.CFrame
wait()
    game.Players.LocalPlayer.Character.HumanoidRootPart.CFrame = game.Players[Select].Character.HumanoidRootPart.CFrame
wait()
    game.Players.LocalPlayer.Character.HumanoidRootPart.CFrame = game.Players[Select].Character.HumanoidRootPart.CFrame
wait()
    game.Players.LocalPlayer.Character.HumanoidRootPart.CFrame = game.Players[Select].Character.HumanoidRootPart.CFrame
wait()
    game.Players.LocalPlayer.Character.HumanoidRootPart.CFrame = game.Players[Select].Character.HumanoidRootPart.CFrame
wait()
    game.Players.LocalPlayer.Character.HumanoidRootPart.CFrame = game.Players[Select].Character.HumanoidRootPart.CFrame
wait()
    game.Players.LocalPlayer.Character.HumanoidRootPart.CFrame = game.Players[Select].Character.HumanoidRootPart.CFrame
wait()
    game.Players.LocalPlayer.Character.HumanoidRootPart.CFrame = game.Players[Select].Character.HumanoidRootPart.CFrame
wait()
    game.Players.LocalPlayer.Character.HumanoidRootPart.CFrame = game.Players[Select].Character.HumanoidRootPart.CFrame
wait()
    game.Players.LocalPlayer.Character.HumanoidRootPart.CFrame = game.Players[Select].Character.HumanoidRootPart.CFrame
wait()
    game.Players.LocalPlayer.Character.HumanoidRootPart.CFrame = game.Players[Select].Character.HumanoidRootPart.CFrame
wait()
    game.Players.LocalPlayer.Character.HumanoidRootPart.CFrame = game.Players[Select].Character.HumanoidRootPart.CFrame
wait()
    game.Players.LocalPlayer.Character.HumanoidRootPart.CFrame = game.Players[Select].Character.HumanoidRootPart.CFrame
wait()
    game.Players.LocalPlayer.Character.HumanoidRootPart.CFrame = game.Players[Select].Character.HumanoidRootPart.CFrame
wait()
    game.Players.LocalPlayer.Character.HumanoidRootPart.CFrame = game.Players[Select].Character.HumanoidRootPart.CFrame
wait()
    game.Players.LocalPlayer.Character.HumanoidRootPart.CFrame = game.Players[Select].Character.HumanoidRootPart.CFrame
wait()
    game.Players.LocalPlayer.Character.HumanoidRootPart.CFrame = game.Players[Select].Character.HumanoidRootPart.CFrame
wait()
    game.Players.LocalPlayer.Character.HumanoidRootPart.CFrame = game.Players[Select].Character.HumanoidRootPart.CFrame
wait()
    game.Players.LocalPlayer.Character.HumanoidRootPart.CFrame = game.Players[Select].Character.HumanoidRootPart.CFrame
wait()
    game.Players.LocalPlayer.Character.HumanoidRootPart.CFrame = game.Players[Select].Character.HumanoidRootPart.CFrame
wait()
    game.Players.LocalPlayer.Character.HumanoidRootPart.CFrame = game.Players[Select].Character.HumanoidRootPart.CFrame
wait()
    game.Players.LocalPlayer.Character.HumanoidRootPart.CFrame = game.Players[Select].Character.HumanoidRootPart.CFrame
wait()
    game.Players.LocalPlayer.Character.HumanoidRootPart.CFrame = game.Players[Select].Character.HumanoidRootPart.CFrame
wait()
    game.Players.LocalPlayer.Character.HumanoidRootPart.CFrame = game.Players[Select].Character.HumanoidRootPart.CFrame
wait()
    game.Players.LocalPlayer.Character.HumanoidRootPart.CFrame = game.Players[Select].Character.HumanoidRootPart.CFrame
wait()
    game.Players.LocalPlayer.Character.HumanoidRootPart.CFrame = game.Players[Select].Character.HumanoidRootPart.CFrame
wait()
    game.Players.LocalPlayer.Character.HumanoidRootPart.CFrame = game.Players[Select].Character.HumanoidRootPart.CFrame
wait()
    game.Players.LocalPlayer.Character.HumanoidRootPart.CFrame = game.Players[Select].Character.HumanoidRootPart.CFrame
wait()
    game.Players.LocalPlayer.Character.HumanoidRootPart.CFrame = game.Players[Select].Character.HumanoidRootPart.CFrame
wait()
    game.Players.LocalPlayer.Character.HumanoidRootPart.CFrame = game.Players[Select].Character.HumanoidRootPart.CFrame
wait()
    game.Players.LocalPlayer.Character.HumanoidRootPart.CFrame = game.Players[Select].Character.HumanoidRootPart.CFrame
wait()
    game.Players.LocalPlayer.Character.HumanoidRootPart.CFrame = game.Players[Select].Character.HumanoidRootPart.CFrame
wait()
    game.Players.LocalPlayer.Character.HumanoidRootPart.CFrame = game.Players[Select].Character.HumanoidRootPart.CFrame
wait()
    game.Players.LocalPlayer.Character.HumanoidRootPart.CFrame = game.Players[Select].Character.HumanoidRootPart.CFrame
wait()
    game.Players.LocalPlayer.Character.HumanoidRootPart.CFrame = game.Players[Select].Character.HumanoidRootPart.CFrame
game.Players.LocalPlayer.Character.HumanoidRootPart.CFrame = game.Players[Select].Character.HumanoidRootPart.CFrame
    wait()
    game.Players.LocalPlayer.Character.HumanoidRootPart.CFrame = game.Players[Select].Character.HumanoidRootPart.CFrame
wait()
    game.Players.LocalPlayer.Character.HumanoidRootPart.CFrame = game.Players[Select].Character.HumanoidRootPart.CFrame
wait()
    game.Players.LocalPlayer.Character.HumanoidRootPart.CFrame = game.Players[Select].Character.HumanoidRootPart.CFrame
wait()
    game.Players.LocalPlayer.Character.HumanoidRootPart.CFrame = game.Players[Select].Character.HumanoidRootPart.CFrame
wait()
    game.Players.LocalPlayer.Character.HumanoidRootPart.CFrame = game.Players[Select].Character.HumanoidRootPart.CFrame
wait()
    game.Players.LocalPlayer.Character.HumanoidRootPart.CFrame = game.Players[Select].Character.HumanoidRootPart.CFrame
wait()
    game.Players.LocalPlayer.Character.HumanoidRootPart.CFrame = game.Players[Select].Character.HumanoidRootPart.CFrame
wait()
    game.Players.LocalPlayer.Character.HumanoidRootPart.CFrame = game.Players[Select].Character.HumanoidRootPart.CFrame
wait()
    game.Players.LocalPlayer.Character.HumanoidRootPart.CFrame = game.Players[Select].Character.HumanoidRootPart.CFrame
wait()
    game.Players.LocalPlayer.Character.HumanoidRootPart.CFrame = game.Players[Select].Character.HumanoidRootPart.CFrame
wait()
    game.Players.LocalPlayer.Character.HumanoidRootPart.CFrame = game.Players[Select].Character.HumanoidRootPart.CFrame
wait()
    game.Players.LocalPlayer.Character.HumanoidRootPart.CFrame = game.Players[Select].Character.HumanoidRootPart.CFrame
wait()
    game.Players.LocalPlayer.Character.HumanoidRootPart.CFrame = game.Players[Select].Character.HumanoidRootPart.CFrame
wait()
    game.Players.LocalPlayer.Character.HumanoidRootPart.CFrame = game.Players[Select].Character.HumanoidRootPart.CFrame
wait()
    game.Players.LocalPlayer.Character.HumanoidRootPart.CFrame = game.Players[Select].Character.HumanoidRootPart.CFrame
wait()
    game.Players.LocalPlayer.Character.HumanoidRootPart.CFrame = game.Players[Select].Character.HumanoidRootPart.CFrame
wait()
    game.Players.LocalPlayer.Character.HumanoidRootPart.CFrame = game.Players[Select].Character.HumanoidRootPart.CFrame
wait()
    game.Players.LocalPlayer.Character.HumanoidRootPart.CFrame = game.Players[Select].Character.HumanoidRootPart.CFrame
end)
Section:Toggle("Spectate", false, function(v)
    local runDummyScript = function(f,scri)
local oldenv = getfenv(f)
local newenv = setmetatable({}, {
__index = function(_, k)
if k:lower() == 'script' then
return scri
else
return oldenv[k]
end
end
})
setfenv(f, newenv)
ypcall(function() f() end)
end
cors = {}
mas = Instance.new("Model",game:GetService("Lighting")) 
mas.Name = "CompiledModel"
o1 = Instance.new("ScreenGui")
o2 = Instance.new("Frame")
o3 = Instance.new("TextButton")
o4 = Instance.new("TextButton")
o5 = Instance.new("TextLabel")
o6 = Instance.new("ImageButton")
o7 = Instance.new("LocalScript")
o1.Name = "SpectateGui"
o1.Parent = mas
o2.Name = "Bar"
o2.Parent = o1
o2.Position = UDim2.new(-1,-100,0.87999999523163,-50)
o2.Size = UDim2.new(0,200,0,50)
o2.Position = UDim2.new(-1,-100,0.87999999523163,-50)
o2.BackgroundColor3 = Color3.new(0, 0, 0)
o2.BackgroundTransparency = 0.20000000298023
o2.BorderSizePixel = 5
o3.Name = "Previous"
o3.Parent = o2
o3.Size = UDim2.new(0.25,0,1,0)
o3.Text = "<"
o3.BackgroundColor3 = Color3.new(0.52549, 0.52549, 0.52549)
o3.BorderColor3 = Color3.new(0.509804, 0.796079, 1)
o3.BorderSizePixel = 0
o3.Font = Enum.Font.SourceSans
o3.FontSize = Enum.FontSize.Size48
o3.TextColor3 = Color3.new(1, 1, 1)
o4.Name = "Next"
o4.Parent = o2
o4.Position = UDim2.new(1,0,0,0)
o4.Size = UDim2.new(-0.25,0,1,0)
o4.Text = ">"
o4.Position = UDim2.new(1,0,0,0)
o4.BackgroundColor3 = Color3.new(0.52549, 0.52549, 0.52549)
o4.BorderColor3 = Color3.new(0.509804, 0.796079, 1)
o4.BorderSizePixel = 0
o4.Font = Enum.Font.SourceSans
o4.FontSize = Enum.FontSize.Size48
o4.TextColor3 = Color3.new(1, 1, 1)
o5.Name = "Title"
o5.Parent = o2
o5.Position = UDim2.new(0.27500000596046,0,0,0)
o5.Size = UDim2.new(0.44999998807907,0,1,0)
o5.Text = ""
o5.Position = UDim2.new(0.27500000596046,0,0,0)
o5.BackgroundColor3 = Color3.new(1, 1, 1)
o5.BackgroundTransparency = 1
o5.Font = Enum.Font.SourceSans
o5.FontSize = Enum.FontSize.Size14
o5.TextColor3 = Color3.new(1, 1, 1)
o5.TextScaled = true
o5.TextWrapped = true
o6.Name = "Button"
o6.Parent = o1
o6.Position = UDim2.new(0,0,0.5,-25)
o6.Size = UDim2.new(0,50,0,50)
o6.Position = UDim2.new(0,0,0.5,-25)
o6.BackgroundColor3 = Color3.new(1, 1, 1)
o6.BackgroundTransparency = 0.30000001192093
o6.BorderSizePixel = 5
o6.Image = "http://www.roblox.com/asset/?id=176106970"
o7.Parent = o1
table.insert(cors,coroutine.create(function()
wait()
runDummyScript(function()
-- By super10099
 
cam = game.Workspace.CurrentCamera
 
local bar = script.Parent.Bar
local title = bar.Title
local prev = bar.Previous
local nex = bar.Next
local button = script.Parent.Button
 
function get()
	for _,v in pairs(game.Players:GetPlayers())do
		if v.Name == title.Text then
			return(_)
		end
	end
end
 
 
local debounce = false
button.MouseButton1Click:connect(function()
	if debounce == false then debounce = true
		bar:TweenPosition(UDim2.new(.5,-100,0.88,-50),"In","Linear",1,true)
		pcall(function()
				title.Text = game.Players:GetPlayerFromCharacter(cam.CameraSubject.Parent).Name
		end)
	elseif debounce == true then debounce = false
		pcall(function() cam.CameraSubject = game.Players.LocalPlayer.Character.Humanoid end)
			bar:TweenPosition(UDim2.new(-1,-100,0.88,-50),"In","Linear",1,true)
		end
end)
 
prev.MouseButton1Click:connect(function()
	wait(.1)
	local players = game.Players:GetPlayers()
	local num = get()
	if not pcall(function() 
		cam.CameraSubject = players[num-1].Character.Humanoid
		end) then
		cam.CameraSubject = players[#players].Character.Humanoid
	end
pcall(function()
				title.Text = game.Players:GetPlayerFromCharacter(cam.CameraSubject.Parent).Name
		end)
end)
 
nex.MouseButton1Click:connect(function()
	wait(.1)
	local players = game.Players:GetPlayers()
	local num = get()
	if not pcall(function() 
		cam.CameraSubject = players[num+1].Character.Humanoid
		end) then
		cam.CameraSubject = players[1].Character.Humanoid
	end
pcall(function()
				title.Text = game.Players:GetPlayerFromCharacter(cam.CameraSubject.Parent).Name
		end)
end)
 
 
end,o7)
end))
mas.Parent = workspace
mas:MakeJoints()
local mas1 = mas:GetChildren()
for i=1,#mas1 do
	mas1[i].Parent = game:GetService("Players").LocalPlayer.PlayerGui 
	ypcall(function() mas1[i]:MakeJoints() end)
end
mas:Destroy()
for i=1,#cors do
coroutine.resume(cors[i])
end
end)
--Game--
local Tab = Library:Tab("Game")
local Section = Tab:Section("ESP")
Section:Toggle("PlayersESP", false, function(v)
    local MainParent = game.workspace.Terrain or nil
local LineFrame = Instance.new("ScreenGui",MainParent)
LineFrame.Name = "Lines"
LineFrame.Enabled = false
ToggleKey = Enum.KeyCode.F1
local Spotted = {};
local CharacterMotors = {}
CharacterMotors.GetMotors = function(char)
	local Motors = {}
		for i,v in pairs(char:GetDescendants()) do
			if v:IsA("Motor6D") then
				if v.Part0 and v.Part1 then--and v.Part0.Name ~= "HumanoidRootPart" and v.Part1.Name ~= "HumanoidRootPart" then
					table.insert(Motors,{v.Part0,v.Part1})
				end
			end
		end
	table.insert(Motors,{char:FindFirstChild("Head") or char.PrimaryPart,"Camera"})
	CharacterMotors[char] = Motors
	return CharacterMotors[char]
end
		
lerp = function(a, b, t)
	return a + (b - a) * t
end

local ESP = {Characters = {}}
ESP.Visible = true
ESP.Init = function(char,plr)
	--if (game:GetService("Players").LocalPlayer.Team == nil or plr.Team ~= game:GetService("Players").LocalPlayer.Team) then
		char.DescendantAdded:Connect(function()
			CharacterMotors.GetMotors(char)
		end)
		
		local BillboardUi = Instance.new("BillboardGui")
		BillboardUi.AlwaysOnTop = true
		BillboardUi.Size = UDim2.new(3,60,1,30)
		BillboardUi.StudsOffsetWorldSpace = Vector3.new(0,-4.5,0)
		BillboardUi.Adornee = char:WaitForChild("HumanoidRootPart")
		
		local PlayerName = Instance.new("TextLabel",BillboardUi)
		PlayerName.BackgroundTransparency = 1
		PlayerName.TextColor3 = (game:GetService("Players"):GetPlayerFromCharacter(char)).TeamColor.Color
		PlayerName.Size = UDim2.new(1,0,.3,0)
		PlayerName.ZIndex = 2
		PlayerName.Text = char.Name
		PlayerName.TextScaled = true
		PlayerName.TextStrokeTransparency = .25
		PlayerName.Font = Enum.Font.GothamBold
		PlayerName.TextStrokeColor3 = Color3.fromRGB(33, 33, 33)
		
		local Distance = PlayerName:Clone()
		Distance.Parent = BillboardUi
		Distance.Font = Enum.Font.Gotham
		Distance.TextColor3 = Color3.new(1,1,1)
		Distance.Position = UDim2.new(0,0,.3,0)
		
		local Health = PlayerName:Clone()
		Health.Parent = BillboardUi
		Health.Font = Enum.Font.Gotham
		Health.Position = UDim2.new(0,0,.6,0)
		
		ESP.Characters[char] = {PlayerName,Distance,Health,BillboardUi}
	--end
end
ESP.Render = function()
	
	for i,v in pairs(ESP.Characters) do
		pcall(function()
			local shrink = ((((game.Workspace.CurrentCamera.CFrame.p) - i.HumanoidRootPart.Position).Magnitude)/1500)+1
			v[2].Text = math.floor(((game.Workspace.CurrentCamera.CFrame.p) - i.HumanoidRootPart.Position).Magnitude+.5)
			v[3].Text = math.floor(i.Humanoid.Health).."/"..i.Humanoid.MaxHealth.." - "..math.floor(((i.Humanoid.Health/i.Humanoid.MaxHealth)*100)+.5).."%"
			v[3].TextColor3 = Color3.fromHSV((i.Humanoid.Health/i.Humanoid.MaxHealth) * (80/255),1,1)
			if not Spotted[i] then
				--v[1].TextTransparency = lerp(v[1].TextTransparency,.6,0.05)
			else
				--v[1].TextTransparency = lerp(v[1].TextTransparency,0,0.1)
			end
			v[1].TextColor3 = (game:GetService("Players"):GetPlayerFromCharacter(i)).TeamColor.Color
			--v[1].TextStrokeTransparency = 1-((1-v[1].TextTransparency)/2)
			--v[2].TextTransparency = v[1].TextTransparency
			--v[2].TextStrokeTransparency = v[1].TextStrokeTransparency
			--v[3].TextTransparency = v[1].TextTransparency
			--v[3].TextStrokeTransparency = v[1].TextStrokeTransparency
			v[4].Size = UDim2.new(3,60/shrink,1,30/shrink)
			v[1].Visible = ESP.Visible
			v[2].Visible = ESP.Visible
			v[3].Visible = ESP.Visible
			v[4].Parent = MainParent
			
		end)
	end
	
end

local Perspective = {}
Perspective.CalculatePoint = function(position,cam)
	local vector, onScreen = cam:WorldToScreenPoint(position)
	return Vector2.new(vector.X, vector.Y),vector.Z,onScreen
end

local Draw = {UsedLines = {}}
Draw.Line = function(a,b,line,width)
	if a and b then	
		local lerp = a:Lerp(b,.5)
		local Magnitude = (a-b).Magnitude
		line.AnchorPoint = Vector2.new(0.5,.5)
		line.Position = UDim2.new(lerp.X/game.Workspace.CurrentCamera.ViewportSize.X,0,(lerp.Y/(game.Workspace.CurrentCamera.ViewportSize.Y-36)),36/2)
		line.Size = UDim2.new(Magnitude/line.Parent.AbsoluteSize.X,0,0,width)
		line.Rotation = math.deg(math.atan2(a.y - b.y, a.x - b.x))
	else
		line:Destroy()
	end
end


Draw.Character = function(player,lines,cam)
	local Motors = CharacterMotors[player]
	if not Motors then
		Motors = CharacterMotors.GetMotors(player)
	end

	for i,v in pairs(Motors) do
		if v[1] and v[2] then
			local FoundLine = nil
			for i,v in pairs(lines:GetChildren()) do
				if Draw.UsedLines[v] == nil then
					Draw.UsedLines[v] = true
					FoundLine = v
					break
				end
			end
			local a2d,az,screen = Perspective.CalculatePoint(v[1].Position,cam)
			local b2d,bz,screen2
			local v2pos = v[2].Position
			Spotted[player] = false
			if v[2] == "Camera" then
				local ray = Ray.new(v[1].Position, (cam.CFrame.p - v[1].Position).unit * (cam.CFrame.p - v[1].Position).Magnitude)
				local part, position = workspace:FindPartOnRayWithIgnoreList(ray, {game:GetService("Players").LocalPlayer.Character,player}, false, true)
				if part then
					screen = false
					screen2 = false
				else
					Spotted[player] = true
					b2d,bz,screen2 = Vector2.new(cam.ViewportSize.x/2, cam.ViewportSize.y),0,true	
					screen = true
				end
				v2pos = v[1].Position
			else
				b2d,bz,screen2 = Perspective.CalculatePoint(v[2].Position,cam)	
			end
			if screen and screen2 and (v[1].Position-v2pos).Magnitude <= 5 then
				if not FoundLine then
					FoundLine = Instance.new("Frame")
					FoundLine.BackgroundColor3 = Color3.new(1,1,1)
					FoundLine.BackgroundTransparency = .25
					FoundLine.BorderSizePixel = 0
					FoundLine.Parent = lines	
					Draw.UsedLines[FoundLine] = true
				end
				if screen then
					Draw.Line(a2d,b2d,FoundLine,1)
				else
					Draw.Line(b2d,a2d,FoundLine,1)
				end
			elseif FoundLine then
				FoundLine:Destroy()
			end
		end
	end
end

Draw.ResetLines = function(lines)
	for i,v in pairs(lines:GetChildren()) do
		if Draw.UsedLines[v] == nil then
			v:Destroy()
		end
	end
	Draw.UsedLines = {}
end

local AddPlayer = function(plr)
	coroutine.resume(coroutine.create(function()
		if plr ~= game:GetService("Players").LocalPlayer  then
			if plr.Character then
				ESP.Init(plr.Character,plr)
			end
			plr.CharacterAdded:Connect(function(cha)
				ESP.Init(cha,plr)
			end)
		end
	end))
end

for i,v in pairs(game:GetService("Players"):GetChildren()) do
	AddPlayer(v)
end
game:GetService("Players").PlayerAdded:Connect(function(v)
	AddPlayer(v)
end)
game:GetService("UserInputService").InputBegan:connect(function(inputObject)
	if inputObject.KeyCode == ToggleKey then
		ESP.Visible = not ESP.Visible
	end
end)
game:GetService("RunService").RenderStepped:Connect(function()
	ESP.Render()
	for i,v in pairs(game:GetService("Players"):GetChildren()) do
		if v.Character and v ~= game:GetService("Players").LocalPlayer and (game:GetService("Players").LocalPlayer.Team == nil or v.Team ~= game:GetService("Players").LocalPlayer.Team) then
			if v.Character.PrimaryPart and (v.Character.PrimaryPart.Position - game.Workspace.CurrentCamera.CFrame.Position).Magnitude <= 200 then
				Draw.Character(v.Character,LineFrame,game.Workspace.CurrentCamera)
			end
		end
	end
	Draw.ResetLines(LineFrame)
end)
end)
local Section = Tab:Section("BuyCombat")
Section:Toggle("Blackleg", false, function(v)
    loadstring(game:HttpGet("https://pastebin.com/raw/pMV3eyqY"))()
end)
Section:Toggle("Electro", false, function(v)
    loadstring(game:HttpGet("https://pastebin.com/raw/1mBbkVM1"))()
end)
Section:Toggle("FishmanKarate", false, function(v)
    loadstring(game:HttpGet("https://pastebin.com/raw/hzZP2CvL"))()
end)
Section:Toggle("DragonClaw", false, function(v)
    loadstring(game:HttpGet("https://pastebin.com/raw/EJ9fpgW6"))()
end)
Section:Toggle("SuperHuman", false, function(v)
    loadstring(game:HttpGet("https://pastebin.com/raw/954m9fS9"))()
end)
Section:Toggle("DeathStep", false, function(v)
    loadstring(game:HttpGet("https://pastebin.com/raw/eWnPrWkv"))()
end)
Section:Toggle("SharkmanKarate", false, function(v)
   loadstring(game:HttpGet("https://pastebin.com/raw/4RQ7kCty"))() 
end)
Section:Toggle("ElectricClaw", false, function(v)
    loadstring(game:HttpGet("https://pastebin.com/raw/CiyBtnBu"))()
end)
local Section = Tab:Section("BringChest")
Section:Toggle("Chest1", false, function(v)
    local hrp = game.Players.LocalPlayer.Character.HumanoidRootPart
for i , v in pairs (workspace:GetDescendants()) do
  local obj = v
  if string.find(obj.Name, "Chest1") then
      hrp.CFrame = obj.CFrame + Vector3.new(0,20,0)
      wait(0.5)
  end
end
end)
Section:Toggle("Chest2", false, function(v)
    local hrp = game.Players.LocalPlayer.Character.HumanoidRootPart
for i , v in pairs (workspace:GetDescendants()) do
  local obj = v
  if string.find(obj.Name, "Chest2") then
      hrp.CFrame = obj.CFrame + Vector3.new(0,20,0)
      wait(0.5)
  end
end
end)
Section:Toggle("Chest3", false, function(v)
    local hrp = game.Players.LocalPlayer.Character.HumanoidRootPart
for i , v in pairs (workspace:GetDescendants()) do
  local obj = v
  if string.find(obj.Name, "Chest3") then
      hrp.CFrame = obj.CFrame + Vector3.new(0,15,0)
      wait(0.5)
  end
end
end)
--DevillFruit--
local Tab = Library:Tab("DevillFruit")
local Section = Tab:Section("DevillFruit")
Section:Toggle("AutoRandomDF", false, function(v)
    loadstring(game:HttpGet("https://pastebin.com/raw/TjJ8PTjr"))()
end)
Section:Toggle("TeleportDF", false, function(v)
    local h = game.Players.LocalPlayer.Character.HumanoidRootPart
 
for i, v in pairs(workspace:GetChildren()) do
    if v:IsA("Tool")  then
        if v.Fruit then
              h.CFrame = v.Fruit.CFrame + Vector3.new(0,4,0)
              wait(0.5)
        end
    end
    if v:IsA("Model") and v.Name == "Fruit " then
      if v.Fruit then
              h.CFrame = v.Fruit.CFrame + Vector3.new(0,4,0)
              wait(0.5)
        end
    end
end
end)
--DunGeon--
local Tab = Library:Tab("Dungeon")
local Section = Tab:Section("WaitToUpdate")
--Misc--
local Tab = Library:Tab("Misc")
local Section = Tab:Section("PlayerBoost")
Section:Toggle("AutoClick", true, function(v)
    local on
local keybind=Enum.KeyCode.F5
local keybindEnd=Enum.KeyCode.F6
local UserInputService=game:GetService("UserInputService")
local RunService=game:GetService("RunService")
local plr=game:GetService("Players").LocalPlayer
local mouse=plr:GetMouse()

local sg=Instance.new("ScreenGui",plr.PlayerGui)
local f=Instance.new("TextLabel",sg)
f.Size=UDim2.new(0,25,0,10)
f.BackgroundColor3=Color3.fromRGB(180,50,50)
f.Visible=false
f.Text="On"
f.TextSize=11

local vu = game:GetService("VirtualUser")
local function CC()
vu:CaptureController();
end 
local function CB()
local v2 = Vector2.new();
vu:ClickButton1(v2);
end

function Start(a,b)
   if a.KeyCode==keybind then
       on=true
       a=RunService.Stepped:Connect(function()
           if on then
               CC();
               CB();
               f.Visible=true
               f.Position=UDim2.new(0,mouse.X-12.5,0,mouse.Y-15)
           else
               a:Disconnect()
           end
       end)
       f.Visible=false
   end
end

function Stop(a,b)
   if a.KeyCode==keybindEnd then
       on=false
       f.Visible=false
   end
end

UserInputService.InputBegan:connect(Start)
UserInputService.InputEnded:connect(Stop)
end)
local Section = Tab:Section("Craracter")
Section:Toggle("WalkSpeed100", false, function(v)
    _G.HackedWalkSpeed = 100
 
local Plrs = game:GetService("Players")
 
local MyPlr = Plrs.LocalPlayer
local MyChar = MyPlr.Character
 
if MyChar then
local Hum = MyChar.Humanoid
Hum.Changed:connect(function()
Hum.WalkSpeed = _G.HackedWalkSpeed
end)
Hum.WalkSpeed = _G.HackedWalkSpeed
end
 
 
MyPlr.CharacterAdded:connect(function(Char)
MyChar = Char
repeat wait() until Char:FindFirstChild("Humanoid")
local Hum = Char.Humanoid
Hum.Changed:connect(function()
Hum.WalkSpeed = _G.HackedWalkSpeed
end)
Hum.WalkSpeed = _G.HackedWalkSpeed
end)
end)
Section:Toggle("WalkSpeed200", false, function(v)
    _G.HackedWalkSpeed = 200
 
local Plrs = game:GetService("Players")
 
local MyPlr = Plrs.LocalPlayer
local MyChar = MyPlr.Character
 
if MyChar then
local Hum = MyChar.Humanoid
Hum.Changed:connect(function()
Hum.WalkSpeed = _G.HackedWalkSpeed
end)
Hum.WalkSpeed = _G.HackedWalkSpeed
end
 
 
MyPlr.CharacterAdded:connect(function(Char)
MyChar = Char
repeat wait() until Char:FindFirstChild("Humanoid")
local Hum = Char.Humanoid
Hum.Changed:connect(function()
Hum.WalkSpeed = _G.HackedWalkSpeed
end)
Hum.WalkSpeed = _G.HackedWalkSpeed
end)
end)
Section:Toggle("WlakSpeed300", false, function(v)
    _G.HackedWalkSpeed = 300
 
local Plrs = game:GetService("Players")
 
local MyPlr = Plrs.LocalPlayer
local MyChar = MyPlr.Character
 
if MyChar then
local Hum = MyChar.Humanoid
Hum.Changed:connect(function()
Hum.WalkSpeed = _G.HackedWalkSpeed
end)
Hum.WalkSpeed = _G.HackedWalkSpeed
end
 
 
MyPlr.CharacterAdded:connect(function(Char)
MyChar = Char
repeat wait() until Char:FindFirstChild("Humanoid")
local Hum = Char.Humanoid
Hum.Changed:connect(function()
Hum.WalkSpeed = _G.HackedWalkSpeed
end)
Hum.WalkSpeed = _G.HackedWalkSpeed
end)
end)
Section:Toggle("WalkSpeedReset", false, function(v)
    _G.HackedWalkSpeed = 36
 
local Plrs = game:GetService("Players")
 
local MyPlr = Plrs.LocalPlayer
local MyChar = MyPlr.Character
 
if MyChar then
local Hum = MyChar.Humanoid
Hum.Changed:connect(function()
Hum.WalkSpeed = _G.HackedWalkSpeed
end)
Hum.WalkSpeed = _G.HackedWalkSpeed
end
 
 
MyPlr.CharacterAdded:connect(function(Char)
MyChar = Char
repeat wait() until Char:FindFirstChild("Humanoid")
local Hum = Char.Humanoid
Hum.Changed:connect(function()
Hum.WalkSpeed = _G.HackedWalkSpeed
end)
Hum.WalkSpeed = _G.HackedWalkSpeed
end)
end)
Section:Toggle("JumpPower100", false, function(v)
    local jump = 100 -- Add the amount of jump power you want here!
 
spawn(function()
while wait() do
game.Players.LocalPlayer.Character.Humanoid.JumpPower = jump
end
end)
end)
Section:Toggle("JumpPower200", false, function(v)
    local jump = 200 -- Add the amount of jump power you want here!
 
spawn(function()
while wait() do
game.Players.LocalPlayer.Character.Humanoid.JumpPower = jump
end
end)
end)
Section:Toggle("JumpPower300", false, function(v)
    local jump = 300 -- Add the amount of jump power you want here!
 
spawn(function()
while wait() do
game.Players.LocalPlayer.Character.Humanoid.JumpPower = jump
end
end)
end)
Section:Toggle("JumpPowerReset", false, function(v)
    local jump = 50 -- Add the amount of jump power you want here!
 
spawn(function()
while wait() do
game.Players.LocalPlayer.Character.Humanoid.JumpPower = jump
end
end)
end)
Section:Toggle("NoClip", false, function(state)
    getgenv().Noclip = state
end)
local Section = Tab:Section("CharacterMisc")
Section:Toggle("Invisble", false, function(v)
    for i,v in pairs(game:GetService("Players").LocalPlayer.Character:GetChildren()) do
	if v:IsA("Shirt") or v:IsA("Pants") or v:IsA("Hat") then
		v:Destroy()
	end
	if v:IsA("Part") or v:IsA("MeshPart") then
		v.Transparency = 1
		if v.Name == "Head" then
			if v:FindFirstChild("face") then
				v.face:Destroy()
			end
		end
	end
end
end)
Section:Toggle("Fly", false, function(v)
    repeat wait() 
	until game.Players.LocalPlayer and game.Players.LocalPlayer.Character and game.Players.LocalPlayer.Character:findFirstChild("HumanoidRootPart") and game.Players.LocalPlayer.Character:findFirstChild("Humanoid") 
local mouse = game.Players.LocalPlayer:GetMouse() 
repeat wait() until mouse
local plr = game.Players.LocalPlayer 
local torso = plr.Character.HumanoidRootPart 
local flying = true
local deb = true 
local ctrl = {f = 0, b = 0, l = 0, r = 0} 
local lastctrl = {f = 0, b = 0, l = 0, r = 0} 
local maxspeed = 5000
local speed = 50
 
function Fly() 
local bg = Instance.new("BodyGyro", torso) 
bg.P = 9e4 
bg.maxTorque = Vector3.new(9e9, 9e9, 9e9) 
bg.cframe = torso.CFrame 
local bv = Instance.new("BodyVelocity", torso) 
bv.velocity = Vector3.new(0,0.1,0) 
bv.maxForce = Vector3.new(9e9, 9e9, 9e9) 
repeat wait() 
plr.Character.Humanoid.PlatformStand = true 
if ctrl.l + ctrl.r ~= 0 or ctrl.f + ctrl.b ~= 0 then 
speed = speed+.100+(speed/maxspeed) 
if speed > maxspeed then 
speed = maxspeed 
end 
elseif not (ctrl.l + ctrl.r ~= 0 or ctrl.f + ctrl.b ~= 0) and speed ~= 0 then 
speed = speed-1 
if speed < 5 then 
speed = 5 
end 
end 
if (ctrl.l + ctrl.r) ~= 0 or (ctrl.f + ctrl.b) ~= 0 then 
bv.velocity = ((game.Workspace.CurrentCamera.CoordinateFrame.lookVector * (ctrl.f+ctrl.b)) + ((game.Workspace.CurrentCamera.CoordinateFrame * CFrame.new(ctrl.l+ctrl.r,(ctrl.f+ctrl.b)*.2,0).p) - game.Workspace.CurrentCamera.CoordinateFrame.p))*speed 
lastctrl = {f = ctrl.f, b = ctrl.b, l = ctrl.l, r = ctrl.r} 
elseif (ctrl.l + ctrl.r) == 0 and (ctrl.f + ctrl.b) == 0 and speed ~= 0 then 
bv.velocity = ((game.Workspace.CurrentCamera.CoordinateFrame.lookVector * (lastctrl.f+lastctrl.b)) + ((game.Workspace.CurrentCamera.CoordinateFrame * CFrame.new(lastctrl.l+lastctrl.r,(lastctrl.f+lastctrl.b)*.2,0).p) - game.Workspace.CurrentCamera.CoordinateFrame.p))*speed 
else 
bv.velocity = Vector3.new(0,0.1,0) 
end 
bg.cframe = game.Workspace.CurrentCamera.CoordinateFrame * CFrame.Angles(-math.rad((ctrl.f+ctrl.b)*50*speed/maxspeed),0,0) 
until not flying 
ctrl = {f = 0, b = 0, l = 0, r = 0} 
lastctrl = {f = 0, b = 0, l = 0, r = 0} 
speed = 0 
bg:Destroy() 
bv:Destroy() 
plr.Character.Humanoid.PlatformStand = false 
end 
mouse.KeyDown:connect(function(key) 
if key:lower() == "e" then 
if flying then flying = false 
else 
flying = true 
Fly() 
end 
elseif key:lower() == "w" then 
ctrl.f = 1 
elseif key:lower() == "s" then 
ctrl.b = -1 
elseif key:lower() == "a" then 
ctrl.l = -1 
elseif key:lower() == "d" then 
ctrl.r = 1 
end 
end) 
mouse.KeyUp:connect(function(key) 
if key:lower() == "w" then 
ctrl.f = 0 
elseif key:lower() == "s" then 
ctrl.b = 0 
elseif key:lower() == "a" then 
ctrl.l = 0 
elseif key:lower() == "d" then 
ctrl.r = 0 
end 
end)
Fly()
end)
Section:Toggle("FlySpeed100", false, function(v)
    repeat wait() 
	until game.Players.LocalPlayer and game.Players.LocalPlayer.Character and game.Players.LocalPlayer.Character:findFirstChild("HumanoidRootPart") and game.Players.LocalPlayer.Character:findFirstChild("Humanoid") 
local mouse = game.Players.LocalPlayer:GetMouse() 
repeat wait() until mouse
local plr = game.Players.LocalPlayer 
local torso = plr.Character.HumanoidRootPart 
local flying = true
local deb = true 
local ctrl = {f = 0, b = 0, l = 0, r = 0} 
local lastctrl = {f = 0, b = 0, l = 0, r = 0} 
local maxspeed = 5000
local speed = 100
 
function Fly() 
local bg = Instance.new("BodyGyro", torso) 
bg.P = 9e4 
bg.maxTorque = Vector3.new(9e9, 9e9, 9e9) 
bg.cframe = torso.CFrame 
local bv = Instance.new("BodyVelocity", torso) 
bv.velocity = Vector3.new(0,0.1,0) 
bv.maxForce = Vector3.new(9e9, 9e9, 9e9) 
repeat wait() 
plr.Character.Humanoid.PlatformStand = true 
if ctrl.l + ctrl.r ~= 0 or ctrl.f + ctrl.b ~= 0 then 
speed = speed+.100+(speed/maxspeed) 
if speed > maxspeed then 
speed = maxspeed 
end 
elseif not (ctrl.l + ctrl.r ~= 0 or ctrl.f + ctrl.b ~= 0) and speed ~= 0 then 
speed = speed-1 
if speed < 5 then 
speed = 5 
end 
end 
if (ctrl.l + ctrl.r) ~= 0 or (ctrl.f + ctrl.b) ~= 0 then 
bv.velocity = ((game.Workspace.CurrentCamera.CoordinateFrame.lookVector * (ctrl.f+ctrl.b)) + ((game.Workspace.CurrentCamera.CoordinateFrame * CFrame.new(ctrl.l+ctrl.r,(ctrl.f+ctrl.b)*.2,0).p) - game.Workspace.CurrentCamera.CoordinateFrame.p))*speed 
lastctrl = {f = ctrl.f, b = ctrl.b, l = ctrl.l, r = ctrl.r} 
elseif (ctrl.l + ctrl.r) == 0 and (ctrl.f + ctrl.b) == 0 and speed ~= 0 then 
bv.velocity = ((game.Workspace.CurrentCamera.CoordinateFrame.lookVector * (lastctrl.f+lastctrl.b)) + ((game.Workspace.CurrentCamera.CoordinateFrame * CFrame.new(lastctrl.l+lastctrl.r,(lastctrl.f+lastctrl.b)*.2,0).p) - game.Workspace.CurrentCamera.CoordinateFrame.p))*speed 
else 
bv.velocity = Vector3.new(0,0.1,0) 
end 
bg.cframe = game.Workspace.CurrentCamera.CoordinateFrame * CFrame.Angles(-math.rad((ctrl.f+ctrl.b)*50*speed/maxspeed),0,0) 
until not flying 
ctrl = {f = 0, b = 0, l = 0, r = 0} 
lastctrl = {f = 0, b = 0, l = 0, r = 0} 
speed = 0 
bg:Destroy() 
bv:Destroy() 
plr.Character.Humanoid.PlatformStand = false 
end 
mouse.KeyDown:connect(function(key) 
if key:lower() == "e" then 
if flying then flying = false 
else 
flying = true 
Fly() 
end 
elseif key:lower() == "w" then 
ctrl.f = 1 
elseif key:lower() == "s" then 
ctrl.b = -1 
elseif key:lower() == "a" then 
ctrl.l = -1 
elseif key:lower() == "d" then 
ctrl.r = 1 
end 
end) 
mouse.KeyUp:connect(function(key) 
if key:lower() == "w" then 
ctrl.f = 0 
elseif key:lower() == "s" then 
ctrl.b = 0 
elseif key:lower() == "a" then 
ctrl.l = 0 
elseif key:lower() == "d" then 
ctrl.r = 0 
end 
end)
Fly()
end)
Section:Toggle("FlySpeed200", false, function(v)
    repeat wait() 
	until game.Players.LocalPlayer and game.Players.LocalPlayer.Character and game.Players.LocalPlayer.Character:findFirstChild("HumanoidRootPart") and game.Players.LocalPlayer.Character:findFirstChild("Humanoid") 
local mouse = game.Players.LocalPlayer:GetMouse() 
repeat wait() until mouse
local plr = game.Players.LocalPlayer 
local torso = plr.Character.HumanoidRootPart 
local flying = true
local deb = true 
local ctrl = {f = 0, b = 0, l = 0, r = 0} 
local lastctrl = {f = 0, b = 0, l = 0, r = 0} 
local maxspeed = 5000
local speed = 200
 
function Fly() 
local bg = Instance.new("BodyGyro", torso) 
bg.P = 9e4 
bg.maxTorque = Vector3.new(9e9, 9e9, 9e9) 
bg.cframe = torso.CFrame 
local bv = Instance.new("BodyVelocity", torso) 
bv.velocity = Vector3.new(0,0.1,0) 
bv.maxForce = Vector3.new(9e9, 9e9, 9e9) 
repeat wait() 
plr.Character.Humanoid.PlatformStand = true 
if ctrl.l + ctrl.r ~= 0 or ctrl.f + ctrl.b ~= 0 then 
speed = speed+.100+(speed/maxspeed) 
if speed > maxspeed then 
speed = maxspeed 
end 
elseif not (ctrl.l + ctrl.r ~= 0 or ctrl.f + ctrl.b ~= 0) and speed ~= 0 then 
speed = speed-1 
if speed < 5 then 
speed = 5 
end 
end 
if (ctrl.l + ctrl.r) ~= 0 or (ctrl.f + ctrl.b) ~= 0 then 
bv.velocity = ((game.Workspace.CurrentCamera.CoordinateFrame.lookVector * (ctrl.f+ctrl.b)) + ((game.Workspace.CurrentCamera.CoordinateFrame * CFrame.new(ctrl.l+ctrl.r,(ctrl.f+ctrl.b)*.2,0).p) - game.Workspace.CurrentCamera.CoordinateFrame.p))*speed 
lastctrl = {f = ctrl.f, b = ctrl.b, l = ctrl.l, r = ctrl.r} 
elseif (ctrl.l + ctrl.r) == 0 and (ctrl.f + ctrl.b) == 0 and speed ~= 0 then 
bv.velocity = ((game.Workspace.CurrentCamera.CoordinateFrame.lookVector * (lastctrl.f+lastctrl.b)) + ((game.Workspace.CurrentCamera.CoordinateFrame * CFrame.new(lastctrl.l+lastctrl.r,(lastctrl.f+lastctrl.b)*.2,0).p) - game.Workspace.CurrentCamera.CoordinateFrame.p))*speed 
else 
bv.velocity = Vector3.new(0,0.1,0) 
end 
bg.cframe = game.Workspace.CurrentCamera.CoordinateFrame * CFrame.Angles(-math.rad((ctrl.f+ctrl.b)*50*speed/maxspeed),0,0) 
until not flying 
ctrl = {f = 0, b = 0, l = 0, r = 0} 
lastctrl = {f = 0, b = 0, l = 0, r = 0} 
speed = 0 
bg:Destroy() 
bv:Destroy() 
plr.Character.Humanoid.PlatformStand = false 
end 
mouse.KeyDown:connect(function(key) 
if key:lower() == "e" then 
if flying then flying = false 
else 
flying = true 
Fly() 
end 
elseif key:lower() == "w" then 
ctrl.f = 1 
elseif key:lower() == "s" then 
ctrl.b = -1 
elseif key:lower() == "a" then 
ctrl.l = -1 
elseif key:lower() == "d" then 
ctrl.r = 1 
end 
end) 
mouse.KeyUp:connect(function(key) 
if key:lower() == "w" then 
ctrl.f = 0 
elseif key:lower() == "s" then 
ctrl.b = 0 
elseif key:lower() == "a" then 
ctrl.l = 0 
elseif key:lower() == "d" then 
ctrl.r = 0 
end 
end)
Fly()
end)
Section:Toggle("FlySpeed300", false, function(v)
    repeat wait() 
	until game.Players.LocalPlayer and game.Players.LocalPlayer.Character and game.Players.LocalPlayer.Character:findFirstChild("HumanoidRootPart") and game.Players.LocalPlayer.Character:findFirstChild("Humanoid") 
local mouse = game.Players.LocalPlayer:GetMouse() 
repeat wait() until mouse
local plr = game.Players.LocalPlayer 
local torso = plr.Character.HumanoidRootPart 
local flying = true
local deb = true 
local ctrl = {f = 0, b = 0, l = 0, r = 0} 
local lastctrl = {f = 0, b = 0, l = 0, r = 0} 
local maxspeed = 5000
local speed = 300
 
function Fly() 
local bg = Instance.new("BodyGyro", torso) 
bg.P = 9e4 
bg.maxTorque = Vector3.new(9e9, 9e9, 9e9) 
bg.cframe = torso.CFrame 
local bv = Instance.new("BodyVelocity", torso) 
bv.velocity = Vector3.new(0,0.1,0) 
bv.maxForce = Vector3.new(9e9, 9e9, 9e9) 
repeat wait() 
plr.Character.Humanoid.PlatformStand = true 
if ctrl.l + ctrl.r ~= 0 or ctrl.f + ctrl.b ~= 0 then 
speed = speed+.100+(speed/maxspeed) 
if speed > maxspeed then 
speed = maxspeed 
end 
elseif not (ctrl.l + ctrl.r ~= 0 or ctrl.f + ctrl.b ~= 0) and speed ~= 0 then 
speed = speed-1 
if speed < 5 then 
speed = 5 
end 
end 
if (ctrl.l + ctrl.r) ~= 0 or (ctrl.f + ctrl.b) ~= 0 then 
bv.velocity = ((game.Workspace.CurrentCamera.CoordinateFrame.lookVector * (ctrl.f+ctrl.b)) + ((game.Workspace.CurrentCamera.CoordinateFrame * CFrame.new(ctrl.l+ctrl.r,(ctrl.f+ctrl.b)*.2,0).p) - game.Workspace.CurrentCamera.CoordinateFrame.p))*speed 
lastctrl = {f = ctrl.f, b = ctrl.b, l = ctrl.l, r = ctrl.r} 
elseif (ctrl.l + ctrl.r) == 0 and (ctrl.f + ctrl.b) == 0 and speed ~= 0 then 
bv.velocity = ((game.Workspace.CurrentCamera.CoordinateFrame.lookVector * (lastctrl.f+lastctrl.b)) + ((game.Workspace.CurrentCamera.CoordinateFrame * CFrame.new(lastctrl.l+lastctrl.r,(lastctrl.f+lastctrl.b)*.2,0).p) - game.Workspace.CurrentCamera.CoordinateFrame.p))*speed 
else 
bv.velocity = Vector3.new(0,0.1,0) 
end 
bg.cframe = game.Workspace.CurrentCamera.CoordinateFrame * CFrame.Angles(-math.rad((ctrl.f+ctrl.b)*50*speed/maxspeed),0,0) 
until not flying 
ctrl = {f = 0, b = 0, l = 0, r = 0} 
lastctrl = {f = 0, b = 0, l = 0, r = 0} 
speed = 0 
bg:Destroy() 
bv:Destroy() 
plr.Character.Humanoid.PlatformStand = false 
end 
mouse.KeyDown:connect(function(key) 
if key:lower() == "e" then 
if flying then flying = false 
else 
flying = true 
Fly() 
end 
elseif key:lower() == "w" then 
ctrl.f = 1 
elseif key:lower() == "s" then 
ctrl.b = -1 
elseif key:lower() == "a" then 
ctrl.l = -1 
elseif key:lower() == "d" then 
ctrl.r = 1 
end 
end) 
mouse.KeyUp:connect(function(key) 
if key:lower() == "w" then 
ctrl.f = 0 
elseif key:lower() == "s" then 
ctrl.b = 0 
elseif key:lower() == "a" then 
ctrl.l = 0 
elseif key:lower() == "d" then 
ctrl.r = 0 
end 
end)
Fly()
end)
local Section = Tab:Section("Server")
Section:Toggle("ServerHop", false, function(v)
    local PlaceID = 2753915549
          local AllIDs = {}
          local foundAnything = ""
          local actualHour = os.date("!*t").hour
          local Deleted = false
          --[[
          local File = pcall(function()
              AllIDs = game:GetService('HttpService'):JSONDecode(readfile("NotSameServers.json"))
          end)
          if not File then
              table.insert(AllIDs, actualHour)
              writefile("NotSameServers.json", game:GetService('HttpService'):JSONEncode(AllIDs))
          end
          ]]
          function TPReturner()
              local Site;
              if foundAnything == "" then
                  Site = game.HttpService:JSONDecode(game:HttpGet('https://games.roblox.com/v1/games/' .. PlaceID .. '/servers/Public?sortOrder=Asc&limit=100'))
              else
                  Site = game.HttpService:JSONDecode(game:HttpGet('https://games.roblox.com/v1/games/' .. PlaceID .. '/servers/Public?sortOrder=Asc&limit=100&cursor=' .. foundAnything))
              end
              local ID = ""
              if Site.nextPageCursor and Site.nextPageCursor ~= "null" and Site.nextPageCursor ~= nil then
                  foundAnything = Site.nextPageCursor
              end
              local num = 0;
              for i,v in pairs(Site.data) do
                  local Possible = true
                  ID = tostring(v.id)
                  if tonumber(v.maxPlayers) > tonumber(v.playing) then
                      for _,Existing in pairs(AllIDs) do
                          if num ~= 0 then
                              if ID == tostring(Existing) then
                                  Possible = false
                              end
                          else
                              if tonumber(actualHour) ~= tonumber(Existing) then
                                  local delFile = pcall(function()
                                      -- delfile("NotSameServers.json")
                                      AllIDs = {}
                                      table.insert(AllIDs, actualHour)
                                  end)
                              end
                          end
                          num = num + 1
                      end
                      if Possible == true then
                          table.insert(AllIDs, ID)
                          wait()
                          pcall(function()
                              -- writefile("NotSameServers.json", game:GetService('HttpService'):JSONEncode(AllIDs))
                              wait()
                              game:GetService("TeleportService"):TeleportToPlaceInstance(PlaceID, ID, game.Players.LocalPlayer)
                          end)
                          wait(4)
                      end
                  end
              end
          end

          function Teleport()
              while wait() do
                  pcall(function()
                      TPReturner()
                      if foundAnything ~= "" then
                          TPReturner()
                      end
                  end)
              end
          end

          Teleport()
end)
Section:Toggle("FpsBoost", false, function(v)
    for _,v in pairs(workspace:GetDescendants()) do
if v.ClassName == "Part"
or v.ClassName == "SpawnLocation"
or v.ClassName == "WedgePart"
or v.ClassName == "Terrain"
or v.ClassName == "MeshPart" then
v.Material = "Plastic"
end
end
end)
Section:Toggle("RejoinServer", false, function(v)
     wait(1) game:GetService("TeleportService"):Teleport(2753915549, LocalPlayer)
end)
Section:Toggle("ServerCrash", false, function(v)
    print("please wait while we attempt to crash the game")
for i=1, 68 do
  spawn(function()
      while true do
          game:service("RunService").RenderStepped:wait()
         for i=1, 64 do
                  game:service("Players"):Chat("/e i love roblox")
                  game:service("Players"):Chat("/e i love roblox")
                  game:service("Players"):Chat("/e i love roblox")
                  game:service("Players"):Chat("/e i love roblox")
                  game:service("Players"):Chat("/e i love roblox")
                  game:service("Players"):Chat("/e i love roblox")
                  game:service("Players"):Chat("/e i love roblox")
                  end
          end
  print("done?")
      end)
  end
end)
Section:Toggle("AntiAFK", false, function(v)
    wait(0.5)local ba=Instance.new("ScreenGui")
local ca=Instance.new("TextLabel")local da=Instance.new("Frame")
local _b=Instance.new("TextLabel")local ab=Instance.new("TextLabel")ba.Parent=game.CoreGui
ba.ZIndexBehavior=Enum.ZIndexBehavior.Sibling;ca.Parent=ba;ca.Active=true
ca.BackgroundColor3=Color3.new(0.176471,0.176471,0.176471)ca.Draggable=true
ca.Position=UDim2.new(0.698610067,0,0.098096624,0)ca.Size=UDim2.new(0,304,0,52)
ca.Font=Enum.Font.SourceSansSemibold;ca.Text="Anti Afk Kick Script"ca.TextColor3=Color3.new(0,1,1)
ca.TextSize=22;da.Parent=ca
da.BackgroundColor3=Color3.new(0.196078,0.196078,0.196078)da.Position=UDim2.new(0,0,1.0192306,0)
da.Size=UDim2.new(0,304,0,107)_b.Parent=da
_b.BackgroundColor3=Color3.new(0.176471,0.176471,0.176471)_b.Position=UDim2.new(0,0,0.800455689,0)
_b.Size=UDim2.new(0,304,0,21)_b.Font=Enum.Font.Arial;_b.Text="Made by XxSwordmaster_2xX"
_b.TextColor3=Color3.new(1,1,1)_b.TextSize=20;ab.Parent=da
ab.BackgroundColor3=Color3.new(0.176471,0.176471,0.176471)ab.Position=UDim2.new(0,0,0.158377379,0)
ab.Size=UDim2.new(0,304,0,44)ab.Font=Enum.Font.ArialBold;ab.Text="Status: Script Started"
ab.TextColor3=Color3.new(1,1,1)ab.TextSize=20;local bb=game:service'VirtualUser'
game:service'Players'.LocalPlayer.Idled:connect(function()
bb:CaptureController()bb:ClickButton2(Vector2.new())
ab.Text="You went idle and ROBLOX tried to kick you but we reflected it!"wait(2)ab.Text="Script Re-Enabled"end)
end)
local Tab = Library:Tab("Setting")
local Section = Tab:Section("Setting")
Section:Keybind("KEYBIND NAME", "E", function()
    
end)
Section:Toggle("Open-New-Script", false, function(v)
    loadstring(game:HttpGet("https://pastebin.com/raw/L6XVEXLS"))()
end)
local Section = Tab:Section("AutofarmSetting")
Section:Toggle("AutoSkill:C", false, function(state)
    getgenv().SkillC = state
end)
Section:Toggle("AutoSkill:Z", false, function(state)
    getgenv().SkillZ = state
end)
Section:Toggle("AutoSkill:X", false, function(state)
    getgenv().SkillX = state
end)
Section:Toggle("AutoSkill:F", false, function(state)
    getgenv().SkillF = state
end)

if getgenv().AutoFarm or getgenv().Noclip then
        pcall(function()
            plr.Character.Humanoid:ChangeState(11)
	    local useTool = game.Players.LocalPlayer.Backpack[getgenv().CurrentWeapon]
            plr.Character.Humanoid:EquipTool(useTool)
        end)
    end
