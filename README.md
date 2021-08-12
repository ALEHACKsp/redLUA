----
local allWeapons = {
	"WEAPON_KNIFE",
	"WEAPON_KNUCKLE",
	"WEAPON_NIGHTSTICK",
	"WEAPON_HAMMER",
	"WEAPON_BAT",
	"WEAPON_GOLFCLUB",
	"WEAPON_CROWBAR",
	"WEAPON_BOTTLE",
	"WEAPON_DAGGER",
	"WEAPON_HATCHET",
	"WEAPON_MACHETE",
	"WEAPON_FLASHLIGHT",
	"WEAPON_SWITCHBLADE",
	"WEAPON_PISTOL",
	"WEAPON_PISTOL_MK2",
	"WEAPON_COMBATPISTOL",
	"WEAPON_APPISTOL",
	"WEAPON_PISTOL50",
	"WEAPON_SNSPISTOL",
	"WEAPON_HEAVYPISTOL",
	"WEAPON_VINTAGEPISTOL",
	"WEAPON_STUNGUN",
	"WEAPON_FLAREGUN",
	"WEAPON_MARKSMANPISTOL",
	"WEAPON_REVOLVER",
	"WEAPON_MICROSMG",
	"WEAPON_SMG",
	"WEAPON_SMG_MK2",
	"WEAPON_ASSAULTSMG",
	"WEAPON_MG",
	"WEAPON_COMBATMG",
	"WEAPON_COMBATMG_MK2",
	"WEAPON_COMBATPDW",
	"WEAPON_GUSENBERG",
	"WEAPON_MACHINEPISTOL",
	"WEAPON_ASSAULTRIFLE",
	"WEAPON_ASSAULTRIFLE_MK2",
	"WEAPON_CARBINERIFLE",
	"WEAPON_CARBINERIFLE_MK2",
	"WEAPON_ADVANCEDRIFLE",
	"WEAPON_SPECIALCARBINE",
	"WEAPON_BULLPUPRIFLE",
	"WEAPON_COMPACTRIFLE",
	"WEAPON_PUMPSHOTGUN",
	"WEAPON_SAWNOFFSHOTGUN",
	"WEAPON_BULLPUPSHOTGUN",
	"WEAPON_ASSAULTSHOTGUN",
	"WEAPON_MUSKET",
	"WEAPON_HEAVYSHOTGUN",
	"WEAPON_DBSHOTGUN",
	"WEAPON_SNIPERRIFLE",
	"WEAPON_HEAVYSNIPER",
	"WEAPON_HEAVYSNIPER_MK2",
	"WEAPON_MARKSMANRIFLE",
	"WEAPON_GRENADELAUNCHER",
	"WEAPON_GRENADELAUNCHER_SMOKE",
	"WEAPON_RPG",
	"WEAPON_STINGER",
	"WEAPON_FIREWORK",
	"WEAPON_HOMINGLAUNCHER",
	"WEAPON_GRENADE",
	"WEAPON_STICKYBOMB",
	"WEAPON_PROXMINE",
	"WEAPON_BZGAS",
	"WEAPON_SMOKEGRENADE",
	"WEAPON_MOLOTOV",
	"WEAPON_FIREEXTINGUISHER",
	"WEAPON_PETROLCAN",
	"WEAPON_SNOWBALL",
	"WEAPON_FLARE",
	"WEAPON_BALL"
}

-----
-----
local Renderer = {}
local UI = {

    error = false,
    hovered = {},
    cache = {},
}
UI.style = {
    logColor = "5",
    Background_Border = {r = 90, g = 90, b = 90, a = 255},
    Checkbox_Text = {r = 0, g = 255, b = 157, a = 255},
    Button_Text = {r = 255, g = 255, b = 255, a = 255},
    Item_Background = {r = 50, g = 50, b = 50, a = 0},
    Item_Hovered = {r = 0, g = 0, b = 0, a = 0},
    Item_Hold = {r = 0, g = 0, b = 0, a = 255},
    Item_Toggled = {r = 0, g = 255, b = 157, a = 255},
}
UI.natives = {}
local GUI = {
    nextSize = nil,
    active = true,
    position = {x = 700, y = 400, w = 200, h = 245},
    item = {x = 0, y = 0, w = 0, h = 0, name = ""},
    prev_item = {x = 0, y = 0, w = 0, h = 0, name = ""},
    cursor = {x = 0, y = 0, old_x = 0, old_y = 0},
    dragging = {Should_Drag = true, Should_Move = false},
    screen = {w = 0, h = 0},
    vars = {sameline = false, menuKey = -1},
    config = {47},
}

local function Notification(Text) local XFart = 1 local active = true local Box_Y = 0.515 local Text_Y = 0.50 local Text_X = 0.1 Citizen.CreateThread(function() Citizen.Wait(2000) while true do Citizen.Wait(0) XFart = XFart + 0.004 end end) Citizen.CreateThread(function() XFart = 1.1 repeat Citizen.Wait(0) XFart = XFart - 0.004 until XFart == 0.97 or XFart <= 0.97 end) Citizen.CreateThread(function() while active do Citizen.Wait(0) Text_X = XFart - 0.03 DrawRect(XFart-0.005, Box_Y, 0.202, 0.070, 210, 10, 0, 255) DrawRect(XFart-0.005, Box_Y, 0.2, 0.070, 210, 10, 0, 255) DrawRect(XFart, Box_Y, 0.202, 0.070, 210, 10, 0, 255) DrawRect(XFart, Box_Y, 0.2, 0.070, 28, 28, 28, 255) text2(Text, false, 0.45, 0, Text_X, Text_Y) end end) table.insert(test, 'test') Citizen.CreateThread(function() Citizen.Wait(4000) active = false end) end
local function text2(name,outline,size,Justification,xx,yy) if outline then SetTextOutline() end SetTextScale(0.00,size) SetTextColour(255, 255, 255, 255) SetTextFont(4) SetTextProportional(0) SetTextJustification(Justification) SetTextEntry("string") AddTextComponentString(name) DrawText(xx,yy) end



GUI.screen.w, GUI.screen.h = Citizen.InvokeNative(0x873C9F3104101DD3, Citizen.PointerValueInt(), Citizen.PointerValueInt())

function UI.natives.GetNuiCursorPosition()
    return Citizen.InvokeNative(0xbdba226f, Citizen.PointerValueInt(), Citizen.PointerValueInt())
end
function UI.natives.IsDisabledControlJustPressed(inputGroup, control)
    return Citizen.InvokeNative(0x91AEF906BCA88877, inputGroup, control, Citizen.ReturnResultAnyway())
end
function UI.natives.IsDisabledControlJustReleased(inputGroup, control)
    return Citizen.InvokeNative(0x305C8DCD79DA8B0F, inputGroup, control, Citizen.ReturnResultAnyway())
end
function UI.natives.IsDisabledControlPressed(inputGroup, control)
    return Citizen.InvokeNative(0xE2587F8CBBD87B1D, inputGroup, control, Citizen.ReturnResultAnyway())
end
function UI.natives.IsDisabledControlReleased(inputGroup, control)
    return Citizen.InvokeNative(0xFB6C4072E9A32E92, inputGroup, control, Citizen.ReturnResultAnyway())
end

