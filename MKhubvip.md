local Players = game:GetService("Players")
local RunService = game:GetService("RunService")
local UIS = game:GetService("UserInputService")

local LP = Players.LocalPlayer
local Camera = workspace.CurrentCamera

local C = {
	Aimbot = false,
	ESP = false,
	Noclip = false,
	TeamCheck = true,
	WallCheck = true,
	Speed = 16,
	FOV = 100,
	TargetPart = "Head"
}

local Gui = Instance.new("ScreenGui")
Gui.Name = "MKHub"
Gui.ResetOnSpawn = false
Gui.ZIndexBehavior = Enum.ZIndexBehavior.Sibling
Gui.Parent = LP:WaitForChild("PlayerGui")

local Main = Instance.new("Frame")
Main.Size = UDim2.fromOffset(270,430)
Main.Position = UDim2.new(.5,-135,.5,-215)
Main.BackgroundColor3 = Color3.fromRGB(8,18,38)
Main.BorderSizePixel = 0
Main.Parent = Gui

Instance.new("UICorner",Main).CornerRadius = UDim.new(0,16)

local Stroke = Instance.new("UIStroke",Main)
Stroke.Color = Color3.fromRGB(40,130,255)
Stroke.Thickness = 1.5

local Top = Instance.new("Frame")
Top.Size = UDim2.new(1,0,0,60)
Top.BackgroundColor3 = Color3.fromRGB(12,35,72)
Top.BorderSizePixel = 0
Top.Parent = Main

Instance.new("UICorner",Top).CornerRadius = UDim.new(0,16)

local Title = Instance.new("TextLabel")
Title.Size = UDim2.new(1,-65,1,0)
Title.Position = UDim2.fromOffset(18,0)
Title.BackgroundTransparency = 1
Title.Text = "🕷  MK HUB"
Title.TextColor3 = Color3.fromRGB(100,190,255)
Title.TextXAlignment = Enum.TextXAlignment.Left
Title.Font = Enum.Font.GothamBold
Title.TextSize = 22
Title.Parent = Top

local Close = Instance.new("TextButton")
Close.Size = UDim2.fromOffset(34,34)
Close.Position = UDim2.new(1,-45,0,13)
Close.BackgroundColor3 = Color3.fromRGB(190,45,60)
Close.Text = "×"
Close.TextColor3 = Color3.new(1,1,1)
Close.TextSize = 23
Close.Font = Enum.Font.GothamBold
Close.Parent = Top
Instance.new("UICorner",Close).CornerRadius = UDim.new(0,10)

local Content = Instance.new("ScrollingFrame")
Content.Size = UDim2.new(1,-16,1,-68)
Content.Position = UDim2.fromOffset(8,65)
Content.BackgroundTransparency = 1
Content.BorderSizePixel = 0
Content.ScrollBarThickness = 3
Content.CanvasSize = UDim2.fromOffset(0,520)
Content.Parent = Main

local Layout = Instance.new("UIListLayout",Content)
Layout.Padding = UDim.new(0,8)

local Padding = Instance.new("UIPadding",Content)
Padding.PaddingLeft = UDim.new(0,5)
Padding.PaddingRight = UDim.new(0,5)

local function Section(Text)
	local L = Instance.new("TextLabel")
	L.Size = UDim2.new(1,0,0,25)
	L.BackgroundTransparency = 1
	L.Text = Text
	L.TextColor3 = Color3.fromRGB(120,180,240)
	L.TextXAlignment = Enum.TextXAlignment.Left
	L.Font = Enum.Font.GothamBold
	L.TextSize = 12
	L.Parent = Content
end

