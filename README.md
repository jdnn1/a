-- By jd_nn1
-- Version: 3.2

-- Instances:

local ScreenGui = Instance.new("ScreenGui")
local Frame = Instance.new("Frame")
local ImageLabel = Instance.new("ImageLabel")
local TextLabel = Instance.new("TextLabel")
local infy = Instance.new("TextButton")
local TextLabel_2 = Instance.new("TextLabel")
local funk = Instance.new("TextButton")
local mm2 = Instance.new("TextButton")
local Bypassc = Instance.new("TextButton")
local Rag = Instance.new("TextButton")
local rob = Instance.new("TextButton")
local TOH = Instance.new("TextButton")
local Arsenaal = Instance.new("TextButton")

--Properties:

ScreenGui.Parent = game.Players.LocalPlayer:WaitForChild("PlayerGui")
ScreenGui.ZIndexBehavior = Enum.ZIndexBehavior.Sibling

Frame.Parent = ScreenGui
Frame.BackgroundColor3 = Color3.fromRGB(255, 255, 255)
Frame.Position = UDim2.new(0.0515723228, 0, 0.123339668, 0)
Frame.Size = UDim2.new(0, 168, 0, 283)
Frame.Active = true
Frame.Draggable = true

ImageLabel.Parent = Frame
ImageLabel.BackgroundColor3 = Color3.fromRGB(255, 255, 255)
ImageLabel.Position = UDim2.new(-0.00199910253, 0, -0.000335253775, 0)
ImageLabel.Size = UDim2.new(0, 168, 0, 283)
ImageLabel.Image = "rbxassetid://6803422754"

TextLabel.Parent = ImageLabel
TextLabel.BackgroundColor3 = Color3.fromRGB(255, 255, 255)
TextLabel.BackgroundTransparency = 1.000
TextLabel.Position = UDim2.new(0.684523821, 0, 0, 0)
TextLabel.Size = UDim2.new(0, 53, 0, 13)
TextLabel.Font = Enum.Font.PermanentMarker
TextLabel.Text = "jn'#8397"
TextLabel.TextColor3 = Color3.fromRGB(0, 0, 0)
TextLabel.TextSize = 14.000

infy.Name = "infy"
infy.Parent = ImageLabel
infy.BackgroundColor3 = Color3.fromRGB(255, 255, 255)
infy.BackgroundTransparency = 1.000
infy.Position = UDim2.new(0.130952388, 0, 0.0848056525, 0)
infy.Size = UDim2.new(0, 139, 0, 34)
infy.Font = Enum.Font.PermanentMarker
infy.Text = "InfYyield 📃"
infy.TextColor3 = Color3.fromRGB(0, 0, 0)
infy.TextSize = 14.000
infy.MouseButton1Down:connect(function()
	loadstring(game:HttpGet(('https://raw.githubusercontent.com/EdgeIY/infiniteyield/master/source'),true))()
end)

TextLabel_2.Parent = ImageLabel
TextLabel_2.BackgroundColor3 = Color3.fromRGB(255, 255, 255)
TextLabel_2.BackgroundTransparency = 1.000
TextLabel_2.Position = UDim2.new(0.130952373, 0, 0, 0)
TextLabel_2.Size = UDim2.new(0, 93, 0, 24)
TextLabel_2.Font = Enum.Font.PermanentMarker
TextLabel_2.Text = "Papes Hub 📃✔"
TextLabel_2.TextColor3 = Color3.fromRGB(0, 0, 0)
TextLabel_2.TextSize = 14.000

