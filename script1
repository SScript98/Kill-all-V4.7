--[[
    Kill All V4 Full (компактный, современный, все функции)
    ...
    Доработка: 6 тем, кнопки тоже меняют цвет при смене темы.
]]

local MENU_SIZE = UDim2.new(0, 249, 0, 395)
local BUTTON_HEIGHT = 30
local BUTTON_PADDING = 4

local themes = {
	[1] = {
		MENU_COLOR = Color3.fromRGB(230, 236, 245),
		BUTTON_COLOR = Color3.fromRGB(255, 255, 255),
		BUTTON_COLOR_ACT = Color3.fromRGB(200, 235, 255),
		TEXT = Color3.fromRGB(60, 80, 120),
		TITLE = Color3.fromRGB(80, 90, 110),
		NAME = "Светлая",
		ICON = "🎨",
	},
	[2] = {
		MENU_COLOR = Color3.fromRGB(33, 34, 44),
		BUTTON_COLOR = Color3.fromRGB(50, 55, 70),
		BUTTON_COLOR_ACT = Color3.fromRGB(45, 90, 120),
		TEXT = Color3.fromRGB(220, 230, 255),
		TITLE = Color3.fromRGB(130, 170, 245),
		NAME = "Тёмная",
		ICON = "🌙",
	},
	[3] = {
		MENU_COLOR = Color3.fromRGB(240, 235, 220),
		BUTTON_COLOR = Color3.fromRGB(255, 247, 210),
		BUTTON_COLOR_ACT = Color3.fromRGB(255, 210, 120),
		TEXT = Color3.fromRGB(150, 110, 40),
		TITLE = Color3.fromRGB(120, 90, 30),
		NAME = "Солнечная",
		ICON = "🌞",
	},
	[4] = {
		MENU_COLOR = Color3.fromRGB(50, 65, 60),
		BUTTON_COLOR = Color3.fromRGB(70, 120, 90),
		BUTTON_COLOR_ACT = Color3.fromRGB(80, 200, 130),
		TEXT = Color3.fromRGB(205, 255, 220),
		TITLE = Color3.fromRGB(170, 255, 170),
		NAME = "Зелёная",
		ICON = "🌿",
	},
	[5] = {
		MENU_COLOR = Color3.fromRGB(45, 40, 60),
		BUTTON_COLOR = Color3.fromRGB(90, 80, 130),
		BUTTON_COLOR_ACT = Color3.fromRGB(170, 140, 255),
		TEXT = Color3.fromRGB(255, 220, 255),
		TITLE = Color3.fromRGB(200, 160, 255),
		NAME = "Фиолетовая",
		ICON = "💜",
	},
	[6] = {
		MENU_COLOR = Color3.fromRGB(25, 30, 38),
		BUTTON_COLOR = Color3.fromRGB(32, 45, 75),
		BUTTON_COLOR_ACT = Color3.fromRGB(70, 120, 210),
		TEXT = Color3.fromRGB(255, 255, 255),
		TITLE = Color3.fromRGB(120, 180, 255),
		NAME = "Синяя",
		ICON = "🦋",
	}
}
local currentTheme = 1
local function getTheme()
	return themes[currentTheme]
end

local FONT = Enum.Font.SourceSansSemibold

local DEFAULT_WAIT_TIME = 0.5
local MIN_WAIT_TIME = 0.5
local MAX_WAIT_TIME = 2.5
local MAX_DELAY_BUTTONS = 5

local DEFAULT_DISTANCE = 1
local MIN_DISTANCE = 1
local MAX_DISTANCE = 10

local Players = game:GetService("Players")
local LocalPlayer = Players.LocalPlayer
local UserInputService = game:GetService("UserInputService")
local RunService = game:GetService("RunService")
local Camera = workspace.CurrentCamera

if LocalPlayer.PlayerGui:FindFirstChild("KillAllV4Menu") then
	LocalPlayer.PlayerGui.KillAllV4Menu:Destroy()
end

local mainGui = Instance.new("ScreenGui")
mainGui.Name = "KillAllV4Menu"
mainGui.ResetOnSpawn = false
mainGui.Parent = LocalPlayer.PlayerGui

local menuFrame = Instance.new("Frame")
menuFrame.Size = MENU_SIZE
menuFrame.Position = UDim2.new(0, 36, 0, 120)
menuFrame.BackgroundColor3 = getTheme().MENU_COLOR
menuFrame.BorderSizePixel = 0
menuFrame.Active = true
menuFrame.Draggable = true
menuFrame.Name = "Menu"
menuFrame.Parent = mainGui

-- Кнопка-дизайнер в левом верхнем углу
local designerBtn = Instance.new("TextButton")
designerBtn.Size = UDim2.new(0, 28, 0, 28)
designerBtn.Position = UDim2.new(0, 4, 0, 4)
designerBtn.BackgroundTransparency = 1
designerBtn.Text = getTheme().ICON or "🎨"
designerBtn.Font = FONT
designerBtn.TextSize = 20
designerBtn.TextColor3 = getTheme().TEXT
designerBtn.ZIndex = 11
designerBtn.Parent = menuFrame

-- Кнопка "свернуть/развернуть"
local COLLAPSED_HEIGHT = 36
local EXPANDED_SIZE = menuFrame.Size
local COLLAPSED_SIZE = UDim2.new(EXPANDED_SIZE.X.Scale, EXPANDED_SIZE.X.Offset, 0, COLLAPSED_HEIGHT)

local collapseBtn = Instance.new("TextButton")
collapseBtn.Size = UDim2.new(0, 28, 0, 28)
collapseBtn.Position = UDim2.new(1, -32, 0, 4)
collapseBtn.BackgroundTransparency = 1
collapseBtn.Text = "–"
collapseBtn.Font = FONT
collapseBtn.TextSize = 23
collapseBtn.TextColor3 = getTheme().TEXT
collapseBtn.ZIndex = 10
collapseBtn.Parent = menuFrame