local function Toggle(Name,Desc,Callback)
	local Frame = Instance.new("Frame")
	Frame.Size = UDim2.new(1,0,0,52)
	Frame.BackgroundColor3 = Color3.fromRGB(15,31,58)
	Frame.BorderSizePixel = 0
	Frame.Parent = Content
	Instance.new("UICorner",Frame).CornerRadius = UDim.new(0,11)

	local N = Instance.new("TextLabel")
	N.Size = UDim2.new(1,-75,0,22)
	N.Position = UDim2.fromOffset(12,5)
	N.BackgroundTransparency = 1
	N.Text = Name
	N.TextColor3 = Color3.new(1,1,1)
	N.TextXAlignment = Enum.TextXAlignment.Left
	N.Font = Enum.Font.GothamBold
	N.TextSize = 13
	N.Parent = Frame

	local D = Instance.new("TextLabel")
	D.Size = UDim2.new(1,-75,0,18)
	D.Position = UDim2.fromOffset(12,27)
	D.BackgroundTransparency = 1
	D.Text = Desc
	D.TextColor3 = Color3.fromRGB(130,150,180)
	D.TextXAlignment = Enum.TextXAlignment.Left
	D.Font = Enum.Font.Gotham
	D.TextSize = 10
	D.Parent = Frame

	local Switch = Instance.new("TextButton")
	Switch.Size = UDim2.fromOffset(48,25)
	Switch.Position = UDim2.new(1,-60,.5,-12)
	Switch.BackgroundColor3 = Color3.fromRGB(45,55,75)
	Switch.Text = ""
	Switch.Parent = Frame
	Instance.new("UICorner",Switch).CornerRadius = UDim.new(1,0)

	local Circle = Instance.new("Frame")
	Circle.Size = UDim2.fromOffset(19,19)
	Circle.Position = UDim2.fromOffset(3,3)
	Circle.BackgroundColor3 = Color3.fromRGB(180,190,200)
	Circle.Parent = Switch
	Instance.new("UICorner",Circle).CornerRadius = UDim.new(1,0)

	local State = false

	Switch.MouseButton1Click:Connect(function()
		State = not State

		if State then
			Switch.BackgroundColor3 = Color3.fromRGB(35,125,255)
			Circle.Position = UDim2.new(1,-22,.5,-9)
		else
			Switch.BackgroundColor3 = Color3.fromRGB(45,55,75)
			Circle.Position = UDim2.fromOffset(3,3)
		end

		Callback(State)
	end)
end

local function Input(Name,Default,Callback)
	local Frame = Instance.new("Frame")
	Frame.Size = UDim2.new(1,0,0,50)
	Frame.BackgroundColor3 = Color3.fromRGB(15,31,58)
	Frame.BorderSizePixel = 0
	Frame.Parent = Content
	Instance.new("UICorner",Frame).CornerRadius = UDim.new(0,11)

	local Label = Instance.new("TextLabel")
	Label.Size = UDim2.new(.55,0,1,0)
	Label.Position = UDim2.fromOffset(12,0)
	Label.BackgroundTransparency = 1
	Label.Text = Name
	Label.TextColor3 = Color3.new(1,1,1)
	Label.TextXAlignment = Enum.TextXAlignment.Left
	Label.Font = Enum.Font.GothamBold
	Label.TextSize = 13
	Label.Parent = Frame

	local Box = Instance.new("TextBox")
	Box.Size = UDim2.fromOffset(80,32)
	Box.Position = UDim2.new(1,-92,.5,-16)
	Box.BackgroundColor3 = Color3.fromRGB(8,20,40)
	Box.TextColor3 = Color3.fromRGB(120,195,255)
	Box.Text = tostring(Default)
	Box.Font = Enum.Font.GothamBold
	Box.TextSize = 13
	Box.ClearTextOnFocus = false
	Box.Parent = Frame
	Instance.new("UICorner",Box).CornerRadius = UDim.new(0,8)

	Box.FocusLost:Connect(function()
		local Value = tonumber(Box.Text)
		if Value then
			Callback(Value,Box)
		end
	end)
end

Section("COMBAT")

Toggle("Aimbot","Aim assist • alvo selecionado",function(Value)
	C.Aimbot = Value
end)

Toggle("Team Check","Ignora jogadores do seu time",function(Value)
	C.TeamCheck = Value
end)

Toggle("Wall Check","Verifica obstáculos",function(Value)
	C.WallCheck = Value
end)

Section("VISUAL")

Toggle("ESP","Box • nome • vida • distância",function(Value)
	C.ESP = Value
end)

Section("MOVEMENT")

Toggle("Noclip","Atravessar objetos",function(Value)
	C.Noclip = Value
end)

Input("Speed",16,function(Value)
	C.Speed = math.clamp(Value,1,100)

	local Character = LP.Character
	local Humanoid = Character and Character:FindFirstChildOfClass("Humanoid")

	if Humanoid then
		Humanoid.WalkSpeed = C.Speed
	end
end)

Section("AIM SETTINGS")

Input("FOV",100,function(Value)
	C.FOV = math.clamp(Value,0,200)
end)

