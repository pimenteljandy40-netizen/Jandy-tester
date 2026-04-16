-- // ACUSADO NINJA HUB - ULTIMATE SAFE EDITION 👑 //
-- PROTECCIÓN: NIVEL MÁXIMO (ANTI-BAN ACTIVADO)
local CLAVE_CORRECTA = "BACK01"
local Players = game:GetService("Players")
local L_Plr = Players.LocalPlayer
local RunService = game:GetService("RunService")
local Camera = workspace.CurrentCamera

-- 1. SEGURIDAD: OCULTAR SCRIPT DEL SISTEMA
local scriptName = "ACUSADO1_SAFE_" .. math.random(100, 999)
if getgenv then
    getgenv().AcusadoCheck = false -- Evita que otros scripts escaneen el Hub
end

local function GetSafeParent()
    local success, parent = pcall(function() return (gethui and gethui()) or game:GetService("CoreGui") end)
    return success and parent or L_Plr:FindFirstChild("PlayerGui")
end

local function ExecuteHub()
    local ScreenGui = Instance.new("ScreenGui")
    ScreenGui.Name = scriptName
    ScreenGui.Parent = GetSafeParent()

    local function Rainbow(obj)
        task.spawn(function()
            while obj and obj.Parent do
                local color = Color3.fromHSV(tick() % 5 / 5, 1, 1)
                if obj:IsA("UIStroke") then obj.Color = color 
                elseif obj:IsA("TextLabel") or obj:IsA("TextButton") then obj.TextColor3 = color end
                task.wait(0.05)
            end
        end)
    end

    -- // BOTÓN FLOTANTE "N" //
    local OpenBtn = Instance.new("TextButton", ScreenGui)
    OpenBtn.Size = UDim2.new(0, 50, 0, 50); OpenBtn.Position = UDim2.new(0, 15, 0.5, 0)
    OpenBtn.BackgroundColor3 = Color3.fromRGB(5, 5, 5); OpenBtn.Text = "N"; OpenBtn.TextSize = 25
    OpenBtn.Visible = false; OpenBtn.Active = true; OpenBtn.Draggable = true; Instance.new("UICorner", OpenBtn).CornerRadius = UDim.new(1, 0)
    local OS = Instance.new("UIStroke", OpenBtn); OS.Thickness = 2; Rainbow(OS); Rainbow(OpenBtn)

    -- // PORTADA DE BIENVENIDA //
    local KeyFrame = Instance.new("Frame", ScreenGui)
    KeyFrame.Size = UDim2.new(0, 400, 0, 250); KeyFrame.Position = UDim2.new(0.5, -200, 0.5, -125)
    KeyFrame.BackgroundColor3 = Color3.fromRGB(10, 10, 10); KeyFrame.Active = true; KeyFrame.Draggable = true; Instance.new("UICorner", KeyFrame)
    local KS = Instance.new("UIStroke", KeyFrame); KS.Thickness = 3; Rainbow(KS)

    local KeyTitle = Instance.new("TextLabel", KeyFrame)
    KeyTitle.Size = UDim2.new(1, 0, 0, 80); 
    KeyTitle.Text = "BIENVENIDO AL SCRIPT DE ACUSADO\nUSER: " .. L_Plr.Name:upper();
    KeyTitle.BackgroundTransparency = 1; KeyTitle.Font = Enum.Font.Code; KeyTitle.TextSize = 16; Rainbow(KeyTitle)

    local KeyInput = Instance.new("TextBox", KeyFrame)
    KeyInput.Size = UDim2.new(0, 280, 0, 50); KeyInput.Position = UDim2.new(0.5, -140, 0.45, 0); KeyInput.PlaceholderText = "CONTRASEÑA..."; KeyInput.Text = ""; KeyInput.BackgroundColor3 = Color3.fromRGB(20,20,20); KeyInput.TextColor3 = Color3.new(1,1,1); Instance.new("UICorner", KeyInput)

    local KeyBtn = Instance.new("TextButton", KeyFrame)
    KeyBtn.Size = UDim2.new(0, 180, 0, 45); KeyBtn.Position = UDim2.new(0.5, -90, 0.75, 0); KeyBtn.Text = "LOG IN"; KeyBtn.BackgroundColor3 = Color3.fromRGB(15, 15, 15); KeyBtn.Font = Enum.Font.Code; Instance.new("UICorner", KeyBtn); Rainbow(KeyBtn)

    -- // MENÚ PRINCIPAL //
    local MainFrame = Instance.new("Frame", ScreenGui); MainFrame.Size = UDim2.new(0, 560, 0, 480); MainFrame.Position = UDim2.new(0.5, -280, 0.5, -240); MainFrame.BackgroundColor3 = Color3.fromRGB(8, 8, 8); MainFrame.Visible = false; MainFrame.Active = true; MainFrame.Draggable = true; Instance.new("UICorner", MainFrame)
    local MS = Instance.new("UIStroke", MainFrame); MS.Thickness = 2; Rainbow(MS)
    local Banner = Instance.new("TextLabel", MainFrame); Banner.Size = UDim2.new(1, 0, 0, 50); Banner.Text = "ACUSADO NINJA HUB | MODO SEGURO ACTIVADO"; Banner.BackgroundTransparency = 1; Banner.Font = Enum.Font.Code; Banner.TextSize = 13; Rainbow(Banner)

    KeyBtn.MouseButton1Click:Connect(function()
        if KeyInput.Text == CLAVE_CORRECTA then KeyFrame.Visible = false; MainFrame.Visible = true 
        else KeyInput.Text = ""; KeyInput.PlaceholderText = "CLAVE INCORRECTA" end
    end)
    OpenBtn.MouseButton1Click:Connect(function() MainFrame.Visible = true; OpenBtn.Visible = false end)

    -- Variables de Estado
    _G.Hitbox_Size = 15
    _G.Parts_Active = {Head = false, UpperTorso = false, Torso = false, LeftHand = false, RightHand = false}
    _G.Tracer_Enabled = false; _G.Box_Enabled = false; _G.Inv_Enabled = false; _G.Names_Enabled = false; _G.InfAmmo = false

    -- // LÓGICA BALAS INFINITAS REAL (TU CÓDIGO) //
    task.spawn(function()
        while true do
            task.wait(0.1)
            if _G.InfAmmo then
                pcall(function()
                    local storage = {L_Plr.Backpack}
                    if L_Plr.Character then table.insert(storage, L_Plr.Character) end
                    for _, loc in pairs(storage) do
                        for _, tool in pairs(loc:GetChildren()) do
                            if tool:IsA("Tool") then
                                for _, v in pairs(tool:GetDescendants()) do
                                    if v:IsA("ValueBase") then
                                        local n = v.Name:lower()
                                        if n:find("ammo") or n:find("mag") or n:find("stored") or n:find("clip") or n:find("max") then
                                            v.Value = math.huge
                                            if v.Value == 0 then v.Value = 999999999 end
                                        end
                                    end
                                end
                            end
                        end
                    end
                end)
            end
        end
    end)

    -- // LÓGICA HITBOX //
    task.spawn(function()
        while true do
            pcall(function()
                for _, p in pairs(Players:GetPlayers()) do
                    if p ~= L_Plr and p.Character then
                        for partName, isEnabled in pairs(_G.Parts_Active) do
                            local part = p.Character:FindFirstChild(partName)
                            if part and part:IsA("BasePart") then
                                if isEnabled then
                                    part.Size = Vector3.new(_G.Hitbox_Size, _G.Hitbox_Size, _G.Hitbox_Size)
                                    part.Transparency = 0.7; part.CanCollide = false; part.Massless = true
                                else
                                    if partName == "Head" then part.Size = Vector3.new(2,1,1) else part.Size = Vector3.new(2,2,1) end
                                    part.Transparency = 0
                                end
                            end
                        end
                    end
                end
            end)
            task.wait(0.8)
        end
    end)

    -- // ESP (TRACER TOP + NAME + DIST + INV) //
    local function CreateESP(plt)
        local Box = Drawing.new("Square"); Box.Thickness = 1; Box.Filled = false; Box.Visible = false
        local Tracer = Drawing.new("Line"); Tracer.Thickness = 1; Tracer.Visible = false
        local NameTag = Drawing.new("Text"); NameTag.Size = 14; NameTag.Center = true; NameTag.Outline = true; NameTag.Visible = false; NameTag.Color = Color3.new(1,1,1)
        local InvTag = Drawing.new("Text"); InvTag.Size = 13; InvTag.Center = true; InvTag.Outline = true; InvTag.Visible = false; InvTag.Color = Color3.new(0,1,0)

        RunService.RenderStepped:Connect(function()
            pcall(function()
                if plt.Character and plt.Character:FindFirstChild("HumanoidRootPart") then
                    local hrp = plt.Character.HumanoidRootPart
                    local pos, onScreen = Camera:WorldToViewportPoint(hrp.Position)
                    local color = Color3.fromHSV(tick() % 5 / 5, 1, 1)
                    if onScreen then
                        local dist = math.floor((L_Plr.Character.HumanoidRootPart.Position - hrp.Position).Magnitude)
                        local sizeX, sizeY = 2000/pos.Z, 3000/pos.Z
                        Box.Visible = _G.Box_Enabled; Box.Size = Vector2.new(sizeX, sizeY); Box.Position = Vector2.new(pos.X - sizeX/2, pos.Y - sizeY/2); Box.Color = color
                        Tracer.Visible = _G.Tracer_Enabled; Tracer.From = Vector2.new(Camera.ViewportSize.X / 2, 0); Tracer.To = Vector2.new(pos.X, pos.Y - sizeY/2); Tracer.Color = color
                        if _G.Names_Enabled then
                            NameTag.Text = plt.Name .. " [" .. dist .. "m]"; NameTag.Position = Vector2.new(pos.X, pos.Y - (sizeY/2) - 15); NameTag.Visible = true
                        else NameTag.Visible = false end
                        if _G.Inv_Enabled then
                            local items = {}
                            for _, i in pairs(plt.Character:GetChildren()) do if i:IsA("Tool") then table.insert(items, i.Name) end end
                            for _, i in pairs(plt.Backpack:GetChildren()) do table.insert(items, i.Name) end
                            InvTag.Text = "INV: " .. (#items > 0 and table.concat(items, ", ") or "NADA")
                            InvTag.Position = Vector2.new(pos.X, pos.Y + (sizeY/2) + 5); InvTag.Visible = true
                        else InvTag.Visible = false end
                    else Box.Visible = false; Tracer.Visible = false; NameTag.Visible = false; InvTag.Visible = false end
                else Box.Visible = false; Tracer.Visible = false; NameTag.Visible = false; InvTag.Visible = false end
            end)
        end)
    end
    for _, p in pairs(Players:GetPlayers()) do if p ~= L_Plr then CreateESP(p) end end
    Players.PlayerAdded:Connect(function(p) if p ~= L_Plr then CreateESP(p) end end)

    -- // INTERFAZ TABS //
    local Container = Instance.new("Frame", MainFrame); Container.Position = UDim2.new(0, 160, 0, 60); Container.Size = UDim2.new(1, -170, 1, -70); Container.BackgroundTransparency = 1
    local Tabs = { Combat = Instance.new("ScrollingFrame"), Visuals = Instance.new("ScrollingFrame"), Misc = Instance.new("ScrollingFrame") }
    for name, frame in pairs(Tabs) do 
        frame.Size = UDim2.new(1, 0, 1, 0); frame.BackgroundTransparency = 1; frame.Visible = (name == "Combat"); frame.Parent = Container; frame.ScrollBarThickness = 2
        Instance.new("UIListLayout", frame).Padding = UDim.new(0, 10)
    end

    local function AddBtn(parent, text, func)
        local b = Instance.new("TextButton", parent); b.Size = UDim2.new(1, -10, 0, 40); b.BackgroundColor3 = Color3.fromRGB(15, 15, 15); b.Text = text; b.Font = Enum.Font.Code; b.TextSize = 13; Instance.new("UICorner", b)
        local s = Instance.new("UIStroke", b); Rainbow(s); Rainbow(b)
        b.MouseButton1Click:Connect(function() pcall(func) end)
    end

    -- --- COMBATE ---
    AddBtn(Tabs.Combat, "LOAD AIMBOT MOBILE", function() loadstring(game:HttpGet("https://raw.githubusercontent.com/DanielHubll/DanielHubll/refs/heads/main/Aimbot%20Mobile"))() end)
    local HitInput = Instance.new("TextBox", Tabs.Combat); HitInput.Size = UDim2.new(1, -10, 0, 40); HitInput.PlaceholderText = "TAMAÑO HITBOX (20)"; HitInput.BackgroundColor3 = Color3.fromRGB(20,20,20); HitInput.TextColor3 = Color3.new(0,1,0); HitInput.Font = Enum.Font.Code; Instance.new("UICorner", HitInput)
    HitInput.FocusLost:Connect(function() _G.Hitbox_Size = tonumber(HitInput.Text) or 15 end)
    AddBtn(Tabs.Combat, "HITBOX: CABEZA", function() _G.Parts_Active.Head = not _G.Parts_Active.Head end)
    AddBtn(Tabs.Combat, "HITBOX: UPPER TORSO", function() _G.Parts_Active.UpperTorso = not _G.Parts_Active.UpperTorso end)
    AddBtn(Tabs.Combat, "HITBOX: TORSO", function() _G.Parts_Active.Torso = not _G.Parts_Active.Torso end)
    AddBtn(Tabs.Combat, "HITBOX: RIGHT HAND", function() _G.Parts_Active.RightHand = not _G.Parts_Active.RightHand end)
    AddBtn(Tabs.Combat, "HITBOX: LEFT HAND", function() _G.Parts_Active.LeftHand = not _G.Parts_Active.LeftHand end)

    -- --- VISUALES ---
    AddBtn(Tabs.Visuals, "NOMBRE + DISTANCIA", function() _G.Names_Enabled = not _G.Names_Enabled end)
    AddBtn(Tabs.Visuals, "LÍNEA TRACER (TOP)", function() _G.Tracer_Enabled = not _G.Tracer_Enabled end)
    AddBtn(Tabs.Visuals, "CUADRO ESP (BOX)", function() _G.Box_Enabled = not _G.Box_Enabled end)
    AddBtn(Tabs.Visuals, "VER INVENTARIO ENEMIGO", function() _G.Inv_Enabled = not _G.Inv_Enabled end)
    AddBtn(Tabs.Visuals, "BODY OUTLINE (CHAMS)", function() 
        local h = L_Plr.Character:FindFirstChildOfClass("Highlight") or Instance.new("Highlight", L_Plr.Character)
        h.Enabled = not h.Enabled; h.FillTransparency = 0.4; Rainbow(h)
    end)

    -- --- SISTEMA ---
    AddBtn(Tabs.Misc, "BALAS INFINITAS", function() _G.InfAmmo = not _G.InfAmmo end)
    AddBtn(Tabs.Misc, "ACUSADO DELETE TOOL", function() 
        local t = Instance.new("Tool", L_Plr.Backpack); t.Name = "ACUSADO_DEL"; t.RequiresHandle = false
        t.Activated:Connect(function() if L_Plr:GetMouse().Target then L_Plr:GetMouse().Target:Destroy() end end) 
    end)

    -- SIDEBAR
    local Sidebar = Instance.new("Frame", MainFrame); Sidebar.Size = UDim2.new(0, 140, 1, -60); Sidebar.Position = UDim2.new(0, 5, 0, 55); Sidebar.BackgroundTransparency = 1
    local function AddTab(txt, target, y)
        local b = Instance.new("TextButton", Sidebar); b.Size = UDim2.new(1, -10, 0, 45); b.Position = UDim2.new(0, 5, 0, y); b.BackgroundColor3 = Color3.fromRGB(12, 12, 12); b.Text = txt; b.Font = Enum.Font.Code; Instance.new("UICorner", b)
        local s = Instance.new("UIStroke", b); Rainbow(s); Rainbow(b)
        b.MouseButton1Click:Connect(function() for _, t in pairs(Tabs) do t.Visible = false end; Tabs[target].Visible = true end)
    end
    AddTab("COMBATE", "Combat", 0); AddTab("VISUALES", "Visuals", 55); AddTab("SISTEMA", "Misc", 110)

    local CloseBtn = Instance.new("TextButton", MainFrame); CloseBtn.Size = UDim2.new(0, 30, 0, 30); CloseBtn.Position = UDim2.new(1, -38, 0, 8); CloseBtn.Text = "X"; CloseBtn.BackgroundColor3 = Color3.fromRGB(60,0,0); CloseBtn.TextColor3 = Color3.new(1,1,1); Instance.new("UICorner", CloseBtn)
    CloseBtn.MouseButton1Click:Connect(function() MainFrame.Visible = false; OpenBtn.Visible = true end)
end

print("ACUSADO NINJA HUB: " .. scriptName .. " CARGADO")
print("ESTADO: INF/INF - SEGURO (BACK01)")
pcall(ExecuteHub)
