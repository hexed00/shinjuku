--[[
    EMORCE DEMONS v2.1+ — AXION+ EDITION
    Full Orca-style UI - Red Theme
    Starts on Scripts | Local image caching | Working themes | Floating Widget Toggle
    NEW IN v2.1 (AXION+):
      + INFINITE YIELD & AZURE MODDED script cards (with cached images)
      + Fly Speed / WalkSpeed / JumpPower SLIDERS (fly bar + jump bar)
      + Server JobId SEARCH BAR — paste a server id, find it or force join it
      + Copy button right on the current server row
      + Friends in server counter (X/Y) + friend hearts on the player list
      + Rich notifications — icons, slide-in, live progress bar, per-script names
      + Script hub search bar + category filter chips
      + Session stats card (uptime, scripts executed, last executed)
      + Custom keybinds (F fly / N noclip / J infinite jump) — toggleable
      + CHAT SPY TOGGLE on Options — "emorce chat spy enabled"
      + ADMIN CMDS (.tp / .spec / .unspec) with ON/OFF toggle
      + DES HOOD STAND bot (_G.BotOwner)
    KEPT FROM v2.0:
      Server browser, premium profile, expanded hub, live player list,
      keybind system, ESP preview, more scripts, better UX,
      Unspectate button on Players page, Map Cleaner in Quick Actions,
      Shinjuku Pack uses Axion's clean scripts
]]
if not game:IsLoaded() then
    game.Loaded:Wait()
end
local Players = game:GetService("Players")
local TweenService = game:GetService("TweenService")
local UserInputService = game:GetService("UserInputService")
local RunService = game:GetService("RunService")
local HttpService = game:GetService("HttpService")
local CoreGui = game:GetService("CoreGui")
local TeleportService = game:GetService("TeleportService")
local StarterGui = game:GetService("StarterGui")
local Lighting = game:GetService("Lighting")
local ReplicatedStorage = game:GetService("ReplicatedStorage")
local TextChatService = game:GetService("TextChatService")
local player = Players.LocalPlayer
local mouse = player:GetMouse()
-- ========== SAFE CLIPBOARD ==========
local function Copy(text)
    if setclipboard then
        setclipboard(text)
        return true
    end
    return false
end
local function CopyNotify(text, label)
    if Copy(text) then
        Notify("Copied", label .. " copied to clipboard", 2, Theme.Success, "⧉")
    else
        Notify("Clipboard", "Executor does not support setclipboard", 3, Theme.Warning, "!")
    end
end
-- ========== LOCAL IMAGE CACHING ==========
local shinImageUrl = "https://i.pinimg.com/736x/42/de/d5/42ded506cb69f48fad09de00cdf3e54f.jpg"
local zeeImageUrl = "https://i.pinimg.com/736x/25/be/32/25be32ec558bcebae21b2c49e81c7f63.jpg"
local fishingImageUrl = "https://i.pinimg.com/736x/1c/67/72/1c6772582c706e811b6e9f7419d539f8.jpg"
local flyImageUrl = "https://i.pinimg.com/736x/51/84/12/5184126423b1a422eec70dd5fe2953aa.jpg"
local tpImageUrl = "https://i.pinimg.com/736x/3e/ab/96/3eab967f64db0eb2b2c1832a25062afa.jpg"
local matchaImageUrl = "https://i.pinimg.com/736x/1f/65/2b/1f652b430fbf71f4e8f7ccd4855c79cd.jpg"
local profileImageUrl = "https://i.pinimg.com/736x/7c/0c/8b/7c0c8bea6a5492d3a5ce847af5aaee87.jpg"
local optiImageUrl = "https://i.pinimg.com/736x/72/bb/b4/72bbb4403fa7299de4fba8e138982b6b.jpg"
local gazerImageUrl = "https://i.pinimg.com/736x/e1/9c/07/e19c070bfb9c2a5f087a9953725cd0cd.jpg"
local limbImageUrl = "https://i.pinimg.com/736x/cc/2e/be/cc2ebe5ca1f5d5399ec24ae1b0197a4e.jpg"
local aimbotImageUrl = "https://i.pinimg.com/736x/34/39/a1/3439a1d3c7a258d44c72f0db2f73a0e6.jpg"
local drivingImageUrl = "https://i.pinimg.com/736x/5e/5b/90/5e5b9063f868d63dfd773ecc02400327.jpg"
local infYieldImageUrl = "https://i.pinimg.com/736x/1d/5d/58/1d5d58d39a8337241d1dfad4068c37f5.jpg"
local azureImageUrl = "https://i.pinimg.com/736x/2a/6c/73/2a6c73eaa84ea9a275abbc773784f5bf.jpg"
local nightsImageUrl = "https://i.pinimg.com/1200x/d5/05/45/d505453274884456a103151437c010f9.jpg"
local desHoodImageUrl = "https://i.pinimg.com/736x/d8/d4/df/d8d4dfc3b4079cb054a591a9342248cf.jpg"
local shinImagePath = "emorce_shinjuku.png"
local zeeImagePath = "emorce_zee.png"
local fishingImagePath = "emorce_fishing.png"
local flyImagePath = "emorce_fly.png"
local tpImagePath = "emorce_tp.png"
local matchaImagePath = "emorce_matcha.png"
local profileImagePath = "emorce_profile.png"
local optiImagePath = "emorce_opti.png"
local gazerImagePath = "emorce_gazer.png"
local limbImagePath = "emorce_limb.png"
local aimbotImagePath = "emorce_aimbot.png"
local drivingImagePath = "emorce_driving.png"
local infYieldImagePath = "emorce_infyield.png"
local azureImagePath = "emorce_azure.png"
local nightsImagePath = "emorce_nights.png"
local desHoodImagePath = "emorce_deshood.png"
pcall(function()
    writefile(shinImagePath, game:HttpGet(shinImageUrl))
    writefile(zeeImagePath, game:HttpGet(zeeImageUrl))
    writefile(fishingImagePath, game:HttpGet(fishingImageUrl))
    writefile(flyImagePath, game:HttpGet(flyImageUrl))
    writefile(tpImagePath, game:HttpGet(tpImageUrl))
    writefile(matchaImagePath, game:HttpGet(matchaImageUrl))
    writefile(profileImagePath, game:HttpGet(profileImageUrl))
    writefile(optiImagePath, game:HttpGet(optiImageUrl))
    writefile(gazerImagePath, game:HttpGet(gazerImageUrl))
    writefile(limbImagePath, game:HttpGet(limbImageUrl))
    writefile(aimbotImagePath, game:HttpGet(aimbotImageUrl))
    writefile(drivingImagePath, game:HttpGet(drivingImageUrl))
    writefile(infYieldImagePath, game:HttpGet(infYieldImageUrl))
    writefile(azureImagePath, game:HttpGet(azureImageUrl))
    writefile(nightsImagePath, game:HttpGet(nightsImageUrl))
    writefile(desHoodImagePath, game:HttpGet(desHoodImageUrl))
end)
local function getImage(path)
    if isfile and isfile(path) then
        if getsynasset then
            return getsynasset(path)
        elseif getcustomasset then
            return getcustomasset(path)
        end
    end
    return ""
end
-- Theme
local Theme = {
    Background = Color3.fromRGB(12, 12, 14),
    Surface = Color3.fromRGB(22, 22, 26),
    SurfaceHover = Color3.fromRGB(32, 32, 38),
    Accent = Color3.fromRGB(220, 30, 40),
    AccentDark = Color3.fromRGB(160, 20, 30),
    AccentLight = Color3.fromRGB(255, 70, 80),
    Text = Color3.fromRGB(255, 255, 255),
    TextDim = Color3.fromRGB(180, 180, 190),
    TextMuted = Color3.fromRGB(120, 120, 130),
    Border = Color3.fromRGB(40, 40, 48),
    Success = Color3.fromRGB(50, 200, 100),
    Danger = Color3.fromRGB(255, 60, 60),
    Warning = Color3.fromRGB(255, 180, 40),
    Info = Color3.fromRGB(60, 140, 255),
    Friend = Color3.fromRGB(255, 90, 160),
}
local State = {
    Open = true,
    CurrentPage = "Scripts",
    Flight = false,
    FlySpeed = 80,
    Speed = 16,
    Jump = 50,
    IsWidget = false,
    Noclip = false,
    InfiniteJump = false,
    ESP = false,
    Fullbright = false,
    AntiAFK = true,
    WalkSpeed = 16,
    JumpPower = 50,
    SelectedPlayer = nil,
    ServerList = {},
    Notifications = {},
    ServerJobs = {},
    TotalFriends = nil,
    FriendCache = {},
    ExecCount = 0,
    LastExec = "—",
    SessionStart = os.clock(),
    SessionLabels = nil,
    CurrentFilter = "All",
    SearchText = "",
    CustomKeybinds = false,
    ChatSpy = true,
    AdminCmds = true,
}
-- Cleanup
pcall(function()
    if CoreGui:FindFirstChild("EmorceDemons") then
        CoreGui.EmorceDemons:Destroy()
    end
end)
local ScreenGui = Instance.new("ScreenGui")
ScreenGui.Name = "EmorceDemons"
ScreenGui.ResetOnSpawn = false
ScreenGui.ZIndexBehavior = Enum.ZIndexBehavior.Sibling
ScreenGui.IgnoreGuiInset = true
ScreenGui.Parent = CoreGui
-- ========== NOTIFICATION SYSTEM v2 ==========
local NotifContainer = Instance.new("Frame")
NotifContainer.Name = "NotifContainer"
NotifContainer.Size = UDim2.new(0, 320, 1, 0)
NotifContainer.Position = UDim2.new(1, -340, 0, 20)
NotifContainer.BackgroundTransparency = 1
NotifContainer.Parent = ScreenGui
local NotifLayout = Instance.new("UIListLayout")
NotifLayout.Padding = UDim.new(0, 8)
NotifLayout.SortOrder = Enum.SortOrder.LayoutOrder
NotifLayout.VerticalAlignment = Enum.VerticalAlignment.Top
NotifLayout.Parent = NotifContainer
local function Notify(title, message, duration, color, icon)
    duration = duration or 3
    color = color or Theme.Accent
    icon = icon or "✔"
    local notif = Instance.new("Frame")
    notif.Size = UDim2.new(1, 0, 0, 64)
    notif.BackgroundColor3 = Theme.Surface
    notif.BorderSizePixel = 0
    notif.Position = UDim2.new(0, 40, 0, 0)
    notif.Parent = NotifContainer
    local nc = Instance.new("UICorner")
    nc.CornerRadius = UDim.new(0, 10)
    nc.Parent = notif
    local stroke = Instance.new("UIStroke")
    stroke.Color = color
    stroke.Thickness = 2
    stroke.Parent = notif
    local iconBg = Instance.new("Frame")
    iconBg.Size = UDim2.new(0, 34, 0, 34)
    iconBg.Position = UDim2.new(0, 12, 0, 14)
    iconBg.BackgroundColor3 = color
    iconBg.BorderSizePixel = 0
    iconBg.Parent = notif
    local iconC = Instance.new("UICorner")
    iconC.CornerRadius = UDim.new(1, 0)
    iconC.Parent = iconBg
    local iconL = Instance.new("TextLabel")
    iconL.Size = UDim2.new(1, 0, 1, 0)
    iconL.BackgroundTransparency = 1
    iconL.Text = icon
    iconL.TextColor3 = Color3.fromRGB(255, 255, 255)
    iconL.TextSize = 16
    iconL.Font = Enum.Font.GothamBold
    iconL.Parent = iconBg
    local bar = Instance.new("Frame")
    bar.Size = UDim2.new(0, 4, 1, -8)
    bar.Position = UDim2.new(0, 0, 0, 4)
    bar.BackgroundColor3 = color
    bar.BorderSizePixel = 0
    bar.Parent = notif
    local titleL = Instance.new("TextLabel")
    titleL.Size = UDim2.new(1, -70, 0, 20)
    titleL.Position = UDim2.new(0, 56, 0, 10)
    titleL.BackgroundTransparency = 1
    titleL.Text = title
    titleL.TextColor3 = Theme.Text
    titleL.TextSize = 14
    titleL.Font = Enum.Font.GothamBold
    titleL.TextXAlignment = Enum.TextXAlignment.Left
    titleL.TextTruncate = Enum.TextTruncate.AtEnd
    titleL.Parent = notif
    local msgL = Instance.new("TextLabel")
    msgL.Size = UDim2.new(1, -70, 0, 26)
    msgL.Position = UDim2.new(0, 56, 0, 30)
    msgL.BackgroundTransparency = 1
    msgL.Text = message
    msgL.TextColor3 = Theme.TextDim
    msgL.TextSize = 12
    msgL.Font = Enum.Font.Gotham
    msgL.TextXAlignment = Enum.TextXAlignment.Left
    msgL.TextYAlignment = Enum.TextYAlignment.Top
    msgL.TextWrapped = true
    msgL.Parent = notif
    local progress = Instance.new("Frame")
    progress.Size = UDim2.new(1, -8, 0, 3)
    progress.Position = UDim2.new(0, 4, 1, -5)
    progress.BackgroundColor3 = color
    progress.BackgroundTransparency = 0.35
    progress.BorderSizePixel = 0
    progress.Parent = notif
    local pc2 = Instance.new("UICorner")
    pc2.CornerRadius = UDim.new(1, 0)
    pc2.Parent = progress
    notif.BackgroundTransparency = 1
    iconBg.BackgroundTransparency = 1
    for _, c in pairs(notif:GetDescendants()) do
        if c:IsA("TextLabel") then c.TextTransparency = 1 end
        if c:IsA("UIStroke") then c.Transparency = 1 end
        if c:IsA("Frame") and c ~= notif then c.BackgroundTransparency = 1 end
    end
    TweenService:Create(notif, TweenInfo.new(0.3, Enum.EasingStyle.Quad, Enum.EasingDirection.Out), {
        BackgroundTransparency = 0,
        Position = UDim2.new(0, 0, 0, 0)
    }):Play()
    TweenService:Create(iconBg, TweenInfo.new(0.3), {BackgroundTransparency = 0}):Play()
    for _, c in pairs(notif:GetDescendants()) do
        if c:IsA("TextLabel") then
            TweenService:Create(c, TweenInfo.new(0.3), {TextTransparency = 0}):Play()
        end
        if c:IsA("UIStroke") then
            TweenService:Create(c, TweenInfo.new(0.3), {Transparency = 0}):Play()
        end
        if c:IsA("Frame") and c ~= notif then
            TweenService:Create(c, TweenInfo.new(0.3), {BackgroundTransparency = 0}):Play()
        end
    end
    TweenService:Create(progress, TweenInfo.new(duration, Enum.EasingStyle.Linear), {
        Size = UDim2.new(0, 0, 0, 3)
    }):Play()
    task.delay(duration, function()
        if not notif.Parent then return end
        TweenService:Create(notif, TweenInfo.new(0.35), {
            BackgroundTransparency = 1,
            Position = UDim2.new(0, 40, 0, 0)
        }):Play()
        TweenService:Create(iconBg, TweenInfo.new(0.35), {BackgroundTransparency = 1}):Play()
        for _, c in pairs(notif:GetDescendants()) do
            if c:IsA("TextLabel") then
                TweenService:Create(c, TweenInfo.new(0.35), {TextTransparency = 1}):Play()
            end
            if c:IsA("UIStroke") then
                TweenService:Create(c, TweenInfo.new(0.35), {Transparency = 1}):Play()
            end
            if c:IsA("Frame") and c ~= notif then
                TweenService:Create(c, TweenInfo.new(0.35), {BackgroundTransparency = 1}):Play()
            end
        end
        task.wait(0.45)
        notif:Destroy()
    end)
end

-- ========== CHAT SPY ==========
local chatWindow = TextChatService:FindFirstChild("ChatWindowConfiguration")
local function SetChatSpy(enabled)
    State.ChatSpy = enabled
    if chatWindow then
        pcall(function() chatWindow.Enabled = enabled end)
    end
    Notify("Chat Spy", enabled and "emorce chat spy enabled" or "emorce chat spy disabled", 3, enabled and Theme.Success or Theme.Info, "💬")
