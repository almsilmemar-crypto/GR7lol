-- اسم السكربت: GR7
local Players = game:GetService("Players")
local Workspace = game:GetService("Workspace")
local ReplicatedStorage = game:GetService("ReplicatedStorage")
local player = Players.LocalPlayer
local playerName = player.Name
local container = Workspace:WaitForChild(playerName)

local weaponSettings = {
    ["Sniper"] = {
        AimDelay = 0.10,
        Recoil = 4.5,
        Instability = 2.7,
        Scope = false
    },
    ["G36"] = {
        AimDelay = 0.10,
    },
    -- إعدادات السلاح GR7 بنفس هيكل وباقي الميزات
    ["GR7"] = {
        AimDelay = 0.35,
        Recoil = 5.2,
        Instability = 2.1,
        Scope = true
    }
}

local function applySettings(inst)
    local settings = weaponSettings[inst.Name]
    if settings then
        for attr, value in pairs(settings) do
            inst:SetAttribute(attr, value)
        end
    end
end

-- تطبيق الإعدادات على العناصر الموجودة مسبقاً
for _, inst in ipairs(container:GetChildren()) do
    applySettings(inst)
end

-- تطبيق الإعدادات عند إضافة أي سلاح جديد
container.ChildAdded:Connect(function(inst)
    task.wait() 
    applySettings(inst)
end)