local TargetButton = Instance.new("TextButton")
TargetButton.Size = UDim2.new(1,0,0,45)
TargetButton.BackgroundColor3 = Color3.fromRGB(15,31,58)
TargetButton.Text = "TARGET: HEAD"
TargetButton.TextColor3 = Color3.fromRGB(100,190,255)
TargetButton.Font = Enum.Font.GothamBold
TargetButton.TextSize = 13
TargetButton.Parent = Content
Instance.new("UICorner",TargetButton).CornerRadius = UDim.new(0,11)

TargetButton.MouseButton1Click:Connect(function()
	if C.TargetPart == "Head" then
		C.TargetPart = "UpperTorso"
		TargetButton.Text = "TARGET: TORSO"
	else
		C.TargetPart = "Head"
		TargetButton.Text = "TARGET: HEAD"
	end
end)

local Open = Instance.new("TextButton")
Open.Size = UDim2.fromOffset(62,62)
Open.Position = UDim2.new(0,20,.5,-31)
Open.BackgroundColor3 = Color3.fromRGB(12,50,105)
Open.Text = "MK"
Open.TextColor3 = Color3.fromRGB(110,200,255)
Open.TextSize = 19
Open.Font = Enum.Font.GothamBold
Open.Visible = false
Open.Active = true
Open.Parent = Gui

Instance.new("UICorner",Open).CornerRadius = UDim.new(1,0)

local OpenStroke = Instance.new("UIStroke",Open)
OpenStroke.Color = Color3.fromRGB(60,160,255)
OpenStroke.Thickness = 2

local Dragging = false
local DragStart
local StartPosition

Open.InputBegan:Connect(function(Input)
	if Input.UserInputType == Enum.UserInputType.MouseButton1
	or Input.UserInputType == Enum.UserInputType.Touch then

		Dragging = true
		DragStart = Input.Position
		StartPosition = Open.Position

		Input.Changed:Connect(function()
			if Input.UserInputState == Enum.UserInputState.End then
				Dragging = false
			end
		end)
	end
end)

UIS.InputChanged:Connect(function(Input)
	if not Dragging then return end

	if Input.UserInputType == Enum.UserInputType.MouseMovement
	or Input.UserInputType == Enum.UserInputType.Touch then

		local Delta = Input.Position - DragStart

		Open.Position = UDim2.new(
			StartPosition.X.Scale,
			StartPosition.X.Offset + Delta.X,
			StartPosition.Y.Scale,
			StartPosition.Y.Offset + Delta.Y
		)
	end
end)

local function CloseHub()
	Main.Visible = false
	Open.Visible = true
end

local function OpenHub()
	Main.Visible = true
	Open.Visible = false
end

Close.MouseButton1Click:Connect(CloseHub)
Open.MouseButton1Click:Connect(OpenHub)

UIS.InputBegan:Connect(function(Input,Processed)
	if Processed then return end

	if Input.KeyCode == Enum.KeyCode.RightShift then
		if Main.Visible then
			CloseHub()
		else
			OpenHub()
		end
	end
end)

local FOVCircle = Instance.new("Frame")
FOVCircle.BackgroundTransparency = 1
FOVCircle.Visible = false
FOVCircle.Parent = Gui
Instance.new("UICorner",FOVCircle).CornerRadius = UDim.new(1,0)

local FOVStroke = Instance.new("UIStroke",FOVCircle)
FOVStroke.Color = Color3.fromRGB(70,170,255)
FOVStroke.Thickness = 2

local ESPs = {}

local function RemoveESP(Player)
	if ESPs[Player] then
		for _,Object in ipairs(ESPs[Player]) do
			if typeof(Object) == "RBXScriptConnection" then
				Object:Disconnect()
			elseif Object then
				Object:Destroy()
			end
		end
		ESPs[Player] = nil
	end
end