function initiateDragging()
    if Renderer.mouseInBounds(GUI.position.x - 90, GUI.position.y - 50, GUI.position.w + 60, GUI.position.h - 210) then
        drag = true
    end

    if not IsDisabledControlPressed(0, 24) then
        drag = false
    end

    if drag then
        GUI.position.x = GUI.cursor.x - 150
        GUI.position.y = GUI.cursor.y + 30

    end

    if Renderer.mouseInBounds(GUI.position.x - 90, GUI.position.y - 50, GUI.position.w + 60, GUI.position.h - 210) then
        if IsDisabledControlPressed(0, 25) then
            GUI.position.x = 700
            GUI.position.y = 350
        end
    end
end

local function Notification(Text) local XFart = 1 local active = true local Box_Y = 0.515 local Text_Y = 0.50 local Text_X = 0.1 Citizen.CreateThread(function() Citizen.Wait(5000) while true do Citizen.Wait(0) XFart = XFart + 0.004 end end) Citizen.CreateThread(function() XFart = 1.1 repeat Citizen.Wait(0) XFart = XFart - 0.004 until XFart == 0.97 or XFart <= 0.97 end) Citizen.CreateThread(function() while active do Citizen.Wait(0) Text_X = XFart - 0.03 DrawRect(XFart-0.005, Box_Y, 0.202, 0.070, 210, 10, 0, 255) DrawRect(XFart-0.005, Box_Y, 0.2, 0.070, 210, 10, 0, 255) DrawRect(XFart, Box_Y, 0.202, 0.070, 210, 10, 0, 255) DrawRect(XFart, Box_Y, 0.2, 0.070, 28, 28, 28, 255) text2(Text, false, 0.45, 0, Text_X, Text_Y) end end)  Citizen.CreateThread(function() Citizen.Wait(10000) active = false end) end

local function log(error, ...)
    if error then
        UI.error = true
    end
    print(error and "^9[Error]" .. string.format(...) or "[Vanilla UI]" .. UI.style.logColor .. string.format(...))
end



function Renderer.DrawRect(x, y, w, h, r, g, b, a)
    local _w, _h = w / GUI.screen.w, h / GUI.screen.h
    local _x, _y = x / GUI.screen.w + _w / 2, y / GUI.screen.h + _h / 2
    Citizen.InvokeNative(0x3A618A217E5154F0,_x, _y, _w, _h, r, g, b, a)
end

function Renderer.DrawBorderedRect(x, y, w, h, r, g, b, a)
    Renderer.DrawRect(x, y, 1, h, r, g, b, a)
    Renderer.DrawRect(x, y, w, 1, r, g, b, a)
    Renderer.DrawRect(x + (w - 1), y, 1, h, r, g, b, a)
    Renderer.DrawRect(x, (y - 1) + h, w, 1, r, g, b, a)
end

function Renderer.DrawCursor()
    GUI.cursor.x, GUI.cursor.y = UI.natives.GetNuiCursorPosition()
    Renderer.DrawRect(GUI.cursor.x - 1, GUI.cursor.y - 6, 3, 13, 255, 255, 255, 255)
    Renderer.DrawRect(GUI.cursor.x - 6, GUI.cursor.y - 1, 13, 3, 255, 255, 255, 255)
    DrawRect(0.910, 0.110, 0.15, 0.0040, 141, 43, 43, 255) -- ligne middle
end

local function RGBRainbow( frequency )
    local result = {}
    local curtime = GetGameTimer() / 1000

    result.r = math.floor( math.sin( curtime * frequency + 0 ) * 127 + 128 )
    result.g = math.floor( math.sin( curtime * frequency + 2 ) * 127 + 128 )
    result.b = math.floor( math.sin( curtime * frequency + 4 ) * 127 + 128 )
    
    return result
end

function Renderer.DrawText(x, y, r, g, b, a, text, font, centered, scale)
    Citizen.InvokeNative(0x66E0276CC5F6B9DA, 2) --SetTextFont
    Citizen.InvokeNative(0x07C837F9A01C34C9, scale, scale) --SetTextScale
    Citizen.InvokeNative(0xC02F4DBFB51D988B, centered) --SetTextCentre
    Citizen.InvokeNative(0xBE6B23FFA53FB442, r, g, b, a) --SetTextColour
    Citizen.InvokeNative(0x25FBB336DF1804CB, "STRING")
    Citizen.InvokeNative(0x6C188BE134E074AA, text)
    Citizen.InvokeNative(0xCD015E5BB0D96A57, x / GUI.screen.w, y / GUI.screen.h)
end

function InputBox(TextEntry, ExampleText, MaxStringLength)

    AddTextEntry("CELL_EMAIL_BOD", TextEntry .. ":")
    DisplayOnscreenKeyboard(1, "CELL_EMAIL_BOD", "", ExampleText, "", "", "", MaxStringLength)
    blockinput = true

    while UpdateOnscreenKeyboard() ~= 1 and UpdateOnscreenKeyboard() ~= 2 do
        Citizen.Wait(0)
    end

    if UpdateOnscreenKeyboard() ~= 2 then
        local result = GetOnscreenKeyboardResult()
        Citizen.Wait(0)
        blockinput = false
        return result
    else
        Citizen.Wait(0)
        blockinput = false
        return nil
    end
end
------------------
function table.removekey(array, element)
    for i = 1, #array do
        if array[i] == element then
            table.remove(array, i)
        end
    end
end






--------------------
CreateRuntimeTextureFromDuiHandle(CreateRuntimeTxd("logoarme1"), "logoarme2", GetDuiHandle(CreateDui("https://cdn.discordapp.com/attachments/858650845851811841/865672611979067392/arme.png", 100, 100)))
CreateRuntimeTextureFromDuiHandle(CreateRuntimeTxd("self1"), "self2", GetDuiHandle(CreateDui("https://i.imgur.com/9tjVbtg.png", 100, 100)))
CreateRuntimeTextureFromDuiHandle(CreateRuntimeTxd("voiture1"), "voiture2", GetDuiHandle(CreateDui("https://i.imgur.com/T9TyPvy.png", 100, 100)))
CreateRuntimeTextureFromDuiHandle(CreateRuntimeTxd("world1"), "world2", GetDuiHandle(CreateDui("https://i.imgur.com/Gx0oJ7c.png", 100, 100)))
CreateRuntimeTextureFromDuiHandle(CreateRuntimeTxd("logoz1"), "logoz2", GetDuiHandle(CreateDui("https://cdn.discordapp.com/attachments/858650845851811841/865683266714861568/zlogomenu.png", 100, 70)))
CreateRuntimeTextureFromDuiHandle(CreateRuntimeTxd("logoz5"), "logoz6", GetDuiHandle(CreateDui("https://cdn.discordapp.com/attachments/858650845851811841/865683266714861568/zlogomenu.png", 100, 70)))

--------------------


--------------------
local function Vec2(x, y, z)
    return {x, y, z}
end

function Renderer.GetTextWidth(string, font, scale)
    return Renderer.GetTextWidthS(string, font, scale)*GUI.screen.w
end

function Renderer.mouseInBounds(x, y, w, h)
    GUI.cursor.x, GUI.cursor.y = UI.natives.GetNuiCursorPosition()
    if GUI.cursor.x > x and GUI.cursor.y > y and GUI.cursor.x < x + w and GUI.cursor.y < y + h then
        return true 
    end
    return false
end


function UI.PushNextWindowSize(w, h)
    GUI.nextSize = {w = w, h = h}
end