-- Титул
local title = Instance.new("TextLabel")
title.Size = UDim2.new(1, 0, 0, 30)
title.Position = UDim2.new(0, 0, 0, 2)
title.BackgroundTransparency = 1
title.Text = "Kill All V4.7"
title.Font = FONT
title.TextSize = 20
title.TextColor3 = getTheme().TITLE
title.Parent = menuFrame

-- Кнопка Kill All
local killAllBtn = Instance.new("TextButton")
killAllBtn.Size = UDim2.new(1, -20, 0, BUTTON_HEIGHT)
killAllBtn.Position = UDim2.new(0, 10, 0, 34)
killAllBtn.BackgroundColor3 = getTheme().BUTTON_COLOR
killAllBtn.BorderSizePixel = 0
killAllBtn.Text = "Kill All"
killAllBtn.Font = FONT
killAllBtn.TextSize = 15
killAllBtn.TextColor3 = getTheme().TEXT
killAllBtn.AutoButtonColor = true
killAllBtn.Parent = menuFrame

-- Счётчик
local progressLabel = Instance.new("TextLabel")
progressLabel.Size = UDim2.new(1, -20, 0, 16)
progressLabel.Position = UDim2.new(0, 10, 0, 34+BUTTON_HEIGHT+BUTTON_PADDING)
progressLabel.BackgroundTransparency = 1
progressLabel.Text = "Ожидание..."
progressLabel.Font = FONT
progressLabel.TextSize = 13
progressLabel.TextColor3 = Color3.fromRGB(90, 120, 140)
progressLabel.Parent = menuFrame

-- Быстрый выбор задержки
local delays = {0.5, 1, 1.5, 2, 2.5}
local delayBtns = {}
local yStart = 34+BUTTON_HEIGHT+BUTTON_PADDING+18
local btnW, btnH = 40, BUTTON_HEIGHT-6

local delayLabel = Instance.new("TextLabel")
delayLabel.Size = UDim2.new(1, -20, 0, 16)
delayLabel.Position = UDim2.new(0, 10, 0, yStart)
delayLabel.BackgroundTransparency = 1
delayLabel.Text = "Задержка, сек:"
delayLabel.Font = FONT
delayLabel.TextSize = 13
delayLabel.TextColor3 = Color3.fromRGB(110, 130, 160)
delayLabel.Parent = menuFrame

local waitTime = DEFAULT_WAIT_TIME
local function findDelayIndex(val)
	for i, v in ipairs(delays) do
		if v == val then return i end
	end
	return #delays
end

local function applyTheme()
	local theme = getTheme()
	menuFrame.BackgroundColor3 = theme.MENU_COLOR
	title.TextColor3 = theme.TITLE
	killAllBtn.BackgroundColor3 = theme.BUTTON_COLOR
	killAllBtn.TextColor3 = theme.TEXT
	collapseBtn.TextColor3 = theme.TEXT
	designerBtn.TextColor3 = theme.TEXT
	designerBtn.Text = theme.ICON or "🎨"

	for _, b in ipairs(delayBtns) do
		b.BackgroundColor3 = theme.BUTTON_COLOR
		b.TextColor3 = theme.TEXT
	end
	if delayBtns[findDelayIndex(waitTime)] then
		delayBtns[findDelayIndex(waitTime)].BackgroundColor3 = theme.BUTTON_COLOR_ACT
		delayBtns[findDelayIndex(waitTime)].TextColor3 = theme.TEXT
	end

	otherBox.BackgroundColor3 = theme.BUTTON_COLOR
	otherBox.TextColor3 = theme.TEXT
	otherSetBtn.BackgroundColor3 = Color3.fromRGB(210, 240, 255)
	otherSetBtn.TextColor3 = theme.TEXT
	removeBtn.BackgroundColor3 = Color3.fromRGB(255, 230, 220)
	removeBtn.TextColor3 = Color3.fromRGB(160, 40, 40)
	distValueBox.BackgroundColor3 = theme.BUTTON_COLOR
	distValueBox.TextColor3 = theme.TEXT
	distMinusBtn.BackgroundColor3 = Color3.fromRGB(200, 220, 240)
	distMinusBtn.TextColor3 = theme.TEXT
	distPlusBtn.BackgroundColor3 = Color3.fromRGB(200, 220, 240)
	distPlusBtn.TextColor3 = theme.TEXT
	killLoopBtn.BackgroundColor3 = killLoop and Color3.fromRGB(255, 230, 120) or theme.BUTTON_COLOR
	killLoopBtn.TextColor3 = Color3.fromRGB(160, 120, 10)
	lockFirstPersonBtn.BackgroundColor3 = lockFirstPerson and Color3.fromRGB(210,240,255) or theme.BUTTON_COLOR
	lockFirstPersonBtn.TextColor3 = theme.TEXT
	autoFollowBtn.BackgroundColor3 = autoFollow and Color3.fromRGB(210,240,255) or theme.BUTTON_COLOR
	autoFollowBtn.TextColor3 = theme.TEXT
	aimBotBtn.BackgroundColor3 = aimBot and Color3.fromRGB(210,240,255) or theme.BUTTON_COLOR
	aimBotBtn.TextColor3 = theme.TEXT
	teamIgnoreBtn.BackgroundColor3 = teamIgnore and Color3.fromRGB(210, 240, 255) or theme.BUTTON_COLOR
	teamIgnoreBtn.TextColor3 = Color3.fromRGB(60, 110, 180)
end

