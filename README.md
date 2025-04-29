
local Library = loadstring(game:HttpGet("https://raw.githubusercontent.com/xHeptc/Kavo-UI-Library/main/source.lua"))()
local Window = Library.CreateLib("FIlmXr01 [ Encounters ⚔️ Fighting ]", "GrapeTheme")
local Tab = Window:NewTab("Main")
local Section = Tab:NewSection("Main")
Section:NewToggle("InfCharge", "", function(v)
_G.InfCharge = v
end)
Section:NewToggle("InfEnergy", "", function(v)
_G.InfEnergy = v
end)
Section:NewToggle("No Cooldown", "", function(v)
_G.Nocooldown = v
end)
Section:NewButton("HitBox", "", function()
game:GetService("RunService").RenderStepped:connect(function()
for i,v in next, (game:GetService("Players"):GetPlayers()) do
    if v.Name ~= game:GetService("Players").LocalPlayer.Name then
    v.Character.HumanoidRootPart.Size = Vector3.new(25,25,25)
    v.Character.HumanoidRootPart.Transparency = 0.5
    v.Character.HumanoidRootPart.CanCollide = false
    end
end
end)
end)

-- สร้างปุ่ม Toggle ใหม่ที่ไม่เกี่ยวกับ GUI เดิม
local ScreenGui = Instance.new("ScreenGui")
ScreenGui.Name = "CustomToggleGui"
ScreenGui.ResetOnSpawn = false
ScreenGui.Parent = game.Players.LocalPlayer:WaitForChild("PlayerGui")

-- สร้างปุ่ม Toggle
local ToggleButton = Instance.new("TextButton")
ToggleButton.Size = UDim2.new(0, 150, 0, 50)
ToggleButton.Position = UDim2.new(0, 20, 0, 200)
ToggleButton.Text = "Toggle UI: OFF"  -- ตั้งข้อความเริ่มต้นเป็น OFF
ToggleButton.BackgroundColor3 = Color3.fromRGB(50, 50, 50)
ToggleButton.TextColor3 = Color3.fromRGB(255, 255, 255)
ToggleButton.Font = Enum.Font.SourceSans
ToggleButton.TextSize = 20
ToggleButton.Parent = ScreenGui

-- ตัวแปรสถานะ
local isToggled = false

-- เมื่อคลิกปุ่มนี้ จะทำงานเหมือนการกด RightControl
ToggleButton.MouseButton1Click:Connect(function()
    -- เปลี่ยนสถานะ Toggle
    isToggled = not isToggled

    if isToggled then
        ToggleButton.Text = "OFF"  -- เปลี่ยนข้อความเป็น ON
        ToggleButton.BackgroundColor3 = Color3.fromRGB(50, 50, 50)  -- เปลี่ยนสีปุ่มเป็นเขียว
    else
        ToggleButton.Text = "ON"  -- เปลี่ยนข้อความเป็น OFF
        ToggleButton.BackgroundColor3 = Color3.fromRGB(0, 170, 0)  -- เปลี่ยนสีปุ่มเป็นเทา
    end

    -- เรียกใช้ฟังก์ชันที่ผูกกับ RightControl (แสดง/ซ่อน UI)
    pcall(function()
        Library:ToggleUI()
    end)
end)




name = tostring(game.Players.LocalPlayer.Name)
a = hookfunction(wait,function(b)
    if b ~= 0 and tostring(getcallingscript(a)) ~= "nil" and tonumber(b) < 2.5 and _G.Nocooldown == true then
        return a()
    end
        return a(b)
end)
spawn(function()
    while wait() do
        if _G.InfCharge then
            pcall(function()
game:GetService("Workspace")[name].Charge.Value = 100
            end)
        end
    end
end)
spawn(function()
    while wait() do
if _G.InfEnergy then
    pcall(function()
game:GetService("Workspace")[name].Energy.Value = 100
            end)
        end
    end
end)
Section:NewKeybind("KeybindText", "KeybindInfo", Enum.KeyCode.RightControl, function()
	Library:ToggleUI()
end)