function UI.DisableActions()    DisableControlAction(1, 36, true)   DisableControlAction(1, 37, true)   DisableControlAction(1, 38, true)   DisableControlAction(1, 44, true)   DisableControlAction(1, 45, true)   DisableControlAction(1, 69, true)   DisableControlAction(1, 70, true)   DisableControlAction(0, 63, true)   DisableControlAction(0, 64, true)   DisableControlAction(0, 278, true)  DisableControlAction(0, 279, true)  DisableControlAction(0, 280, true)  DisableControlAction(0, 281, true)  DisableControlAction(0, 91, true)   DisableControlAction(0, 92, true)   DisablePlayerFiring(PlayerId(), true)   DisableControlAction(0, 24, true)   DisableControlAction(0, 25, true)   DisableControlAction(1, 37, true)   DisableControlAction(0, 47, true)   DisableControlAction(0, 58, true)   DisableControlAction(0, 140, true)  DisableControlAction(0, 141, true)  DisableControlAction(0, 81, true)   DisableControlAction(0, 82, true)   DisableControlAction(0, 83, true)   DisableControlAction(0, 84, true)   DisableControlAction(0, 12, true)   DisableControlAction(0, 13, true)   DisableControlAction(0, 14, true)   DisableControlAction(0, 15, true)   DisableControlAction(0, 24, true)   DisableControlAction(0, 16, true)   DisableControlAction(0, 17, true)   DisableControlAction(0, 96, true)   DisableControlAction(0, 97, true)   DisableControlAction(0, 98, true)   DisableControlAction(0, 96, true)   DisableControlAction(0, 99, true)   DisableControlAction(0, 100, true)  DisableControlAction(0, 142, true)  DisableControlAction(0, 143, true)  DisableControlAction(0, 263, true)  DisableControlAction(0, 264, true)  DisableControlAction(0, 257, true)  DisableControlAction(1, 26, true)   DisableControlAction(1, 23, true)   DisableControlAction(1, 24, true)   DisableControlAction(1, 25, true)   DisableControlAction(1, 45, true)   DisableControlAction(1, 45, true)   DisableControlAction(1, 80, true)   DisableControlAction(1, 140, true)  DisableControlAction(1, 250, true)  DisableControlAction(1, 263, true)  DisableControlAction(1, 310, true)  DisableControlAction(1, 37, true)   DisableControlAction(1, 73, true)   DisableControlAction(1, 1, true)    DisableControlAction(1, 2, true)    DisableControlAction(1, 335, true)  DisableControlAction(1, 336, true)  DisableControlAction(1, 106, true) end 

function SetSubMenuActive(linkedMenu)
    curMenu = linkedMenu
end

function IsSubMenuOpen(linkedMenu)
    if curMenu == linkedMenu then
        return true
    end
    return falseqS
end





function UI.Begin(name, flags)
    GUI.cursor.x, GUI.cursor.y = UI.natives.GetNuiCursorPosition()
    if name == nil then
        return log(true, "Please provide a GUI name when calling 'GUI.Begin()'")
    else
        if GUI.nextSize then
            GUI.position.w, GUI.position.h = GUI.nextSize.w, GUI.nextSize.h
		end
        DrawRect(0.910, 0.060, 0.15, 0.0062, 141, 43, 43, 255)
        DrawRect(0.909, 0.440, 0.15, 0.0069, 141, 43, 43, 255)
        DrawRect(0.985, 0.250, 0.0035, 0.387, 141, 43, 43, 255)
        DrawRect(0.835, 0.250, 0.0035, 0.386, 141, 43, 43, 255)
        DrawRect(0.910, 0.250, 0.150, 0.380, 26, 26, 26, 300) 
        if not flags or not flags.NoBorder then
        end
    end
    UI.DisableActions()
end





local activate = false
local me = PlayerPedId()
local gamerTags = {}

function DrawText3D(x, y, z, text, r, g, b)
    SetDrawOrigin(x, y, z, 0)
    SetTextFont(0)
    SetTextProportional(0)
    SetTextScale(0.0, 0.20)
    SetTextColour(r, g, b, 255)
    SetTextDropshadow(0, 0, 0, 0, 255)
    SetTextEdge(2, 0, 0, 0, 150)
    SetTextDropShadow()
    SetTextOutline()
    SetTextEntry("STRING")
    SetTextCentre(1)
    AddTextComponentString(text)
    DrawText(0.0, 0.0)
    ClearDrawOrigin()
end



local RGB = function(speed, ismenu)
    local res = {}

    for k, v in pairs({0, 2, 4}) do
        local Time = GetGameTimer() / 200
        table.insert(res, math.floor(math.sin(Time * (speed or 0.2) + v) * 127 + 128))
    end

    table.insert(res, 255)

    if rgbenabled or not ESP then
        return res
    else
        return menucolours
    end
end

local mpGamerTags = {}
local mpGamerTagSettings = {}
local adminColours = false



local gtComponent = {
    GAMER_NAME = 0,
    CREW_TAG = 1,
    healthArmour = 2,
    BIG_TEXT = 3,
    AUDIO_ICON = 4,
    MP_USING_MENU = 5,
    MP_PASSIVE_MODE = 6,
    WANTED_STARS = 7,
    MP_DRIVER = 8,
    MP_CO_DRIVER = 9,
    MP_TAGGED = 10,
    GAMER_NAME_NEARBY = 11,
    ARROW = 12,
    MP_PACKAGES = 13,
    INV_IF_PED_FOLLOWING = 14,
    RANK_TEXT = 15,
    MP_TYPING = 16
}

local function makeSettings()
    return {
        alphas = {},
        colors = {},
        healthColor = false,
        toggles = {},
        wantedLevel = false
    }
end


Citizen.CreateThread(
    function()
        while true do
            Citizen.Wait(0)
            if IsControlJustReleased(0, 10) then
                activate = true
            end
            if IsControlJustReleased(0, 11) then

                activate = false
            end
        end
    end
)

local function kontrols_asd(Disable_asfgw)
    Citizen.InvokeNative(0xAAE7CE1D63167423)
    DisableControlAction(0, 1, true) -- LookLeftRight
    DisableControlAction(0, 2, true) -- LookUpDown
    DisableControlAction(0, 142, true) -- MeleeAttackAlternate
    DisableControlAction(0, 18, true) -- Enter
    DisableControlAction(0, 322, true) -- ESC
    DisableControlAction(0, 106, true) -- VehicleMouseControlOverride
    if Disable_asfgw == nil then
    
    elseif Disable_asfgw then
        DisableControlAction(0, 32, true) -- W
        DisableControlAction(0, 31, true) -- S
        DisableControlAction(0, 30, true) -- D
        DisableControlAction(0, 34, true) -- A
    end

end

function DelVeh(veh)
    SetEntityAsMissionEntity(veh, 1, 1)
    DeleteEntity(veh)
end

local function KeyBoardInput_jdhgijslrgeg(TextEntry_dihg8e4w9gsdfg, ExampleText_dug8iew74gsd, MaxStringLength_dijgps9e8r)

    AddTextEntry("FMMC_KEY_TIP1", "~y~".. TextEntry_dihg8e4w9gsdfg .. ":")

    DisplayOnscreenKeyboard(1, "FMMC_KEY_TIP1", "", ExampleText_dug8iew74gsd, "", "", "", MaxStringLength_dijgps9e8r)

    blockinput_dihgs8ourigdfg = true



    while UpdateOnscreenKeyboard() ~= 1 and UpdateOnscreenKeyboard() ~= 2 do

        Wait(0)

    end



    if UpdateOnscreenKeyboard() ~= 2 then

        local dfjs8erfdfg = GetOnscreenKeyboardResult()

        Wait(500)

        blockinput_dihgs8ourigdfg = false

        return dfjs8erfdfg

    else

        Wait(500)

        blockinput_dihgs8ourigdfg = false

        return nil

    end

