# bt-target
 
Dependencies: https://github.com/mkafrin/PolyZone

## Updated functionality
My fork of bt-target includes the following options:
* Pass all data through to the target event in the data table 
* Add vehicle bone support
* Disable the ability to aima/attack while in interactive mode
* Check overall job grade to access the menu 
* Check individual option job grades 


```lua
Citizen.CreateThread(function()
    local coffee = {
        690372739,
    }
    AddTargetModel(coffee, {
        options = {
            {
                event = "coffeeevent",
                icon = "fas fa-coffee",
                label = "Coffee",
                item = "coffee",
                price = 5,
                grade = 1,  --This defines the minimum grade of the jobs defined below to access this option
                anything_else = "You can pass any data through this table",
                mytable = { name = 'mytable', description = 'including another table'},
            },
        },
        job = {["all"] = grade { grade = 0}} -- Allow you to define overall grade requirements to access any option within this interaction
        distance = 2.5
    })
end)

RegisterNetEvent('coffeeevent')
AddEventHandler('coffeeevent',function(data)
    print("You purchased a " .. data.item .. " for $" .. data.price .. ". Enjoy!")
end)
```

Icons: https://fontawesome.com/

Here a simple target tracking script that tracks where your player is looking at. Coords and models can be used. You can add multiple payphone models for example and when your player looks at it. It activates the UI to trigger an event. Polyzones can be used also. Its uses 0.00 ms (0.16% CPU Time) when idle. This can be used in multiple scripts to help with optimisation. Press ALT to activate. Using RegisterKeyMapping removes the need of checking if key has been pressed in a thread and players can customise the keybind in the ESCAPE menu. You can also create multiple options per target. Read the example to learn how to use it.

Example: 

```lua
Citizen.CreateThread(function()
    local peds = {
        `a_f_m_bevhills_02`,
    }
    AddTargetModel(peds, {
        options = {
            {
                event = "Random 1event",
                icon = "fas fa-dumpster",
                label = "Random 1",
            },
            {
                event = "Random 2event",
                icon = "fas fa-dumpster",
                label = "Random 2",
                grade = 1,
            },
            {
                event = "Random 3event",
                icon = "fas fa-dumpster",
                label = "Random 3",
                grade = 2,
            },
            {
                event = "Random 4event",
                icon = "fas fa-dumpster",
                label = "Random 4",
                grade = 3,
            },
        },
        job = {["garbage"] = {grade = 0}}
        distance = 2.5
    })

    local coffee = {
        690372739,
    }
    AddTargetModel(coffee, {
        options = {
            {
                event = "coffeeevent",
                icon = "fas fa-coffee",
                label = "Coffee",
            },
        },
        job = {["all"] = {grade = 0}}
        distance = 2.5
    })
    
    AddBoxZone("PoliceDuty", vector3(441.79, -982.07, 30.69), 0.4, 0.6, {
	name="PoliceDuty",
	heading=91,
	debugPoly=false,
	minZ=30.79,
	maxZ=30.99
    }, {
        options = {
            {
                event = "signon",
                icon = "far fa-clipboard",
                label = "Sign On",
            },
            {
                event = "signoff",
                icon = "far fa-clipboard",
                label = "Sign Off",
            },
        },
        job = {["police"] = {grade = 0}, ["ambulance"] = { grade = 0}, ["mechanic"] = {grade =0 }},
        distance = 1.5
    })
end)
```