end

-- Keep chat spy alive while enabled
task.spawn(function()
    while task.wait(1.5) do
        if State.ChatSpy and chatWindow then
            pcall(function() chatWindow.Enabled = true end)
        end
    end
end)

-- ========== MAIN WINDOW ==========
local Main = Instance.new("Frame")
Main.Name = "Main"
Main.Size = UDim2.new(0, 980, 0, 620)
Main.Position = UDim2.new(0.5, -490, 0.5, -310)
Main.BackgroundColor3 = Theme.Background
Main.BorderSizePixel = 0
Main.ClipsDescendants = true
Main.Parent = ScreenGui
local MainCorner = Instance.new("UICorner")
MainCorner.CornerRadius = UDim.new(0, 18)
MainCorner.Parent = Main
local MainStroke = Instance.new("UIStroke")
MainStroke.Color = Theme.Accent
MainStroke.Thickness = 2
MainStroke.Transparency = 0.4
MainStroke.Parent = Main
-- Drag
local dragging, dragStart, startPos
Main.InputBegan:Connect(function(input)
    if input.UserInputType == Enum.UserInputType.MouseButton1 then
        dragging = true
        dragStart = input.Position
        startPos = Main.Position
    end
end)
UserInputService.InputChanged:Connect(function(input)
    if dragging and input.UserInputType == Enum.UserInputType.MouseMovement then
        local delta = input.Position - dragStart
        Main.Position = UDim2.new(startPos.X.Scale, startPos.X.Offset + delta.X, startPos.Y.Scale, startPos.Y.Offset + delta.Y)
    end
end)
UserInputService.InputEnded:Connect(function(input)
    if input.UserInputType == Enum.UserInputType.MouseButton1 then
        dragging = false
    end
end)
-- ========== SIDEBAR ==========
local Sidebar = Instance.new("Frame")
Sidebar.Name = "Sidebar"
Sidebar.Size = UDim2.new(0, 78, 1, 0)
Sidebar.BackgroundColor3 = Color3.fromRGB(16, 16, 20)
Sidebar.BorderSizePixel = 0
Sidebar.Parent = Main
local SideCorner = Instance.new("UICorner")
SideCorner.CornerRadius = UDim.new(0, 18)
SideCorner.Parent = Sidebar
local Logo = Instance.new("TextLabel")
Logo.Size = UDim2.new(1, 0, 0, 58)
Logo.BackgroundTransparency = 1
Logo.Text = "ED"
Logo.TextColor3 = Theme.Accent
Logo.TextScaled = true
Logo.Font = Enum.Font.GothamBlack
Logo.Parent = Sidebar
local LogoSub = Instance.new("TextLabel")
LogoSub.Size = UDim2.new(1, 0, 0, 14)
LogoSub.Position = UDim2.new(0, 0, 0, 48)
LogoSub.BackgroundTransparency = 1
LogoSub.Text = "v2.1+"
LogoSub.TextColor3 = Theme.TextMuted
LogoSub.TextSize = 11
LogoSub.Font = Enum.Font.Gotham
LogoSub.Parent = Sidebar
local NavContainer = Instance.new("Frame")
NavContainer.Size = UDim2.new(1, 0, 1, -160)
NavContainer.Position = UDim2.new(0, 0, 0, 70)
NavContainer.BackgroundTransparency = 1
NavContainer.Parent = Sidebar
local NavList = Instance.new("UIListLayout")
NavList.Padding = UDim.new(0, 6)
NavList.HorizontalAlignment = Enum.HorizontalAlignment.Center
NavList.SortOrder = Enum.SortOrder.LayoutOrder
NavList.Parent = NavContainer
local Content = Instance.new("Frame")
Content.Name = "Content"
Content.Size = UDim2.new(1, -78, 1, 0)
Content.Position = UDim2.new(0, 78, 0, 0)
Content.BackgroundTransparency = 1
Content.Parent = Main
local Pages = {}
local function CreatePage(name)
    local page = Instance.new("Frame")
    page.Name = name
    page.Size = UDim2.new(1, 0, 1, 0)
    page.BackgroundTransparency = 1
    page.Visible = false
    page.Parent = Content
    Pages[name] = page
    return page
end
local function MakeNav(name, icon, order)
    local btn = Instance.new("TextButton")
    btn.Name = name
    btn.Size = UDim2.new(0, 52, 0, 52)
    btn.BackgroundColor3 = name == State.CurrentPage and Theme.Accent or Color3.fromRGB(28, 28, 34)
    btn.Text = icon
    btn.TextColor3 = Theme.Text
    btn.TextSize = 20
    btn.Font = Enum.Font.GothamBold
    btn.LayoutOrder = order
    btn.Parent = NavContainer
    local c = Instance.new("UICorner")
    c.CornerRadius = UDim.new(0, 12)
    c.Parent = btn
    btn.MouseButton1Click:Connect(function()
        State.CurrentPage = name
        for _, b in pairs(NavContainer:GetChildren()) do
            if b:IsA("TextButton") then
                TweenService:Create(b, TweenInfo.new(0.2), {
                    BackgroundColor3 = b.Name == name and Theme.Accent or Color3.fromRGB(28, 28, 34)
                }):Play()
            end
        end
        UpdatePages()
    end)
    return btn
end
MakeNav("Scripts", "⚡", 1)
MakeNav("Home", "⌂", 2)
MakeNav("Apps", "⊞", 3)
MakeNav("Servers", "🌐", 4)
MakeNav("Players", "👤", 5)
MakeNav("Options", "⚙", 6)
-- Close / Widget buttons
local CloseBtn = Instance.new("TextButton")
CloseBtn.Size = UDim2.new(0, 28, 0, 28)
CloseBtn.Position = UDim2.new(1, -40, 0, 12)
CloseBtn.BackgroundTransparency = 1
CloseBtn.Text = "✕"
CloseBtn.TextColor3 = Theme.AccentLight
CloseBtn.TextSize = 18
CloseBtn.Font = Enum.Font.GothamBold
CloseBtn.Parent = Main
CloseBtn.MouseButton1Click:Connect(function()
    Main.Visible = false
end)
local WidgetBtn = Instance.new("TextButton")
WidgetBtn.Size = UDim2.new(0, 42, 0, 42)
WidgetBtn.Position = UDim2.new(1, -58, 0, 12)
WidgetBtn.BackgroundColor3 = Color3.fromRGB(0, 180, 60)
WidgetBtn.Text = "◉"
WidgetBtn.TextColor3 = Theme.Text
WidgetBtn.TextSize = 22
WidgetBtn.Font = Enum.Font.GothamBold
WidgetBtn.Parent = Main
local WidgetStroke = Instance.new("UIStroke")
WidgetStroke.Color = Color3.fromRGB(0, 255, 100)
WidgetStroke.Thickness = 2
WidgetStroke.Parent = WidgetBtn
local WBCorner = Instance.new("UICorner")
WBCorner.CornerRadius = UDim.new(1, 0)
WBCorner.Parent = WidgetBtn
-- ========== SLIDER FACTORY ==========
local function CreateSlider(parent, title, minV, maxV, default, yPos, callback)
    local container = Instance.new("Frame")
    container.Size = UDim2.new(1, -32, 0, 54)
    container.Position = UDim2.new(0, 16, 0, yPos)
    container.BackgroundColor3 = Color3.fromRGB(30, 22, 28)
    container.BorderSizePixel = 0
    container.Parent = parent
    local cc = Instance.new("UICorner")
    cc.CornerRadius = UDim.new(0, 8)
    cc.Parent = container
    local titleL = Instance.new("TextLabel")
    titleL.Size = UDim2.new(1, -16, 0, 18)
    titleL.Position = UDim2.new(0, 12, 0, 6)
    titleL.BackgroundTransparency = 1
    titleL.Text = title .. ": " .. tostring(default)
    titleL.TextColor3 = Theme.Text
    titleL.TextSize = 12
    titleL.Font = Enum.Font.GothamBold
    titleL.TextXAlignment = Enum.TextXAlignment.Left
    titleL.Parent = container
    local track = Instance.new("Frame")
    track.Size = UDim2.new(1, -24, 0, 6)
    track.Position = UDim2.new(0, 12, 0, 36)
    track.BackgroundColor3 = Color3.fromRGB(50, 35, 42)
    track.BorderSizePixel = 0
    track.Parent = container
    local tc = Instance.new("UICorner")
    tc.CornerRadius = UDim.new(1, 0)
    tc.Parent = track
    local fill = Instance.new("Frame")
    fill.Size = UDim2.new(0, 0, 1, 0)
    fill.BackgroundColor3 = Theme.Accent
    fill.BorderSizePixel = 0
    fill.Parent = track
    local fc = Instance.new("UICorner")
    fc.CornerRadius = UDim.new(1, 0)
    fc.Parent = fill
    local knob = Instance.new("Frame")
    knob.Size = UDim2.new(0, 14, 0, 14)
    knob.Position = UDim2.new(0, -7, 0.5, -7)
    knob.BackgroundColor3 = Theme.AccentLight
    knob.BorderSizePixel = 0
    knob.ZIndex = 2
    knob.Parent = track
    local kc = Instance.new("UICorner")
    kc.CornerRadius = UDim.new(1, 0)
    kc.Parent = knob
    local kstroke = Instance.new("UIStroke")
    kstroke.Color = Color3.fromRGB(255, 255, 255)
    kstroke.Thickness = 1.5
    kstroke.Transparency = 0.3
    kstroke.Parent = knob
    local slider = {Value = default}
    local silent = true
    local function SetValue(newVal, fireCallback)
        newVal = math.clamp(math.floor(newVal + 0.5), minV, maxV)
        slider.Value = newVal
        local pct = (newVal - minV) / (maxV - minV)
        fill.Size = UDim2.new(pct, 0, 1, 0)
        knob.Position = UDim2.new(pct, -7, 0.5, -7)
        titleL.Text = title .. ": " .. tostring(newVal)
        if fireCallback and callback then
            task.spawn(callback, newVal)
        end
    end
    local function SetFromX(x)
        local rel = math.clamp((x - track.AbsolutePosition.X) / math.abs(track.AbsoluteSize.X), 0, 1)
        SetValue(minV + (maxV - minV) * rel, not silent)
    end
    local draggingSlider = false
    track.InputBegan:Connect(function(input)
        if input.UserInputType == Enum.UserInputType.MouseButton1 then
            draggingSlider = true
            SetFromX(input.Position.X)
        end
    end)
    knob.InputBegan:Connect(function(input)
        if input.UserInputType == Enum.UserInputType.MouseButton1 then
            draggingSlider = true
        end
    end)
    UserInputService.InputChanged:Connect(function(input)
        if draggingSlider and input.UserInputType == Enum.UserInputType.MouseMovement then
            SetFromX(input.Position.X)
        end
    end)
    UserInputService.InputEnded:Connect(function(input)
        if input.UserInputType == Enum.UserInputType.MouseButton1 then
            draggingSlider = false
        end
    end)
    SetValue(default, false)
    silent = false
    slider.Set = SetValue
    slider.Label = titleL
    slider.Container = container
    return slider
