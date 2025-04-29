
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