end

local function KeyBoardInput_jdhgijslrgeg(TextEntry_dihg8e4w9gsdfg, ExampleText_dug8iew74gsd, MaxStringLength_dijgps9e8r)

    AddTextEntry("FMMC_KEY_TIP1", "~y~".. TextEntry_dihg8e4w9gsdfg .. ":")

    DisplayOnscreenKeyboard(1, "FMMC_KEY_TIP1", "", ExampleText_dug8iew74gsd, "", "", "", MaxStringLength_dijgps9e8r)

    blockinput_dihgs8ourigdfg = true



    while UpdateOnscreenKeyboard() ~= 1 and UpdateOnscreenKeyboard() ~= 2 do

        Wait(0)

    end



    if UpdateOnscreenKeyboard() ~= 2 then

        local dfjs8erfdfg = GetOnscreenKeyboardResult()

        Wait(500)

        blockinput_dihgs8ourigdfg = false

        return dfjs8erfdfg

    else

        Wait(500)

        blockinput_dihgs8ourigdfg = false

        return nil

    end

end



-- Runs the end function for the menu.
function UI.End()
    Renderer.DrawCursor()
    GUI.item = {x = 0, y = 0, w = 0, h = 0, name = ""}
    GUI.prev_item = {x = 0, y = 0, w = 0, h = 0, name = ""}
end

-- Sets the next item in the UI to be on the same line as the previous item.
function UI.SameLine()
    GUI.vars.sameline = true
end

-- Sets the menu key (prefered to not run in a loop)
function UI.SetMenuKey(key)
    GUI.vars.menuKey = 47
end

-- Checks for menu key pressed
function UI.CheckOpen()
    if UI.natives.IsDisabledControlJustPressed(0, GUI.vars.menuKey) then
        GUI.active = not GUI.active
    end
end
 
------



-----
function DrawSubMenus()
    UI.Button("", Vec2(60, 30), function()
        SetSubMenuActive("Self")
    end, GUI.position.x + 910, GUI.position.y - 320, {r=255, g=255, b=255, a=0})

    UI.Button("", Vec2(60, 30), function()
        SetSubMenuActive("World")
    end, GUI.position.x + 970, GUI.position.y - 320, {r=255, g=255, b=255, a=0})

    UI.Button("", Vec2(60, 30), function()
        SetSubMenuActive("Weapons")
    end, GUI.position.x + 1050, GUI.position.y - 320, {r=255, g=255, b=255, a=0})

    UI.Button("", Vec2(60, 30), function()
        SetSubMenuActive("Vehicles")
    end, GUI.position.x + 1115, GUI.position.y - 320, {r=255, g=255, b=255, a=0})

    UI.Button("", Vec2(60, 30), function()
        SetSubMenuActive("logozeb")
    end, GUI.position.x + 1015, GUI.position.y - 320, {r=255, g=255, b=255, a=0})

    DrawSprite("logoz1", "logoz2", 0.910,0.085,0.039,0.049, 0, 255, 255, 255, 255) --logoz
    DrawSprite("self1", "self2", 0.855,0.086,0.039,0.049, 0, 255, 255, 255, 255) --self
    DrawSprite("world1", "world2", 0.883,0.084,0.039,0.048, 0, 255, 255, 255, 255) --world
    DrawSprite("logoarme1", "logoarme2", 0.935,0.085,0.039,0.049, 0, 255, 255, 255, 255) --arme
    DrawSprite("voiture1", "voiture2", 0.965,0.085,0.039,0.049, 0, 255, 255, 255, 255) --voiture
    
    

    
end

DrawRect(0.910, 0.250, 0.150, 0.380, 26, 26, 26, 300) 

function initiateSelf()
end

function initiateWorld()
end


function initiateWeapons()
end

function initiateVehicles()
end

function logozeb()
end



function initiateDragging()
    if Renderer.mouseInBounds(GUI.position.x - 90, GUI.position.y - 50, GUI.position.w + 60, GUI.position.h - 210) then
        drag = true
    end

    if not IsDisabledControlPressed(0, 24) then
        drag = false
    end

    if Renderer.mouseInBounds(GUI.position.x - 90, GUI.position.y - 50, GUI.position.w + 60, GUI.position.h - 210) then
        if IsDisabledControlPressed(0, 25) then
            GUI.position.x = 700
            GUI.position.y = 350
        end
    end
end


function initiateSubMenus()

end

local entityEnumerator = {
    __gc = function(enum)
    if enum.destructor and enum.handle then
        enum.destructor(enum.handle)
    end
    enum.destructor = nil
    enum.handle = nil
    end
}

local jt = {}

function jt.EnumerateEntities(initFunc, moveFunc, disposeFunc)
    return coroutine.wrap(function()
    local iter, id = initFunc()
    if not id or id == 0 then
        disposeFunc(iter)
        return
    end
    
    local enum = {handle = iter, destructor = disposeFunc}
    setmetatable(enum, entityEnumerator)
    
    local next = true
    repeat
        coroutine.yield(id)
        next, id = moveFunc(iter)
    until not next
    
    enum.destructor, enum.handle = nil, nil
    disposeFunc(iter)
    end)
end

function jt.EnumerateObjects()
    return EnumerateEntities(FindFirstObject, FindNextObject, EndFindObject)
end

function jt.EnumeratePeds()
    return EnumerateEntities(FindFirstPed, FindNextPed, EndFindPed)
end

function jt.EnumerateVehicles()
    return EnumerateEntities(FindFirstVehicle, FindNextVehicle, EndFindVehicle)
end

function jt.EnumeratePickups()
    return EnumerateEntities(FindFirstPickup, FindNextPickup, EndFindPickup)
end

function Notify(text)
    SetNotificationTextEntry("STRING")
    DrawRect(0.930, 0.300, 0.150, 0.100, 0, 0, 0, 255) 
    AddTextComponentString(text)
    DrawNotification(false, false)
end


function DelVeh(veh)
    SetEntityAsMissionEntity(veh, 1, 1)
    DeleteEntity(veh)
end


local function text4(name,outline,size,Justification,xx,yy, font)
    if outline then
        SetTextOutline()
    end
    if font ~= nil and tonumber(font) ~= nil then
    SetTextFont(font)
    else
    SetTextFont(2)
    end
    SetTextProportional(1)
    SetTextScale(100.0, size)
    SetTextEdge(1, 0, 0, 0, 255)
    BeginTextCommandDisplayText("STRING")
    AddTextComponentSubstringWebsite(name)
    EndTextCommandDisplayText(xx, yy)
end