local function CreateESP(Player)
	if Player == LP or not C.ESP then return end

	RemoveESP(Player)

	local Character = Player.Character
	if not Character then return end

	local Root = Character:FindFirstChild("HumanoidRootPart")
	local Humanoid = Character:FindFirstChildOfClass("Humanoid")

	if not Root or not Humanoid then return end

	local Color = Color3.fromRGB(50,160,255)

	if Player.Team then
		Color = Player.Team.TeamColor.Color
	end

	local Box = Instance.new("BoxHandleAdornment")
	Box.Name = "MK_Box"
	Box.Adornee = Root
	Box.AlwaysOnTop = true
	Box.ZIndex = 5
	Box.Size = Vector3.new(4,6,2)
	Box.Transparency = .55
	Box.Color3 = Color
	Box.Parent = Root

	local Tag = Instance.new("BillboardGui")
	Tag.Name = "MK_ESP"
	Tag.Size = UDim2.fromOffset(190,65)
	Tag.StudsOffset = Vector3.new(0,4,0)
	Tag.AlwaysOnTop = true
	Tag.Parent = Root

	local Text = Instance.new("TextLabel")
	Text.Size = UDim2.fromScale(1,1)
	Text.BackgroundTransparency = 1
	Text.TextColor3 = Color
	Text.TextStrokeTransparency = .2
	Text.Font = Enum.Font.GothamBold
	Text.TextSize = 12
	Text.Parent = Tag

	local Connection

	Connection = RunService.RenderStepped:Connect(function()
		if not C.ESP or not Player.Parent or not Character.Parent then
			Connection:Disconnect()
			return
		end

		local MyRoot = LP.Character and LP.Character:FindFirstChild("HumanoidRootPart")
		local Distance = MyRoot and math.floor((Root.Position-MyRoot.Position).Magnitude) or 0

		Text.Text =
			Player.Name..
			"\nHP: "..math.floor(Humanoid.Health)..
			"/"..math.floor(Humanoid.MaxHealth)..
			"\n"..Distance.." studs"
	end)

	ESPs[Player] = {Box,Tag,Connection}
end

local function ValidTarget(Player)
	if Player == LP then return false end

	if C.TeamCheck and LP.Team and Player.Team == LP.Team then
		return false
	end

	local Character = Player.Character
	if not Character then return false end

	local Humanoid = Character:FindFirstChildOfClass("Humanoid")
	local Part = Character:FindFirstChild(C.TargetPart)

	if not Humanoid or Humanoid.Health <= 0 or not Part then
		return false
	end

	if C.WallCheck then
		local Params = RaycastParams.new()
		Params.FilterType = Enum.RaycastFilterType.Exclude
		Params.FilterDescendantsInstances = {LP.Character}

		local Result = workspace:Raycast(
			Camera.CFrame.Position,
			Part.Position-Camera.CFrame.Position,
			Params
		)

		if Result and not Result.Instance:IsDescendantOf(Character) then
			return false
		end
	end

	return true
end

local function GetTarget()
	local BestPart
	local BestDistance = C.FOV
	local Center = Camera.ViewportSize/2

	for _,Player in ipairs(Players:GetPlayers()) do
		if ValidTarget(Player) then
			local Part = Player.Character:FindFirstChild(C.TargetPart)

			if Part then
				local Screen,Visible = Camera:WorldToViewportPoint(Part.Position)

				if Visible and Screen.Z > 0 then
					local Distance = (
						Vector2.new(Screen.X,Screen.Y)-
						Vector2.new(Center.X,Center.Y)
					).Magnitude

					if Distance <= BestDistance then
						BestDistance = Distance
						BestPart = Part
					end
				end
			end
		end
	end

	return BestPart
end

RunService.RenderStepped:Connect(function()
	if C.Aimbot then
		local TargetPart = GetTarget()

		if TargetPart then
			Camera.CFrame = CFrame.lookAt(
				Camera.CFrame.Position,
				TargetPart.Position
			)
		end
	end

	local Size = math.clamp(C.FOV,0,200)*2

	FOVCircle.Size = UDim2.fromOffset(Size,Size)
	FOVCircle.Position = UDim2.new(.5,-Size/2,.5,-Size/2)
	FOVCircle.Visible = C.Aimbot and C.FOV > 0
end)

RunService.Stepped:Connect(function()
	if C.Noclip and LP.Character then
		for _,Part in ipairs(LP.Character:GetDescendants()) do
			if Part:IsA("BasePart") then
				Part.CanCollide = false
			end
		end
	end
end)

RunService.Heartbeat:Connect(function()
	if C.ESP then
		for _,Player in ipairs(Players:GetPlayers()) do
			if Player ~= LP and not ESPs[Player] then
				CreateESP(Player)
			end
		end
	end
end)

LP.CharacterAdded:Connect(function(Character)
	local Humanoid = Character:WaitForChild("Humanoid")
	Humanoid.WalkSpeed = C.Speed
end)

Players.PlayerAdded:Connect(function(Player)
	Player.CharacterAdded:Connect(function()
		task.wait(.5)

		if C.ESP then
			CreateESP(Player)
		end
	end)
end)

Players.PlayerRemoving:Connect(RemoveESP)
