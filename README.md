local UI = game:GetService("Players").LocalPlayer.PlayerGui.MainGui.PaintFrame.GridHolder.Grid


local function press(a)
    game:GetService("VirtualInputManager"):SendKeyEvent(true, tostring(a), false, game)
end
print("Executed")
local ChatEvent = game:GetService"ReplicatedStorage".DefaultChatSystemChatEvents.SayMessageRequest
print("Locals Loaded")
getgenv().MessageStatus = false;
getgenv().Message = "thanks:)"
local debounce = false;
print("Globals Loaded")

print("Executed")

game.Players.LocalPlayer.leaderstats.Sold.Changed:Connect(function()
    if getgenv().MessageStatus == true then
        if not debounce then
            debounce = true
            wait(1)
            print("Try Chat")
            ChatEvent:FireServer(getgenv().Message,"All")
            wait(0.5)
            debounce = false
        end
    end
end)

for i,v in pairs(getconnections(game:GetService("Players").LocalPlayer.Idled)) do
    v:Disable()
end

getgenv().Library = loadstring(game:HttpGet("https://raw.githubusercontent.com/RTrade/Voidz/main/API/Networks/swordhook-network.lua"))() --you can go into the github link and copy all of it and modify it for yourself.
getgenv().Window = getgenv().Library:CreateWindow('Starving artist', Vector2.new(550, 627), Enum.KeyCode.LeftShift) 

local Test = Window:CreateTab("main")
local Test2 = Test:CreateSector("main","left")
Test2:AddToggle("auto thanks",false,function(state)
getgenv().MessageStatus = state
    print(state)
end)
Test2:AddTextbox("http link",false,function(testing)
test = testing
end)

Test2:AddTextbox("message ",false,function(hi)
getgenv().Message = hi
end)
Test2:AddButton("beta https draw",function()
local image = test -- image you want to import
      		local resolutionX = 32 -- usually it's 32 but it might change depending on the frame?
      		local resolutionY = 32 -- usually it's 32 but it might change depending on the frame?

-- epic coding stuf --

local grid = nil
local s, e = pcall(function()
    if game.Players.LocalPlayer.PlayerGui:FindFirstChild'MainGui':FindFirstChild'PaintFrame':FindFirstChild'Grid' then
        grid = game.Players.LocalPlayer.PlayerGui.MainGui.PaintFrame.Grid
    elseif game.Players.LocalPlayer.PlayerGui:FindFirstChild'PaintFrame':FindFirstChild'GridHolder':FindFirstChild'Grid' then
        grid = game.Players.LocalPlayer.PlayerGui.MainGui.PaintFrame.GridHolder.Grid
    else
        warn('cannot execute script')
        return
    end
end)
if e then
    local s1, e1 = pcall(function()
        grid = game.Players.LocalPlayer.PlayerGui.MainGui.PaintFrame.GridHolder.Grid
    end)
    if e1 then
        warn('cannot execute script')
        return
    end
end
local h = game:GetService("HttpService")

function getjson(url)
    local begin = game:HttpGet("https://aut.matthew-gamerga.repl.co/get?url="..url)
    if (begin == 'the file size is too big!') then
        return 'fstb'
    else
        local json = h:JSONDecode(begin)
        return json
    end
end

function import(url)
  local pixels = getjson(url)
  local cells = {}
  local index = 1
    if (pixels == 'fstb') then
        game.StarterGui:SetCore(
            "SendNotification",
            {
                Title = "error",
                Text = "the file size exceeds three megabytes, "
                .."to prevent people from crashing my vps replit i have set"
                .." the cap to amount. sorry for the inconvenience"
            }
        )
    else
        grid['1'].BackgroundColor3 = Color3.fromRGB(
            pixels[1][1],
            pixels[1][2],
            pixels[1][3]
        )
        for y = 1, resolutionX, 1 do
            for x = 1, resolutionY, 1 do
                pcall(function()
                    local pixel = pixels[index]
                    index = index + 1 -- index += 1 doesn't work wtf
                    local r = pixels[index][1]
                    local g = pixels[index][2]
                    local b = pixels[index][3]
                    grid[tostring(index)].BackgroundColor3 = Color3.fromRGB(r, g, b)
                    table.insert(cells, pixel)
                end)
            end
        end
        pcall(function()
            local pixel = pixels[index]
            index = index + 1 -- index += 1 doesn't work wtf
            local r = pixels[index][1]
            local g = pixels[index][2]
            local b = pixels[index][3]
            grid[tostring(index)].BackgroundColor3 = Color3.fromRGB(r, g, b)
            table.insert(cells, pixel)
        end)
        game.StarterGui:SetCore(
            "SendNotification",
            {
                Title = "done",
                Text = "finished importing, check the drawing grid timer 300 sec is 5mins"
            }
        )
    end
end

import(image)
wait(1)
local countdownLabel = game:GetService("Players").LocalPlayer.PlayerGui.MainGui.PaintFrame.NextButton.Label

local countdownTime = 300

while countdownTime > 0 do
    countdownLabel.Text = tostring(countdownTime)
    wait(1)
    countdownTime = countdownTime - 1
end

countdownLabel.Text = "NEXT"
  	end)



Test2:AddButton("copy discord friend server",function()
setclipboard("https://discord.gg/7bdykXT4ew")
end)
Test2:AddButton("copy discord main",function()
setclipboard("https://discord.gg/sDJyW37VYv")
end)
Test2:AddSlider("beg time", 0,0,300,1,function(v)
timer = v
end)

Test2:AddTextbox("beg message",false,function(ve)
begmessage = ve
end)


Test2:AddToggle("auto beg",false,function(state)
getgenv().beg = state
while getgenv().beg do 
game:GetService("ReplicatedStorage"):WaitForChild("DefaultChatSystemChatEvents"):WaitForChild("SayMessageRequest"):FireServer(begmessage,"All")
wait(timer)
end
end)