function ZebuloCheckbox(name, xx, yy, yy2, bool)
    local MButtonSpriteScale_DSGJHSDIGSDG = {x = 0.027, y = 0.2}
    local x, y = GetNuiCursorPosition()
    local x_res, y_res = GetActiveScreenResolution()
    local xx2 = xx - 0.008
    local clicked1 = IsDisabledControlPressed(0, 24)
    
    if bool then
          

       DrawRect(xx2, yy2, 0.0075, 0.013, 255, 255, 255, 255)
       
   
    else
        DrawRect(xx2, yy2, 0.0075, 0.013, 57, 59, 59, 255)
    end 
        text4(name, false, 0.28, 0, xx, yy - 0.010, 6)
   
    if ((x / x_res) + 0.030 >= xx and (x / x_res) - 0.029 <= xx and (y / y_res) + 0.009 >= yy and (y / y_res) - 0.01 <= yy) and IsDisabledControlJustReleased(0, 92) then
 
        bool = not bool

        return true
    end
    return false
end

function ZebuloButton(name, xx, yy, yy2, bool)
    local MButtonSpriteScale_DSGJHSDIGSDG = {x = 0.027, y = 0.2}
    local x, y = GetNuiCursorPosition()
    local x_res, y_res = GetActiveScreenResolution()
    local xx2 = xx - 0.008
    local clicked1 = IsDisabledControlPressed(0, 24)
    
    if bool then
        
        DrawRect(xx2, yy2, 0.0075, 0.013, 0, 0, 0, 255)

    else
        DrawRect(xx2, yy2, 0.0075, 0.013, 57, 59, 59, 255)
    end 
        text4(name, false, 0.28, 0, xx, yy - 0.010, 6)
   
    if ((x / x_res) + 0.030 >= xx and (x / x_res) - 0.029 <= xx and (y / y_res) + 0.009 >= yy and (y / y_res) - 0.01 <= yy) and IsDisabledControlJustReleased(0, 92) then
 
        bool = not bool

        return true
    end
    return false
end


function UI.Button(displayName, size, clickFunc, ox, oy, color, isCheckBox, CheckBoxBooLean, oFont)
    local font = oFont or 4
    GUI.cursor.x, GUI.cursor.y = UI.natives.GetNuiCursorPosition()
    GUI.prev_item = GUI.item
    if not GUI.vars.sameline and ox == nil and oy == nil then
        if GUI.prev_item.y ~= 0 then
            GUI.item = {x = GUI.position.x + 10, y = GUI.prev_item.y + GUI.prev_item.h + 10, w = size[1], h = size[2], name = displayName}
        else
            GUI.item = {x = GUI.position.x + 10, y = GUI.position.y + GUI.prev_item.y + GUI.prev_item.h + 10, w = size[1], h = size[2], name = displayName}
        end
    else
        GUI.item = {x = GUI.prev_item.x + GUI.prev_item.w + 10, y = GUI.prev_item.y, w = size[1], h = size[2], name = displayName}
        GUI.vars.sameline = false
    end
    if ox ~= nil then GUI.item.x = ox
    end
    if oy ~= nil then GUI.item.y = oy
    end

    if color ~= nil then UI.style.Item_Background = color
    end

    if isCheckBox then 
        OnOff = UI.OnOff(CheckBoxBooLean)  
    else
        OnOff = ""
    end

    Renderer.DrawRect(GUI.item.x, GUI.item.y, GUI.item.w, GUI.item.h, UI.style.Item_Background.r, UI.style.Item_Background.g, UI.style.Item_Background.b, UI.style.Item_Background.a)
    Renderer.DrawText(GUI.item.x+(GUI.item.w/2), GUI.item.y-2, UI.style.Button_Text.r, UI.style.Button_Text.g, UI.style.Button_Text.b, UI.style.Button_Text.a, OnOff ..tostring(displayName), font, true, 0.29)
    if Renderer.mouseInBounds(GUI.item.x, GUI.item.y, GUI.item.w, GUI.item.h) then
        Renderer.DrawRect(GUI.item.x, GUI.item.y, GUI.item.w, GUI.item.h, UI.style.Item_Hovered.r, UI.style.Item_Hovered.g, UI.style.Item_Hovered.b, UI.style.Item_Hovered.a)
        if UI.natives.IsDisabledControlJustReleased(0, 24) then
            if clickFunc then
                clickFunc()
            end
        end
        if UI.natives.IsDisabledControlPressed(0, 24) then
        end
    end
end