local function updateDelayButtons(selectedIndex)
	for _, b in ipairs(delayBtns) do b:Destroy() end
	delayBtns = {}
	for i, v in ipairs(delays) do
		local btn = Instance.new("TextButton")
		btn.Size = UDim2.new(0, btnW, 0, btnH)
		btn.Position = UDim2.new(0, 10+(i-1)*(btnW+6), 0, yStart+18)
		btn.BackgroundColor3 = getTheme().BUTTON_COLOR
		btn.BorderSizePixel = 0
		btn.Text = tostring(v)
		btn.Font = FONT
		btn.TextSize = 15
		btn.TextColor3 = getTheme().TEXT
		btn.Parent = menuFrame
		btn.MouseButton1Click:Connect(function()
			waitTime = v
			for j, b2 in ipairs(delayBtns) do
				b2.BackgroundColor3 = getTheme().BUTTON_COLOR
				b2.TextColor3 = getTheme().TEXT
			end
			btn.BackgroundColor3 = getTheme().BUTTON_COLOR_ACT
			btn.TextColor3 = getTheme().TEXT
		end)
		delayBtns[i] = btn
	end
	local active = selectedIndex or findDelayIndex(waitTime)
	if delayBtns[active] then
		for j, b in ipairs(delayBtns) do
			b.BackgroundColor3 = getTheme().BUTTON_COLOR
			b.TextColor3 = getTheme().TEXT
		end
		delayBtns[active].BackgroundColor3 = getTheme().BUTTON_COLOR_ACT
		delayBtns[active].TextColor3 = getTheme().TEXT
		waitTime = delays[active]
	end
end

updateDelayButtons(findDelayIndex(DEFAULT_WAIT_TIME))

-- === КНОПКИ ДРУГОЕ/УДАЛИТЬ ===
local otherBox = Instance.new("TextBox")
otherBox.Size = UDim2.new(0, 61, 0, btnH)
otherBox.Position = UDim2.new(0, 10, 0, yStart+18+btnH+8)
otherBox.PlaceholderText = "Другое"
otherBox.Text = ""
otherBox.Font = FONT
otherBox.TextSize = 14
otherBox.TextColor3 = getTheme().TEXT
otherBox.BackgroundColor3 = getTheme().BUTTON_COLOR
otherBox.BorderSizePixel = 0
otherBox.ClearTextOnFocus = false
otherBox.Parent = menuFrame

local otherSetBtn = Instance.new("TextButton")
otherSetBtn.Size = UDim2.new(0, 52, 0, btnH)
otherSetBtn.Position = UDim2.new(0, 77, 0, yStart+18+btnH+8)
otherSetBtn.BackgroundColor3 = Color3.fromRGB(210, 240, 255)
otherSetBtn.BorderSizePixel = 0
otherSetBtn.Text = "Добавить"
otherSetBtn.Font = FONT
otherSetBtn.TextSize = 13
otherSetBtn.TextColor3 = getTheme().TEXT
otherSetBtn.Parent = menuFrame

local removeBtn = Instance.new("TextButton")
removeBtn.Size = UDim2.new(0, 52, 0, btnH)
removeBtn.Position = UDim2.new(0, 135, 0, yStart+18+btnH+8)
removeBtn.BackgroundColor3 = Color3.fromRGB(255, 230, 220)
removeBtn.BorderSizePixel = 0
removeBtn.Text = "Удалить"
removeBtn.Font = FONT
removeBtn.TextSize = 13
removeBtn.TextColor3 = Color3.fromRGB(160, 40, 40)
removeBtn.Parent = menuFrame

