
local Bypasses = {
    ["ass"] = "as{{aieixzvzx:s}}",
    ["asshole"] = "as{{aieixzvzx:shole}}",
    ["bitch"] = "bit{{aieixzvzx:ch}}",
    ["boobs"] = "boo{{aieixzvzx:bs}}",
    ["blowjob"] = "blowj{{aieixzvzx:ob}}",
    ["butt"] = "bu{{aieixzvzx:tt}}",
    ["butthole"] = "but{{aieixzvzx:thole}}",
    ["cock"] = "co{{aieixzvzx:ck}}",
    ["cunt"] = "cu{{aieixzvzx:nt}}",
    ["cum"] = "cu{{aieixzvzx:m}}",
    ["dick"] = "di{{zczxczvz:ck}}",
    ["dyke"] = "dy{{aieixzvzx:ke}}",
    ["faggot"] = "fa{{aieixzvzx:ggot}}",
    ["fuck"] = "fu{{aieixzvzx:ck}}",
    ["gaylord"] = "gayl{{aieixzvzx:ord}}",
    ["hentai"] = "hen{{aieixzvzx:tai}}",
    ["kike"] = "ki{{aieixzvzx:ke}}",
    ["lmao"] = "lma{{aieixzvzx:o}}",
    ["motherfucker"] = "motherf{{aieixzvzx:ucker}}",
    ["nazism"] = "naz{{aieixzvzx:ism}}",
    ["nazist"] = "naz{{aieixzvzx:ist}}",
    ["nigga"] = "ni{{aieixzvzx:gga}}",
    ["nigger"] = "ni{{aieixzvzx:gger}}",
    ["niggers"] = "ni{{aieixzvzx:ggers}}",
    ["piss"] = "p{{aieixzvzx:iss}}",
    ["penis"] = "pe{{aieixzvzx:nis}}",
    ["pedofile"] = "ped{{aieixzvzx:ofile}}",
    ["pussy"] = "pu{{aieixzvzx:ssy}}",
    ["rape"] = "ra{{aieixzvzx:pe}}",
    ["raping"] = "ra{{aieixzvzx:ping}}",
    ["shit"] = "sh{{aieixzvzx:it}}",
    ["slut"] = "sl{{aieixzvzx:ut}}",
    ["stfu"] = "st{{aieixzvzx:fu}}",
    ["squirt"] = "squi{{aieixzvzx:rt}}",
    ["sex"] = "se{{aieixzvzx:x}}",
    ["tits"] = "ti{{aieixzvzx:ts}}",
    ["terrorist"] = "terror{{aieixzvzx:ist}}",
    ["whore"] = "who{{aieixzvzx:re}}",
    ["discord"] = "disco{{aieixzvzx:rd}}",
    ["kys"] = "k{{aieixzvzx:ys}}",
    ["kill"] = "ki{{aieixzvzx:ll}}"
}

local ReplicatedStorage = game:GetService("ReplicatedStorage")
local Remote = ReplicatedStorage:FindFirstChild("SayMessageRequest", true)

local ChatBypass; ChatBypass = hookmetamethod(Remote, "__namecall", function(self, ...)
    local Method = getnamecallmethod()
    local Arguments = {...}
    
    if self == Remote and Method == "FireServer" then
        local Message = Arguments[1]
        local Split = Message:split(" ")
        local FinalMessage = ""

        for _, x in next, Split do
            for _, Bypass in next, Bypasses do
                if x:lower() == _ then
                    if x:upper() ~= x then
                        Message = Message:gsub(x, Bypass)
                        FinalMessage = Message .. " ng"
                    else
                        Message = Message:gsub(x, Bypass):upper()
                        FinalMessage = Message:gsub(x, Bypass):upper() .. " ng"
                    end
                end
            end
        end
        
        if FinalMessage ~= "" then
            Arguments[1] = FinalMessage
        end
        
        return ChatBypass(self, unpack(Arguments))
    end
    
    return ChatBypass(self, ...)
end)