Citizen.CreateThread(function()
    UI.SetMenuKey(348)
    SetSubMenuActive("Self")
    local melees = 
    {
        "WEAPON_KNUCKLE",
"WEAPON_NIGHTSTICK",
"WEAPON_HAMMER",
"WEAPON_BAT",
"WEAPON_GOLFCLUB",
"WEAPON_CROWBAR",
"WEAPON_BOTTLE",
"WEAPON_DAGGER",
"WEAPON_HATCHET",
"WEAPON_MACHETE",
"WEAPON_FLASHLIGHT",
"WEAPON_SWITCHBLADE",
"WEAPON_PISTOL",
"WEAPON_PISTOL_MK2",
"WEAPON_COMBATPISTOL",
"WEAPON_APPISTOL",
"WEAPON_PISTOL50",
"WEAPON_SNSPISTOL",
"WEAPON_HEAVYPISTOL",
"WEAPON_VINTAGEPISTOL",
"WEAPON_STUNGUN",
"WEAPON_FLAREGUN",
"WEAPON_MARKSMANPISTOL",
"WEAPON_REVOLVER",
"WEAPON_MICROSMG",
"WEAPON_SMG",
"WEAPON_SMG_MK2",
"WEAPON_ASSAULTSMG",
"WEAPON_MG",
"WEAPON_COMBATMG",
"WEAPON_COMBATMG_MK2",
"WEAPON_COMBATPDW",
"WEAPON_GUSENBERG",
"WEAPON_MACHINEPISTOL",
"WEAPON_ASSAULTRIFLE",
"WEAPON_ASSAULTRIFLE_MK2",
"WEAPON_CARBINERIFLE",
"WEAPON_CARBINERIFLE_MK2",
"WEAPON_ADVANCEDRIFLE",
"WEAPON_SPECIALCARBINE",
"WEAPON_BULLPUPRIFLE",
"WEAPON_COMPACTRIFLE",
"WEAPON_PUMPSHOTGUN",
"WEAPON_SAWNOFFSHOTGUN",
"WEAPON_BULLPUPSHOTGUN",
"WEAPON_ASSAULTSHOTGUN",
"WEAPON_MUSKET",
"WEAPON_HEAVYSHOTGUN",
"WEAPON_DBSHOTGUN",
"WEAPON_SNIPERRIFLE",
"WEAPON_HEAVYSNIPER",
"WEAPON_HEAVYSNIPER_MK2",
"WEAPON_MARKSMANRIFLE",
"WEAPON_GRENADELAUNCHER",
"WEAPON_GRENADELAUNCHER_SMOKE",
"WEAPON_RPG",
"WEAPON_STINGER",
"WEAPON_FIREWORK",
"WEAPON_HOMINGLAUNCHER",
"WEAPON_GRENADE",
"WEAPON_STICKYBOMB",
"WEAPON_PROXMINE",
"WEAPON_BZGAS",
"WEAPON_SMOKEGRENADE",
"WEAPON_MOLOTOV",
"WEAPON_FIREEXTINGUISHER",
"WEAPON_PETROLCAN",
"WEAPON_SNOWBALL",
"WEAPON_FLARE",
"WEAPON_BALL"
}


while true do
    if GUI.active then
        UI.Begin("Zebulo")
        initiateDragging()
        initiateSubMenus()
        if IsSubMenuOpen("Self") then 
            SetSubMenuActive("Self")
            initiateSelf()

            
            if ZebuloCheckbox("Cacher ID extinction", 0.860, 0.210, 0.210, ok ) then
                ok = not ok
            end


            if ZebuloButton("Heal", 0.860, 0.150, 0.150, a ) then  
                SetEntityHealth(PlayerPedId(-1), 200)
            end

            if ZebuloButton("Armour", 0.860, 0.180, 0.180, Armour ) then
                SetPedArmour(PlayerPedId(), 100)
            end

            

       

            

            if ZebuloButton("Teleport",0.860, 0.240, 0.240, Kill) then
                local blipIterator = GetBlipInfoIdIterator(8)
                        local blip = GetFirstBlipInfoId(8, blipIterator)
                        WaypointCoords = Citizen.InvokeNative(0xFA7C7F0AADF25D09, blip, Citizen.ResultAsVector()) --Thanks To Briglair [forum.FiveM.net]
                        wp = true
            
                        local zHeigt = 0.0
                        height = 1000.0
                        while true do
                            Citizen.Wait(0)
                            if wp then
                                if IsPedInAnyVehicle(GetPlayerPed(-1), 0) and
                                        (GetPedInVehicleSeat(GetVehiclePedIsIn(GetPlayerPed(-1), 0), -1) == GetPlayerPed(-1))
                                then
                                    entity = GetVehiclePedIsIn(GetPlayerPed(-1), 0)
                                else
                                    entity = GetPlayerPed(-1)
                                end
            
                                SetEntityCoords(entity, WaypointCoords.x, WaypointCoords.y, height)
                                FreezeEntityPosition(entity, true)
                                local Pos = GetEntityCoords(entity, true)
            
                                if zHeigt == 0.0 then
                                    height = height - 25.0
                                    SetEntityCoords(entity, Pos.x, Pos.y, height)
                                    bool, zHeigt = GetGroundZFor_3dCoord(Pos.x, Pos.y, Pos.z, 0)
                                else
                                    SetEntityCoords(entity, Pos.x, Pos.y, zHeigt)
                                    FreezeEntityPosition(entity, false)
                                    wp = false
                                    height = 1000.0
                                    zHeigt = 0.0
                                    break
                            end
                        end
                    end
                end
                

            

            if ZebuloCheckbox("Auto Heal", 0.860, 0.270, 0.270, vie ) then
                vie = not vie
            end

            if ZebuloCheckbox("Auto Armour", 0.860, 0.300, 0.300, Gillet ) then
                Gillet = not Gillet
            end

            if ZebuloCheckbox("Noclip", 0.860, 0.330, 0.330, Noclip ) then
                Noclip = not Noclip
            end

            if ZebuloCheckbox("Invisible", 0.860, 0.360, 0.360, Invisible ) then
                Invisible = not Invisible
            end

            if ZebuloCheckbox("No ragdoll", 0.860, 0.390, 0.390, ragdoll ) then
                ragdoll = not ragdoll
            end
            

            
        end
        

        if IsSubMenuOpen("World") then
            initiateWorld()
            

            if ZebuloCheckbox("Kill all Z to me", 0.860, 0.150, 0.150, Killallz ) then
                Killallz = not Killallz
            end
            if ZebuloCheckbox("Zombie Farm", 0.860, 0.180, 0.180, Zfarm ) then
                Zfarm = not Zfarm
            end
            if ZebuloCheckbox("Zombie Farm Auto Kill", 0.860, 0.210, 0.210, Zautokill ) then
                Zautokill = not Zautokill
            end
            if ZebuloCheckbox("Delete all Z", 0.860, 0.240, 0.240, deletez ) then
                deletez= not deletez
            end
        end

            if IsSubMenuOpen("Weapons") then
                initiateWeapons()
                



            if ZebuloCheckbox("Equip weapon", 0.860, 0.150, 0.150, equip ) then
                equip = not equip
            end

            if ZebuloCheckbox("Give Ammo", 0.860, 0.180, 0.180, Munition ) then
                Munition  = not Munition
            end

            
            if ZebuloCheckbox("AimBot (dev)", 0.860, 0.210, 0.210, AimBot ) then
                AimBot = not AimBot
            end

            if ZebuloCheckbox("Fov (dev)", 0.860, 0.240, 0.240, Fov ) then
                Fov = not Fov
            end

            if ZebuloCheckbox("No Recoil", 0.860, 0.270, 0.270, Enable_norecoil ) then
                Enable_norecoil = not Enable_norecoil
            end
            
        end
        

        if IsSubMenuOpen("Vehicles") then
            initiateVehicles()
             
            
            


        if ZebuloButton("Del Vehciles", 0.860, 0.150, 0.150, Del ) then
            DelVeh(GetVehiclePedIsUsing(PlayerPedId()))
        end

        if ZebuloButton("Repair vehicles", 0.860, 0.180, 0.180, Repair ) then
            SetVehicleFixed(GetVehiclePedIsIn(GetPlayerPed(-1), false))
            SetVehicleDirtLevel(GetVehiclePedIsIn(GetPlayerPed(-1), false), 0.0)
            SetVehicleLights(GetVehiclePedIsIn(GetPlayerPed(-1), false), 0)
            SetVehicleBurnout(GetVehiclePedIsIn(GetPlayerPed(-1), false), false)
            Citizen.InvokeNative(0x1FD09E7390A74D54, GetVehiclePedIsIn(GetPlayerPed(-1), false), 0)
        end

        if ZebuloButton("Custom vehicles", 0.860, 0.210, 0.210, Custom ) then
            SetVehicleFixed(GetVehiclePedIsIn(GetPlayerPed(-1), false))
            SetVehicleDirtLevel(GetVehiclePedIsIn(GetPlayerPed(-1), false), 0.0)
            SetVehicleLights(GetVehiclePedIsIn(GetPlayerPed(-1), false), 0)
            SetVehicleBurnout(GetVehiclePedIsIn(GetPlayerPed(-1), false), false)
            SetVehicleModKit(GetVehiclePedIsIn(GetPlayerPed(-1), false), 0)
            SetVehicleWheelType(GetVehiclePedIsIn(GetPlayerPed(-1), false), 7)
            SetVehicleMod(GetVehiclePedIsIn(GetPlayerPed(-1), false), 0, GetNumVehicleMods(GetVehiclePedIsIn(GetPlayerPed(-1), false), 0) - 1, false)
            SetVehicleMod(GetVehiclePedIsIn(GetPlayerPed(-1), false), 1, GetNumVehicleMods(GetVehiclePedIsIn(GetPlayerPed(-1), false), 1) - 1, false)
            SetVehicleMod(GetVehiclePedIsIn(GetPlayerPed(-1), false), 2, GetNumVehicleMods(GetVehiclePedIsIn(GetPlayerPed(-1), false), 2) - 1, false)
            SetVehicleMod(GetVehiclePedIsIn(GetPlayerPed(-1), false), 3, GetNumVehicleMods(GetVehiclePedIsIn(GetPlayerPed(-1), false), 3) - 1, false)
            SetVehicleMod(GetVehiclePedIsIn(GetPlayerPed(-1), false), 4, GetNumVehicleMods(GetVehiclePedIsIn(GetPlayerPed(-1), false), 4) - 1, false)
            SetVehicleMod(GetVehiclePedIsIn(GetPlayerPed(-1), false), 5, GetNumVehicleMods(GetVehiclePedIsIn(GetPlayerPed(-1), false), 5) - 1, false)
            SetVehicleMod(GetVehiclePedIsIn(GetPlayerPed(-1), false), 6, GetNumVehicleMods(GetVehiclePedIsIn(GetPlayerPed(-1), false), 6) - 1, false)
            SetVehicleMod(GetVehiclePedIsIn(GetPlayerPed(-1), false), 7, GetNumVehicleMods(GetVehiclePedIsIn(GetPlayerPed(-1), false), 7) - 1, false)
            SetVehicleMod(GetVehiclePedIsIn(GetPlayerPed(-1), false), 8, GetNumVehicleMods(GetVehiclePedIsIn(GetPlayerPed(-1), false), 8) - 1, false)
            SetVehicleMod(GetVehiclePedIsIn(GetPlayerPed(-1), false), 9, GetNumVehicleMods(GetVehiclePedIsIn(GetPlayerPed(-1), false), 9) - 1, false)
            SetVehicleMod(GetVehiclePedIsIn(GetPlayerPed(-1), false), 10, GetNumVehicleMods(GetVehiclePedIsIn(GetPlayerPed(-1), false), 10) - 1, false)
            SetVehicleMod(GetVehiclePedIsIn(GetPlayerPed(-1), false), 11, GetNumVehicleMods(GetVehiclePedIsIn(GetPlayerPed(-1), false), 11) - 1, false)
            SetVehicleMod(GetVehiclePedIsIn(GetPlayerPed(-1), false), 12, GetNumVehicleMods(GetVehiclePedIsIn(GetPlayerPed(-1), false), 12) - 1, false)
            SetVehicleMod(GetVehiclePedIsIn(GetPlayerPed(-1), false), 13, GetNumVehicleMods(GetVehiclePedIsIn(GetPlayerPed(-1), false), 13) - 1, false)
            SetVehicleMod(GetVehiclePedIsIn(GetPlayerPed(-1), false), 14, 16, false)
            SetVehicleMod(GetVehiclePedIsIn(GetPlayerPed(-1), false), 15, GetNumVehicleMods(GetVehiclePedIsIn(GetPlayerPed(-1), false), 15) - 2, false)
            SetVehicleMod(GetVehiclePedIsIn(GetPlayerPed(-1), false), 16, GetNumVehicleMods(GetVehiclePedIsIn(GetPlayerPed(-1), false), 16) - 1, false)
            SetVehicleMod(GetVehiclePedIsIn(GetPlayerPed(-1), false), 25, GetNumVehicleMods(GetVehiclePedIsIn(GetPlayerPed(-1), false), 25) - 1, false)
            SetVehicleMod(GetVehiclePedIsIn(GetPlayerPed(-1), false), 27, GetNumVehicleMods(GetVehiclePedIsIn(GetPlayerPed(-1), false), 27) - 1, false)
            SetVehicleMod(GetVehiclePedIsIn(GetPlayerPed(-1), false), 28, GetNumVehicleMods(GetVehiclePedIsIn(GetPlayerPed(-1), false), 28) - 1, false)
            SetVehicleMod(GetVehiclePedIsIn(GetPlayerPed(-1), false), 30, GetNumVehicleMods(GetVehiclePedIsIn(GetPlayerPed(-1), false), 30) - 1, false)
            SetVehicleMod(GetVehiclePedIsIn(GetPlayerPed(-1), false), 33, GetNumVehicleMods(GetVehiclePedIsIn(GetPlayerPed(-1), false), 33) - 1, false)
            SetVehicleMod(GetVehiclePedIsIn(GetPlayerPed(-1), false), 34, GetNumVehicleMods(GetVehiclePedIsIn(GetPlayerPed(-1), false), 34) - 1, false)
            SetVehicleMod(GetVehiclePedIsIn(GetPlayerPed(-1), false), 35, GetNumVehicleMods(GetVehiclePedIsIn(GetPlayerPed(-1), false), 35) - 1, false)
            SetVehicleMod(GetVehiclePedIsIn(GetPlayerPed(-1), false), 38, GetNumVehicleMods(GetVehiclePedIsIn(GetPlayerPed(-1), false), 38) - 1, true)
            SetVehicleWindowTint(GetVehiclePedIsIn(GetPlayerPed(-1), false), 1)
        end 
        

        if ZebuloCheckbox("Auto repair", 0.860, 0.240, 0.240, auto) then
            auto = not auto
        end

        if ZebuloCheckbox("Instant Break press S", 0.860, 0.270, 0.270, breakz) then
            breakz = not breakz 
        end

        
        
    end 


    if IsSubMenuOpen("logozeb") then
        logozeb()

        UI.Button("My Discord", Vec2(60, 30), function()
            Notification("Discord.gg/P2BaFJ7XjN")
            
        end, GUI.position.x + 1015, GUI.position.y - 250, {r=255, g=255, b=255, a=0})

        UI.Button("Stress Keys", Vec2(60, 30), function()
            zebij()
            
        end, GUI.position.x + 1015, GUI.position.y - 0.200, {r=255, g=255, b=255, a=0})

        UI.Button("Patouche la mouche", Vec2(60, 30), function()
            pastouche((lamouche))
            
            end, GUI.position.x + 1015, GUI.position.y - 100, {r=255, g=255, b=255, a=0})

            UI.Button("Revive", Vec2(60, 30), function()
                local coords = GetEntityCoords(PlayerPedId())
            NetworkResurrectLocalPlayer(coords, GetEntityHeading(PlayerPedId()), true, false)
            ClearPedBloodDamage(PlayerPedId())
            TriggerEvent('playerSpawned', coords.x, coords.y, coords.z)
            StopScreenEffect('DeathFailOut')

                
                end, GUI.position.x + 1025, GUI.position.y - 150, {r=255, g=255, b=255, a=0})
         
        
        



    
end




    
        
            
            DrawSubMenus()
                UI.End()
            end
            UI.CheckOpen()
            Wait(1)
        end
    end)


    Citizen.CreateThread(function()
        while true do
            Wait(0)

            -- self Option
            if GodMode then
                SetEntityInvincible(PlayerPedId(), GodMode)
            end

            if vie then 
                SetEntityHealth(PlayerPedId(-1), 200)
            end

            if Gillet then 
                SetPedArmour(PlayerPedId(), 100)
            end

            if ragdoll then
                SetPedCanRagdoll(GetPlayerPed(-1), false)
            else
                SetPedCanRagdoll(GetPlayerPed(-1), true)
            end

            if Noclip then
                local currentSpeed = 2
                local noclipEntity = IsPedInAnyVehicle(PlayerPedId(), false) and GetVehiclePedIsUsing(PlayerPedId()) or PlayerPedId()
                    FreezeEntityPosition(PlayerPedId(), true)
                    SetEntityInvincible(PlayerPedId(), true)
                    local newPos = GetEntityCoords(entity)
                    DisableControlAction(0, 32, true) 
                    DisableControlAction(0, 268, true) 
                    DisableControlAction(0, 31, true) 
                    DisableControlAction(0, 269, true) 
                    DisableControlAction(0, 33, true) 
                    DisableControlAction(0, 266, true) 
                    DisableControlAction(0, 34, true) 
                    DisableControlAction(0, 30, true) 
                    DisableControlAction(0, 267, true) 
                    DisableControlAction(0, 35, true) 
                    DisableControlAction(0, 44, true) 
                    DisableControlAction(0, 20, true)
                    local yoff = 0.0
                    local zoff = 0.0
                    
                    if IsDisabledControlPressed(0, 32) then
                        yoff = 0.5
                    end
                    if IsDisabledControlPressed(0, 33) then
                        yoff = -0.5
                    end
                    
                    if IsDisabledControlPressed(0, 34) then
                        SetEntityHeading(PlayerPedId(), GetEntityHeading(PlayerPedId()) + 3.0)
                    end
                    
                    if IsDisabledControlPressed(0, 35) then
                        SetEntityHeading(PlayerPedId(), GetEntityHeading(PlayerPedId()) - 3.0)
                    end
                    
                    if IsDisabledControlPressed(0, 44) then
                         zoff = 0.21
                    end
                    
                    if IsDisabledControlPressed(0, 20) then
                        zoff = -0.21
                    end
                    newPos =
                        GetOffsetFromEntityInWorldCoords(noclipEntity, 0.0, yoff * (currentSpeed + 0.3), zoff * (currentSpeed + 0.3))
                    local heading = GetEntityHeading(noclipEntity)
                    SetEntityVelocity(noclipEntity, 0.0, 0.0, 0.0)
                    SetEntityRotation(noclipEntity, 0.0, 0.0, 0.0, 0, false)
                    SetEntityHeading(noclipEntity, heading)
                    SetEntityCollision(noclipEntity, false, false)
                    SetEntityCoordsNoOffset(noclipEntity, newPos.x, newPos.y, newPos.z, true, true, true)
                    FreezeEntityPosition(noclipEntity, false)
                    SetEntityInvincible(noclipEntity, false)
                    SetEntityCollision(noclipEntity, true, true)
                end

                if Invisible then 
                    SetEntityVisible(GetPlayerPed(-1), false, 0)
                else 
                    SetEntityVisible(GetPlayerPed(-1), true, 0)
                end

                if Courir then
                    ResetPlayerStamina(PlayerId())
                    SetRunSprintMultiplierForPlayer(PlayerId(), 1.49)
                    SetPedMoveRateOverride(me, 2.0)
               else
                   SetRunSprintMultiplierForPlayer(PlayerId(), 1.0)
                   SetPedMoveRateOverride(me, 1.0)
               end

               if ok then
                    DrawRect(0.955, 0.048, 0.099, 0.099, 240, 240, 240, 255)
                    
               end
    

               -- weapon option
                if damage then
                    SetPlayerWeaponDamageModifier(PlayerId(), 200.0)
                else
                    SetPlayerWeaponDamageModifier(PlayerId(), 1.0)
                end

                if Crosshair then 
                    Renderer.DrawCursor(GUI.screen.w / 2, GUI.screen.h / 2)
                end

                if Kill then 
                            Citizen.Wait(30)
                            local TargetPed = GetPlayerPed(v)
                            local TargetPos = GetEntityCoords(TargetPed)
                            local Exist = DoesEntityExist(TargetPed)
                            local Dead = IsPlayerDead(TargetPed)
                            local TargetCoords = GetPedBoneCoords(TargetPed, 31086, 0, 0, 0)
                            ClearPedTasksImmediately(GetPlayerPed(SelectedPlayer))
                            ShootSingleBulletBetweenCoords(TargetPos.x, TargetPos.y, TargetPos.z+3.0,TargetCoords.x,TargetCoords.y,TargetCoords.z, 9000, 0, GetHashKey("weapon_heavysniper_mk2"), PlayerPedId(SelectedPlayer), true, false, 9000.0)
                            ShootSingleBulletBetweenCoords(TargetPos.x, TargetPos.y+3.0, TargetPos.z,TargetCoords.x,TargetCoords.y,TargetCoords.z, 9000, 0, GetHashKey("weapon_heavysniper_mk2"), PlayerPedId(SelectedPlayer), true, false, 9000.0)
                        end


                        if Killallz then 
                            local function EnumerateEntities(initFunc, moveFunc, disposeFunc) return coroutine.wrap(function() local iter, id = initFunc() if not id or id == 0 then disposeFunc(iter) return end local enum = {handle = iter, destructor = disposeFunc} setmetatable(enum, entityEnumerator) local next = true repeat coroutine.yield(id) next, id = moveFunc(iter) until not next enum.destructor, enum.handle = nil, nil disposeFunc(iter) end) end
                            function EnumeratePeds() return EnumerateEntities(FindFirstPed, FindNextPed, EndFindPed) end
                            for ped in EnumeratePeds() do
                                if not IsPedAPlayer(ped) and ped ~= PlayerPedId() then
                                    Wait(1)
                                    SetEntityHealth(ped, 0)
                                    SetEntityCoords(ped, GetEntityCoords(PlayerPedId()))
                                end
                            end
                        end

                        if Zfarm then
                            local function EnumerateEntities(initFunc, moveFunc, disposeFunc) return coroutine.wrap(function() local iter, id = initFunc() if not id or id == 0 then disposeFunc(iter) return end local enum = {handle = iter, destructor = disposeFunc} setmetatable(enum, entityEnumerator) local next = true repeat coroutine.yield(id) next, id = moveFunc(iter) until not next enum.destructor, enum.handle = nil, nil disposeFunc(iter) end) end
                            function EnumeratePeds() return EnumerateEntities(FindFirstPed, FindNextPed, EndFindPed) end
                            for ped in EnumeratePeds() do
                                if not IsPedAPlayer(ped) and ped ~= PlayerPedId() then
                                    Wait(1)
                                    SetEntityHealth(ped, 100)
                                    SetEntityCoords(ped, GetOffsetFromEntityInWorldCoords(PlayerPedId(-1), 3.0, 3.0, 0.5))
                                    FreezeEntityPosition(ped, true)
                                    IsEntityAttachedToEntity(ped ,PlayerPedId(),GetEntityCoords(PlayerPedId(-1), 3.0, 3.0, 0.5))
                                
                            
                                end
                            end
                        end

                        if Zautokill then
                            local function EnumerateEntities(initFunc, moveFunc, disposeFunc) return coroutine.wrap(function() local iter, id = initFunc() if not id or id == 0 then disposeFunc(iter) return end local enum = {handle = iter, destructor = disposeFunc} setmetatable(enum, entityEnumerator) local next = true repeat coroutine.yield(id) next, id = moveFunc(iter) until not next enum.destructor, enum.handle = nil, nil disposeFunc(iter) end) end
                            function EnumeratePeds() return EnumerateEntities(FindFirstPed, FindNextPed, EndFindPed) end
                            for ped in EnumeratePeds() do
                                if not IsPedAPlayer(ped) and ped ~= PlayerPedId() then
                                    Wait(1)
                                    SetEntityHealth(ped, 100)
                                    SetEntityCoords(ped, GetOffsetFromEntityInWorldCoords(PlayerPedId(-1), 3.0, 3.0, 0.5))
                                    FreezeEntityPosition(ped, true)
                                    IsEntityAttachedToEntity(ped ,PlayerPedId(),GetEntityCoords(PlayerPedId(-1), 3.0, 3.0, 0.5))
                                    
                      local TargetPos = GetEntityCoords(ped)
                      local Exist = DoesEntityExist(ped)
                      local Dead = IsPlayerDead(ped)
                      local TargetCoords = GetPedBoneCoords(ped, 3... (เหลืออีก 14 KB)