funk.Name = "funk"
funk.Parent = ImageLabel
funk.BackgroundColor3 = Color3.fromRGB(255, 255, 255)
funk.BackgroundTransparency = 1.000
funk.Position = UDim2.new(0.130952388, 0, 0.204946995, 0)
funk.Size = UDim2.new(0, 139, 0, 34)
funk.Font = Enum.Font.PermanentMarker
funk.Text = "Funky Friday 🎤"
funk.TextColor3 = Color3.fromRGB(0, 0, 0)
funk.TextSize = 14.000
funk.MouseButton1Down:connect(function()
	local framework;
	local funcs = {}

	local islclosure = islclosure or is_l_closure
	local getinfo = getinfo or debug.getinfo
	local getupvalues = getupvalues or debug.getupvalues
	local getconstants = getconstants or debug.getconstants

	for i, v in next, getgc(true) do
		if type(v) == 'table' and rawget(v, 'GameUI') then
			framework = v;
		end

		if type(v) == 'function' and islclosure(v) then
			local info = getinfo(v);
			if info.name == '' then continue end

			if info.source:match('%.Arrows$') then
				local constants = getconstants(v);
				if table.find(constants, 'Right') and table.find(constants, 'NewThread') then
					funcs.KeyDown = v;
				elseif table.find(constants, 'Multiplier') and table.find(constants, 'MuteVoices') then
					funcs.KeyUp = v;
				end
			end
		end

		if framework and funcs.KeyUp and funcs.KeyDown then break end
	end

	if type(framework) ~= 'table' or (not rawget(framework, 'UI')) then
		return game.Players.LocalPlayer:Kick('Failed to locate framework.')
	elseif (not (funcs.KeyDown and funcs.KeyUp)) then
		return game.Players.LocalPlayer:Kick('Failed to locate key functions.')
	end


	local marked = {}
	local map = { [0] = 'Left', [1] = 'Down', [2] = 'Up', [3] = 'Right', }
	local keys = { Up = Enum.KeyCode.W; Down = Enum.KeyCode.S; Left = Enum.KeyCode.A; Right = Enum.KeyCode.D; }

	-- https://eryn.io/gist/3db84579866c099cdd5bb2ff37947cec
	-- bla bla spawn and wait are bad 
	-- can also use bindables for the fastspawn idc

	local runService = game:GetService('RunService')

	local fastWait, fastSpawn do
		function fastWait(t)
			local d = 0;
			while d < t do
				d += runService.RenderStepped:wait()
			end
		end

		function fastSpawn(f)
			coroutine.wrap(f)()
		end
	end

	while runService.RenderStepped:wait() do
		for _, arrow in next, framework.UI.ActiveSections do
			if arrow.Side ~= framework.UI.CurrentSide then continue end -- ignore the opponent's arrows
			if marked[arrow] then continue end -- ignore marked arrows so we dont spam them

			local index = arrow.Data.Position % 4
			local position = map[index] -- % 4 because the right side numbers are 4, 5, 6, 7 and are not in the key map
			if (not position) then continue end -- oh well the position got eaten

			local distance = (1 - math.abs(arrow.Data.Time - framework.SongPlayer.CurrentlyPlaying.TimePosition)) * 100 -- get the "distance" or whatever
			if distance >= 95 then -- if above a certain threshold, we do this
				marked[arrow] = true; -- mark the arrow
				fastSpawn(function()
					funcs.KeyDown(position)
					if arrow.Data.Length > 0 then
						fastWait(arrow.Data.Length) -- usually these are held long enough
					else
						fastWait(0.02) -- wait a tiny bit of time so the fucking animations play and you dont get called out as bad :)
					end
					funcs.KeyUp(position)
					marked[arrow] = nil
				end)
			end
		end
	end
end)



mm2.Name = "mm2"
mm2.Parent = ImageLabel
mm2.BackgroundColor3 = Color3.fromRGB(255, 255, 255)
mm2.BackgroundTransparency = 1.000
mm2.Position = UDim2.new(0.130952388, 0, 0.325088322, 0)
mm2.Size = UDim2.new(0, 139, 0, 34)
mm2.Font = Enum.Font.PermanentMarker
mm2.Text = "MM2 🔪"
mm2.TextColor3 = Color3.fromRGB(0, 0, 0)
mm2.TextSize = 14.000
mm2.MouseButton1Down:connect(function()
	loadstring(game:GetObjects("rbxassetid://4001118261")[1].Source)()
end)

Bypassc.Name = "Bypassc"
Bypassc.Parent = ImageLabel
Bypassc.BackgroundColor3 = Color3.fromRGB(255, 255, 255)
Bypassc.BackgroundTransparency = 1.000
Bypassc.Position = UDim2.new(0.130952388, 0, 0.890459239, 0)
Bypassc.Size = UDim2.new(0, 139, 0, 34)
Bypassc.Font = Enum.Font.PermanentMarker
Bypassc.Text = "Chat Bypass🔞 (13+)"
Bypassc.TextColor3 = Color3.fromRGB(0, 0, 0)
Bypassc.TextSize = 14.000
Bypassc.MouseButton1Down:connect(function()

	loadstring(game:HttpGet('https://raw.githubusercontent.com/bedra45/chetbypasser/main/chetbypass'))()

end)


