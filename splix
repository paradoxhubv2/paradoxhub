--[[


                                          💩💩 Self leak due to people reselling a 4 year old broken cheat..???? 💩💩
                              💩💩 For any questions or issues message https://discord.com/users/709795069355360258 on discord. 💩💩


]]
do -- Prefetch
    if not isfolder("splix") then
        makefolder("splix")
    end
    --
    if not isfile("splix/library.lua") then
        writefile("splix/library.lua", game:HttpGet("https://raw.githubusercontent.com/matas3535/SplixPrivateDrawingLibrary/main/Library.lua"))
    end
    --
    if not isfolder("splix/assets") then
        makefolder("splix/assets")
    end
    --
    if not isfolder("splix/cfgs") then
        makefolder("splix/cfgs")
    end
    --
    for i=1, 8 do
        if not isfile("splix/cfgs/config-"..i..".splx") then
            writefile("splix/cfgs/config-"..i..".splx", "[]")
        end
    end
end
--
do -- Main
    -- // Variables
    local library, utility, pointers, theme = loadfile("splix/library.lua")()
    local cieluv = (function()local CIELUV = {} do
	local clamp = math.clamp
	local C3 = Color3.new
	local black = C3(0, 0, 0)

	-- Convert from linear RGB to scaled CIELUV
	local function RgbToLuv13(c)
		local r, g, b = c.r, c.g, c.b
		-- Apply inverse gamma correction
		r = r < 0.0404482362771076 and r/12.92 or 0.87941546140213*(r + 0.055)^2.4
		g = g < 0.0404482362771076 and g/12.92 or 0.87941546140213*(g + 0.055)^2.4
		b = b < 0.0404482362771076 and b/12.92 or 0.87941546140213*(b + 0.055)^2.4
		-- sRGB->XYZ->CIELUV
		local y = 0.2125862307855956*r + 0.71517030370341085*g + 0.0722004986433362*b
		local z = 3.6590806972265883*r + 11.4426895800574232*g + 4.1149915024264843*b
		local l = y > 0.008856451679035631 and 116*y^(1/3) - 16 or 903.296296296296*y
		if z > 1e-15 then
			local x = 0.9257063972951867*r - 0.8333736323779866*g - 0.09209820666085898*b
			return l, l*x/z, l*(9*y/z - 0.46832)
		else
			return l, -0.19783*l, -0.46832*l
		end
	end

	function CIELUV:Lerp(c0, c1)
		local l0, u0, v0 = RgbToLuv13(c0)
		local l1, u1, v1 = RgbToLuv13(c1)

		-- The inputs aren't needed anymore, so don't drag out their lifetimes
		c0, c1 = nil, nil

		return function(t)
			-- Interpolate
			local l = (1 - t)*l0 + t*l1
			if l < 0.0197955 then
				return black
			end
			local u = ((1 - t)*u0 + t*u1)/l + 0.19783
			local v = ((1 - t)*v0 + t*v1)/l + 0.46832

			-- CIELUV->XYZ
			local y = (l + 16)/116
			y = y > 0.206896551724137931 and y*y*y or 0.12841854934601665*y - 0.01771290335807126
			local x = y*u/v
			local z = y*((3 - 0.75*u)/v - 5)

			-- XYZ->linear sRGB
			local r =  7.2914074*x - 1.5372080*y - 0.4986286*z
			local g = -2.1800940*x + 1.8757561*y + 0.0415175*z
			local b =  0.1253477*x - 0.2040211*y + 1.0569959*z

			-- Adjust for the lowest out-of-bounds component
			if r < 0 and r < g and r < b then
				r, g, b = 0, g - r, b - r
			elseif g < 0 and g < b then
				r, g, b = r - g, 0, b - g
			elseif b < 0 then
				r, g, b = r - b, g - b, 0
			end

			return C3(
				-- Apply gamma correction and clamp the result
				clamp(r < 3.1306684425e-3 and 12.92*r or 1.055*r^(1/2.4) - 0.055, 0, 1),
				clamp(g < 3.1306684425e-3 and 12.92*g or 1.055*g^(1/2.4) - 0.055, 0, 1),
				clamp(b < 3.1306684425e-3 and 12.92*b or 1.055*b^(1/2.4) - 0.055, 0, 1)
			)
		end
	end
end

return CIELUV
end)()
    --
    local rss = game:GetService("ReplicatedStorage")
    local uis = game:GetService("UserInputService")
    local rs = game:GetService("RunService")
    local plrs = game:GetService("Players")
    local ws = game:GetService("Workspace")
    local light = game:GetService("Lighting")
    local plr = plrs.LocalPlayer
    local splix = {shared = {
        offset = Vector2.new()
    }}
    -- // Ui Instances - Shared
    local lib = library:New({name = os.date("Splix - Private | %A, %B", os.time())..os.date(" %d", os.time())..utility:GetSubPrefix(os.date(" %d", os.time()))..os.date(", %Y.", os.time())})
    lib.uibind = Enum.KeyCode.Home
    --
    local aimbot = lib:Page({name = "Aimbot"})
    local visuals = lib:Page({name = "Visuals"})
    local misc = lib:Page({name = "Miscellaneous"})
    local exploits = lib:Page({name = "Exploits"})
    local setting = lib:Page({name = "Settings"})
    --
    local aimbot_main, aimbot_offsets, aimbot_deadzone, aimbot_extra = aimbot:MultiSection({sections = {"Main", "Offsets", "Deadzone", "Extra"}, side = "left", size = 341})
    local aimbot_cobypass = aimbot:Section({name = "Cursor-Offset", side = "Left"})
    local aimbot_fov = aimbot:Section({name = "Fov-Circle", side = "right"})
    local aimbot_prediction = aimbot:Section({name = "Prediction", side = "right"})
    local aimbot_misc = aimbot:Section({name = "Miscellaneous", side = "right"})
    --
    local visuals_enemies, visuals_teamates, visuals_allies, visual_self = visuals:MultiSection({sections = {"Enemies", "Team", "Allies", "Self"}, side = "left", size = 200})
    local visuals_lighting = visuals:Section({name = "Lighting", side = "right"})
    --
    local settings_config = setting:Section({name = "Config", side = "right"})
    local settings_extra = setting:Section({name = "Extra", side = "right"})
    --
    aimbot_main:Toggle({name = "Enabled", def = false, pointer = "aimbotmain_enabled"}):Keybind({def = Enum.KeyCode.E, keybindname = "Aimbot", mode = "Hold", pointer = "aimbotmain_keybind"})
    aimbot_main:Slider({name = "X-Smoothness", min = 1, max = 30, def = 1.5, decimals = 0.125, pointer = "aimbotmain_smoothnessx"})
    aimbot_main:Slider({name = "Y-Smoothness", min = 1, max = 30, def = 2, decimals = 0.125, pointer = "aimbotmain_smoothnessy"})
    aimbot_main:Toggle({name = "Team-Check", def = true, pointer = "aimbotmain_teamcheck_enabled"})
    aimbot_main:Toggle({name = "Wall-Check", def = true, pointer = "aimbotmain_wallcheck_enabled"})
    aimbot_main:Toggle({name = "Visible-Check", def = false, pointer = "aimbotmain_visiblecheck_enabled"})
    aimbot_main:Toggle({name = "Readjustment", def = true, pointer = "aimbotmain_readjustment_enabled"}):Keybind({def = Enum.UserInputType.MouseButton2, keybindname = "Readjusting", mode = "Hold", pointer = "aimbotmain_readjustment_keybind"})
    aimbot_main:Dropdown({name = "Hit-Part Method", options = {"Closest", "Random"}, def = "Closest", pointer = "aimbotmain_hitpart_method"})
    aimbot_main:Multibox({name = "Hit-Part", min = 1, options = {"Head", "Torso", "Arms", "Legs"}, def = {"Head", "Torso"}, pointer = "aimbotmain_hitpart"})
    aimbot_main:Dropdown({name = "Check-Type", options = {"Mouse", "Distance", "Health"}, def = "Mouse", pointer = "aimbotmain_checktype"})
    aimbot_main:Dropdown({name = "Wall-Check Origin", options = {"Camera", "Head", "Torso"}, def = "Camera", pointer = "aimbotmain_wallcheck_origin"})
    --
    aimbot_offsets:Toggle({name = "Enabled", def = false, pointer = "aimbotoffsets_enabled"})
    aimbot_offsets:Toggle({name = "Curves-Enabled", def = false, pointer = "aimbotoffsets_curves_enabled"})
    aimbot_offsets:Slider({name = "X-Multiplier", min = 1, max = 30, def = 1.5, decimals = 0.1, pointer = "aimbotoffsets_multiplierx"})
    aimbot_offsets:Slider({name = "Y-Multiplier", min = 1, max = 30, def = 2, decimals = 0.1, pointer = "aimbotoffsets_multipliery"})
    aimbot_offsets:Slider({name = "Offset-Time", min = 100, max = 2000, def = 500, decimals = 1, suffix = "ms", pointer = "aimbotoffsets_time"})
    aimbot_offsets:Dropdown({name = "Tweening Method", options = {"Linear", "Sine", "Quad", "Quart", "Quint", "Circular", "Cubic"}, def = "Linear", pointer = "aimbotoffsets_tweentype_enabled"})
    aimbot_offsets:Slider({name = "Curves-Time", min = 100, max = 2000, def = 500, decimals = 1, suffix = "ms", pointer = "aimbotoffsets_time"})
    aimbot_offsets:Slider({name = "Curves-Multiplier", min = 1, max = 10, def = 3, decimals = 1, pointer = "aimbotoffsets_curves_multiplier"})
    --
    aimbot_deadzone:Toggle({name = "Enabled", def = false, pointer = "aimbotdeadzone_enabled"})
    aimbot_deadzone:Toggle({name = "Body-Based", def = false, pointer = "aimbotdeadzone_bodybased"})
    aimbot_deadzone:Slider({name = "Field-Of-View", min = 5, max = 300, def = 1, decimals = 1, suffix = "°", pointer = "aimbotdeadzone_fov"})
    aimbot_deadzone:Toggle({name = "Show-FOV", def = true, pointer = "aimbotdeadzone_fov_enabled"}):Colorpicker({info = "Fov-Color", transparency = 0.5, default = Color3.fromRGB(200, 100, 100), pointer = "aimbotdeadzone_fov_color"})
    aimbot_deadzone:Toggle({name = "FOV-On-Body", def = true, pointer = "aimbotdeadzone_fovbody_enabled"})
    --
    aimbot_extra:Dropdown({name = "Aimbot-Type", options = {"Relative", "Absolute", "Camera", "Camera Relative"}, def = "Relative", pointer = "aimbotextra_type"})
    aimbot_extra:Toggle({name = "Tool-Only", def = false, pointer = "aimbotextra_tool"})
    aimbot_extra:Toggle({name = "Random-Smoothness", def = false, pointer = "aimbotextra_rsmoothness"})
    aimbot_extra:Slider({name = "Minimum-Smoothness", min = 1, max = 30, def = 2.5, decimals = 0.125, pointer = "aimbotextra_rs_min"})
    aimbot_extra:Slider({name = "Maximum-Smoothness", min = 1, max = 30, def = 10.5, decimals = 0.125, pointer = "aimbotextra_rs_max"})
    aimbot_extra:Slider({name = "Maximum-Range", min = 5, max = 1000, def = 250, decimals = 0.5, suffix = "cm", pointer = "aimbotextra_rs_maxrange"})
    aimbot_extra:Slider({name = "Minimum-Range", min = 0.5, max = 150, def = 1, decimals = 0.5, suffix = "cm", pointer = "aimbotextra_rs_minrange"})
    --
    aimbot_cobypass:Toggle({name = "Cursor-Offset Bypass", def = false, pointer = "aimbotcobypass_enabled"})
    aimbot_cobypass:Slider({name = "X-Offset", min = -200, max = 200, def = 10, decimals = 1, suffix = "px", pointer = "aimbotcobypass_xoffset"})
    aimbot_cobypass:Slider({name = "Y-Offset", min = -200, max = 200, def = 10, decimals = 1, suffix = "px", pointer = "aimbotcobypass_yoffset"})
    aimbot_cobypass:Toggle({name = "Use-Manual Offset", def = false, pointer = "aimbotcobypass_manual"})
    aimbot_cobypass:Toggle({name = "Visualize Cursor-Offset", def = false, pointer = "aimbotcobypass_visualize"}):Colorpicker({info = "Visualize Cursor-Offset", default = Color3.fromRGB(200, 0, 200), pointer = "aimbotcobypass_color"})
    aimbot_cobypass:Dropdown({name = "Bypass Method", options = {"Hook", "Calculation"}, def = "Calculation", pointer = "aimbotcobypass_type"})
    --
    local aimbotfov_enabled = aimbot_fov:Toggle({name = "Enabled", def = false, pointer = "aimbotfov_enabled"})
    aimbotfov_enabled:Colorpicker({info = "Fov-Color", transparency = 0, default = Color3.fromRGB(255, 255, 255), pointer = "aimbotfov_color"})
    aimbotfov_enabled:Colorpicker({info = "Fov-Locking Color", transparency = 0, default = Color3.fromRGB(255, 0, 0), pointer = "aimbotfov_locking_color"})
    aimbot_fov:Toggle({name = "Outline-Enabled", def = true, pointer = "aimbotfov_outline_enabled"}):Colorpicker({info = "Outline-Color", transparency = 0, default = Color3.fromRGB(25, 25, 25), pointer = "aimbotfov_outline_color"})
    aimbot_fov:Toggle({name = "Filled-Enabled", def = false, pointer = "aimbotfov_filled_enabled"}):Colorpicker({info = "Filled-Color", transparency = 0.8, default = Color3.fromRGB(255,255,255), pointer = "aimbotfov_filled_color"})
    aimbot_fov:Slider({name = "Field-Of-View", min = 5, max = 500, def = 125, decimals = 1, suffix = "°", pointer = "aimbotfov_fov"})
    aimbot_fov:Toggle({name = "Velocity-Based", def = true, pointer = "aimbotfov_velocity"})
    aimbot_fov:Slider({name = "Velocity-Mulitplier", min = 0.1, max = 1.5, def = 0.45, decimals = 0.025, suffix = "st", pointer = "aimbotfov_velocitymult"})
    aimbot_fov:Slider({name = "FOV-Sides", min = 6, max = 100, def = 30, decimals = 1, pointer = "aimbotfov_sides"})
    aimbot_fov:Slider({name = "FOV-Thickness", min = 0.5, max = 2.5, def = 0.6, decimals = 0.1, pointer = "aimbotfov_thickness"})
    aimbot_fov:Toggle({name = "Above-UI", def = true, pointer = "aimbotfov_above"})
    --
    aimbot_prediction:Toggle({name = "Enabled", def = false, pointer = "aimbotprediction_enabled"})
    aimbot_prediction:Slider({name = "Strength", min = 1, max = 10, def = 1.735, decimals = 0.05, pointer = "aimbotprediction_strength"})
    aimbot_prediction:Dropdown({name = "Prediction-Type", options = {"CFrame", "Velocity"}, def = "Velocity", pointer = "aimbotprediction_type"})
    aimbot_prediction:Toggle({name = "Adjust-For-Ping", def = true, pointer = "aimbotprediction_pingadjust"})
    --
    aimbot_misc:Toggle({name = "Hard-Lock", def = false, pointer = "aimbotmisc_hardlock"})
    aimbot_misc:Slider({name = "Target-Switch", min = 1, max = 2000, def = 1, decimals = 1, suffix = "ms", pointer = "aimbotmisc_switch"})
    --
    local box = visuals_enemies:Toggle({name = "Box-Esp", def = false, pointer = "visuals_enemies_boxenabled"})
    box:Colorpicker({info = "ESP-Box Color", transparency = 0, default = Color3.fromRGB(255, 255, 255), pointer = "visuals_enemies_boxcolor"})
    box:Colorpicker({info = "ESP-Box Locking Color", transparency = 0, default = Color3.fromRGB(255, 0, 0), pointer = "visuals_enemies_boxlockcolor"})
    visuals_enemies:Toggle({name = "Box-Outline", def = false, pointer = "visuals_enemies_boxoutlineenabled"}):Colorpicker({info = "ESP-Box Outline Color", transparency = 0, default = Color3.fromRGB(0, 0, 0), pointer = "visuals_enemies_boxoutlinecolor"})
    local hb = visuals_enemies:Toggle({name = "Health-Bar", def = false, pointer = "visuals_enemies_healthbarenabled"})
    hb:Colorpicker({info = "Health-Bar High Color", default = Color3.fromRGB(0, 255, 0), pointer = "visuals_enemies_healthhighcolor"})
    hb:Colorpicker({info = "Health-Bar Low Color", default = Color3.fromRGB(255, 0, 0), pointer = "visuals_enemies_healthlowcolor"})
    visuals_enemies:Toggle({name = "Esp-Title", def = false, pointer = "visuals_enemies_titleenabled"}):Colorpicker({info = "ESP-Title Color", default = Color3.fromRGB(255, 255, 255), pointer = "visuals_enemies_titlecolor"})
    visuals_enemies:Toggle({name = "Esp-Info", def = false, pointer = "visuals_enemies_infoenabled"}):Colorpicker({info = "ESP-Info Color", default = Color3.fromRGB(255, 0, 0), pointer = "visuals_enemies_infocolor"})
    --
    visuals_teamates:Toggle({name = "Box-Esp", def = false, pointer = "visuals_teamates_boxenabled"}):Colorpicker({info = "ESP-Box Color", transparency = 0, default = Color3.fromRGB(255, 255, 255), pointer = "visuals_teamates_boxcolor"})
    visuals_teamates:Toggle({name = "Box-Outline", def = false, pointer = "visuals_teamates_boxoutlineenabled"}):Colorpicker({info = "ESP-Box Outline Color", transparency = 0, default = Color3.fromRGB(0, 0, 0), pointer = "visuals_teamates_boxoutlinecolor"})
    local hb = visuals_teamates:Toggle({name = "Health-Bar", def = false, pointer = "visuals_teamates_healthbarenabled"})
    hb:Colorpicker({info = "Health-Bar High Color", default = Color3.fromRGB(0, 255, 0), pointer = "visuals_teamates_healthhighcolor"})
    hb:Colorpicker({info = "Health-Bar Low Color", default = Color3.fromRGB(255, 0, 0), pointer = "visuals_teamates_healthlowcolor"})
    visuals_teamates:Toggle({name = "Esp-Title", def = false, pointer = "visuals_teamates_titleenabled"}):Colorpicker({info = "ESP-Title Color", default = Color3.fromRGB(255, 255, 255), pointer = "visuals_teamates_titlecolor"})
    visuals_teamates:Toggle({name = "Esp-Info", def = false, pointer = "visuals_teamates_infoenabled"}):Colorpicker({info = "ESP-Info Color", default = Color3.fromRGB(255, 0, 0), pointer = "visuals_teamates_infocolor"})
    visuals_teamates:Slider({name = "Text-Size", min = 2, max = 30, def = 13, decimals = 1, pointer = "visuals_teamates_textsize"})
    visuals_teamates:Toggle({name = "Auto-Text Size", def = false, pointer = "visuals_teamates_autotextsize"})
    --[[
    visuals_lighting:Toggle({name = "Ambient", def = false, pointer = "visuals_lighting_ambient", callback = function(bool) if bool then lightlib:changeLighting("Ambient", pointers.visuals_lighting_ambientcolor:Get().Color) else lightlib:removeLighting("Ambient") end end}):Colorpicker({info = "Ambient Color", default = Color3.fromRGB(130, 0, 225), pointer = "visuals_lighting_ambientcolor", callback = function(val) if pointers.visuals_lighting_ambient:Get() then lightlib:changeLighting("Ambient", val) end end})
    local colorshift = visuals_lighting:Toggle({name = "ColorShift", def = false, pointer = "visuals_lighting_colorshift", callback = function(bool) if bool then lightlib:changeLighting("ColorShift_Bottom", pointers.visuals_lighting_colorshiftbottom:Get().Color) lightlib:changeLighting("ColorShift_Top", pointers.visuals_lighting_colorshifttop:Get().Color) else lightlib:removeLighting("ColorShift_Bottom") lightlib:removeLighting("ColorShift_Top") end end})
    colorshift:Colorpicker({info = "Colorshift-Bottom Color", default = Color3.fromRGB(0, 140, 255), pointer = "visuals_lighting_colorshiftbottom", callback = function(val) if pointers.visuals_lighting_colorshift:Get() then lightlib:changeLighting("ColorShift_Bottom", val) lightlib:changeLighting("ColorShift_Top", pointers.visuals_lighting_colorshifttop:Get().Color) end end})
    colorshift:Colorpicker({info = "Colorshift-Top Color", default = Color3.fromRGB(255, 0, 255), pointer = "visuals_lighting_colorshifttop", callback = function(val) if pointers.visuals_lighting_colorshift:Get() then lightlib:changeLighting("ColorShift_Bottom", pointers.visuals_lighting_colorshiftbottom:Get().Color) lightlib:changeLighting("ColorShift_Top", val) end end})
    visuals_lighting:Toggle({name = "Better-Lighting", def = false, pointer = "visuals_lighting_betterlighting", function(bool) sethiddenproperty(light, "Technology", bool and "ShadowMap" or "Legacy") end})
    --]]
    settings_config:ConfigBox({})
    settings_config:ButtonHolder({buttons = {{"Load", function() lib:LoadConfig(readfile("splix/cfgs/config-"..pointers.configbox:Get()..".splx")) end}, {"Save", function() writefile("splix/cfgs/config-"..pointers.configbox:Get()..".splx", lib:GetConfig()) end}}})
    settings_config:Label({name = "Unloading will fully unload\neverything, so save your\nconfig before unloading.", middle = true})
    settings_config:Button({name = "Unload", callback = function() lib:Unload() 
        --lightlib:Unload() 
    end})
    --
    settings_extra:Toggle({name = "Watermark", def = false, pointer = "settingsextra_watermark", callback = function(bool) lib.watermark:Update("Visible", bool) end})
    settings_extra:Toggle({name = "Keybinds-List", def = false, pointer = "settingsextra_keybindslist", callback = function(bool) lib.keybindslist:Update("Visible", bool) end})
    -- // Functions - Main
    do
        function rayCastVisible(target, origin, ignore, distance)
            ignore = ignore or {}
            distance = distance or 2048
            --
    		local ray = Ray.new(origin.CFrame.Position, (target.Position - origin.CFrame.Position).unit * distance)
    		local part = ws:FindPartOnRayWithIgnoreList(ray, ignore)
            --
    		if part and part:IsDescendantOf(target.Parent) then
    			return true
            end
            --
            return false
        end
        --
        function worldToScreen(part)
            local vector, onScreen = ws.CurrentCamera:WorldToViewportPoint(part.Position)
            return Vector2.new(vector.X,vector.Y), onScreen
        end
        --
        function convertParts(parts)
            local new = {}
            --
            if table.find(parts, "Head") then
                new[#new + 1] = "Head"
                new[#new + 1] = "HeadHB"
                new[#new + 1] = "FakeHead"
            end
            --
            if table.find(parts, "Torso") then
                new[#new + 1] = "UpperTorso"
                new[#new + 1] = "LowerTorso"
                new[#new + 1] = "Torso"
            end
            --
            if table.find(parts, "Arms") then
                new[#new + 1] = "LeftUpperArm"
                new[#new + 1] = "RightUpperArm"
                new[#new + 1] = "Left Arm"
                new[#new + 1] = "Right Arm"
                new[#new + 1] = "LeftLowerArm"
                new[#new + 1] = "RightLowerArm"
                new[#new + 1] = "LeftHand"
                new[#new + 1] = "RightHand"
            end
            --
            if table.find(parts, "Legs") then
                new[#new + 1] = "LeftUpperLeg"
                new[#new + 1] = "RightUpperLeg"
                new[#new + 1] = "Left Leg"
                new[#new + 1] = "Right Leg"
                new[#new + 1] = "LeftLowerLeg"
                new[#new + 1] = "RightLowerLeg"
                new[#new + 1] = "LeftFoot"
                new[#new + 1] = "RightFoot"
            end
            --
            return new
        end
        --
        function getCharacter(player)
            return player.Character
        end
        --
        function getLegitTarget()
            local target = nil
            local closest = math.huge
            --
            for index, player in pairs(plrs:GetPlayers()) do
                if player ~= plr and getCharacter(player) and not (pointers.aimbotmain_teamcheck_enabled:Get() and not (player.Team ~= plr.Team) or false) then
                    local character = getCharacter(player)
                    --
                    if character:FindFirstChildOfClass("Humanoid") and character:FindFirstChild("HumanoidRootPart") and character:FindFirstChild("Head") and character:FindFirstChildOfClass("Humanoid").Health > 0 then
                        local currenttarget = nil
                        local currentclosest = math.huge
                        --
                        if pointers.aimbotmain_hitpart_method:Get() == "Closest" then
                            for ind, part in pairs(convertParts(pointers.aimbotmain_hitpart:Get())) do
                                if character:FindFirstChild(part) and character:FindFirstChild(part):IsA("BasePart") and not (pointers.aimbotmain_visiblecheck_enabled:Get() and not (character:FindFirstChild(part).Transparency == 0)) and not (pointers.aimbotmain_wallcheck_enabled:Get() and not rayCastVisible(character:FindFirstChild(part), (pointers.aimbotmain_wallcheck_origin:Get() == "Camera" and ws.CurrentCamera or pointers.aimbotmain_wallcheck_origin:Get() == "Head" and getCharacter(plr):FindFirstChild("Head") or pointers.aimbotmain_wallcheck_origin:Get() == "Torso" and (getCharacter(plr):FindFirstChild("Torso") or getCharacter(plr):FindFirstChild("UpperTorso"))), {getCharacter(plr)}) or false) then
                                    local partpos, onscreen = worldToScreen(character:FindFirstChild(part))
                                    if onscreen then
                                        local fromMouse = (Vector2.new(uis:GetMouseLocation().X, uis:GetMouseLocation().Y) - partpos).magnitude
                                        if not (pointers.aimbotfov_enabled:Get() and not (fromMouse < (pointers.aimbotfov_fov:Get() - ((pointers.aimbotfov_velocity:Get() and ((plr.Character and plr.Character:FindFirstChild("HumanoidRootPart") and ((pointers.aimbotfov_fov:Get() * 0.5) * ((plr.Character:FindFirstChild("HumanoidRootPart").CFrame.p - (plr.Character:FindFirstChild("HumanoidRootPart").CFrame.p + plr.Character:FindFirstChild("HumanoidRootPart").Velocity)).magnitude / 50)) or 0) or 0) or 0) * pointers.aimbotfov_velocitymult:Get()))) or false) and fromMouse < currentclosest then
                                            currenttarget = character:FindFirstChild(part)
                                            currentclosest = fromMouse
                                        end
                                    end
                                end
                            end
                        else
                            local newtarget = {}
                            --
                            for ind, part in pairs(convertParts(pointers.aimbotmain_hitpart:Get())) do
                                if character:FindFirstChild(part) and character:FindFirstChild(part):IsA("BasePart") and not (pointers.aimbotmain_visiblecheck_enabled:Get() and not (character:FindFirstChild(part).Transparency == 0)) and not (pointers.aimbotmain_wallcheck_enabled:Get() and not rayCastVisible(character:FindFirstChild(part), (pointers.aimbotmain_wallcheck_origin:Get() == "Camera" and ws.CurrentCamera or pointers.aimbotmain_wallcheck_origin:Get() == "Head" and getCharacter(plr):FindFirstChild("Head") or pointers.aimbotmain_wallcheck_origin:Get() == "Torso" and (getCharacter(plr):FindFirstChild("Torso") or getCharacter(plr):FindFirstChild("UpperTorso"))), {getCharacter(plr)}) or false) then
                                    local partpos, onscreen = worldToScreen(character:FindFirstChild(part))
                                    if onscreen then
                                        newtarget[#newtarget + 1] = character:FindFirstChild(part)
                                    end
                                end
                            end
                            --
                            if #newtarget > 1 then
                                newpart = newtarget[math.random(1, #newtarget)]
                                local partpos, onscreen = worldToScreen(newpart)
                                --
                                if onscreen then
                                    local fromMouse = (Vector2.new(uis:GetMouseLocation().X, uis:GetMouseLocation().Y) - partpos).magnitude
                                    if not (pointers.aimbotfov_enabled:Get() and not (fromMouse < (pointers.aimbotfov_fov:Get() - ((pointers.aimbotfov_velocity:Get() and ((plr.Character and plr.Character:FindFirstChild("HumanoidRootPart") and ((pointers.aimbotfov_fov:Get() * 0.5) * ((plr.Character:FindFirstChild("HumanoidRootPart").CFrame.p - (plr.Character:FindFirstChild("HumanoidRootPart").CFrame.p + plr.Character:FindFirstChild("HumanoidRootPart").Velocity)).magnitude / 50)) or 0) or 0) or 0) * pointers.aimbotfov_velocitymult:Get()))) or false) and fromMouse < currentclosest then
                                        currenttarget = newpart
                                        currentclosest = fromMouse
                                    end
                                end
                            end
                        end
                        --
                        if currentclosest < closest then
                            target = {player, currenttarget}
                            closest = currentclosest
                        end
                    end
                end
            end
            --
            return target
        end
        --
        function getOffset()
            return Vector2.new(0, 0)
        end
        --
        function handleESP(player)
            local Box = utility:Create("Quad", nil, {Thickness = 1.5, Color = Color3.fromRGB(255, 255, 255), Hidden = true, ZIndex = 45, Visible = false})
            local BoxOutline = utility:Create("Quad", nil, {Thickness = 2.5, Color = Color3.fromRGB(0, 0, 0), Hidden = true, ZIndex = 44, Visible = false})
            --
            local HealthBar = utility:Create("Quad", nil, {Thickness = 1.5, Filled = true, Color = Color3.fromRGB(0, 255, 0), Hidden = true, ZIndex = 45, Visible = false})
            local HealthBarOutline = utility:Create("Quad", nil, {Thickness = 1.5, Filled = false, Color = Color3.fromRGB(0, 0, 0), Hidden = true, ZIndex = 44, Visible = false})
            local HealthBarOutlineFill = utility:Create("Quad", nil, {Thickness = 1.5, Filled = true, Color = Color3.fromRGB(0, 0, 0), Hidden = true, ZIndex = 44, Visible = false})
            --
            local Title = utility:Create("TextLabel", nil, {Text = player.Name, Font = 2, Size = 13, Outline = true, Center = true, Color = Color3.fromRGB(255, 255, 255), Hidden = true, ZIndex = 45, Visible = false})
            local Info = utility:Create("TextLabel", nil, {Text = "info here", Font = 2, Size = 13, Outline = true, Center = true, Color = theme.accent, Hidden = true, ZIndex = 45, Visible = false})
            --
            function updateESP()
                local updateConnection
                updateConnection = utility:Connection(game:GetService("RunService").RenderStepped, function()
                    if player.Character and player.Character:FindFirstChildOfClass("Humanoid") and player.Character:FindFirstChildOfClass("Humanoid").Health > 0 and player.Character:FindFirstChild("HumanoidRootPart") and (player.Character:FindFirstChild("HumanoidRootPart") or player.Character:FindFirstChild("Torso")) and player.Character:FindFirstChild("Head") then
                        local part = (player.Character:FindFirstChild("UpperTorso") or player.Character:FindFirstChild("Torso"))
                        local hrp = player.Character:FindFirstChild("HumanoidRootPart")
                        local partcf = hrp.CFrame - Vector3.new(0, hrp.CFrame.Y, 0) + Vector3.new(0, part.CFrame.Y, 0)
                        local head = player.Character:FindFirstChild("Head")
                        local hum = player.Character:FindFirstChildOfClass("Humanoid")
                        local size = hrp.Size
                        local headsize = head.Size
                        local distance = (ws.CurrentCamera.CFrame.Position - hrp.Position).magnitude
                        --
                        local hd, hdv = ws.CurrentCamera:WorldToViewportPoint((head.CFrame * CFrame.new(0, 0.5, 0)).Position + Vector3.new(0, headsize.Y / 2, 0))
                        --
                        local tr, trv = ws.CurrentCamera:WorldToViewportPoint((partcf * CFrame.new(-size.X, -size.Y, 0)).Position - Vector3.new(0, headsize.Y, 0))
                        local br, brv = ws.CurrentCamera:WorldToViewportPoint((partcf * CFrame.new(-size.X, size.Y, 0)).Position)
                        local tl, tlv = ws.CurrentCamera:WorldToViewportPoint((partcf * CFrame.new(size.X, -size.Y, 0)).Position - Vector3.new(0, headsize.Y, 0))
                        local bl, blv = ws.CurrentCamera:WorldToViewportPoint((partcf * CFrame.new(size.X, size.Y, 0)).Position)
                        --
                        local htr, htlv = ws.CurrentCamera:WorldToViewportPoint((partcf * CFrame.new(size.X, -size.Y, 0) * CFrame.new(0.5, 0, 0)).Position - Vector3.new(0, headsize.Y, 0))
                        local hbr, hblv = ws.CurrentCamera:WorldToViewportPoint((partcf * CFrame.new(size.X, size.Y, 0) * CFrame.new(0.5, 0, 0)).Position)
                        local htl, htlv = ws.CurrentCamera:WorldToViewportPoint((partcf * CFrame.new(size.X, -size.Y, 0) * CFrame.new(0.65, 0, 0)).Position - Vector3.new(0, headsize.Y, 0))
                        local hbl, hblv = ws.CurrentCamera:WorldToViewportPoint((partcf * CFrame.new(size.X, size.Y, 0) * CFrame.new(0.65, 0, 0)).Position)
                        --
                        if (hpv or hdv or trv or brv or tlv or blv or htlv or hblv) then
                            Box.Visible = player.Team ~= plr.Team and pointers.visuals_enemies_boxenabled:Get() or pointers.visuals_teamates_boxenabled:Get()
                            Box.PointA = Vector2.new(tr.X, tr.Y)
                            Box.PointB = Vector2.new(tl.X, tl.Y)
                            Box.PointC = Vector2.new(bl.X, bl.Y)
                            Box.PointD = Vector2.new(br.X, br.Y)
                            Box.Color = plr.Team and pointers.visuals_enemies_boxcolor:Get().Color or pointers.visuals_teamates_boxcolor:Get().Color
                            Box.Transparency = plr.Team and 1 - pointers.visuals_enemies_boxcolor:Get().Transparency or 1 - pointers.visuals_teamates_boxcolor:Get().Transparency
                            --
                            BoxOutline.Visible = player.Team ~= plr.Team and (pointers.visuals_enemies_boxenabled:Get() and pointers.visuals_enemies_boxoutlineenabled:Get()) or (pointers.visuals_teamates_boxenabled:Get() and pointers.visuals_teamates_boxoutlineenabled:Get())
                            BoxOutline.PointA = Box.PointA
                            BoxOutline.PointB = Box.PointB
                            BoxOutline.PointC = Box.PointC
                            BoxOutline.PointD = Box.PointD
                            BoxOutline.Color = player.Team ~= plr.Team and pointers.visuals_enemies_boxoutlinecolor:Get().Color or pointers.visuals_teamates_boxoutlinecolor:Get().Color
                            BoxOutline.Transparency = player.Team ~= plr.Team and 1 - pointers.visuals_enemies_boxoutlinecolor:Get().Transparency or 1 - pointers.visuals_teamates_boxoutlinecolor:Get().Transparency
                            --
                            HealthBar.Visible =  player.Team ~= plr.Team and pointers.visuals_enemies_healthbarenabled:Get() or pointers.visuals_teamates_healthbarenabled:Get()
                            HealthBar.PointA = Vector2.new(htr.X, htr.Y)
                            HealthBar.PointB = Vector2.new(htl.X, htl.Y)
                            HealthBar.PointC = Vector2.new(hbl.X + ((htl.X - hbl.X) * (1 - (hum.Health / hum.MaxHealth))), (hbl.Y) + ((htl.Y - hbl.Y) * (1 - (hum.Health / hum.MaxHealth))))
                            HealthBar.PointD = Vector2.new(hbr.X + ((htr.X - hbr.X) * (1 - (hum.Health / hum.MaxHealth))), (hbr.Y) + ((htr.Y - hbr.Y) * (1 - (hum.Health / hum.MaxHealth))))
                            HealthBar.Transparency = 1
                            HealthBar.Color = cieluv:Lerp((player.Team ~= plr.Team and pointers.visuals_enemies_healthlowcolor:Get().Color or pointers.visuals_teamates_healthlowcolor:Get().Color), (player.Team ~= plr.Team and pointers.visuals_enemies_healthhighcolor:Get().Color or pointers.visuals_teamates_healthhighcolor:Get().Color))(hum.Health / hum.MaxHealth)
                            -- 
                            HealthBarOutline.Visible = player.Team ~= plr.Team and pointers.visuals_enemies_healthbarenabled:Get() or pointers.visuals_teamates_healthbarenabled:Get()
                            HealthBarOutline.PointA = Vector2.new(htr.X, htr.Y)
                            HealthBarOutline.PointB = Vector2.new(htl.X, htl.Y)
                            HealthBarOutline.PointC = Vector2.new(hbl.X, hbl.Y)
                            HealthBarOutline.Transparency = 1
                            HealthBarOutline.PointD = Vector2.new(hbr.X, hbr.Y)
                            -- 
                            HealthBarOutlineFill.Visible = player.Team ~= plr.Team and pointers.visuals_enemies_healthbarenabled:Get() or pointers.visuals_teamates_healthbarenabled:Get()
                            HealthBarOutlineFill.PointA = Vector2.new(htr.X, htr.Y)
                            HealthBarOutlineFill.PointB = Vector2.new(htl.X, htl.Y)
                            HealthBarOutlineFill.PointC = Vector2.new(hbl.X, hbl.Y)
                            HealthBarOutlineFill.PointD = Vector2.new(hbr.X, hbr.Y)
                            HealthBarOutlineFill.Transparency = 1
                            --
                            Title.Visible = player.Team ~= plr.Team and pointers.visuals_enemies_titleenabled:Get() or pointers.visuals_teamates_titleenabled:Get()
                            Title.Position = Vector2.new(hd.X, hd.Y - 30)
                            Title.Color = player.Team ~= plr.Team and pointers.visuals_enemies_titlecolor:Get().Color or pointers.visuals_teamates_titlecolor:Get().Color
                            Title.Size = pointers.visuals_teamates_autotextsize:Get() and math.clamp(1 / distance * 1000, 14, 25) or pointers.visuals_teamates_textsize:Get()
                            Title.Transparency = 1
                            --
                            Info.Visible = player.Team ~= plr.Team and pointers.visuals_enemies_infoenabled:Get() or pointers.visuals_teamates_infoenabled:Get()
                            Info.Position = Vector2.new(hd.X, hd.Y - 15)
                            Info.Color = player.Team ~= plr.Team and pointers.visuals_enemies_infocolor:Get().Color or pointers.visuals_teamates_infocolor:Get().Color
                            Info.Size = pointers.visuals_teamates_autotextsize:Get() and math.clamp(1 / distance * 1000, 14, 25) or pointers.visuals_teamates_textsize:Get()
                            Info.Text = (tostring(math.floor(distance)) .. " / " .. tostring(math.floor(hum.Health)))
                            Info.Transparency = 1
                        else
                            Box.Visible = false
                            BoxOutline.Visible = false
                            HealthBar.Visible = false
                            HealthBarOutline.Visible = false
                            HealthBarOutlineFill.Visible = false
                            Title.Visible = false
                            Info.Visible = false
                        end
                    else
                        Box.Visible = false
                        BoxOutline.Visible = false
                        HealthBar.Visible = false
                        HealthBarOutline.Visible = false
                        HealthBarOutlineFill.Visible = false
                        Title.Visible = false
                        Info.Visible = false
                    end
                    --
                    if player == nil then
                        utility:Disconnect(updateConnection)
                        --
                        utility:Remove(Box, true)
                        utility:Remove(BoxOutline, true)
                        utility:Remove(HealthBar, true)
                        utility:Remove(HealthBarOutline, true)
                        utility:Remove(HealthBarOutlineFill.Visible, true)
                        utility:Remove(Title, true)
                        utility:Remove(Info, true)
                    end
                end)
            end
            --
            coroutine.wrap(updateESP)()
        end
        splix.shared.tick = tick()
        splix.shared.target = nil
        local fovcircle = utility:Create("Circle", nil, {Filled = false, Hidden = true, ZIndex = pointers.aimbotfov_above:Get() and 70 or 45, Visible = false})
        local fovcircle_outline = utility:Create("Circle", nil, {Filled = false, Hidden = true, ZIndex = pointers.aimbotfov_above:Get() and 69 or 44, Visible = false})
        local fovcircle_filled = utility:Create("Circle", nil, {Filled = true, Thickness = 0, Hidden = true, ZIndex = pointers.aimbotfov_above:Get() and 68 or 43, Visible = false})
        --
        utility:Connection(plr.CharacterAdded, function()
            task.wait(0.1)
            --
            splix.shared.offset = getOffset()
        end)
        --
        utility:Connection(rs.RenderStepped, function()
            if pointers.aimbotfov_enabled:Get() then
                --pcall(function()
                    -- // Visible
                    fovcircle.Visible = true
                    -- // Positioning
                    fovcircle.Position = Vector2.new(uis:GetMouseLocation().X + (pointers.aimbotcobypass_enabled:Get() and (pointers.aimbotcobypass_manual:Get() and pointers.aimbotcobypass_xoffset:Get() or splix.shared.offset.X) or 0), uis:GetMouseLocation().Y + (pointers.aimbotcobypass_enabled:Get() and (pointers.aimbotcobypass_manual:Get() and pointers.aimbotcobypass_yoffset:Get() or splix.shared.offset.Y) or 0))
                    -- // Properties
                    fovcircle.Color = (target and (splix.shared.target[1] and splix.shared.target[2] or false) or false) and pointers.aimbotfov_locking_color:Get().Color or pointers.aimbotfov_color:Get().Color
                    fovcircle.Transparency = (target and (splix.shared.target[1] and splix.shared.target[2] or false) or false) and 1 - pointers.aimbotfov_locking_color:Get().Transparency or 1 - pointers.aimbotfov_color:Get().Transparency
                    fovcircle.Radius = pointers.aimbotfov_fov:Get() - ((pointers.aimbotfov_velocity:Get() and ((plr.Character and plr.Character:FindFirstChild("HumanoidRootPart") and ((pointers.aimbotfov_fov:Get() * 0.5) * ((plr.Character:FindFirstChild("HumanoidRootPart").CFrame.p - (plr.Character:FindFirstChild("HumanoidRootPart").CFrame.p + plr.Character:FindFirstChild("HumanoidRootPart").Velocity)).magnitude / 50)) or 0) or 0) or 0) * pointers.aimbotfov_velocitymult:Get())
                    fovcircle.NumSides = pointers.aimbotfov_sides:Get()
                    fovcircle.Thickness = pointers.aimbotfov_thickness:Get()
                    fovcircle.ZIndex = pointers.aimbotfov_above:Get() and 70 or 45
                    --
                    if pointers.aimbotfov_outline_enabled:Get() then
                        fovcircle_outline.Position = fovcircle.Position
                        --
                        fovcircle_outline.Color = pointers.aimbotfov_outline_color:Get().Color
                        fovcircle_outline.Transparency = 1 - pointers.aimbotfov_outline_color:Get().Transparency
                        fovcircle_outline.Visible = true
                        fovcircle_outline.Radius = fovcircle.Radius
                        fovcircle_outline.NumSides = fovcircle.NumSides
                        fovcircle_outline.Thickness = fovcircle.Thickness + (fovcircle.Thickness * 2.5)
                        fovcircle_outline.ZIndex = pointers.aimbotfov_above:Get() and 69 or 44
                    else
                        fovcircle_outline.Visible = false
                    end
                    --
                    if pointers.aimbotfov_filled_enabled:Get() then
                        fovcircle_filled.Position = fovcircle.Position
                        --
                        fovcircle_filled.Color = pointers.aimbotfov_filled_color:Get().Color
                        fovcircle_filled.Transparency = 1 - pointers.aimbotfov_filled_color:Get().Transparency
                        fovcircle_filled.Visible = true
                        fovcircle_filled.Radius = fovcircle.Radius
                        fovcircle_filled.NumSides = fovcircle.NumSides
                        fovcircle_filled.ZIndex = pointers.aimbotfov_above:Get() and 68 or 43
                    else
                        fovcircle_filled.Visible = false
                    end
                --end)
            else
                pcall(function()
                    fovcircle.Visible = false
                    fovcircle_outline.Visible = false
                    fovcircle_filled.Visible = false
                end)
            end
        end)
        --
        utility:Connection(rs.Heartbeat, function()
            if pointers.aimbotmain_keybind:Active() and not pointers.aimbotmain_readjustment_keybind:Active() and getCharacter(plr) and not (pointers.aimbotextra_tool:Get() and not (getCharacter(plr):FindFirstChildOfClass("Tool")) or false) then
                if (tick() - splix.shared.tick) >= (pointers.aimbotmisc_switch:Get() / 1000) then
                    splix.shared.target = getLegitTarget()
                    --
                    if splix.shared.target and splix.shared.target[1] and splix.shared.target[2] then
                        local targetpos = worldToScreen(splix.shared.target[2])
                        local movex, movey = targetpos.X - uis:GetMouseLocation().X - (pointers.aimbotcobypass_enabled:Get() and (pointers.aimbotcobypass_manual:Get() and pointers.aimbotcobypass_xoffset:Get() or splix.shared.offset.X) or 0), targetpos.Y - uis:GetMouseLocation().Y - (pointers.aimbotcobypass_enabled:Get() and (pointers.aimbotcobypass_manual:Get() and pointers.aimbotcobypass_yoffset:Get() or splix.shared.offset.Y) or 0)
                        --
                        local method = pointers.aimbotextra_type:Get()
                        local xsmoothness = pointers.aimbotextra_rsmoothness:Get() and math.abs(math.clamp((math.random(pointers.aimbotextra_rs_min:Get() * 1000, pointers.aimbotextra_rs_max:Get() * 1000) / 1000), 1, 30)) or pointers.aimbotmain_smoothnessx:Get()
                        local ysmoothness = pointers.aimbotextra_rsmoothness:Get() and math.abs(math.clamp((math.random(pointers.aimbotextra_rs_min:Get() * 1000, pointers.aimbotextra_rs_max:Get() * 1000) / 1000), 1, 30)) or pointers.aimbotmain_smoothnessy:Get()
                        --
                        if method == "Relative" then
                            mousemoverel(movex / xsmoothness, movey / ysmoothness)
                        elseif method == "Absolute" then
                            mousemoveabs(uis:GetMouseLocation().X + (movex / xsmoothness), uis:GetMouseLocation().Y + (movey / ysmoothness))
                        elseif method == "Camera" then
                            workspace.CurrentCamera.CFrame = workspace.CurrentCamera.CFrame:Lerp(CFrame.new(ws.CurrentCamera.CFrame.p, splix.shared.target[2].Position),1/((xsmoothness + ysmoothness)/2))
                        elseif method == "Camera Relative" then
                            workspace.CurrentCamera.CFrame = workspace.CurrentCamera.CFrame:Lerp(CFrame.new(ws.CurrentCamera.CFrame.p, splix.shared.target[2].Position),1/((xsmoothness + ysmoothness)/2))
                            mousemoverel(movex / xsmoothness, movey / ysmoothness)
                        end
                    end
                end
            else
                splix.shared.tick = tick()
                splix.shared.target = nil
            end
        end)
        --
        for index, player in pairs(plrs:GetPlayers()) do
            if player ~= plr then 
                handleESP(player)
            end
        end
        --
        do
            local Vak = {}
            local Prime = {4790960806, 5973754207, 5961745093, 6580968658}
            -- 
            if table.find(Vak, game.PlaceId) then -- Vak
                function getOffset()
                    local mouseOffset = require(rss.Modules.Cursor).Offset
                    --
                    local offset = Vector2.new(-(mouseOffset.X), -(mouseOffset.Y))
                    return offset
                end
            elseif table.find(Prime, game.PlaceId) then -- Prime
                function getOffset()
                    local offset = debug.getupvalues(require(rss.WolframV4.Mouse).RandomizeOffset)[1]
                    --
                    return offset
                end
            end
            --
            task.wait()
            --
            splix.shared.offset = getOffset()
        end
        --
        lib:Initialize()
    end
end
