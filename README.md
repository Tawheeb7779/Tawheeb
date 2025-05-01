-- إعدادات الواجهة
local screenGui = Instance.new("ScreenGui")
screenGui.Parent = game.Players.LocalPlayer:WaitForChild("PlayerGui")

local frame = Instance.new("Frame")
frame.Size = UDim2.new(0, 300, 0, 500)
frame.Position = UDim2.new(0.5, -150, 0.5, -250)
frame.BackgroundColor3 = Color3.fromRGB(30, 30, 30)
frame.Parent = screenGui

-- زر الطيران
local flyButton = Instance.new("TextButton")
flyButton.Size = UDim2.new(0, 200, 0, 50)
flyButton.Position = UDim2.new(0.5, -100, 0, 20)
flyButton.Text = "تشغيل الطيران"
flyButton.TextScaled = true
flyButton.BackgroundColor3 = Color3.fromRGB(70, 130, 180)
flyButton.TextColor3 = Color3.new(1, 1, 1)
flyButton.Parent = frame

flyButton.MouseButton1Click:Connect(function()
    loadstring(game:HttpGet("https://pastebin.com/raw/YxU1jv9y"))()
end)

-- تجهيز الشخصية
local char = game.Players.LocalPlayer.Character or game.Players.LocalPlayer.CharacterAdded:Wait()

-- ملابس
local shirtIds = {
    "9059168527",
    "9665807849",
    "10270188752",
    "9448611704"
}

for _, id in pairs(shirtIds) do
    local shirt = Instance.new("Shirt", char)
    shirt.ShirtTemplate = "rbxassetid://" .. id
end

-- تغيير الرأس
local head = char:FindFirstChild("Head")
if head and head:IsA("BasePart") then
    head.MeshId = "rbxassetid://134082579" -- مثال لرأس مخفي
end

-- تأثير النار
local fire = Instance.new("Fire", char:WaitForChild("HumanoidRootPart"))
fire.Size = 10
fire.Heat = 25

-- قائمة الأماكن
local locations = {
    {name = "منزل 1", position = Vector3.new(50, 3, 50)},
    {name = "منزل 2", position = Vector3.new(100, 3, 100)},
    {name = "مستشفى", position = Vector3.new(200, 3, 150)},
    {name = "مدرسة", position = Vector3.new(300, 3, 250)},
    {name = "مركز الشرطة", position = Vector3.new(400, 3, 350)},
    {name = "المطار", position = Vector3.new(500, 3, 450)},
    {name = "المول", position = Vector3.new(600, 3, 550)},
}

-- أزرار التنقل
for i, location in pairs(locations) do
    local button = Instance.new("TextButton")
    button.Size = UDim2.new(1, 0, 0, 30)
    button.Position = UDim2.new(0, 0, 0, 80 + (i * 35))
    button.Text = "الانتقال إلى: " .. location.name
    button.TextColor3 = Color3.new(1, 1, 1)
    button.BackgroundColor3 = Color3.fromRGB(70, 70, 70)
    button.TextScaled = true
    button.Parent = frame

    button.MouseButton1Click:Connect(function()
        char:MoveTo(location.position)
    end)
end

-- معلومات اللاعب
local function addLabel(text, yPos)
    local lbl = Instance.new("TextLabel")
    lbl.Size = UDim2.new(1, 0, 0, 30)
    lbl.Position = UDim2.new(0, 0, 0, yPos)
    lbl.Text = text
    lbl.TextColor3 = Color3.new(1, 1, 1)
    lbl.BackgroundColor3 = Color3.fromRGB(50, 50, 50)
    lbl.TextScaled = true
    lbl.Parent = frame
end

local player = game.Players.LocalPlayer
addLabel("الاسم: " .. player.Name, 340)
addLabel("User ID: " .. player.UserId, 370)
addLabel("تاريخ الإنشاء: " .. player.AccountAge .. " يوم", 400)
addLabel("السكربت: sandShadwoX", 430)

-- زر الإغلاق
local closeButton = Instance.new("TextButton")
closeButton.Size = UDim2.new(0, 100, 0, 40)
closeButton.Position = UDim2.new(0.5, -50, 1, -50)
closeButton.Text = "إغلاق"
closeButton.TextColor3 = Color3.new(1, 1, 1)
closeButton.BackgroundColor3 = Color3.fromRGB(200, 50, 50)
closeButton.TextScaled = true
closeButton.Parent = frame

closeButton.MouseButton1Click:Connect(function()
    screenGui:Destroy()
end)