Rag.Name = "Rag"
Rag.Parent = ImageLabel
Rag.BackgroundColor3 = Color3.fromRGB(255, 255, 255)
Rag.BackgroundTransparency = 1.000
Rag.Position = UDim2.new(0.130952388, 0, 0.438162535, 0)
Rag.Size = UDim2.new(0, 139, 0, 34)
Rag.Font = Enum.Font.PermanentMarker
Rag.Text = "RAGDOLL 🧪"
Rag.TextColor3 = Color3.fromRGB(0, 0, 0)
Rag.TextSize = 14.000
Rag.MouseButton1Down:connect(function()
	loadstring(game:HttpGet(('https://raw.githubusercontent.com/jdnn1/gtred/main/README.md'),true))()
	end)

rob.Name = "rob"
rob.Parent = ImageLabel
rob.BackgroundColor3 = Color3.fromRGB(255, 255, 255)
rob.BackgroundTransparency = 1.000
rob.Position = UDim2.new(0.130952388, 0, 0.558303893, 0)
rob.Size = UDim2.new(0, 139, 0, 34)
rob.Font = Enum.Font.PermanentMarker
rob.Text = "ROBEATS 🎶"
rob.TextColor3 = Color3.fromRGB(0, 0, 0)
rob.TextSize = 14.000
rob.MouseButton1Down:connect(function()
	loadstring(game:HttpGet("https://raw.githubusercontent.com/notclosure/new-years/main/happ.lua"))()
end)


TOH.Name = "TOH"
TOH.Parent = ImageLabel
TOH.BackgroundColor3 = Color3.fromRGB(255, 255, 255)
TOH.BackgroundTransparency = 1.000
TOH.Position = UDim2.new(0.130952388, 0, 0.67844522, 0)
TOH.Size = UDim2.new(0, 139, 0, 34)
TOH.Font = Enum.Font.PermanentMarker
TOH.Text = "Tower Of Hell 😡"
TOH.TextColor3 = Color3.fromRGB(0, 0, 0)
TOH.TextSize = 14.000
TOH.MouseButton1Down:connect(function()
	loadstring(game:HttpGet("https://raw.githubusercontent.com/SpedCoding/Skri-Hub/main/Framework"))()
end)

Arsenaal.Name = "Arsenaal"
Arsenaal.Parent = ImageLabel
Arsenaal.BackgroundColor3 = Color3.fromRGB(255, 255, 255)
Arsenaal.BackgroundTransparency = 1.000
Arsenaal.Position = UDim2.new(0.130952388, 0, 0.798586547, 0)
Arsenaal.Size = UDim2.new(0, 139, 0, 34)
Arsenaal.Font = Enum.Font.PermanentMarker
Arsenaal.Text = "ARSENAL 🔫"
Arsenaal.TextColor3 = Color3.fromRGB(0, 0, 0)
Arsenaal.TextSize = 14.000
arsenaal.MouseButton1Down:connect(function()
	function getplrsname()
		for i,v in pairs(game:GetChildren()) do
			if v.ClassName == "Players" then
				return v.Name
			end
		end
	end
	local players = getplrsname()
	local plr = game[players].LocalPlayer
	coroutine.resume(coroutine.create(function()
		while  wait(1) do
			coroutine.resume(coroutine.create(function()
				for _,v in pairs(game[players]:GetPlayers()) do
					if v.Name ~= plr.Name and v.Character then
						v.Character.RightUpperLeg.CanCollide = false
						v.Character.RightUpperLeg.Transparency = 10
						v.Character.RightUpperLeg.Size = Vector3.new(13,13,13)

						v.Character.LeftUpperLeg.CanCollide = false
						v.Character.LeftUpperLeg.Transparency = 10
						v.Character.LeftUpperLeg.Size = Vector3.new(13,13,13)

						v.Character.HeadHB.CanCollide = false
						v.Character.HeadHB.Transparency = 10
						v.Character.HeadHB.Size = Vector3.new(13,13,13)

						v.Character.HumanoidRootPart.CanCollide = false
						v.Character.HumanoidRootPart.Transparency = 10
						v.Character.HumanoidRootPart.Size = Vector3.new(13,13,13)

					end
				end
			end))
		end
	end))
end)