otherSetBtn.MouseButton1Click:Connect(function()
	local n = tonumber(otherBox.Text)
	if n and n > 0 then
		local newIndex
		if #delays < MAX_DELAY_BUTTONS then
			table.insert(delays, n)
			newIndex = #delays
		else
			delays[#delays] = n
			newIndex = #delays
		end
		waitTime = n
		otherBox.Text = ""
		updateDelayButtons(newIndex)
		progressLabel.Text = (#delays < MAX_DELAY_BUTTONS and "Добавлено: " or "Изменено: ")..n.." сек."
		applyTheme()
	else
		progressLabel.Text = "Некорректное число"
	end
end)

removeBtn.MouseButton1Click:Connect(function()
	if #delays > 1 then
		table.remove(delays, #delays)
		updateDelayButtons(#delays)
		waitTime = delays[#delays]
		progressLabel.Text = "Последняя кнопка удалена"
		applyTheme()
	else
		progressLabel.Text = "Нельзя удалить последнюю!"
	end
end)

-- === РАССТОЯНИЕ ДО ЦЕЛИ ===
local distance = DEFAULT_DISTANCE

local distanceLabel = Instance.new("TextLabel")
distanceLabel.Size = UDim2.new(1, -20, 0, 16)
distanceLabel.Position = UDim2.new(0, 10, 0, yStart+18+btnH+8+btnH+8)
distanceLabel.BackgroundTransparency = 1
distanceLabel.Text = "Расстояние до цели:"
distanceLabel.Font = FONT
distanceLabel.TextSize = 13
distanceLabel.TextColor3 = Color3.fromRGB(120, 120, 160)
distanceLabel.Parent = menuFrame

local distValueBox = Instance.new("TextBox")
distValueBox.Size = UDim2.new(0, 44, 0, btnH)
distValueBox.Position = UDim2.new(0, 10, 0, yStart+18+btnH+8+btnH+8+18)
distValueBox.Text = tostring(distance)
distValueBox.Font = FONT
distValueBox.TextSize = 14
distValueBox.TextColor3 = getTheme().TEXT
distValueBox.BackgroundColor3 = getTheme().BUTTON_COLOR
distValueBox.BorderSizePixel = 0
distValueBox.ClearTextOnFocus = false
distValueBox.Parent = menuFrame

local distMinusBtn = Instance.new("TextButton")
distMinusBtn.Size = UDim2.new(0, 24, 0, btnH)
distMinusBtn.Position = UDim2.new(0, 62, 0, yStart+18+btnH+8+btnH+8+18)
distMinusBtn.BackgroundColor3 = Color3.fromRGB(200, 220, 240)
distMinusBtn.BorderSizePixel = 0
distMinusBtn.Text = "-"
distMinusBtn.Font = FONT
distMinusBtn.TextSize = 16
distMinusBtn.TextColor3 = getTheme().TEXT
distMinusBtn.Parent = menuFrame

local distPlusBtn = Instance.new("TextButton")
distPlusBtn.Size = UDim2.new(0, 24, 0, btnH)
distPlusBtn.Position = UDim2.new(0, 90, 0, yStart+18+btnH+8+btnH+8+18)
distPlusBtn.BackgroundColor3 = Color3.fromRGB(200, 220, 240)
distPlusBtn.BorderSizePixel = 0
distPlusBtn.Text = "+"
distPlusBtn.Font = FONT
distPlusBtn.TextSize = 16
distPlusBtn.TextColor3 = getTheme().TEXT
distPlusBtn.Parent = menuFrame

distMinusBtn.MouseButton1Click:Connect(function()
	distance = math.max(MIN_DISTANCE, distance - 0.5)
	distValueBox.Text = tostring(distance)
end)
distPlusBtn.MouseButton1Click:Connect(function()
	distance = math.min(MAX_DISTANCE, distance + 0.5)
	distValueBox.Text = tostring(distance)
end)
distValueBox.FocusLost:Connect(function(enter)
	local n = tonumber(distValueBox.Text)
	if n and n >= MIN_DISTANCE and n <= MAX_DISTANCE then
		distance = n
	else
		distValueBox.Text = tostring(distance)
	end
end)

-- === ПЕРЕСТАНОВКА КНОПОК: KILL LOOP и LOCK FIRST PERSON ===
-- Сначала Kill Loop, затем Lock First Person

-- Кнопка Kill Loop
local killLoop = false
local killLoopBtn = Instance.new("TextButton")
killLoopBtn.Size = UDim2.new(1, -20, 0, BUTTON_HEIGHT)
killLoopBtn.Position = UDim2.new(0, 10, 0, yStart+18+btnH+8+btnH+8+18+btnH+10)
killLoopBtn.BackgroundColor3 = getTheme().BUTTON_COLOR
killLoopBtn.BorderSizePixel = 0
killLoopBtn.Text = "Kill Loop: OFF"
killLoopBtn.Font = FONT
killLoopBtn.TextSize = 14
killLoopBtn.TextColor3 = Color3.fromRGB(160, 120, 10)
killLoopBtn.AutoButtonColor = true
killLoopBtn.Parent = menuFrame

-- Кнопка Lock First Person
local lockFirstPerson = false
local lockFirstPersonBtn = Instance.new("TextButton")
lockFirstPersonBtn.Size = UDim2.new(1, -20, 0, BUTTON_HEIGHT)
lockFirstPersonBtn.Position = UDim2.new(0, 10, 0, yStart+18+btnH+8+btnH+8+18+btnH+10+BUTTON_HEIGHT+BUTTON_PADDING)
lockFirstPersonBtn.BackgroundColor3 = getTheme().BUTTON_COLOR
lockFirstPersonBtn.BorderSizePixel = 0
lockFirstPersonBtn.Text = "Lock First Person: OFF"
lockFirstPersonBtn.Font = FONT
lockFirstPersonBtn.TextSize = 14
lockFirstPersonBtn.TextColor3 = getTheme().TEXT
lockFirstPersonBtn.AutoButtonColor = true
lockFirstPersonBtn.Parent = menuFrame

lockFirstPersonBtn.MouseButton1Click:Connect(function()
	lockFirstPerson = not lockFirstPerson
	lockFirstPersonBtn.Text = lockFirstPerson and "Lock First Person: ON" or "Lock First Person: OFF"
	lockFirstPersonBtn.BackgroundColor3 = lockFirstPerson and Color3.fromRGB(210,240,255) or getTheme().BUTTON_COLOR
end)

-- Кнопка Auto Follow Target
local autoFollow = false
local autoFollowBtn = Instance.new("TextButton")
autoFollowBtn.Size = UDim2.new(1, -20, 0, BUTTON_HEIGHT)
autoFollowBtn.Position = UDim2.new(0, 10, 0, yStart+18+btnH+8+btnH+8+18+btnH+10+2*(BUTTON_HEIGHT+BUTTON_PADDING))
autoFollowBtn.BackgroundColor3 = getTheme().BUTTON_COLOR
autoFollowBtn.BorderSizePixel = 0
autoFollowBtn.Text = "Auto Follow: OFF"
autoFollowBtn.Font = FONT
autoFollowBtn.TextSize = 14
autoFollowBtn.TextColor3 = getTheme().TEXT
autoFollowBtn.AutoButtonColor = true
autoFollowBtn.Parent = menuFrame

autoFollowBtn.MouseButton1Click:Connect(function()
	autoFollow = not autoFollow
	autoFollowBtn.Text = autoFollow and "Auto Follow: ON" or "Auto Follow: OFF"
	autoFollowBtn.BackgroundColor3 = autoFollow and Color3.fromRGB(210,240,255) or getTheme().BUTTON_COLOR
end)

-- Кнопка Aim Bot
local aimBot = false
local aimBotBtn = Instance.new("TextButton")
aimBotBtn.Size = UDim2.new(1, -20, 0, BUTTON_HEIGHT)
aimBotBtn.Position = UDim2.new(0, 10, 0, yStart+18+btnH+8+btnH+8+18+btnH+10+3*(BUTTON_HEIGHT+BUTTON_PADDING))
aimBotBtn.BackgroundColor3 = getTheme().BUTTON_COLOR
aimBotBtn.BorderSizePixel = 0
aimBotBtn.Text = "Aim Bot: OFF"
aimBotBtn.Font = FONT
aimBotBtn.TextSize = 14
aimBotBtn.TextColor3 = getTheme().TEXT
aimBotBtn.AutoButtonColor = true
aimBotBtn.Parent = menuFrame

aimBotBtn.MouseButton1Click:Connect(function()
	aimBot = not aimBot
	aimBotBtn.Text = aimBot and "Aim Bot: ON" or "Aim Bot: OFF"
	aimBotBtn.BackgroundColor3 = aimBot and Color3.fromRGB(210,240,255) or getTheme().BUTTON_COLOR
end)

-- Кнопка Team Ignore
local teamIgnore = false
local teamIgnoreBtn = Instance.new("TextButton")
teamIgnoreBtn.Size = UDim2.new(1, -20, 0, BUTTON_HEIGHT)
teamIgnoreBtn.Position = UDim2.new(0, 10, 0, yStart+18+btnH+8+btnH+8+18+btnH+10+4*(BUTTON_HEIGHT+BUTTON_PADDING))
teamIgnoreBtn.BackgroundColor3 = getTheme().BUTTON_COLOR
teamIgnoreBtn.BorderSizePixel = 0
teamIgnoreBtn.Text = "Team Ignore: OFF"
teamIgnoreBtn.Font = FONT
teamIgnoreBtn.TextSize = 14
teamIgnoreBtn.TextColor3 = Color3.fromRGB(60, 110, 180)
teamIgnoreBtn.AutoButtonColor = true
teamIgnoreBtn.Parent = menuFrame

-- Текст Kill Loop внизу экрана
local stopKeyLabel = Instance.new("TextLabel")
stopKeyLabel.Size = UDim2.new(1, 0, 0, 28)
stopKeyLabel.Position = UDim2.new(0, 0, 1, -44)
stopKeyLabel.AnchorPoint = Vector2.new(0, 1)
stopKeyLabel.BackgroundTransparency = 1
stopKeyLabel.Text = "Остановить Kill Loop — T"
stopKeyLabel.Font = FONT
stopKeyLabel.TextSize = 18
stopKeyLabel.TextColor3 = Color3.new(1,1,1)
stopKeyLabel.TextStrokeTransparency = 0.25
stopKeyLabel.Visible = false
stopKeyLabel.ZIndex = 50
stopKeyLabel.Parent = mainGui

-- Для скрытия всех элементов кроме титула и кнопки свернуть и designerBtn
local elementsToHide = {}
for _, obj in ipairs(menuFrame:GetChildren()) do
	if obj ~= title and obj ~= collapseBtn and obj ~= designerBtn and obj:IsA("GuiObject") then
		table.insert(elementsToHide, obj)
	end
end

local collapsed = false
collapseBtn.MouseButton1Click:Connect(function()
	collapsed = not collapsed
	if collapsed then
		menuFrame.Size = COLLAPSED_SIZE
		collapseBtn.Text = "+"
		for _, obj in ipairs(elementsToHide) do
			obj.Visible = false
		end
	else
		menuFrame.Size = EXPANDED_SIZE
		collapseBtn.Text = "–"
		for _, obj in ipairs(elementsToHide) do
			obj.Visible = true
		end
	end
end)

-- Переключение темы (цветов)
designerBtn.MouseButton1Click:Connect(function()
	currentTheme = currentTheme + 1
	if currentTheme > #themes then currentTheme = 1 end
	applyTheme()
	updateDelayButtons(findDelayIndex(waitTime))
	progressLabel.Text = "Тема: " .. getTheme().NAME
end)

-- === ЛОГИКА ===
local isKilling = false

local function getAllOtherPlayers()
	local t = {}
	for _, v in ipairs(Players:GetPlayers()) do
		if v ~= LocalPlayer then
			if not teamIgnore or not (v.Team and LocalPlayer.Team and v.Team == LocalPlayer.Team) then
				table.insert(t, v)
			end
		end
	end
	return t
end

teamIgnoreBtn.MouseButton1Click:Connect(function()
	teamIgnore = not teamIgnore
	teamIgnoreBtn.Text = teamIgnore and "Team Ignore: ON" or "Team Ignore: OFF"
	teamIgnoreBtn.BackgroundColor3 = teamIgnore and Color3.fromRGB(210, 240, 255) or getTheme().BUTTON_COLOR
end)

local cameraBackup = {}
local function setFirstPersonLock(enable)
	if enable then
		if not cameraBackup.locked then
			cameraBackup.locked = true
			cameraBackup.MinZoom = LocalPlayer.CameraMinZoomDistance
			cameraBackup.MaxZoom = LocalPlayer.CameraMaxZoomDistance
			cameraBackup.Mode = LocalPlayer.CameraMode
		end
		LocalPlayer.CameraMinZoomDistance = 0.5
		LocalPlayer.CameraMaxZoomDistance = 0.5
		LocalPlayer.CameraMode = Enum.CameraMode.LockFirstPerson
	else
		if cameraBackup.locked then
			LocalPlayer.CameraMinZoomDistance = cameraBackup.MinZoom or 0.5
			LocalPlayer.CameraMaxZoomDistance = cameraBackup.MaxZoom or 0.5
			LocalPlayer.CameraMode = cameraBackup.Mode or Enum.CameraMode.Classic
			cameraBackup = {}
		end
	end
end

local followConnection
local function followTarget(target)
	if followConnection then followConnection:Disconnect() end
	local char = LocalPlayer.Character
	local targetChar = target and target.Character
	if not (char and targetChar and char:FindFirstChild("HumanoidRootPart") and targetChar:FindFirstChild("HumanoidRootPart")) then return end
	local root = char.HumanoidRootPart
	local targetRoot = targetChar.HumanoidRootPart

	followConnection = RunService.Heartbeat:Connect(function()
		if not isKilling or not autoFollow then followConnection:Disconnect() return end
		if not (char and targetChar and char.Parent and targetChar.Parent) then followConnection:Disconnect() return end
		local behindPos = targetRoot.CFrame.Position - targetRoot.CFrame.LookVector * distance
		root.CFrame = CFrame.new(behindPos, targetRoot.Position)
		if lockFirstPerson then
			Camera.CFrame = CFrame.new(root.Position, targetRoot.Position + targetRoot.CFrame.LookVector * 5)
		end
	end)
end

local aimConnection
local function aimAtTargetHead(target)
	if aimConnection then aimConnection:Disconnect() end
	local char = LocalPlayer.Character
	local targetChar = target and target.Character
	if not (char and targetChar and char:FindFirstChild("HumanoidRootPart")) then return end
	local root = char.HumanoidRootPart
	local head = targetChar:FindFirstChild("Head")
	if not head then return end

	aimConnection = RunService.RenderStepped:Connect(function()
		if not isKilling or not aimBot then aimConnection:Disconnect() return end
		if not (char and targetChar and char.Parent and targetChar.Parent and head.Parent) then aimConnection:Disconnect() return end
		Camera.CFrame = CFrame.new(Camera.CFrame.Position, head.Position)
		UserInputService.MouseBehavior = Enum.MouseBehavior.LockCenter
	end)
end

local function stopAimBot()
	if aimConnection then aimConnection:Disconnect() aimConnection = nil end
	UserInputService.MouseBehavior = Enum.MouseBehavior.Default
end

local function teleportBehindPlayer(target)
	local char = LocalPlayer.Character
	local targetChar = target.Character
	if char and targetChar and char:FindFirstChild("HumanoidRootPart") and targetChar:FindFirstChild("HumanoidRootPart") then
		local root = char.HumanoidRootPart
		local targetRoot = targetChar.HumanoidRootPart
		local backOffset = targetRoot.CFrame.LookVector * -distance
		local behindCFrame = targetRoot.CFrame + backOffset
		root.CFrame = CFrame.new(behindCFrame.Position, targetRoot.Position)
		if lockFirstPerson then
			Camera.CFrame = CFrame.new(root.Position, targetRoot.Position + targetRoot.CFrame.LookVector * 5)
		end
	end
end

killAllBtn.MouseButton1Click:Connect(function()
	if isKilling then return end
	if killLoop then
		killLoop = false
		killLoopActive = false
		stopKeyLabel.Visible = false
		killLoopBtn.Text = "Kill Loop: OFF"
		killLoopBtn.BackgroundColor3 = getTheme().BUTTON_COLOR
	end
	isKilling = true
	killAllBtn.Text = "Выполняю..."
	killAllBtn.BackgroundColor3 = Color3.fromRGB(220, 240, 255)
	progressLabel.Text = "Начато!"

	if lockFirstPerson then setFirstPersonLock(true) end

	local others = getAllOtherPlayers()
	local done = 0

	for i, target in ipairs(others) do
		if not isKilling then break end
		teleportBehindPlayer(target)
		if aimBot then aimAtTargetHead(target) end
		if autoFollow then
			followTarget(target)
			local t = 0
			while t < waitTime and isKilling do
				task.wait(0.05)
				t = t + 0.05
			end
			if followConnection then followConnection:Disconnect() followConnection = nil end
		else
			task.wait(waitTime)
		end
		if aimBot then stopAimBot() end
		done = i
		progressLabel.Text = string.format("Пройдено: %d/%d", done, #others)
	end

	progressLabel.Text = "Готово! Пройдено: "..done.."/"..#others
	killAllBtn.Text = "Kill All"
	killAllBtn.BackgroundColor3 = getTheme().BUTTON_COLOR
	isKilling = false

	if lockFirstPerson then setFirstPersonLock(false) end
	if followConnection then followConnection:Disconnect() followConnection = nil end
	stopAimBot()
end)

-- Kill Loop логика
local killLoopActive = false
local killLoopThread = nil

local function startKillLoop()
	if killLoopActive then return end
	killLoopActive = true
	killLoopBtn.Text = "Kill Loop: ON"
	killLoopBtn.BackgroundColor3 = Color3.fromRGB(255, 230, 120)
	stopKeyLabel.Visible = true

	killLoopThread = coroutine.create(function()
		while killLoop do
			isKilling = true
			killAllBtn.Text = "Выполняю..."
			killAllBtn.BackgroundColor3 = Color3.fromRGB(220, 240, 255)
			progressLabel.Text = "Kill Loop!"

			if lockFirstPerson then setFirstPersonLock(true) end

			local others = getAllOtherPlayers()
			local done = 0

			for i, target in ipairs(others) do
				if not killLoop then break end
				teleportBehindPlayer(target)
				if aimBot then aimAtTargetHead(target) end
				if autoFollow then
					followTarget(target)
					local t = 0
					while t < waitTime and killLoop do
						task.wait(0.05)
						t = t + 0.05
					end
					if followConnection then followConnection:Disconnect() followConnection = nil end
				else
					task.wait(waitTime)
				end
				if aimBot then stopAimBot() end
				done = i
				progressLabel.Text = string.format("Пройдено: %d/%d", done, #others)
			end

			progressLabel.Text = "Готово! Пройдено: "..done.."/"..#others
			killAllBtn.Text = "Kill All"
			killAllBtn.BackgroundColor3 = getTheme().BUTTON_COLOR
			isKilling = false

			if lockFirstPerson then setFirstPersonLock(false) end
			if followConnection then followConnection:Disconnect() followConnection = nil end
			stopAimBot()

			for i = 1, 20 do
				if not killLoop then break end
				task.wait(0.05)
			end
		end
		killLoopActive = false
		stopKeyLabel.Visible = false
		killLoopBtn.Text = "Kill Loop: OFF"
		killLoopBtn.BackgroundColor3 = getTheme().BUTTON_COLOR
	end)
	coroutine.resume(killLoopThread)
end

local function stopKillLoop()
	killLoop = false
	killLoopActive = false
	stopKeyLabel.Visible = false
	killLoopBtn.Text = "Kill Loop: OFF"
	killLoopBtn.BackgroundColor3 = getTheme().BUTTON_COLOR
end

killLoopBtn.MouseButton1Click:Connect(function()
	if killLoop then
		stopKillLoop()
	else
		killLoop = true
		startKillLoop()
	end
end)

UserInputService.InputBegan:Connect(function(input, gameProcessed)
	if killLoop and input.UserInputType == Enum.UserInputType.Keyboard and input.KeyCode == Enum.KeyCode.T and not gameProcessed then
		stopKillLoop()
	end
end)

mainGui.AncestryChanged:Connect(function(child, parent)
	if not parent then
		stopKillLoop()
	end
end)

killAllBtn.MouseButton1Click:Connect(function()
	if killLoop then
		stopKillLoop()
	end
end)

-- Применить тему при старте
applyTheme()

--[[
    Kill All V4 Full (сохранение выбранной темы между сессиями и играми)
    - Автоматически сохраняет выбранную тему в файл, если в инжекторе есть writefile/readfile/isfile
    - При запуске скрипта восстанавливает тему из файла, если он есть
    - Файл для сохранения: "KillAllV4Theme.txt"
    - Всё остальное работает как в твоём скрипте (6 тем, перекраска кнопок и т.д.)
]]

local THEME_SAVE_FILE = "KillAllV4Theme.txt"

local function canSave()
	return writefile and readfile and isfile
end

local themes = {
	[1] = {
		MENU_COLOR = Color3.fromRGB(230, 236, 245),
		BUTTON_COLOR = Color3.fromRGB(255, 255, 255),
		BUTTON_COLOR_ACT = Color3.fromRGB(200, 235, 255),
		TEXT = Color3.fromRGB(60, 80, 120),
		TITLE = Color3.fromRGB(80, 90, 110),
		NAME = "Светлая",
		ICON = "🎨",
	},
	[2] = {
		MENU_COLOR = Color3.fromRGB(33, 34, 44),
		BUTTON_COLOR = Color3.fromRGB(50, 55, 70),
		BUTTON_COLOR_ACT = Color3.fromRGB(45, 90, 120),
		TEXT = Color3.fromRGB(220, 230, 255),
		TITLE = Color3.fromRGB(130, 170, 245),
		NAME = "Тёмная",
		ICON = "🌙",
	},
	[3] = {
		MENU_COLOR = Color3.fromRGB(240, 235, 220),
		BUTTON_COLOR = Color3.fromRGB(255, 247, 210),
		BUTTON_COLOR_ACT = Color3.fromRGB(255, 210, 120),
		TEXT = Color3.fromRGB(150, 110, 40),
		TITLE = Color3.fromRGB(120, 90, 30),
		NAME = "Солнечная",
		ICON = "🌞",
	},
	[4] = {
		MENU_COLOR = Color3.fromRGB(50, 65, 60),
		BUTTON_COLOR = Color3.fromRGB(70, 120, 90),
		BUTTON_COLOR_ACT = Color3.fromRGB(80, 200, 130),
		TEXT = Color3.fromRGB(205, 255, 220),
		TITLE = Color3.fromRGB(170, 255, 170),
		NAME = "Зелёная",
		ICON = "🌿",
	},
	[5] = {
		MENU_COLOR = Color3.fromRGB(45, 40, 60),
		BUTTON_COLOR = Color3.fromRGB(90, 80, 130),
		BUTTON_COLOR_ACT = Color3.fromRGB(170, 140, 255),
		TEXT = Color3.fromRGB(255, 220, 255),
		TITLE = Color3.fromRGB(200, 160, 255),
		NAME = "Фиолетовая",
		ICON = "💜",
	},
	[6] = {
		MENU_COLOR = Color3.fromRGB(25, 30, 38),
		BUTTON_COLOR = Color3.fromRGB(32, 45, 75),
		BUTTON_COLOR_ACT = Color3.fromRGB(70, 120, 210),
		TEXT = Color3.fromRGB(255, 255, 255),
		TITLE = Color3.fromRGB(120, 180, 255),
		NAME = "Синяя",
		ICON = "🦋",
	}
}

-- Чтение выбранной темы из файла (или 1 если нет файла/ошибка)
local function loadThemeIndex()
	if canSave() and isfile(THEME_SAVE_FILE) then
		local str = readfile(THEME_SAVE_FILE)
		local idx = tonumber(str)
		if idx and themes[idx] then return idx end
	end
	return 1
end

-- Сохранение выбранной темы (индекса) в файл
local function saveThemeIndex(idx)
	if canSave() and themes[idx] then
		writefile(THEME_SAVE_FILE, tostring(idx))
	end
end

local currentTheme = loadThemeIndex() -- при запуске

local function getTheme()
	return themes[currentTheme]
end

-- Всё остальное как в твоём скрипте...

local FONT = Enum.Font.SourceSansSemibold
local MENU_SIZE = UDim2.new(0, 249, 0, 395)
local BUTTON_HEIGHT = 30
local BUTTON_PADDING = 4

local DEFAULT_WAIT_TIME = 0.5
local MIN_WAIT_TIME = 0.5
local MAX_WAIT_TIME = 2.5
local MAX_DELAY_BUTTONS = 5

local DEFAULT_DISTANCE = 1
local MIN_DISTANCE = 1
local MAX_DISTANCE = 10

local Players = game:GetService("Players")
local LocalPlayer = Players.LocalPlayer
local UserInputService = game:GetService("UserInputService")
local RunService = game:GetService("RunService")
local Camera = workspace.CurrentCamera

if LocalPlayer.PlayerGui:FindFirstChild("KillAllV4Menu") then
	LocalPlayer.PlayerGui.KillAllV4Menu:Destroy()
end

local mainGui = Instance.new("ScreenGui")
mainGui.Name = "KillAllV4Menu"
mainGui.ResetOnSpawn = false
mainGui.Parent = LocalPlayer.PlayerGui

local menuFrame = Instance.new("Frame")
menuFrame.Size = MENU_SIZE
menuFrame.Position = UDim2.new(0, 36, 0, 120)
menuFrame.BackgroundColor3 = getTheme().MENU_COLOR
menuFrame.BorderSizePixel = 0
menuFrame.Active = true
menuFrame.Draggable = true
menuFrame.Name = "Menu"
menuFrame.Parent = mainGui

-- Кнопка-дизайнер в левом верхнем углу
local designerBtn = Instance.new("TextButton")
designerBtn.Size = UDim2.new(0, 28, 0, 28)
designerBtn.Position = UDim2.new(0, 4, 0, 4)
designerBtn.BackgroundTransparency = 1
designerBtn.Text = getTheme().ICON or "🎨"
designerBtn.Font = FONT
designerBtn.TextSize = 20
designerBtn.TextColor3 = getTheme().TEXT
designerBtn.ZIndex = 11
designerBtn.Parent = menuFrame

-- ... (оставшаяся часть твоего скрипта полностью без изменений)

-- Переключение темы (цветов)
designerBtn.MouseButton1Click:Connect(function()
	currentTheme = currentTheme + 1
	if currentTheme > #themes then currentTheme = 1 end
	saveThemeIndex(currentTheme) -- сохраняем выбор
	applyTheme()
	updateDelayButtons(findDelayIndex(waitTime))
	progressLabel.Text = "Тема: " .. getTheme().NAME
end)

-- Применить тему при старте
applyTheme()

--[[
    KillAllV4 with persistent theme (автоматическое сохранение и загрузка темы между всеми играми/плейсами)
    - Файл темы: "SSInjectorData/KillAllV4Theme.txt"
    - Папка создается автоматически
    - Тема применяется автоматически при запуске
    - Аналогично твоему примеру с tabs: readfile/writefile/isfile/appendfile поддерживаются всеми популярными инжекторами
]]

local themeFolder = "SSInjectorData"
local themeFile = themeFolder.."/KillAllV4Theme.txt"

-- Проверка/создание папки
local function ensureFolder()
	if not isfolder or not makefolder then return end
	if not isfolder(themeFolder) then
		makefolder(themeFolder)
	end
end

local function canSave()
	return writefile and readfile and isfile and makefolder and isfolder
end

local themes = {
	[1] = {
		MENU_COLOR = Color3.fromRGB(230, 236, 245),
		BUTTON_COLOR = Color3.fromRGB(255, 255, 255),
		BUTTON_COLOR_ACT = Color3.fromRGB(200, 235, 255),
		TEXT = Color3.fromRGB(60, 80, 120),
		TITLE = Color3.fromRGB(80, 90, 110),
		NAME = "Светлая",
		ICON = "🎨",
	},
	[2] = {
		MENU_COLOR = Color3.fromRGB(33, 34, 44),
		BUTTON_COLOR = Color3.fromRGB(50, 55, 70),
		BUTTON_COLOR_ACT = Color3.fromRGB(45, 90, 120),
		TEXT = Color3.fromRGB(220, 230, 255),
		TITLE = Color3.fromRGB(130, 170, 245),
		NAME = "Тёмная",
		ICON = "🌙",
	},
	[3] = {
		MENU_COLOR = Color3.fromRGB(240, 235, 220),
		BUTTON_COLOR = Color3.fromRGB(255, 247, 210),
		BUTTON_COLOR_ACT = Color3.fromRGB(255, 210, 120),
		TEXT = Color3.fromRGB(150, 110, 40),
		TITLE = Color3.fromRGB(120, 90, 30),
		NAME = "Солнечная",
		ICON = "🌞",
	},
	[4] = {
		MENU_COLOR = Color3.fromRGB(50, 65, 60),
		BUTTON_COLOR = Color3.fromRGB(70, 120, 90),
		BUTTON_COLOR_ACT = Color3.fromRGB(80, 200, 130),
		TEXT = Color3.fromRGB(205, 255, 220),
		TITLE = Color3.fromRGB(170, 255, 170),
		NAME = "Зелёная",
		ICON = "🌿",
	},
	[5] = {
		MENU_COLOR = Color3.fromRGB(45, 40, 60),
		BUTTON_COLOR = Color3.fromRGB(90, 80, 130),
		BUTTON_COLOR_ACT = Color3.fromRGB(170, 140, 255),
		TEXT = Color3.fromRGB(255, 220, 255),
		TITLE = Color3.fromRGB(200, 160, 255),
		NAME = "Фиолетовая",
		ICON = "💜",
	},
	[6] = {
		MENU_COLOR = Color3.fromRGB(25, 30, 38),
		BUTTON_COLOR = Color3.fromRGB(32, 45, 75),
		BUTTON_COLOR_ACT = Color3.fromRGB(70, 120, 210),
		TEXT = Color3.fromRGB(255, 255, 255),
		TITLE = Color3.fromRGB(120, 180, 255),
		NAME = "Синяя",
		ICON = "🦋",
	}
}

-- Функция автосохранения индекса темы
local function saveThemeIndex(idx)
	if canSave() and themes[idx] then
		ensureFolder()
		writefile(themeFile, tostring(idx))
	end
end

-- Функция авто-загрузки темы
local function loadThemeIndex()
	if canSave() and isfile(themeFile) then
		local str = readfile(themeFile)
		local idx = tonumber(str)
		if idx and themes[idx] then return idx end
	end
	return 1
end

local currentTheme = loadThemeIndex() -- Тема ПРИМЕНЯЕТСЯ автоматически при запуске!

local function getTheme()
	return themes[currentTheme]
end

-- ... далее остальной твой скрипт БЕЗ изменений, кроме designerBtn.MouseButton1Click

-- Пример правильного обработчика кнопки смены темы:
designerBtn.MouseButton1Click:Connect(function()
	currentTheme = currentTheme + 1
	if currentTheme > #themes then currentTheme = 1 end
	saveThemeIndex(currentTheme) -- сохраняем выбор при каждом нажатии
	applyTheme()
	updateDelayButtons(findDelayIndex(waitTime))
	progressLabel.Text = "Тема: " .. getTheme().NAME
end)

-- В конце, когда всё GUI создано:
applyTheme()