end
-- ========== SCRIPTS PAGE ==========
local ScriptsPage = CreatePage("Scripts")
local ScriptsTitle = Instance.new("TextLabel")
ScriptsTitle.Size = UDim2.new(1, -40, 0, 40)
ScriptsTitle.Position = UDim2.new(0, 24, 0, 16)
ScriptsTitle.BackgroundTransparency = 1
ScriptsTitle.Text = "Script Hub"
ScriptsTitle.TextColor3 = Theme.Text
ScriptsTitle.TextSize = 26
ScriptsTitle.Font = Enum.Font.GothamBlack
ScriptsTitle.TextXAlignment = Enum.TextXAlignment.Left
ScriptsTitle.Parent = ScriptsPage
local ScriptsSub = Instance.new("TextLabel")
ScriptsSub.Size = UDim2.new(1, -40, 0, 18)
ScriptsSub.Position = UDim2.new(0, 24, 0, 48)
ScriptsSub.BackgroundTransparency = 1
ScriptsSub.Text = "Axion+ edition • 15 scripts • search + filters"
ScriptsSub.TextColor3 = Theme.TextMuted
ScriptsSub.TextSize = 12
ScriptsSub.Font = Enum.Font.Gotham
ScriptsSub.TextXAlignment = Enum.TextXAlignment.Left
ScriptsSub.Parent = ScriptsPage
local ScriptSearch = Instance.new("TextBox")
ScriptSearch.Size = UDim2.new(0.55, 0, 0, 34)
ScriptSearch.Position = UDim2.new(0, 24, 0, 72)
ScriptSearch.BackgroundColor3 = Color3.fromRGB(28, 22, 26)
ScriptSearch.Text = ""
ScriptSearch.PlaceholderText = "🔍 Search scripts..."
ScriptSearch.TextColor3 = Theme.Text
ScriptSearch.PlaceholderColor3 = Theme.TextMuted
ScriptSearch.TextSize = 13
ScriptSearch.Font = Enum.Font.Gotham
ScriptSearch.ClearTextOnFocus = false
ScriptSearch.TextXAlignment = Enum.TextXAlignment.Left
ScriptSearch.Parent = ScriptsPage
local SSCorner = Instance.new("UICorner")
SSCorner.CornerRadius = UDim.new(0, 8)
SSCorner.Parent = ScriptSearch
local SSStroke = Instance.new("UIStroke")
SSStroke.Color = Theme.Border
SSStroke.Thickness = 1
SSStroke.Parent = ScriptSearch
local SSPad = Instance.new("UIPadding")
SSPad.PaddingLeft = UDim.new(0, 10)
SSPad.Parent = ScriptSearch
local ResultsLabel = Instance.new("TextLabel")
ResultsLabel.Size = UDim2.new(0, 200, 0, 34)
ResultsLabel.Position = UDim2.new(0.55, 34, 0, 72)
ResultsLabel.BackgroundTransparency = 1
ResultsLabel.Text = ""
ResultsLabel.TextColor3 = Theme.TextMuted
ResultsLabel.TextSize = 12
ResultsLabel.Font = Enum.Font.Gotham
ResultsLabel.TextXAlignment = Enum.TextXAlignment.Left
ResultsLabel.Parent = ScriptsPage
local ChipsRow = Instance.new("Frame")
ChipsRow.Size = UDim2.new(1, -40, 0, 30)
ChipsRow.Position = UDim2.new(0, 24, 0, 112)
ChipsRow.BackgroundTransparency = 1
ChipsRow.Parent = ScriptsPage
local ChipsList = Instance.new("UIListLayout")
ChipsList.FillDirection = Enum.FillDirection.Horizontal
ChipsList.Padding = UDim.new(0, 8)
ChipsList.SortOrder = Enum.SortOrder.LayoutOrder
ChipsList.Parent = ChipsRow
local ChipButtons = {}
local function MakeChip(name, order)
    local chip = Instance.new("TextButton")
    chip.Size = UDim2.new(0, 70 + #name * 4, 1, 0)
    chip.BackgroundColor3 = name == State.CurrentFilter and Theme.Accent or Color3.fromRGB(30, 22, 26)
    chip.Text = name
    chip.TextColor3 = Theme.TextDim
    chip.TextSize = 12
    chip.Font = Enum.Font.GothamBold
    chip.LayoutOrder = order
    chip.Parent = ChipsRow
    local cc = Instance.new("UICorner")
    cc.CornerRadius = UDim.new(1, 0)
    cc.Parent = chip
    chip.MouseButton1Click:Connect(function()
        State.CurrentFilter = name
        for n, b in pairs(ChipButtons) do
            b.BackgroundColor3 = n == name and Theme.Accent or Color3.fromRGB(30, 22, 26)
            b.TextColor3 = n == name and Theme.Text or Theme.TextDim
        end
        ApplyScriptFilter()
    end)
    ChipButtons[name] = chip
    return chip
end
MakeChip("All", 1)
MakeChip("Pack", 2)
MakeChip("Movement", 3)
MakeChip("Combat", 4)
MakeChip("Admin", 5)
MakeChip("Utility", 6)
local ScriptsScroll = Instance.new("ScrollingFrame")
ScriptsScroll.Size = UDim2.new(1, -40, 1, -160)
ScriptsScroll.Position = UDim2.new(0, 20, 0, 150)
ScriptsScroll.BackgroundTransparency = 1
ScriptsScroll.ScrollBarThickness = 5
ScriptsScroll.ScrollBarImageColor3 = Theme.Accent
ScriptsScroll.CanvasSize = UDim2.new(0, 0, 0, 0)
ScriptsScroll.Parent = ScriptsPage
local ScriptsGrid = Instance.new("UIGridLayout")
ScriptsGrid.CellSize = UDim2.new(0, 270, 0, 195)
ScriptsGrid.CellPadding = UDim2.new(0, 14, 0, 14)
ScriptsGrid.SortOrder = Enum.SortOrder.LayoutOrder
ScriptsGrid.Parent = ScriptsScroll
local Scripts = {
    {Name = "SHINJUKU PACK", Desc = "Fly + Silent Aim v2 + Inf Yield + Underground + Vamp ESP + Vampware + Remote", Category = "Pack", Color = Color3.fromRGB(180, 30, 40), Path = shinImagePath, Url = "PACK"},
    {Name = "INFINITE YIELD", Desc = "Admin commands — 300+ cmds, the classic inf yield", Category = "Admin", Color = Color3.fromRGB(35, 110, 200), Path = infYieldImagePath, Url = "https://raw.githubusercontent.com/EdgeIY/infiniteyield/master/source"},
    {Name = "AZURE MODDED", Desc = "Azure modded menu — unverified, use at your own risk", Category = "Admin", Color = Color3.fromRGB(90, 60, 180), Path = azureImagePath, Url = "https://raw.githubusercontent.com/Actyrn/Scripts/main/AzureModded"},
    {Name = "ZEE DEMORCE", Desc = "Full movement suite", Category = "Movement", Color = Color3.fromRGB(140, 20, 60), Path = zeeImagePath, Url = "https://raw.githubusercontent.com/altr83002-bit/schritpytshinjuku/refs/heads/main/zee.txt"},
    {Name = "FLY", Desc = "Smooth flight script", Category = "Movement", Color = Color3.fromRGB(100, 20, 80), Path = flyImagePath, Url = "https://raw.githubusercontent.com/altr83002-bit/shinjuku_emorce_scripts/refs/heads/main/fly.txt"},
    {Name = "DES HOOD STAND", Desc = "Des Hood Stand bot — set BotOwner then execute", Category = "Utility", Color = Color3.fromRGB(180, 80, 20), Path = desHoodImagePath, Url = "DES_HOOD_STAND"},
    {Name = "TP", Desc = "Teleport tool", Category = "Utility", Color = Color3.fromRGB(160, 40, 30), Path = tpImagePath, Url = "https://raw.githubusercontent.com/altr83002-bit/scripthubforzeee/refs/heads/main/emorceware.tp/lua"},
    {Name = "MATCHA RAGE", Desc = "Combat focused", Category = "Combat", Color = Color3.fromRGB(200, 50, 20), Path = matchaImagePath, Url = "https://raw.githubusercontent.com/hexed00/shinjuku/refs/heads/main/vvs.txt"},
    {Name = "PROFILE VIEWER", Desc = "Copy player profiles", Category = "Utility", Color = Color3.fromRGB(120, 30, 50), Path = profileImagePath, Url = "https://raw.githubusercontent.com/altr83002-bit/the-best/refs/heads/main/profile%20copier"},
    {Name = "SHINJUKU OPTI", Desc = "Performance optimizer", Category = "Utility", Color = Color3.fromRGB(90, 40, 40), Path = optiImagePath, Url = "https://raw.githubusercontent.com/altr83002-bit/schritpytshinjuku/refs/heads/main/optimizer.txt"},
    {Name = "ANIMATION GAZER", Desc = "FE Animation editor", Category = "Utility", Color = Color3.fromRGB(150, 20, 70), Path = gazerImagePath, Url = "https://raw.githubusercontent.com/Gazer-Ha/Reimagined/refs/heads/main/FE%20Animation%20editor"},
    {Name = "HB LIMB", Desc = "Limb extender", Category = "Utility", Color = Color3.fromRGB(170, 30, 50), Path = limbImagePath, Url = "https://raw.githubusercontent.com/AAPVdev/scripts/refs/heads/main/UI_LimbExtender.lua"},
    {Name = "AIMBOT", Desc = "Silent / Legit aimbot", Category = "Combat", Color = Color3.fromRGB(210, 25, 35), Path = aimbotImagePath, Url = "https://pastebin.com/raw/1mifmagj"},
    {Name = "FISHING", Desc = "Auto fishing", Category = "Utility", Color = Color3.fromRGB(80, 40, 60), Path = fishingImagePath, Url = "https://imperialb.in/r/ngxtorvc"},
    {Name = "DRIVING EMPIRE", Desc = "Driving Empire script", Category = "Utility", Color = Color3.fromRGB(40, 120, 200), Path = drivingImagePath, Url = "https://gist.githubusercontent.com/RBXScriptzYT/64273c72ed7e8676ff79d85ff62f8acb/raw"},
    {Name = "99 NIGHTS", Desc = "99 Nights in the Forest script", Category = "Utility", Color = Color3.fromRGB(60, 100, 40), Path = nightsImagePath, Url = "https://raw.githubusercontent.com/VapeVoidware/VW-Add/main/nightsintheforest.lua"},
}
local ScriptCards = {}
local function SafeLoad(name, url)
    Notify("Executing", name .. "...", 10, Theme.Info, "⚡")
    task.spawn(function()
        local ok, err = pcall(function()
            loadstring(game:HttpGet(url))()
        end)
        if ok then
            State.ExecCount = State.ExecCount + 1
            State.LastExec = name
            if State.SessionLabels then
                if State.SessionLabels.exec then
                    State.SessionLabels.exec.Text = tostring(State.ExecCount)
                end
                if State.SessionLabels.last then
                    State.SessionLabels.last.Text = name
                end
            end
            Notify("Executed ✓", name .. " loaded successfully", 3, Theme.Success, "✔")
        else
            Notify("Load Error", name .. ": " .. tostring(err):sub(1, 60), 5, Theme.Danger, "✕")
        end
    end)
end
for i, data in ipairs(Scripts) do
    local card = Instance.new("Frame")
    card.BackgroundColor3 = Theme.Surface
    card.BorderSizePixel = 0
    card.LayoutOrder = i
    card.Parent = ScriptsScroll
    local cardCorner = Instance.new("UICorner")
    cardCorner.CornerRadius = UDim.new(0, 14)
    cardCorner.Parent = card
    local cardStroke = Instance.new("UIStroke")
    cardStroke.Color = Theme.Border
    cardStroke.Thickness = 1
    cardStroke.Parent = card
    local img = Instance.new("ImageLabel")
    img.Size = UDim2.new(0, 70, 0, 70)
    img.Position = UDim2.new(0, 14, 0, 14)
    img.BackgroundColor3 = Color3.fromRGB(30, 30, 36)
    img.Image = getImage(data.Path)
    img.ScaleType = Enum.ScaleType.Crop
    img.Parent = card
    local imgCorner = Instance.new("UICorner")
    imgCorner.CornerRadius = UDim.new(0, 10)
    imgCorner.Parent = img
    local imgStroke = Instance.new("UIStroke")
    imgStroke.Color = data.Color
    imgStroke.Thickness = 2
    imgStroke.Parent = img
    local title = Instance.new("TextLabel")
    title.Size = UDim2.new(1, -100, 0, 26)
    title.Position = UDim2.new(0, 94, 0, 14)
    title.BackgroundTransparency = 1
    title.Text = data.Name
    title.TextColor3 = Theme.Text
    title.TextSize = 15
    title.Font = Enum.Font.GothamBlack
    title.TextXAlignment = Enum.TextXAlignment.Left
    title.TextTruncate = Enum.TextTruncate.AtEnd
    title.Parent = card
    local cat = Instance.new("TextLabel")
    cat.Size = UDim2.new(0, 74, 0, 16)
    cat.Position = UDim2.new(1, -88, 0, 16)
    cat.BackgroundColor3 = data.Color
    cat.BackgroundTransparency = 0.25
    cat.Text = data.Category
    cat.TextColor3 = Theme.Text
    cat.TextSize = 10
    cat.Font = Enum.Font.GothamBold
    cat.Parent = card
    local catC = Instance.new("UICorner")
    catC.CornerRadius = UDim.new(0, 6)
    catC.Parent = cat
    local desc = Instance.new("TextLabel")
    desc.Size = UDim2.new(1, -100, 0, 42)
    desc.Position = UDim2.new(0, 94, 0, 42)
    desc.BackgroundTransparency = 1
    desc.Text = data.Desc
    desc.TextColor3 = Theme.TextDim
    desc.TextSize = 12
    desc.Font = Enum.Font.Gotham
    desc.TextXAlignment = Enum.TextXAlignment.Left
    desc.TextYAlignment = Enum.TextYAlignment.Top
    desc.TextWrapped = true
    desc.Parent = card
    local exec = Instance.new("TextButton")
    exec.Size = UDim2.new(1, -28, 0, 34)
    exec.Position = UDim2.new(0, 14, 1, -48)
    exec.BackgroundColor3 = data.Color
    exec.Text = "EXECUTE"
    exec.TextColor3 = Theme.Text
    exec.TextSize = 14
    exec.Font = Enum.Font.GothamBold
    exec.Parent = card
    local execCorner = Instance.new("UICorner")
    execCorner.CornerRadius = UDim.new(0, 8)
    execCorner.Parent = exec
    exec.MouseButton1Click:Connect(function()
        exec.Text = "LOADING..."
        exec.BackgroundColor3 = Theme.AccentDark
        task.spawn(function()
            if data.Url == "DES_HOOD_STAND" then
                _G.BotOwner = "Sore61lalit"  -- change this to your name
                local ok, err = pcall(function()
                    loadstring(game:HttpGet("https://raw.githubusercontent.com/hexed00/zee/refs/heads/main/veveemorce"))()
                end)
                if ok then
                    State.ExecCount = State.ExecCount + 1
                    State.LastExec = data.Name
                    Notify("Executed ✓", data.Name .. " loaded — BotOwner set", 3, Theme.Success, "✔")
                else
                    Notify("Load Error", tostring(err):sub(1, 80), 5, Theme.Danger, "✕")
                end
            elseif data.Url == "PACK" then
                SafeLoad("Remote", "https://raw.githubusercontent.com/wtfyen/xd/main/wok")
                SafeLoad("Fly", "https://raw.githubusercontent.com/altr83002-bit/shinjuku_emorce_scripts/refs/heads/main/fly.txt")
                SafeLoad("Inf Yield", "https://raw.githubusercontent.com/altr83002-bit/shinjuku_emorce_scripts/refs/heads/main/inf%20yeild.txt")
                SafeLoad("Silent Aim v2", "https://raw.githubusercontent.com/altr83002-bit/shinjuku_emorce_scripts/refs/heads/main/silent%20aim%20v2.txt")
                SafeLoad("Underground", "https://raw.githubusercontent.com/altr83002-bit/shinjuku_emorce_scripts/refs/heads/main/underground")
                SafeLoad("Vamp ESP", "https://raw.githubusercontent.com/altr83002-bit/shinjuku_emorce_scripts/refs/heads/main/vamp%20esp")
                SafeLoad("Vampware", "https://raw.githubusercontent.com/altr83002-bit/shinjuku_emorce_scripts/refs/heads/main/vampware.txt")
            elseif data.Name == "AZURE MODDED" then
                SafeLoad(data.Name, data.Url)
                SafeLoad("Autoshoot", "https://raw.githubusercontent.com/hexed00/zee/refs/heads/main/autoshoot.txt")
            elseif data.Name == "ZEE DEMORCE" then
                SafeLoad(data.Name, data.Url)
                SafeLoad("Autostate", "https://raw.githubusercontent.com/hexed00/zee/refs/heads/main/autostate.txt")
            else
                SafeLoad(data.Name, data.Url)
            end
            task.wait(0.8)
            exec.Text = "✓ DONE"
            exec.BackgroundColor3 = Theme.Success
            task.wait(1.5)
            exec.Text = "EXECUTE"
            exec.BackgroundColor3 = data.Color
        end)
    end)
    ScriptCards[i] = {Frame = card, Data = data}
end
function ApplyScriptFilter()
    local query = State.SearchText
    local shown = 0
    for _, entry in ipairs(ScriptCards) do
        local data = entry.Data
        local matchCat = State.CurrentFilter == "All" or data.Category == State.CurrentFilter
        local nameL = data.Name:lower()
        local descL = data.Desc:lower()
        local matchText = query == "" or nameL:find(query, 1, true) or descL:find(query, 1, true)
        entry.Frame.Visible = matchCat and matchText
        if entry.Frame.Visible then
            shown = shown + 1
        end
    end
    ResultsLabel.Text = shown .. " / " .. #ScriptCards .. " scripts"
end
ScriptSearch:GetPropertyChangedSignal("Text"):Connect(function()
    State.SearchText = ScriptSearch.Text:lower():gsub("^%s+", ""):gsub("%s+$", "")
    ApplyScriptFilter()
end)
ScriptsGrid:GetPropertyChangedSignal("AbsoluteContentSize"):Connect(function()
    ScriptsScroll.CanvasSize = UDim2.new(0, 0, 0, ScriptsGrid.AbsoluteContentSize.Y + 20)
end)
ApplyScriptFilter()
-- ========== HOME PAGE — PREMIUM PROFILE ==========
local HomePage = CreatePage("Home")
local PlayerCard = Instance.new("Frame")
PlayerCard.Size = UDim2.new(0, 300, 0, 380)
PlayerCard.Position = UDim2.new(0, 20, 0, 20)
PlayerCard.BackgroundColor3 = Theme.Surface
PlayerCard.BorderSizePixel = 0
PlayerCard.Parent = HomePage

-- ========== CHAT SPY TOGGLE (Quick Actions - next to Fly) ==========
local QuickCard = Instance.new("Frame")
QuickCard.Name = "QuickCard"
QuickCard.Size = UDim2.new(0, 300, 0, 160)
QuickCard.Position = UDim2.new(0, 340, 0, 20)
QuickCard.BackgroundColor3 = Theme.Surface
QuickCard.BorderSizePixel = 0
QuickCard.Parent = HomePage
local QCCorner = Instance.new("UICorner")
QCCorner.CornerRadius = UDim.new(0, 16)
QCCorner.Parent = QuickCard
local QCStroke = Instance.new("UIStroke")
QCStroke.Color = Theme.Border
QCStroke.Thickness = 1
QCStroke.Parent = QuickCard
local QuickTitle = Instance.new("TextLabel")
QuickTitle.Size = UDim2.new(1, -20, 0, 24)
QuickTitle.Position = UDim2.new(0, 16, 0, 12)
QuickTitle.BackgroundTransparency = 1
QuickTitle.Text = "Quick Actions"
QuickTitle.TextColor3 = Theme.Text
QuickTitle.TextSize = 15
QuickTitle.Font = Enum.Font.GothamBold
QuickTitle.TextXAlignment = Enum.TextXAlignment.Left
QuickTitle.Parent = QuickCard

local ChatSpyBtn = Instance.new("TextButton")
ChatSpyBtn.Size = UDim2.new(0, 130, 0, 34)
ChatSpyBtn.Position = UDim2.new(0, 16, 0, 50)
ChatSpyBtn.BackgroundColor3 = Theme.Success
ChatSpyBtn.Text = "Chat Spy: ON"
ChatSpyBtn.TextColor3 = Theme.Text
ChatSpyBtn.TextSize = 13
ChatSpyBtn.Font = Enum.Font.GothamBold
ChatSpyBtn.Parent = QuickCard
local CSCorner = Instance.new("UICorner")
CSCorner.CornerRadius = UDim.new(0, 8)
CSCorner.Parent = ChatSpyBtn
ChatSpyBtn.MouseButton1Click:Connect(function()
    local newState = not State.ChatSpy
    SetChatSpy(newState)
    ChatSpyBtn.Text = newState and "Chat Spy: ON" or "Chat Spy: OFF"
    ChatSpyBtn.BackgroundColor3 = newState and Theme.Success or Color3.fromRGB(60, 40, 45)
end)

-- Enable Chat Spy on load
SetChatSpy(true)


local PCCorner = Instance.new("UICorner")
PCCorner.CornerRadius = UDim.new(0, 16)
PCCorner.Parent = PlayerCard
local PCStroke = Instance.new("UIStroke")
PCStroke.Color = Theme.Accent
PCStroke.Thickness = 1.5
PCStroke.Transparency = 0.5
PCStroke.Parent = PlayerCard
local ProfileHeader = Instance.new("Frame")
ProfileHeader.Size = UDim2.new(1, 0, 0, 90)
ProfileHeader.BackgroundColor3 = Theme.AccentDark
ProfileHeader.BorderSizePixel = 0
ProfileHeader.Parent = PlayerCard
local PHCorner = Instance.new("UICorner")
PHCorner.CornerRadius = UDim.new(0, 16)
PHCorner.Parent = ProfileHeader
local PHFix = Instance.new("Frame")
PHFix.Size = UDim2.new(1, 0, 0, 20)
PHFix.Position = UDim2.new(0, 0, 1, -20)
PHFix.BackgroundColor3 = Theme.AccentDark
PHFix.BorderSizePixel = 0
PHFix.Parent = ProfileHeader
local AvatarFrame = Instance.new("Frame")
AvatarFrame.Size = UDim2.new(0, 96, 0, 96)
AvatarFrame.Position = UDim2.new(0.5, -48, 0, 42)
AvatarFrame.BackgroundColor3 = Theme.Background
AvatarFrame.Parent = PlayerCard
local AvatarCorner = Instance.new("UICorner")
AvatarCorner.CornerRadius = UDim.new(1, 0)
AvatarCorner.Parent = AvatarFrame
local AvatarStroke = Instance.new("UIStroke")
AvatarStroke.Color = Theme.Accent
AvatarStroke.Thickness = 3
AvatarStroke.Parent = AvatarFrame
local AvatarImg = Instance.new("ImageLabel")
AvatarImg.Size = UDim2.new(1, -6, 1, -6)
AvatarImg.Position = UDim2.new(0, 3, 0, 3)
AvatarImg.BackgroundTransparency = 1
AvatarImg.Image = "https://www.roblox.com/headshot-thumbnail/image?userId=" .. player.UserId .. "&width=150&height=150&format=png"
AvatarImg.Parent = AvatarFrame
local AvatarImgCorner = Instance.new("UICorner")
AvatarImgCorner.CornerRadius = UDim.new(1, 0)
AvatarImgCorner.Parent = AvatarImg
local NameLabel = Instance.new("TextLabel")
NameLabel.Size = UDim2.new(1, -20, 0, 26)
NameLabel.Position = UDim2.new(0, 10, 0, 150)
NameLabel.BackgroundTransparency = 1
NameLabel.Text = player.DisplayName
NameLabel.TextColor3 = Theme.Text
NameLabel.TextSize = 20
NameLabel.Font = Enum.Font.GothamBold
NameLabel.Parent = PlayerCard
local UserLabel = Instance.new("TextLabel")
UserLabel.Size = UDim2.new(1, -20, 0, 18)
UserLabel.Position = UDim2.new(0, 10, 0, 176)
UserLabel.BackgroundTransparency = 1
UserLabel.Text = "@" .. player.Name .. " • ID " .. player.UserId
UserLabel.TextColor3 = Theme.TextDim
UserLabel.TextSize = 12
UserLabel.Font = Enum.Font.Gotham
UserLabel.Parent = PlayerCard
local StatsRow = Instance.new("Frame")
StatsRow.Size = UDim2.new(1, -24, 0, 50)
StatsRow.Position = UDim2.new(0, 12, 0, 205)
StatsRow.BackgroundColor3 = Color3.fromRGB(18, 18, 22)
StatsRow.BorderSizePixel = 0
StatsRow.Parent = PlayerCard
local SRCorner = Instance.new("UICorner")
SRCorner.CornerRadius = UDim.new(0, 10)
SRCorner.Parent = StatsRow
local function MakeMiniStat(text, value, x)
    local f = Instance.new("Frame")
    f.Size = UDim2.new(0.33, -4, 1, 0)
    f.Position = UDim2.new(x, 0, 0, 0)
    f.BackgroundTransparency = 1
    f.Parent = StatsRow
    local v = Instance.new("TextLabel")
    v.Size = UDim2.new(1, 0, 0, 22)
    v.Position = UDim2.new(0, 0, 0, 6)
    v.BackgroundTransparency = 1
    v.Text = value
    v.TextColor3 = Theme.AccentLight
    v.TextSize = 14
    v.Font = Enum.Font.GothamBold
    v.Parent = f
    local t = Instance.new("TextLabel")
    t.Size = UDim2.new(1, 0, 0, 16)
    t.Position = UDim2.new(0, 0, 0, 28)
    t.BackgroundTransparency = 1
    t.Text = text
    t.TextColor3 = Theme.TextMuted
    t.TextSize = 10
    t.Font = Enum.Font.Gotham
    t.Parent = f
    return v
end
local AccountAgeVal = MakeMiniStat("Age", tostring(player.AccountAge) .. "d", 0)
local FriendsVal = MakeMiniStat("Friends", "…", 0.33)
local PlaceVal = MakeMiniStat("Place", tostring(game.PlaceId):sub(-4), 0.66)
local function FriendsInServer()
    local n = 0
    for _, plr in ipairs(Players:GetPlayers()) do
        if plr ~= player then
            local cached = State.FriendCache[plr.UserId]
            if cached == nil then
                local ok, isF = pcall(function()
                    return player:IsFriendsWith(plr.UserId)
                end)
                cached = (ok and isF) or false
                State.FriendCache[plr.UserId] = cached
            end
            if cached then
                n = n + 1
            end
        end
    end
    return n
end
local function UpdateFriendsStat()
    local here = FriendsInServer()
    local total = State.TotalFriends
    FriendsVal.Text = here .. "/" .. (total and tostring(total) or "?")
    FriendsVal.TextColor3 = here > 0 and Theme.Friend or Theme.AccentLight
end
local function FetchFriendCount()
    task.spawn(function()
        local ok, body = pcall(function()
            return game:HttpGet("https://friends.roblox.com/v1/users/" .. player.UserId .. "/friends/count")
        end)
        if ok then
            local ok2, data = pcall(function()
                return HttpService:JSONDecode(body)
            end)
            if ok2 and data and data.count then
                State.TotalFriends = data.count
                UpdateFriendsStat()
            end
        end
    end)
end
FetchFriendCount()
UpdateFriendsStat()
local function MakeProfileBtn(text, y, color, callback)
    local b = Instance.new("TextButton")
    b.Size = UDim2.new(1, -24, 0, 34)
    b.Position = UDim2.new(0, 12, 0, y)
    b.BackgroundColor3 = color
    b.Text = text
    b.TextColor3 = Theme.Text
    b.TextSize = 13
    b.Font = Enum.Font.GothamBold
    b.Parent = PlayerCard
    local c = Instance.new("UICorner")
    c.CornerRadius = UDim.new(0, 8)
    c.Parent = b
    b.MouseButton1Click:Connect(callback)
    return b
end
MakeProfileBtn("Copy User ID", 268, Theme.Accent, function()
    CopyNotify(tostring(player.UserId), "User ID")
end)
MakeProfileBtn("Copy Username", 308, Color3.fromRGB(50, 40, 55), function()
    CopyNotify(player.Name, "Username")
end)
MakeProfileBtn("Open Profile", 348, Color3.fromRGB(40, 30, 50), function()
    pcall(function()
        game:GetService("GuiService"):OpenBrowserWindow("https://www.roblox.com/users/" .. player.UserId .. "/profile")
    end)
end)
local ServerCard = Instance.new("Frame")
ServerCard.Size = UDim2.new(0, 280, 0, 160)
ServerCard.Position = UDim2.new(0, 340, 0, 20)
ServerCard.BackgroundColor3 = Theme.Surface
ServerCard.Parent = HomePage
local SCCorner = Instance.new("UICorner")
SCCorner.CornerRadius = UDim.new(0, 16)
SCCorner.Parent = ServerCard
local SCStroke = Instance.new("UIStroke")
SCStroke.Color = Theme.Border
SCStroke.Thickness = 1
SCStroke.Parent = ServerCard
local ServerTitle = Instance.new("TextLabel")
ServerTitle.Size = UDim2.new(0.6, 0, 0, 24)
ServerTitle.Position = UDim2.new(0, 16, 0, 12)
ServerTitle.BackgroundTransparency = 1
ServerTitle.Text = "Current Server"
ServerTitle.TextColor3 = Theme.Text
ServerTitle.TextSize = 15
ServerTitle.Font = Enum.Font.GothamBold
ServerTitle.TextXAlignment = Enum.TextXAlignment.Left
ServerTitle.Parent = ServerCard
local ServerCopyBtn = Instance.new("TextButton")
ServerCopyBtn.Size = UDim2.new(0, 26, 0, 24)
ServerCopyBtn.Position = UDim2.new(0, 132, 0, 12)
ServerCopyBtn.BackgroundColor3 = Color3.fromRGB(40, 30, 38)
ServerCopyBtn.Text = "⧉"
ServerCopyBtn.TextColor3 = Theme.TextDim
ServerCopyBtn.TextSize = 14
ServerCopyBtn.Font = Enum.Font.GothamBold
ServerCopyBtn.Parent = ServerCard
local SCopyC = Instance.new("UICorner")
SCopyC.CornerRadius = UDim.new(0, 6)
SCopyC.Parent = ServerCopyBtn
ServerCopyBtn.MouseButton1Click:Connect(function()
    CopyNotify(game.JobId or "", "Server JobId")
end)
local PlayersLabel = Instance.new("TextLabel")
PlayersLabel.Size = UDim2.new(1, -20, 0, 20)
PlayersLabel.Position = UDim2.new(0, 16, 0, 42)
PlayersLabel.BackgroundTransparency = 1
PlayersLabel.Text = #Players:GetPlayers() .. " / " .. game.Players.MaxPlayers .. " players"
PlayersLabel.TextColor3 = Theme.TextDim
PlayersLabel.TextSize = 13
PlayersLabel.Font = Enum.Font.Gotham
PlayersLabel.TextXAlignment = Enum.TextXAlignment.Left
PlayersLabel.Parent = ServerCard
local JobLabel = Instance.new("TextLabel")
JobLabel.Size = UDim2.new(1, -20, 0, 18)
JobLabel.Position = UDim2.new(0, 16, 0, 66)
JobLabel.BackgroundTransparency = 1
JobLabel.Text = "Job: " .. (game.JobId and game.JobId:sub(1, 12) .. "..." or "—")
JobLabel.TextColor3 = Theme.TextMuted
JobLabel.TextSize = 11
JobLabel.Font = Enum.Font.Gotham
JobLabel.TextXAlignment = Enum.TextXAlignment.Left
JobLabel.Parent = ServerCard
local PlaceLabel = Instance.new("TextLabel")
PlaceLabel.Size = UDim2.new(1, -20, 0, 18)
PlaceLabel.Position = UDim2.new(0, 16, 0, 86)
PlaceLabel.BackgroundTransparency = 1
PlaceLabel.Text = "PlaceId: " .. tostring(game.PlaceId)
PlaceLabel.TextColor3 = Theme.TextMuted
PlaceLabel.TextSize = 11
PlaceLabel.Font = Enum.Font.Gotham
PlaceLabel.TextXAlignment = Enum.TextXAlignment.Left
PlaceLabel.Parent = ServerCard
local RejoinBtn = Instance.new("TextButton")
RejoinBtn.Size = UDim2.new(0.45, 0, 0, 32)
RejoinBtn.Position = UDim2.new(0.05, 0, 1, -48)
RejoinBtn.BackgroundColor3 = Theme.Accent
RejoinBtn.Text = "Rejoin"
RejoinBtn.TextColor3 = Theme.Text
RejoinBtn.TextSize = 13
RejoinBtn.Font = Enum.Font.GothamBold
RejoinBtn.Parent = ServerCard
local rjC = Instance.new("UICorner")
rjC.CornerRadius = UDim.new(0, 8)
rjC.Parent = RejoinBtn
RejoinBtn.MouseButton1Click:Connect(function()
    Notify("Teleporting", "Rejoining current server...", 3, Theme.Info, "⟳")
    TeleportService:TeleportToPlaceInstance(game.PlaceId, game.JobId, player)
end)
local CopyJobBtn = Instance.new("TextButton")
CopyJobBtn.Size = UDim2.new(0.45, 0, 0, 32)
CopyJobBtn.Position = UDim2.new(0.5, 0, 1, -48)
CopyJobBtn.BackgroundColor3 = Color3.fromRGB(40, 30, 45)
CopyJobBtn.Text = "Copy Job"
CopyJobBtn.TextColor3 = Theme.Text
CopyJobBtn.TextSize = 13
CopyJobBtn.Font = Enum.Font.GothamBold
CopyJobBtn.Parent = ServerCard
local cjC = Instance.new("UICorner")
cjC.CornerRadius = UDim.new(0, 8)
cjC.Parent = CopyJobBtn
CopyJobBtn.MouseButton1Click:Connect(function()
    CopyNotify(game.JobId, "JobId")
end)
local MoveCard = Instance.new("Frame")
MoveCard.Size = UDim2.new(0, 280, 0, 400)
MoveCard.Position = UDim2.new(0, 340, 0, 200)
MoveCard.BackgroundColor3 = Theme.Surface
MoveCard.Parent = HomePage
local MCCorner = Instance.new("UICorner")
MCCorner.CornerRadius = UDim.new(0, 16)
MCCorner.Parent = MoveCard
local MCStroke = Instance.new("UIStroke")
MCStroke.Color = Theme.Border
MCStroke.Thickness = 1
MCStroke.Parent = MoveCard
local MoveTitle = Instance.new("TextLabel")
MoveTitle.Size = UDim2.new(1, -20, 0, 24)
MoveTitle.Position = UDim2.new(0, 16, 0, 12)
MoveTitle.BackgroundTransparency = 1
MoveTitle.Text = "Movement"
MoveTitle.TextColor3 = Theme.Text
MoveTitle.TextSize = 15
MoveTitle.Font = Enum.Font.GothamBold
MoveTitle.TextXAlignment = Enum.TextXAlignment.Left
MoveTitle.Parent = MoveCard
local function MakeToggle(text, y, default, callback)
    local b = Instance.new("TextButton")
    b.Size = UDim2.new(1, -32, 0, 36)
    b.Position = UDim2.new(0, 16, 0, y)
    b.BackgroundColor3 = default and Theme.Success or Color3.fromRGB(40, 30, 40)
    b.Text = text .. (default and " ON" or " OFF")
    b.TextColor3 = Theme.Text
    b.TextSize = 13
    b.Font = Enum.Font.GothamMedium
    b.Parent = MoveCard
    local c = Instance.new("UICorner")
    c.CornerRadius = UDim.new(0, 8)
    c.Parent = b
    local on = default
    b.MouseButton1Click:Connect(function()
        on = not on
        b.BackgroundColor3 = on and Theme.Success or Color3.fromRGB(40, 30, 40)
        b.Text = text .. (on and " ON" or " OFF")
        callback(on)
    end)
    return b
end
local function SetFlight(on)
    State.Flight = on
    local char = player.Character
    if not char then return end
    local hrp = char:FindFirstChild("HumanoidRootPart")
    if not hrp then return end
    if on then
        local bodyVel = Instance.new("BodyVelocity")
        bodyVel.Name = "EmorceFlight"
        bodyVel.MaxForce = Vector3.new(1e5, 1e5, 1e5)
        bodyVel.Velocity = Vector3.zero
        bodyVel.Parent = hrp
        local conn
        conn = RunService.Heartbeat:Connect(function()
            if not State.Flight or not bodyVel or not bodyVel.Parent then
                if conn then conn:Disconnect() end
                return
            end
            local cam = workspace.CurrentCamera
            local move = Vector3.zero
            if UserInputService:IsKeyDown(Enum.KeyCode.W) then move = move + cam.CFrame.LookVector end
            if UserInputService:IsKeyDown(Enum.KeyCode.S) then move = move - cam.CFrame.LookVector end
            if UserInputService:IsKeyDown(Enum.KeyCode.A) then move = move - cam.CFrame.RightVector end
            if UserInputService:IsKeyDown(Enum.KeyCode.D) then move = move + cam.CFrame.RightVector end
            if UserInputService:IsKeyDown(Enum.KeyCode.Space) then move = move + Vector3.new(0, 1, 0) end
            if UserInputService:IsKeyDown(Enum.KeyCode.LeftControl) then move = move - Vector3.new(0, 1, 0) end
            if move.Magnitude > 0.1 then
                bodyVel.Velocity = move.Unit * State.FlySpeed
            else
                bodyVel.Velocity = Vector3.zero
            end
        end)
        Notify("Flight", "ON — speed " .. State.FlySpeed, 2.5, Theme.Success, "✈")
    else
        local bv = hrp:FindFirstChild("EmorceFlight")
        if bv then bv:Destroy() end
        Notify("Flight", "OFF", 2, Theme.Info, "✈")
    end
end
local FlightBtn = MakeToggle("Flight", 48, false, function(on)
    SetFlight(on)
end)
MakeToggle("Noclip", 92, false, function(on)
    State.Noclip = on
end)
MakeToggle("Infinite Jump", 136, false, function(on)
    State.InfiniteJump = on
end)
local FlySlider = CreateSlider(MoveCard, "Fly Speed", 10, 400, 80, 184, function(v)
    State.FlySpeed = v
end)
local WalkSlider = CreateSlider(MoveCard, "WalkSpeed", 16, 500, 16, 242, function(v)
    State.Speed = v
    State.WalkSpeed = v
    local hum = player.Character and player.Character:FindFirstChildOfClass("Humanoid")
    if hum then
        hum.WalkSpeed = v
    end
end)
local JumpSlider = CreateSlider(MoveCard, "Jump Power", 20, 500, 50, 300, function(v)
    State.Jump = v
    State.JumpPower = v
    local hum = player.Character and player.Character:FindFirstChildOfClass("Humanoid")
    if hum then
        pcall(function() hum.UseJumpPower = true end)
        hum.JumpPower = v
    end
end)
local MoveHint = Instance.new("TextLabel")
MoveHint.Size = UDim2.new(1, -32, 0, 16)
MoveHint.Position = UDim2.new(0, 16, 0, 362)
MoveHint.BackgroundTransparency = 1
MoveHint.Text = "drag the bars to go faster"
MoveHint.TextColor3 = Theme.TextMuted
MoveHint.TextSize = 10
MoveHint.Font = Enum.Font.Gotham
MoveHint.TextXAlignment = Enum.TextXAlignment.Left
MoveHint.Parent = MoveCard
local QuickFrame = Instance.new("Frame")
QuickFrame.Size = UDim2.new(0, 280, 0, 420)
QuickFrame.Position = UDim2.new(0, 640, 0, 20)
QuickFrame.BackgroundColor3 = Theme.Surface
QuickFrame.Parent = HomePage
local QFCorner = Instance.new("UICorner")
QFCorner.CornerRadius = UDim.new(0, 16)
QFCorner.Parent = QuickFrame
local QFStroke = Instance.new("UIStroke")
QFStroke.Color = Theme.Border
QFStroke.Thickness = 1
QFStroke.Parent = QuickFrame
local QuickTitle = Instance.new("TextLabel")
QuickTitle.Size = UDim2.new(1, -20, 0, 24)
QuickTitle.Position = UDim2.new(0, 16, 0, 12)
QuickTitle.BackgroundTransparency = 1
QuickTitle.Text = "Quick Actions"
QuickTitle.TextColor3 = Theme.Text
QuickTitle.TextSize = 15
QuickTitle.Font = Enum.Font.GothamBold
QuickTitle.TextXAlignment = Enum.TextXAlignment.Left
QuickTitle.Parent = QuickFrame
local function QuickBtn(text, y, callback)
    local b = Instance.new("TextButton")
    b.Size = UDim2.new(1, -32, 0, 36)
    b.Position = UDim2.new(0, 16, 0, y)
    b.BackgroundColor3 = Color3.fromRGB(35, 20, 25)
    b.Text = text
    b.TextColor3 = Theme.Text
    b.TextSize = 13
    b.Font = Enum.Font.GothamMedium
    b.Parent = QuickFrame
    local c = Instance.new("UICorner")
    c.CornerRadius = UDim.new(0, 8)
    c.Parent = b
    b.MouseButton1Click:Connect(callback)
    return b
end
QuickBtn("Rejoin Server", 48, function()
    Notify("Teleporting", "Rejoining server...", 3, Theme.Info, "⟳")
    TeleportService:TeleportToPlaceInstance(game.PlaceId, game.JobId, player)
end)
QuickBtn("Copy Job ID", 92, function()
    CopyNotify(game.JobId, "JobId")
end)
QuickBtn("Copy Place ID", 136, function()
    CopyNotify(tostring(game.PlaceId), "PlaceId")
end)
QuickBtn("Fullbright Toggle", 180, function()
    State.Fullbright = not State.Fullbright
    if State.Fullbright then
        Lighting.Brightness = 2
        Lighting.ClockTime = 14
        Lighting.FogEnd = 100000
        Lighting.GlobalShadows = false
        Lighting.OutdoorAmbient = Color3.fromRGB(128, 128, 128)
        Notify("Fullbright", "Enabled", 2, Theme.Success, "☀")
    else
        Lighting.Brightness = 1
        Lighting.ClockTime = 14
        Lighting.FogEnd = 100000
        Lighting.GlobalShadows = true
        Notify("Fullbright", "Disabled", 2, Theme.Info, "☾")
    end
end)
QuickBtn("Anti-AFK", 224, function()
    State.AntiAFK = not State.AntiAFK
    Notify("Anti-AFK", State.AntiAFK and "Enabled" or "Disabled", 2, Theme.Success, "⏱")
end)
QuickBtn("Destroy UI", 268, function()
    ScreenGui:Destroy()
end)
QuickBtn("Refresh Server Info", 312, function()
    PlayersLabel.Text = #Players:GetPlayers() .. " / " .. game.Players.MaxPlayers .. " players"
    JobLabel.Text = "Job: " .. (game.JobId and game.JobId:sub(1, 12) .. "..." or "—")
    UpdateFriendsStat()
    Notify("Refreshed", "Server info updated", 2, Theme.Info, "⟳")
end)
QuickBtn("Map Cleaner", 356, function()
    local cleaned = 0
    local keep = {
        Terrain = true,
        Camera = true,
        CurrentCamera = true,
    }
    for _, obj in ipairs(workspace:GetChildren()) do
        if not keep[obj.Name] and not obj:IsA("Terrain") and not obj:IsA("Camera") then
            local isChar = false
            for _, plr in ipairs(Players:GetPlayers()) do
                if plr.Character and obj == plr.Character then
                    isChar = true
                    break
                end
            end
            if not isChar then
                pcall(function()
                    obj:Destroy()
                    cleaned = cleaned + 1
                end)
            end
        end
    end
    for _, obj in ipairs(workspace:GetDescendants()) do
        if obj:IsA("BasePart") and (obj.Name == "Part" or obj.Name == "MeshPart" or obj.Name:lower():find("debris") or obj.Name:lower():find("trash") or obj.Name:lower():find("junk")) then
            pcall(function()
                obj:Destroy()
                cleaned = cleaned + 1
            end)
        end
    end
    Notify("Map Cleaner", "Removed " .. cleaned .. " objects", 3, Theme.Success, "🧹")
end)
local SessionCard = Instance.new("Frame")
SessionCard.Size = UDim2.new(0, 280, 0, 150)
SessionCard.Position = UDim2.new(0, 640, 0, 452)
SessionCard.BackgroundColor3 = Theme.Surface
SessionCard.Parent = HomePage
local SeCCorner = Instance.new("UICorner")
SeCCorner.CornerRadius = UDim.new(0, 16)
SeCCorner.Parent = SessionCard
local SeCStroke = Instance.new("UIStroke")
SeCStroke.Color = Theme.Border
SeCStroke.Thickness = 1
SeCStroke.Parent = SessionCard
local SessionTitle = Instance.new("TextLabel")
SessionTitle.Size = UDim2.new(1, -20, 0, 22)
SessionTitle.Position = UDim2.new(0, 16, 0, 10)
SessionTitle.BackgroundTransparency = 1
SessionTitle.Text = "Session"
SessionTitle.TextColor3 = Theme.Text
SessionTitle.TextSize = 14
SessionTitle.Font = Enum.Font.GothamBold
SessionTitle.TextXAlignment = Enum.TextXAlignment.Left
SessionTitle.Parent = SessionCard
local function SessionRow(label, value, y)
    local l = Instance.new("TextLabel")
    l.Size = UDim2.new(0.55, 0, 0, 20)
    l.Position = UDim2.new(0, 16, 0, y)
    l.BackgroundTransparency = 1
    l.Text = label
    l.TextColor3 = Theme.TextMuted
    l.TextSize = 12
    l.Font = Enum.Font.Gotham
    l.TextXAlignment = Enum.TextXAlignment.Left
    l.Parent = SessionCard
    local v = Instance.new("TextLabel")
    v.Size = UDim2.new(0.4, 0, 0, 20)
    v.Position = UDim2.new(0.55, 0, 0, y)
    v.BackgroundTransparency = 1
    v.Text = value
    v.TextColor3 = Theme.Text
    v.TextSize = 12
    v.Font = Enum.Font.GothamBold
    v.TextXAlignment = Enum.TextXAlignment.Left
    v.Parent = SessionCard
    return v
end
local UptimeVal = SessionRow("Uptime", "0m 0s", 38)
local ExecVal = SessionRow("Scripts executed", "0", 62)
local LastVal = SessionRow("Last executed", "—", 86)
local FriendsHereVal = SessionRow("Friends here", "0", 110)
State.SessionLabels = {
    uptime = UptimeVal,
    exec = ExecVal,
    last = LastVal,
    friends = FriendsHereVal,
}
task.spawn(function()
    while true do
        task.wait(1)
        if State.SessionLabels and State.SessionLabels.uptime and State.SessionLabels.uptime.Parent then
            local t = math.floor(os.clock() - State.SessionStart)
            local m = math.floor(t / 60)
            local s = t % 60
            local text
            if m >= 60 then
                text = math.floor(m / 60) .. "h " .. (m % 60) .. "m"
            else
                text = m .. "m " .. s .. "s"
            end
            State.SessionLabels.uptime.Text = text
            State.SessionLabels.friends.Text = tostring(FriendsInServer())
        else
            break
        end
    end
end)
-- ========== APPS PAGE ==========
local AppsPage = CreatePage("Apps")
local AppsTitle = Instance.new("TextLabel")
AppsTitle.Size = UDim2.new(1, -40, 0, 40)
AppsTitle.Position = UDim2.new(0, 24, 0, 16)
AppsTitle.BackgroundTransparency = 1
AppsTitle.Text = "Script Library"
AppsTitle.TextColor3 = Theme.Text
AppsTitle.TextSize = 26
AppsTitle.Font = Enum.Font.GothamBlack
AppsTitle.TextXAlignment = Enum.TextXAlignment.Left
AppsTitle.Parent = AppsPage
local AppsScroll = Instance.new("ScrollingFrame")
AppsScroll.Size = UDim2.new(1, -40, 1, -70)
AppsScroll.Position = UDim2.new(0, 20, 0, 60)
AppsScroll.BackgroundTransparency = 1
AppsScroll.ScrollBarThickness = 4
AppsScroll.ScrollBarImageColor3 = Theme.Accent
AppsScroll.CanvasSize = UDim2.new(0, 0, 0, 0)
AppsScroll.Parent = AppsPage
local AppsGrid = Instance.new("UIGridLayout")
AppsGrid.CellSize = UDim2.new(0, 260, 0, 145)
AppsGrid.CellPadding = UDim2.new(0, 14, 0, 14)
AppsGrid.SortOrder = Enum.SortOrder.LayoutOrder
AppsGrid.Parent = AppsScroll
for i, data in ipairs(Scripts) do
    local card = Instance.new("Frame")
    card.BackgroundColor3 = data.Color
    card.BorderSizePixel = 0
    card.LayoutOrder = i
    card.Parent = AppsScroll
    local cardCorner = Instance.new("UICorner")
    cardCorner.CornerRadius = UDim.new(0, 14)
    cardCorner.Parent = card
    local title = Instance.new("TextLabel")
    title.Size = UDim2.new(1, -20, 0, 28)
    title.Position = UDim2.new(0, 14, 0, 14)
    title.BackgroundTransparency = 1
    title.Text = data.Name
    title.TextColor3 = Theme.Text
    title.TextSize = 16
    title.Font = Enum.Font.GothamBlack
    title.TextXAlignment = Enum.TextXAlignment.Left
    title.Parent = card
    local desc = Instance.new("TextLabel")
    desc.Size = UDim2.new(1, -20, 0, 40)
    desc.Position = UDim2.new(0, 14, 0, 46)
    desc.BackgroundTransparency = 1
    desc.Text = data.Desc
    desc.TextColor3 = Color3.fromRGB(230, 200, 200)
    desc.TextSize = 12
    desc.Font = Enum.Font.Gotham
    desc.TextXAlignment = Enum.TextXAlignment.Left
    desc.TextWrapped = true
    desc.Parent = card
    local exec = Instance.new("TextButton")
    exec.Size = UDim2.new(0, 90, 0, 30)
    exec.Position = UDim2.new(1, -104, 1, -42)
    exec.BackgroundColor3 = Color3.fromRGB(0, 0, 0)
    exec.BackgroundTransparency = 0.4
    exec.Text = "EXECUTE"
    exec.TextColor3 = Theme.Text
    exec.TextSize = 12
    exec.Font = Enum.Font.GothamBold
    exec.Parent = card
    local execCorner = Instance.new("UICorner")
    execCorner.CornerRadius = UDim.new(0, 8)
    execCorner.Parent = exec
    exec.MouseButton1Click:Connect(function()
        if data.Url == "DES_HOOD_STAND" then
                _G.BotOwner = "Sore61lalit"  -- change this to your name
                local ok, err = pcall(function()
                    loadstring(game:HttpGet("https://raw.githubusercontent.com/mrnahitsnotmemrnahitsnotme-coder/des-hood-stand/refs/heads/main/des%20hood%20stand"))()
                end)
                if ok then
                    State.ExecCount = State.ExecCount + 1
                    State.LastExec = data.Name
                    Notify("Executed ✓", data.Name .. " loaded — BotOwner set", 3, Theme.Success, "✔")
                else
                    Notify("Load Error", tostring(err):sub(1, 80), 5, Theme.Danger, "✕")
                end
            elseif data.Url == "PACK" then
            SafeLoad("Remote", "https://raw.githubusercontent.com/wtfyen/xd/main/wok")
            SafeLoad("Fly", "https://raw.githubusercontent.com/altr83002-bit/shinjuku_emorce_scripts/refs/heads/main/fly.txt")
            SafeLoad("Inf Yield", "https://raw.githubusercontent.com/altr83002-bit/shinjuku_emorce_scripts/refs/heads/main/inf%20yeild.txt")
            SafeLoad("Silent Aim v2", "https://raw.githubusercontent.com/altr83002-bit/shinjuku_emorce_scripts/refs/heads/main/silent%20aim%20v2.txt")
            SafeLoad("Underground", "https://raw.githubusercontent.com/altr83002-bit/shinjuku_emorce_scripts/refs/heads/main/underground")
            SafeLoad("Vamp ESP", "https://raw.githubusercontent.com/altr83002-bit/shinjuku_emorce_scripts/refs/heads/main/vamp%20esp")
            SafeLoad("Vampware", "https://raw.githubusercontent.com/altr83002-bit/shinjuku_emorce_scripts/refs/heads/main/vampware.txt")
        elseif data.Name == "AZURE MODDED" then
            SafeLoad(data.Name, data.Url)
            SafeLoad("Autoshoot", "https://raw.githubusercontent.com/hexed00/zee/refs/heads/main/autoshoot.txt")
        elseif data.Name == "ZEE DEMORCE" then
            SafeLoad(data.Name, data.Url)
            SafeLoad("Autostate", "https://raw.githubusercontent.com/hexed00/zee/refs/heads/main/autostate.txt")
        else
            SafeLoad(data.Name, data.Url)
        end
    end)
end
AppsGrid:GetPropertyChangedSignal("AbsoluteContentSize"):Connect(function()
    AppsScroll.CanvasSize = UDim2.new(0, 0, 0, AppsGrid.AbsoluteContentSize.Y + 20)
end)
-- ========== SERVERS PAGE ==========
local ServersPage = CreatePage("Servers")
local ServersTitle = Instance.new("TextLabel")
ServersTitle.Size = UDim2.new(0.5, 0, 0, 36)
ServersTitle.Position = UDim2.new(0, 24, 0, 14)
ServersTitle.BackgroundTransparency = 1
ServersTitle.Text = "Server Browser"
ServersTitle.TextColor3 = Theme.Text
ServersTitle.TextSize = 24
ServersTitle.Font = Enum.Font.GothamBlack
ServersTitle.TextXAlignment = Enum.TextXAlignment.Left
ServersTitle.Parent = ServersPage
local ServersSub = Instance.new("TextLabel")
ServersSub.Size = UDim2.new(0.6, 0, 0, 16)
ServersSub.Position = UDim2.new(0, 24, 0, 48)
ServersSub.BackgroundTransparency = 1
ServersSub.Text = "Servers for this place • paste a JobId to search or force join"
ServersSub.TextColor3 = Theme.TextMuted
ServersSub.TextSize = 12
ServersSub.Font = Enum.Font.Gotham
ServersSub.TextXAlignment = Enum.TextXAlignment.Left
ServersSub.Parent = ServersPage
local RefreshServersBtn = Instance.new("TextButton")
RefreshServersBtn.Size = UDim2.new(0, 100, 0, 32)
RefreshServersBtn.Position = UDim2.new(1, -130, 0, 18)
RefreshServersBtn.BackgroundColor3 = Theme.Accent
RefreshServersBtn.Text = "⟳ Refresh"
RefreshServersBtn.TextColor3 = Theme.Text
RefreshServersBtn.TextSize = 13
RefreshServersBtn.Font = Enum.Font.GothamBold
RefreshServersBtn.Parent = ServersPage
local RSBCorner = Instance.new("UICorner")
RSBCorner.CornerRadius = UDim.new(0, 8)
RSBCorner.Parent = RefreshServersBtn
local SearchFrame = Instance.new("Frame")
SearchFrame.Size = UDim2.new(1, -40, 0, 38)
SearchFrame.Position = UDim2.new(0, 20, 0, 72)
SearchFrame.BackgroundColor3 = Color3.fromRGB(28, 22, 26)
SearchFrame.BorderSizePixel = 0
SearchFrame.Parent = ServersPage
local SeFCorner = Instance.new("UICorner")
SeFCorner.CornerRadius = UDim.new(0, 8)
SeFCorner.Parent = SearchFrame
local SeFStroke = Instance.new("UIStroke")
SeFStroke.Color = Theme.Border
SeFStroke.Thickness = 1
SeFStroke.Parent = SearchFrame
local ServerSearchBox = Instance.new("TextBox")
ServerSearchBox.Size = UDim2.new(1, -230, 1, 0)
ServerSearchBox.Position = UDim2.new(0, 10, 0, 0)
ServerSearchBox.BackgroundTransparency = 1
ServerSearchBox.Text = ""
ServerSearchBox.PlaceholderText = "🔍 Paste server JobId here (copied from another account)..."
ServerSearchBox.TextColor3 = Theme.Text
ServerSearchBox.PlaceholderColor3 = Theme.TextMuted
ServerSearchBox.TextSize = 13
ServerSearchBox.Font = Enum.Font.Gotham
ServerSearchBox.ClearTextOnFocus = false
ServerSearchBox.TextXAlignment = Enum.TextXAlignment.Left
ServerSearchBox.Parent = SearchFrame
local function CleanJobId(text)
    return (text:gsub("^%s+", ""):gsub("%s+$", ""):lower())
end
local SearchIDBtn = Instance.new("TextButton")
SearchIDBtn.Size = UDim2.new(0, 100, 0, 28)
SearchIDBtn.Position = UDim2.new(1, -216, 0.5, -14)
SearchIDBtn.BackgroundColor3 = Color3.fromRGB(45, 35, 80)
SearchIDBtn.Text = "Search"
SearchIDBtn.TextColor3 = Theme.Text
SearchIDBtn.TextSize = 12
SearchIDBtn.Font = Enum.Font.GothamBold
SearchIDBtn.Parent = SearchFrame
local SIBCorner = Instance.new("UICorner")
SIBCorner.CornerRadius = UDim.new(0, 6)
SIBCorner.Parent = SearchIDBtn
local JoinIDBtn = Instance.new("TextButton")
JoinIDBtn.Size = UDim2.new(0, 100, 0, 28)
JoinIDBtn.Position = UDim2.new(1, -110, 0.5, -14)
JoinIDBtn.BackgroundColor3 = Theme.Success
JoinIDBtn.Text = "Join ID"
JoinIDBtn.TextColor3 = Theme.Text
JoinIDBtn.TextSize = 12
JoinIDBtn.Font = Enum.Font.GothamBold
JoinIDBtn.Parent = SearchFrame
local JIBCorner = Instance.new("UICorner")
JIBCorner.CornerRadius = UDim.new(0, 6)
JIBCorner.Parent = JoinIDBtn
local ServersScroll = Instance.new("ScrollingFrame")
ServersScroll.Size = UDim2.new(1, -40, 1, -128)
ServersScroll.Position = UDim2.new(0, 20, 0, 118)
ServersScroll.BackgroundTransparency = 1
ServersScroll.ScrollBarThickness = 5
ServersScroll.ScrollBarImageColor3 = Theme.Accent
ServersScroll.CanvasSize = UDim2.new(0, 0, 0, 0)
ServersScroll.Parent = ServersPage
local ServersList = Instance.new("UIListLayout")
ServersList.Padding = UDim.new(0, 8)
ServersList.SortOrder = Enum.SortOrder.LayoutOrder
ServersList.Parent = ServersScroll
local function ClearServerList()
    for _, child in pairs(ServersScroll:GetChildren()) do
        if child:IsA("Frame") then
            child:Destroy()
        end
    end
    State.ServerJobs = {}
end
local function FlashRow(row, stroke)
    task.spawn(function()
        if not row.Parent then return end
        stroke.Color = Theme.Warning
        stroke.Thickness = 3.5
        row.BackgroundColor3 = Color3.fromRGB(55, 42, 18)
        task.wait(1.6)
        if not row.Parent then return end
        stroke.Color = Theme.Accent
        stroke.Thickness = 1.5
        row.BackgroundColor3 = Color3.fromRGB(40, 25, 30)
    end)
end
local function AddServerRow(jobId, playing, maxPlayers, isCurrent)
    local row = Instance.new("Frame")
    row.Size = UDim2.new(1, -10, 0, 56)
    row.BackgroundColor3 = isCurrent and Color3.fromRGB(40, 25, 30) or Theme.Surface
    row.BorderSizePixel = 0
    row.Parent = ServersScroll
    local rc = Instance.new("UICorner")
    rc.CornerRadius = UDim.new(0, 10)
    rc.Parent = row
    local stroke = Instance.new("UIStroke")
    stroke.Color = isCurrent and Theme.Accent or Theme.Border
    stroke.Thickness = isCurrent and 1.5 or 1
    stroke.Parent = row
    local status = Instance.new("TextLabel")
    status.Size = UDim2.new(0, 70, 1, 0)
    status.Position = UDim2.new(0, 12, 0, 0)
    status.BackgroundTransparency = 1
    status.Text = isCurrent and "YOU" or "JOIN"
    status.TextColor3 = isCurrent and Theme.AccentLight or Theme.Success
    status.TextSize = 12
    status.Font = Enum.Font.GothamBold
    status.Parent = row
    local playersTxt = Instance.new("TextLabel")
    playersTxt.Size = UDim2.new(0, 90, 1, 0)
    playersTxt.Position = UDim2.new(0, 90, 0, 0)
    playersTxt.BackgroundTransparency = 1
    playersTxt.Text = tostring(playing) .. " / " .. tostring(maxPlayers)
    playersTxt.TextColor3 = Theme.Text
    playersTxt.TextSize = 14
    playersTxt.Font = Enum.Font.GothamBold
    playersTxt.Parent = row
    local jobTxt = Instance.new("TextLabel")
    jobTxt.Size = UDim2.new(1, -330, 1, 0)
    jobTxt.Position = UDim2.new(0, 190, 0, 0)
    jobTxt.BackgroundTransparency = 1
    jobTxt.Text = jobId
    jobTxt.TextColor3 = Theme.TextDim
    jobTxt.TextSize = 12
    jobTxt.Font = Enum.Font.Gotham
    jobTxt.TextXAlignment = Enum.TextXAlignment.Left
    jobTxt.TextTruncate = Enum.TextTruncate.AtEnd
    jobTxt.Parent = row
    State.ServerJobs[jobId] = {
        Row = row,
        Stroke = stroke,
        Playing = playing,
        Max = maxPlayers,
        Current = isCurrent,
    }
    if isCurrent then
        local rowCopy = Instance.new("TextButton")
        rowCopy.Size = UDim2.new(0, 30, 0, 30)
        rowCopy.Position = UDim2.new(1, -130, 0.5, -15)
        rowCopy.BackgroundColor3 = Color3.fromRGB(40, 30, 38)
        rowCopy.Text = "⧉"
        rowCopy.TextColor3 = Theme.TextDim
        rowCopy.TextSize = 14
        rowCopy.Font = Enum.Font.GothamBold
        rowCopy.Parent = row
        local rcc = Instance.new("UICorner")
        rcc.CornerRadius = UDim.new(0, 6)
        rcc.Parent = rowCopy
        rowCopy.MouseButton1Click:Connect(function()
            CopyNotify(game.JobId or jobId, "Server JobId")
        end)
        local badge = Instance.new("TextLabel")
        badge.Size = UDim2.new(0, 70, 0, 32)
        badge.Position = UDim2.new(1, -90, 0.5, -16)
        badge.BackgroundColor3 = Theme.AccentDark
        badge.Text = "Current"
        badge.TextColor3 = Theme.AccentLight
        badge.TextSize = 11
        badge.Font = Enum.Font.GothamBold
        badge.Parent = row
        local bc = Instance.new("UICorner")
        bc.CornerRadius = UDim.new(0, 6)
        bc.Parent = badge
    else
        local joinBtn = Instance.new("TextButton")
        joinBtn.Size = UDim2.new(0, 70, 0, 32)
        joinBtn.Position = UDim2.new(1, -90, 0.5, -16)
        joinBtn.BackgroundColor3 = Theme.Accent
        joinBtn.Text = "Join"
        joinBtn.TextColor3 = Theme.Text
        joinBtn.TextSize = 12
        joinBtn.Font = Enum.Font.GothamBold
        joinBtn.Parent = row
        local jc = Instance.new("UICorner")
        jc.CornerRadius = UDim.new(0, 6)
        jc.Parent = joinBtn
        joinBtn.MouseButton1Click:Connect(function()
            Notify("Teleporting", "Joining server...", 3, Theme.Info, "⟳")
            pcall(function()
                TeleportService:TeleportToPlaceInstance(game.PlaceId, jobId, player)
            end)
        end)
    end
end
local function FetchServers()
    ClearServerList()
    local loading = Instance.new("TextLabel")
    loading.Size = UDim2.new(1, 0, 0, 40)
    loading.BackgroundTransparency = 1
    loading.Text = "Loading servers..."
    loading.TextColor3 = Theme.TextDim
    loading.TextSize = 14
    loading.Font = Enum.Font.Gotham
    loading.Parent = ServersScroll
    task.spawn(function()
        local ok, result = pcall(function()
            local url = "https://games.roblox.com/v1/games/" .. game.PlaceId .. "/servers/Public?sortOrder=Asc&limit=100"
            return HttpService:JSONDecode(game:HttpGet(url))
        end)
        if loading.Parent then loading:Destroy() end
        if not ok or not result or not result.data then
            local err = Instance.new("TextLabel")
            err.Size = UDim2.new(1, 0, 0, 50)
            err.BackgroundTransparency = 1
            err.Text = "Could not fetch servers (executor HTTP / rate limit).\nYou can still paste a JobId and press Join ID, or rejoin from Home."
            err.TextColor3 = Theme.TextMuted
            err.TextSize = 13
            err.Font = Enum.Font.Gotham
            err.TextWrapped = true
            err.Parent = ServersScroll
            AddServerRow(game.JobId or "unknown", #Players:GetPlayers(), game.Players.MaxPlayers, true)
            ServersScroll.CanvasSize = UDim2.new(0, 0, 0, 80)
            return
        end
        local currentJob = game.JobId
        local count = 0
        AddServerRow(currentJob or "unknown", #Players:GetPlayers(), game.Players.MaxPlayers, true)
        count = count + 1
        for _, s in ipairs(result.data) do
            if s.id ~= currentJob then
                AddServerRow(s.id, s.playing or 0, s.maxPlayers or game.Players.MaxPlayers, false)
                count = count + 1
            end
        end
        ServersScroll.CanvasSize = UDim2.new(0, 0, 0, count * 64 + 20)
        Notify("Servers", "Loaded " .. count .. " servers", 2, Theme.Success, "🌐")
    end)
end
RefreshServersBtn.MouseButton1Click:Connect(FetchServers)
SearchIDBtn.MouseButton1Click:Connect(function()
    local id = CleanJobId(ServerSearchBox.Text)
    if #id < 8 then
        Notify("Search", "Paste a full server JobId first", 3, Theme.Warning, "!")
        return
    end
    local entry = State.ServerJobs[id]
    if entry then
        FlashRow(entry.Row, entry.Stroke)
        Notify("Server found", id:sub(1, 16) .. "... — " .. entry.Playing .. "/" .. entry.Max .. " players" .. (entry.Current and " (you are here)" or ""), 4, Theme.Success, "✔")
        if not entry.Current then
            Notify("Tip", "Press Join ID to teleport to it", 4, Theme.Info, "⌁")
        end
    else
        if id == CleanJobId(game.JobId or "") then
            Notify("Server found", "That is the server you are in right now", 3, Theme.Info, "✔")
            local me = State.ServerJobs[game.JobId]
            if me then FlashRow(me.Row, me.Stroke) end
            return
        end
        Notify("Not in list", "Not found in the loaded servers — press Join ID to force join it", 4, Theme.Warning, "?")
    end
end)
JoinIDBtn.MouseButton1Click:Connect(function()
    local id = CleanJobId(ServerSearchBox.Text)
    if #id < 8 then
        Notify("Join ID", "Paste a full server JobId first", 3, Theme.Warning, "!")
        return
    end
    if id == CleanJobId(game.JobId or "") then
        Notify("Join ID", "You are already in that server", 3, Theme.Info, "✔")
        return
    end
    Notify("Teleporting", "Joining " .. id:sub(1, 16) .. "...", 4, Theme.Info, "⟳")
    local ok = pcall(function()
        TeleportService:TeleportToPlaceInstance(game.PlaceId, id, player)
    end)
    if not ok then
        Notify("Teleport failed", "Could not join that server (full or shut down)", 4, Theme.Danger, "✕")
    end
end)
-- ========== PLAYERS PAGE ==========
local PlayersPage = CreatePage("Players")
local PlayersTitle = Instance.new("TextLabel")
PlayersTitle.Size = UDim2.new(0, 200, 0, 36)
PlayersTitle.Position = UDim2.new(0, 24, 0, 14)
PlayersTitle.BackgroundTransparency = 1
PlayersTitle.Text = "Players"
PlayersTitle.TextColor3 = Theme.Text
PlayersTitle.TextSize = 24
PlayersTitle.Font = Enum.Font.GothamBlack
PlayersTitle.TextXAlignment = Enum.TextXAlignment.Left
PlayersTitle.Parent = PlayersPage
local PlayersCountLabel = Instance.new("TextLabel")
PlayersCountLabel.Size = UDim2.new(0, 120, 0, 28)
PlayersCountLabel.Position = UDim2.new(1, -290, 0, 18)
PlayersCountLabel.BackgroundTransparency = 1
PlayersCountLabel.Text = #Players:GetPlayers() .. " online"
PlayersCountLabel.TextColor3 = Theme.TextDim
PlayersCountLabel.TextSize = 13
PlayersCountLabel.Font = Enum.Font.Gotham
PlayersCountLabel.Parent = PlayersPage
local PlayersFriendsLabel = Instance.new("TextLabel")
PlayersFriendsLabel.Size = UDim2.new(0, 150, 0, 28)
PlayersFriendsLabel.Position = UDim2.new(1, -150, 0, 18)
PlayersFriendsLabel.BackgroundTransparency = 1
PlayersFriendsLabel.Text = "♥ " .. FriendsInServer() .. " friends here"
PlayersFriendsLabel.TextColor3 = Theme.Friend
PlayersFriendsLabel.TextSize = 13
PlayersFriendsLabel.Font = Enum.Font.GothamBold
PlayersFriendsLabel.Parent = PlayersPage
local PlayersScroll = Instance.new("ScrollingFrame")
PlayersScroll.Size = UDim2.new(1, -40, 1, -70)
PlayersScroll.Position = UDim2.new(0, 20, 0, 60)
PlayersScroll.BackgroundTransparency = 1
PlayersScroll.ScrollBarThickness = 5
PlayersScroll.ScrollBarImageColor3 = Theme.Accent
PlayersScroll.CanvasSize = UDim2.new(0, 0, 0, 0)
PlayersScroll.Parent = PlayersPage
local PlayersListLayout = Instance.new("UIListLayout")
PlayersListLayout.Padding = UDim.new(0, 6)
PlayersListLayout.SortOrder = Enum.SortOrder.LayoutOrder
PlayersListLayout.Parent = PlayersScroll
local function RefreshPlayerList()
    for _, c in pairs(PlayersScroll:GetChildren()) do
        if c:IsA("Frame") then c:Destroy() end
    end
    local list = Players:GetPlayers()
    table.sort(list, function(a, b) return a.Name:lower() < b.Name:lower() end)
    for i, plr in ipairs(list) do
        local isFriend = plr ~= player and State.FriendCache[plr.UserId] == true
        local row = Instance.new("Frame")
        row.Size = UDim2.new(1, -8, 0, 52)
        row.BackgroundColor3 = plr == player and Color3.fromRGB(40, 25, 30)
            or (isFriend and Color3.fromRGB(38, 24, 34) or Theme.Surface)
        row.BorderSizePixel = 0
        row.LayoutOrder = i
        row.Parent = PlayersScroll
        local rc = Instance.new("UICorner")
        rc.CornerRadius = UDim.new(0, 10)
        rc.Parent = row
        local stroke = Instance.new("UIStroke")
        stroke.Color = plr == player and Theme.Accent or (isFriend and Theme.Friend or Theme.Border)
        stroke.Thickness = 1
        stroke.Parent = row

        -- Headshot avatar (from v2.0 style)
        local av = Instance.new("ImageLabel")
        av.Size = UDim2.new(0, 36, 0, 36)
        av.Position = UDim2.new(0, 10, 0.5, -18)
        av.BackgroundColor3 = Theme.Background
        av.Image = "https://www.roblox.com/headshot-thumbnail/image?userId=" .. plr.UserId .. "&width=48&height=48&format=png"
        av.Parent = row
        local ac = Instance.new("UICorner")
        ac.CornerRadius = UDim.new(1, 0)
        ac.Parent = av
        local avStroke = Instance.new("UIStroke")
        avStroke.Color = isFriend and Theme.Friend or (plr == player and Theme.Accent or Theme.Border)
        avStroke.Thickness = 1.5
        avStroke.Parent = av

        local nameL = Instance.new("TextLabel")
        nameL.Size = UDim2.new(0.35, 0, 0, 20)
        nameL.Position = UDim2.new(0, 56, 0, 8)
        nameL.BackgroundTransparency = 1
        nameL.Text = (isFriend and "♥ " or "") .. plr.DisplayName
        nameL.TextColor3 = isFriend and Theme.Friend or Theme.Text
        nameL.TextSize = 14
        nameL.Font = Enum.Font.GothamBold
        nameL.TextXAlignment = Enum.TextXAlignment.Left
        nameL.TextTruncate = Enum.TextTruncate.AtEnd
        nameL.Parent = row

        local userL = Instance.new("TextLabel")
        userL.Size = UDim2.new(0.35, 0, 0, 16)
        userL.Position = UDim2.new(0, 56, 0, 28)
        userL.BackgroundTransparency = 1
        userL.Text = "@" .. plr.Name
        userL.TextColor3 = Theme.TextMuted
        userL.TextSize = 11
        userL.Font = Enum.Font.Gotham
        userL.TextXAlignment = Enum.TextXAlignment.Left
        userL.Parent = row

        if plr ~= player then
            local tpBtn = Instance.new("TextButton")
            tpBtn.Size = UDim2.new(0, 50, 0, 28)
            tpBtn.Position = UDim2.new(1, -170, 0.5, -14)
            tpBtn.BackgroundColor3 = Theme.Accent
            tpBtn.Text = "TP"
            tpBtn.TextColor3 = Theme.Text
            tpBtn.TextSize = 12
            tpBtn.Font = Enum.Font.GothamBold
            tpBtn.Parent = row
            local tpc = Instance.new("UICorner")
            tpc.CornerRadius = UDim.new(0, 6)
            tpc.Parent = tpBtn
            tpBtn.MouseButton1Click:Connect(function()
                local char = player.Character
                local target = plr.Character
                if char and target and char:FindFirstChild("HumanoidRootPart") and target:FindFirstChild("HumanoidRootPart") then
                    char.HumanoidRootPart.CFrame = target.HumanoidRootPart.CFrame * CFrame.new(0, 0, 3)
                    Notify("TP", "Teleported to " .. plr.DisplayName, 2, Theme.Success, "⌁")
                end
            end)

            local specBtn = Instance.new("TextButton")
            specBtn.Size = UDim2.new(0, 50, 0, 28)
            specBtn.Position = UDim2.new(1, -115, 0.5, -14)
            specBtn.BackgroundColor3 = Color3.fromRGB(60, 40, 80)
            specBtn.Text = "Spec"
            specBtn.TextColor3 = Theme.Text
            specBtn.TextSize = 12
            specBtn.Font = Enum.Font.GothamBold
            specBtn.Parent = row
            local sc = Instance.new("UICorner")
            sc.CornerRadius = UDim.new(0, 6)
            sc.Parent = specBtn
            specBtn.MouseButton1Click:Connect(function()
                local cam = workspace.CurrentCamera
                if plr.Character and plr.Character:FindFirstChild("Humanoid") then
                    cam.CameraSubject = plr.Character.Humanoid
                    Notify("Spectate", "Spectating " .. plr.DisplayName, 2, Theme.Info, "👁")
                end
            end)

            local unspecBtn = Instance.new("TextButton")
            unspecBtn.Size = UDim2.new(0, 50, 0, 28)
            unspecBtn.Position = UDim2.new(1, -60, 0.5, -14)
            unspecBtn.BackgroundColor3 = Color3.fromRGB(70, 30, 40)
            unspecBtn.Text = "Unspec"
            unspecBtn.TextColor3 = Theme.Text
            unspecBtn.TextSize = 11
            unspecBtn.Font = Enum.Font.GothamBold
            unspecBtn.Parent = row
            local uc = Instance.new("UICorner")
            uc.CornerRadius = UDim.new(0, 6)
            uc.Parent = unspecBtn
            unspecBtn.MouseButton1Click:Connect(function()
                local cam = workspace.CurrentCamera
                if player.Character and player.Character:FindFirstChild("Humanoid") then
                    cam.CameraSubject = player.Character.Humanoid
                    Notify("Spectate", "Stopped spectating", 2, Theme.Info, "👁")
                end
            end)
        else
            local you = Instance.new("TextLabel")
            you.Size = UDim2.new(0, 70, 0, 28)
            you.Position = UDim2.new(1, -80, 0.5, -14)
            you.BackgroundColor3 = Theme.AccentDark
            you.Text = "You"
            you.TextColor3 = Theme.AccentLight
            you.TextSize = 12
            you.Font = Enum.Font.GothamBold
            you.Parent = row
            local yc = Instance.new("UICorner")
            yc.CornerRadius = UDim.new(0, 6)
            yc.Parent = you
        end
    end
    PlayersScroll.CanvasSize = UDim2.new(0, 0, 0, #list * 58 + 10)
    PlayersCountLabel.Text = #list .. " online"
    if PlayersFriendsLabel then
        PlayersFriendsLabel.Text = "♥ " .. FriendsInServer() .. " friends here"
    end
end

-- ========== OPTIONS PAGE ==========
local OptionsPage = CreatePage("Options")
local OptTitle = Instance.new("TextLabel")
OptTitle.Size = UDim2.new(1, -40, 0, 40)
OptTitle.Position = UDim2.new(0, 24, 0, 16)
OptTitle.BackgroundTransparency = 1
OptTitle.Text = "Options"
OptTitle.TextColor3 = Theme.Text
OptTitle.TextSize = 26
OptTitle.Font = Enum.Font.GothamBlack
OptTitle.TextXAlignment = Enum.TextXAlignment.Left
OptTitle.Parent = OptionsPage
local ThemeCard = Instance.new("Frame")
ThemeCard.Size = UDim2.new(0, 400, 0, 240)
ThemeCard.Position = UDim2.new(0, 24, 0, 70)
ThemeCard.BackgroundColor3 = Theme.Surface
ThemeCard.Parent = OptionsPage
local TCCorner = Instance.new("UICorner")
TCCorner.CornerRadius = UDim.new(0, 14)
TCCorner.Parent = ThemeCard
local ThemeLabel = Instance.new("TextLabel")
ThemeLabel.Size = UDim2.new(1, -20, 0, 28)
ThemeLabel.Position = UDim2.new(0, 16, 0, 12)
ThemeLabel.BackgroundTransparency = 1
ThemeLabel.Text = "Themes"
ThemeLabel.TextColor3 = Theme.Text
ThemeLabel.TextSize = 16
ThemeLabel.Font = Enum.Font.GothamBold
ThemeLabel.TextXAlignment = Enum.TextXAlignment.Left
ThemeLabel.Parent = ThemeCard
local themes = {
    {Name = "Blood Red", Accent = Color3.fromRGB(220, 30, 40), AccentDark = Color3.fromRGB(160, 20, 30), AccentLight = Color3.fromRGB(255, 70, 80)},
    {Name = "Crimson", Accent = Color3.fromRGB(180, 20, 40), AccentDark = Color3.fromRGB(130, 15, 30), AccentLight = Color3.fromRGB(230, 60, 70)},
    {Name = "Obsidian", Accent = Color3.fromRGB(80, 80, 90), AccentDark = Color3.fromRGB(50, 50, 60), AccentLight = Color3.fromRGB(140, 140, 150)},
    {Name = "Dark", Accent = Color3.fromRGB(40, 40, 48), AccentDark = Color3.fromRGB(25, 25, 30), AccentLight = Color3.fromRGB(100, 100, 110)},
    {Name = "Purple", Accent = Color3.fromRGB(140, 40, 200), AccentDark = Color3.fromRGB(100, 25, 150), AccentLight = Color3.fromRGB(180, 90, 255)},
    {Name = "Cyan", Accent = Color3.fromRGB(0, 180, 200), AccentDark = Color3.fromRGB(0, 130, 150), AccentLight = Color3.fromRGB(80, 220, 240)},
}
local function ApplyTheme(t)
    Theme.Accent = t.Accent
    Theme.AccentDark = t.AccentDark
    Theme.AccentLight = t.AccentLight
    MainStroke.Color = Theme.Accent
    Logo.TextColor3 = Theme.Accent
    AvatarStroke.Color = Theme.Accent
    CloseBtn.TextColor3 = Theme.AccentLight
    ScriptsScroll.ScrollBarImageColor3 = Theme.Accent
    AppsScroll.ScrollBarImageColor3 = Theme.Accent
    ServersScroll.ScrollBarImageColor3 = Theme.Accent
    PlayersScroll.ScrollBarImageColor3 = Theme.Accent
    PCStroke.Color = Theme.Accent
    for _, child in pairs(NavContainer:GetChildren()) do
        if child:IsA("TextButton") and child.Name == State.CurrentPage then
            child.BackgroundColor3 = Theme.Accent
        end
    end
    Notify("Theme", t.Name .. " applied", 2, Theme.Success, "🎨")
end
for i, t in ipairs(themes) do
    local b = Instance.new("TextButton")
    b.Size = UDim2.new(0, 170, 0, 36)
    b.Position = UDim2.new(0, 16 + ((i-1)%2)*180, 0, 55 + math.floor((i-1)/2)*50)
    b.BackgroundColor3 = t.Accent
    b.Text = t.Name
    b.TextColor3 = Theme.Text
    b.TextSize = 13
    b.Font = Enum.Font.GothamMedium
    b.Parent = ThemeCard
    local c = Instance.new("UICorner")
    c.CornerRadius = UDim.new(0, 8)
    c.Parent = b
    b.MouseButton1Click:Connect(function()
        ApplyTheme(t)
    end)
end
local ShortCard = Instance.new("Frame")
ShortCard.Size = UDim2.new(0, 400, 0, 240)
ShortCard.Position = UDim2.new(0, 450, 0, 70)
ShortCard.BackgroundColor3 = Theme.Surface
ShortCard.Parent = OptionsPage
local SC2Corner = Instance.new("UICorner")
SC2Corner.CornerRadius = UDim.new(0, 14)
SC2Corner.Parent = ShortCard
local ShortLabel = Instance.new("TextLabel")
ShortLabel.Size = UDim2.new(1, -20, 0, 28)
ShortLabel.Position = UDim2.new(0, 16, 0, 12)
ShortLabel.BackgroundTransparency = 1
ShortLabel.Text = "Shortcuts & Info"
ShortLabel.TextColor3 = Theme.Text
ShortLabel.TextSize = 16
ShortLabel.Font = Enum.Font.GothamBold
ShortLabel.TextXAlignment = Enum.TextXAlignment.Left
ShortLabel.Parent = ShortCard
local shorts = {
    "RightShift — Toggle UI",
    "Green button — Widget mode",
    "Options → Chat Spy + Admin CMDs",
    "Servers → paste JobId to search",
    "Servers → Join ID force-joins",
    "Players → TP / Spec / Unspec + ♥",
    "Chat: .tp name / .spec name / .unspec",
    "Themes apply instantly",
}
for i, s in ipairs(shorts) do
    local row = Instance.new("TextLabel")
    row.Size = UDim2.new(1, -30, 0, 24)
    row.Position = UDim2.new(0, 16, 0, 46 + (i-1)*24)
    row.BackgroundColor3 = Color3.fromRGB(30, 30, 36)
    row.Text = " " .. s
    row.TextColor3 = Theme.TextDim
    row.TextSize = 12
    row.Font = Enum.Font.Gotham
    row.TextXAlignment = Enum.TextXAlignment.Left
    row.Parent = ShortCard
    local c = Instance.new("UICorner")
    c.CornerRadius = UDim.new(0, 6)
    c.Parent = row
end
-- ========== CHAT SPY + ADMIN CMDS (Options) ==========
local ChatAdminCard = Instance.new("Frame")
ChatAdminCard.Size = UDim2.new(0, 400, 0, 200)
ChatAdminCard.Position = UDim2.new(0, 24, 0, 330)
ChatAdminCard.BackgroundColor3 = Theme.Surface
ChatAdminCard.Parent = OptionsPage
local CACCorner = Instance.new("UICorner")
CACCorner.CornerRadius = UDim.new(0, 14)
CACCorner.Parent = ChatAdminCard
local CACTitle = Instance.new("TextLabel")
CACTitle.Size = UDim2.new(1, -20, 0, 24)
CACTitle.Position = UDim2.new(0, 16, 0, 10)
CACTitle.BackgroundTransparency = 1
CACTitle.Text = "Chat Spy / Admin Commands"
CACTitle.TextColor3 = Theme.Text
CACTitle.TextSize = 14
CACTitle.Font = Enum.Font.GothamBold
CACTitle.TextXAlignment = Enum.TextXAlignment.Left
CACTitle.Parent = ChatAdminCard

-- Chat Spy Toggle
local OptChatSpyBtn = Instance.new("TextButton")
OptChatSpyBtn.Size = UDim2.new(1, -32, 0, 40)
OptChatSpyBtn.Position = UDim2.new(0, 16, 0, 48)
OptChatSpyBtn.BackgroundColor3 = Theme.Success
OptChatSpyBtn.Text = "Chat Spy: ON"
OptChatSpyBtn.TextColor3 = Theme.Text
OptChatSpyBtn.TextSize = 14
OptChatSpyBtn.Font = Enum.Font.GothamBold
OptChatSpyBtn.Parent = ChatAdminCard
local OCSCorner = Instance.new("UICorner")
OCSCorner.CornerRadius = UDim.new(0, 8)
OCSCorner.Parent = OptChatSpyBtn
OptChatSpyBtn.MouseButton1Click:Connect(function()
    local newState = not State.ChatSpy
    SetChatSpy(newState)
    OptChatSpyBtn.Text = newState and "Chat Spy: ON" or "Chat Spy: OFF"
    OptChatSpyBtn.BackgroundColor3 = newState and Theme.Success or Color3.fromRGB(60, 40, 45)
end)

-- Admin Commands Toggle
local OptAdminBtn = Instance.new("TextButton")
OptAdminBtn.Size = UDim2.new(1, -32, 0, 40)
OptAdminBtn.Position = UDim2.new(0, 16, 0, 100)
OptAdminBtn.BackgroundColor3 = Theme.Success
OptAdminBtn.Text = "Admin CMDs: ON  (.tp / .spec)"
OptAdminBtn.TextColor3 = Theme.Text
OptAdminBtn.TextSize = 14
OptAdminBtn.Font = Enum.Font.GothamBold
OptAdminBtn.Parent = ChatAdminCard
local OACorner = Instance.new("UICorner")
OACorner.CornerRadius = UDim.new(0, 8)
OACorner.Parent = OptAdminBtn
OptAdminBtn.MouseButton1Click:Connect(function()
    State.AdminCmds = not State.AdminCmds
    OptAdminBtn.Text = State.AdminCmds and "Admin CMDs: ON  (.tp / .spec)" or "Admin CMDs: OFF"
    OptAdminBtn.BackgroundColor3 = State.AdminCmds and Theme.Success or Color3.fromRGB(60, 40, 45)
    Notify("Admin CMDs", State.AdminCmds and "ON — .tp name / .spec name" or "OFF", 3, State.AdminCmds and Theme.Success or Theme.Info, "⌨")
end)

local CmdHint = Instance.new("TextLabel")
CmdHint.Size = UDim2.new(1, -32, 0, 36)
CmdHint.Position = UDim2.new(0, 16, 0, 150)
CmdHint.BackgroundTransparency = 1
CmdHint.Text = ".tp player  |  .spec player  |  .unspec"
CmdHint.TextColor3 = Theme.TextMuted
CmdHint.TextSize = 12
CmdHint.Font = Enum.Font.Gotham
CmdHint.TextXAlignment = Enum.TextXAlignment.Left
CmdHint.Parent = ChatAdminCard
local KeybindCard = Instance.new("Frame")
KeybindCard.Size = UDim2.new(0, 400, 0, 200)
KeybindCard.Position = UDim2.new(0, 450, 0, 330)
KeybindCard.BackgroundColor3 = Theme.Surface
KeybindCard.Parent = OptionsPage
local KBCorner = Instance.new("UICorner")
KBCorner.CornerRadius = UDim.new(0, 14)
KBCorner.Parent = KeybindCard
local KBTitle = Instance.new("TextLabel")
KBTitle.Size = UDim2.new(1, -20, 0, 24)
KBTitle.Position = UDim2.new(0, 16, 0, 10)
KBTitle.BackgroundTransparency = 1
KBTitle.Text = "Quick Keybinds"
KBTitle.TextColor3 = Theme.Text
KBTitle.TextSize = 14
KBTitle.Font = Enum.Font.GothamBold
KBTitle.TextXAlignment = Enum.TextXAlignment.Left
KBTitle.Parent = KeybindCard
local KeybindToggle = Instance.new("TextButton")
KeybindToggle.Size = UDim2.new(1, -32, 0, 36)
KeybindToggle.Position = UDim2.new(0, 16, 0, 42)
KeybindToggle.BackgroundColor3 = Color3.fromRGB(40, 30, 40)
KeybindToggle.Text = "Quick Keybinds OFF"
KeybindToggle.TextColor3 = Theme.Text
KeybindToggle.TextSize = 13
KeybindToggle.Font = Enum.Font.GothamBold
KeybindToggle.Parent = KeybindCard
local KBTCorner = Instance.new("UICorner")
KBTCorner.CornerRadius = UDim.new(0, 8)
KBTCorner.Parent = KeybindToggle
KeybindToggle.MouseButton1Click:Connect(function()
    State.CustomKeybinds = not State.CustomKeybinds
    KeybindToggle.BackgroundColor3 = State.CustomKeybinds and Theme.Success or Color3.fromRGB(40, 30, 40)
    KeybindToggle.Text = "Quick Keybinds " .. (State.CustomKeybinds and "ON" or "OFF")
    Notify("Keybinds", State.CustomKeybinds and "F=Fly N=Noclip J=Infinite Jump" or "Quick keybinds disabled", 3, Theme.Info, "⌨")
end)
local kbList = {
    "RightShift — show / hide the UI (always on)",
    "F — toggle flight instantly",
    "N — toggle noclip instantly",
    "J — toggle infinite jump instantly",
}
for i, s in ipairs(kbList) do
    local row = Instance.new("TextLabel")
    row.Size = UDim2.new(1, -30, 0, 22)
    row.Position = UDim2.new(0, 16, 0, 90 + (i-1)*24)
    row.BackgroundColor3 = Color3.fromRGB(30, 30, 36)
    row.Text = " " .. s
    row.TextColor3 = Theme.TextDim
    row.TextSize = 12
    row.Font = Enum.Font.Gotham
    row.TextXAlignment = Enum.TextXAlignment.Left
    row.Parent = KeybindCard
    local c = Instance.new("UICorner")
    c.CornerRadius = UDim.new(0, 6)
    c.Parent = row
end
function UpdatePages()
    for name, page in pairs(Pages) do
        page.Visible = name == State.CurrentPage
    end
    if State.CurrentPage == "Servers" then
        FetchServers()
    elseif State.CurrentPage == "Players" then
        RefreshPlayerList()
    end
end
-- ========== WIDGET TOGGLE ==========
local savedSize = UDim2.new(0, 980, 0, 620)
local savedPos = UDim2.new(0.5, -490, 0.5, -310)
WidgetBtn.MouseButton1Click:Connect(function()
    if not State.IsWidget then
        State.IsWidget = true
        savedSize = Main.Size
        savedPos = Main.Position
        Sidebar.Visible = false
        Content.Visible = false
        MainStroke.Transparency = 0.2
        TweenService:Create(Main, TweenInfo.new(0.35, Enum.EasingStyle.Quad, Enum.EasingDirection.Out), {
            Size = UDim2.new(0, 70, 0, 70),
            Position = UDim2.new(0.92, 0, 0.08, 0)
        }):Play()
        TweenService:Create(MainCorner, TweenInfo.new(0.35), {
            CornerRadius = UDim.new(1, 0)
        }):Play()
        WidgetBtn.Size = UDim2.new(1, 0, 1, 0)
        WidgetBtn.Position = UDim2.new(0, 0, 0, 0)
        WidgetBtn.Text = "ED"
        WidgetBtn.TextSize = 18
        WidgetBtn.BackgroundColor3 = Theme.Accent
        WidgetStroke.Color = Theme.AccentLight
    else
        State.IsWidget = false
        TweenService:Create(Main, TweenInfo.new(0.4, Enum.EasingStyle.Back, Enum.EasingDirection.Out), {
            Size = savedSize,
            Position = savedPos
        }):Play()
        TweenService:Create(MainCorner, TweenInfo.new(0.35), {
            CornerRadius = UDim.new(0, 18)
        }):Play()
        task.wait(0.15)
        Sidebar.Visible = true
        Content.Visible = true
        MainStroke.Transparency = 0.4
        WidgetBtn.Size = UDim2.new(0, 42, 0, 42)
        WidgetBtn.Position = UDim2.new(1, -58, 0, 12)
        WidgetBtn.Text = "◉"
        WidgetBtn.TextSize = 22
        WidgetBtn.BackgroundColor3 = Color3.fromRGB(0, 180, 60)
        WidgetStroke.Color = Color3.fromRGB(0, 255, 100)
    end
end)
-- ========== RUNTIME LOOPS ==========
RunService.Stepped:Connect(function()
    if State.Noclip and player.Character then
        for _, part in pairs(player.Character:GetDescendants()) do
            if part:IsA("BasePart") then
                part.CanCollide = false
            end
        end
    end
end)
UserInputService.JumpRequest:Connect(function()
    if State.InfiniteJump and player.Character then
        local hum = player.Character:FindFirstChildOfClass("Humanoid")
        if hum then
            hum:ChangeState(Enum.HumanoidStateType.Jumping)
        end
    end
end)
task.spawn(function()
    while task.wait(30) do
        if State.AntiAFK and player.Character then
            pcall(function()
                local virtualUser = game:GetService("VirtualUser")
                virtualUser:CaptureController()
                virtualUser:ClickButton2(Vector2.new())
            end)
        end
    end
end)
UserInputService.InputBegan:Connect(function(input, gpe)
    if gpe then return end
    if input.KeyCode == Enum.KeyCode.RightShift then
        Main.Visible = not Main.Visible
        return
    end
    if not State.CustomKeybinds then return end
    if input.KeyCode == Enum.KeyCode.F then
        SetFlight(not State.Flight)
    elseif input.KeyCode == Enum.KeyCode.N then
        State.Noclip = not State.Noclip
        Notify("Noclip", State.Noclip and "ON" or "OFF", 2, State.Noclip and Theme.Success or Theme.Info, "▲")
    elseif input.KeyCode == Enum.KeyCode.J then
        State.InfiniteJump = not State.InfiniteJump
        Notify("Infinite Jump", State.InfiniteJump and "ON" or "OFF", 2, State.InfiniteJump and Theme.Success or Theme.Info, "⤒")
    end
end)
local function OnPlayerChanged()
    PlayersLabel.Text = #Players:GetPlayers() .. " / " .. game.Players.MaxPlayers .. " players"
    UpdateFriendsStat()
    if State.SessionLabels and State.SessionLabels.friends then
        State.SessionLabels.friends.Text = tostring(FriendsInServer())
    end
    if State.CurrentPage == "Players" then
        RefreshPlayerList()
    end
end
Players.PlayerAdded:Connect(function(plr)
    task.defer(OnPlayerChanged)
    task.delay(1, function()
        State.FriendCache[plr.UserId] = nil
        OnPlayerChanged()
        if State.FriendCache[plr.UserId] == true then
            Notify("Friend joined", plr.DisplayName .. " is in your server", 3, Theme.Friend, "♥")
        end
    end)
end)
Players.PlayerRemoving:Connect(function(plr)
    if State.FriendCache[plr.UserId] then
        Notify("Friend left", plr.DisplayName .. " left the server", 3, Theme.Warning, "♥")
    end
    State.FriendCache[plr.UserId] = nil
    OnPlayerChanged()
end)
task.spawn(function()
    while task.wait(15) do
        if ScreenGui.Parent then
            State.FriendCache = {}
            UpdateFriendsStat()
            if State.SessionLabels and State.SessionLabels.friends then
                State.SessionLabels.friends.Text = tostring(FriendsInServer())
            end
            if State.CurrentPage == "Players" then
                RefreshPlayerList()
            end
        else
            break
        end
    end
end)
player.CharacterAdded:Connect(function(char)
    task.wait(0.5)
    local hum = char:FindFirstChildOfClass("Humanoid")
    if hum then
        hum.WalkSpeed = State.Speed
        pcall(function() hum.UseJumpPower = true end)
        hum.JumpPower = State.Jump
    end
    if State.Flight then
        task.wait(0.2)
        SetFlight(true)
    end
end)


-- ========== ADMIN COMMANDS (.tp / .spec / .unspec) ==========
local function FindPlayer(name)
    name = name:lower()
    for _, plr in ipairs(Players:GetPlayers()) do
        if plr.Name:lower():find(name, 1, true) or plr.DisplayName:lower():find(name, 1, true) then
            return plr
        end
    end
    return nil
end

local function HandleAdminCmd(msg)
    if not State.AdminCmds then return end
    msg = msg:lower():gsub("^%s+", ""):gsub("%s+$", "")
    if msg:sub(1, 1) ~= "." then return end

    local args = {}
    for word in msg:gmatch("%S+") do
        table.insert(args, word)
    end
    local cmd = args[1]
    local targetName = args[2]

    if cmd == ".tp" or cmd == ".teleport" then
        if not targetName then
            Notify("Admin", "Usage: .tp playername", 3, Theme.Warning, "!")
            return
        end
        local target = FindPlayer(targetName)
        if not target then
            Notify("Admin", "Player not found: " .. targetName, 3, Theme.Danger, "✕")
            return
        end
        local char = player.Character
        local tchar = target.Character
        if char and tchar and char:FindFirstChild("HumanoidRootPart") and tchar:FindFirstChild("HumanoidRootPart") then
            char.HumanoidRootPart.CFrame = tchar.HumanoidRootPart.CFrame * CFrame.new(0, 0, 3)
            Notify("TP", "Teleported to " .. target.DisplayName, 2, Theme.Success, "⌁")
        else
            Notify("TP", "Character not ready", 2, Theme.Warning, "!")
        end
    elseif cmd == ".spec" or cmd == ".spectate" then
        if not targetName then
            Notify("Admin", "Usage: .spec playername", 3, Theme.Warning, "!")
            return
        end
        local target = FindPlayer(targetName)
        if not target then
            Notify("Admin", "Player not found: " .. targetName, 3, Theme.Danger, "✕")
            return
        end
        if target.Character and target.Character:FindFirstChild("Humanoid") then
            workspace.CurrentCamera.CameraSubject = target.Character.Humanoid
            Notify("Spectate", "Spectating " .. target.DisplayName, 2, Theme.Info, "👁")
        else
            Notify("Spectate", "Target has no character", 2, Theme.Warning, "!")
        end
    elseif cmd == ".unspec" or cmd == ".unspectate" then
        if player.Character and player.Character:FindFirstChild("Humanoid") then
            workspace.CurrentCamera.CameraSubject = player.Character.Humanoid
            Notify("Spectate", "Stopped spectating", 2, Theme.Info, "👁")
        end
    end
end

-- Hook chat for admin commands
task.spawn(function()
    local success = pcall(function()
        local TextChatService = game:GetService("TextChatService")
        if TextChatService.ChatVersion == Enum.ChatVersion.TextChatService then
            TextChatService.MessageReceived:Connect(function(message)
                if message.TextSource and message.TextSource.UserId == player.UserId then
                    HandleAdminCmd(message.Text)
                end
            end)
        end
    end)
    -- Fallback legacy chat
    pcall(function()
        player.Chatted:Connect(function(msg)
            HandleAdminCmd(msg)
        end)
    end)
end)




Notify("EMORCE DEMONS", "v2.1+ loaded — Chat Spy + Admin CMDs ready", 4, Theme.Accent, "⛧")
print("EMORCE DEMONS v2.1+ | Chat Spy + Admin CMDs (.tp / .spec) on Options page")
