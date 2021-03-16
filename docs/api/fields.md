# Fields
Fields have to be in the ```laux/xenin_jobcreator/fields/``` folder. If it doesn't exist, just create a folder matching that path

To create a field it's heavily recommended you use [LAUX](https://gitlab.com/sleeppyy/laux) as fields are built using LAUX classes.
```laux
class MyField extends XeninJC.Field
    -- your field code
end

MyField.register("my_field", MyField)
```
As you're extending XeninJC.Field, you have access to all attributes & methods on XeninJC.Field. 

# Helpers
These are the methods & attributes that are meant as helpers methods.

## setJobTableValue
Used to set a custom variable on the job table
```laux
self:setJobTableValue(tbl: table, key: string, value: any)
```
**Arguments**
1. The job table you wish to set a value on
2. The key
3. The value

## getJobTableValue
Used to get a custom variable on the job table.
```laux
self:getJobTableValue(tbl: table, key: string): any
```
**Arguments**
1. The job table you wish to read from
2. The variable key
**Returns**
1. The value that matches that specific key. If it doesn't exist it'll be nil

## getValue
Used to get the fields value.
```laux
self:getValue(): any
```
**Returns**
1. The fields value

# Overwrites
These are the possible ones you might wanna overwrite. Not all of them are required, but the required ones are marked.

## manipulateJobTable
Allows modifying the raw DarkRP job table.
```laux
class Field extends XeninJC.Field
    manipulateJobTable(tbl)
        if (self:isEnabled()) then
            self:setJobTableValue(tbl, "my_custom_field", self:getValue())
        else
            self:setJobTableValue(tbl, "my_custom_field", nil)
        end
    end
end
```
## setValue
Overwrite this if you wish to enforce a specific data type
```laux
class Field extends XeninJC.Field
    setValue(value)
        self.value = tonumber(value)
    end
end
```

## isValid
**Required**

Used to indicate if a specific value is considered value.

**Must** return a Promise, as this supports async checks.
```laux
class Field extends XeninJC.Field
    isValid(value = self:getValue())
        local p = XeninUI.Promises.new()

        -- :resolve() is same as successful
        if (!self:isEnabled()) then return p:resolve() end
        
        -- Max we consider value here is 100, if over we :reject()
        if (value > 100) then return p:reject() end

        -- If we get past all checks we resolve
        return p:resolve()
    end
end
```
## getNetwork
**Required**

Used to instruct the addon how to write & read the networking
```laux
class Field extends XeninJC.Field
    getNetwork()
        return {
            write = () =>
                net.WriteInt(self:getValue(), 32)
            end,
            readAndSet = () =>
                self:setValue(net.ReadInt(32))
            end,
        }
    end
end
```
## isEnabled
**Required**

Used to tell the addon if the field is enabled in the config. You need a static and non-static method for this

How to add this option is explained later in **onConfigLoad**
```laux
static isEnabled()
    return tobool(XeninJC.Config:get("my_field_enabled"))
end
isEnabled()
    return tobool(XeninJC.Config:get("my_field_enabled"))
end
```
## onPlayerLoadout
An optional method. Useful if you want to set a players health/weapons/etc.
```laux
class Field extends XeninJC.Field
    onPlayerLoadout(ply, tbl)
        stopif !self:isEnabled()

        ply.myCustomField = self:getJobTableValue(tbl, "my_custom_field")
    end
end
```
## getCheckout
Used to inform the UI how to display the field at job checkout.
```laux
class Field extends XeninJC.Field
    getCheckout(job, field)
        return {
            id = () =>
                return "my_field"
            end,
            name = () =>
                return "My Field!"
            end,
            getPrice = () =>
                return XeninJC.Controller:formatCurrency(field:calculatePrice(), true)
            end
        }
    end
end
```
## getPreviewUI
Used to describe how the field should be displayed in the preview UI (non-editing UI, i.e "My Jobs" preview tab)
```laux
class Field extends XeninJC.Field
    getPreviewUI(job)
        return {
            title = "My Field",
            value = string.Comma(self:getValue()),
            valueColor = Color(255, 127, 0)
        }
    end
end
```
## getUI
Used to describe the UI that should be used in the job creation/editing UI.

**expand on this**
```laux
class Field extends XeninJC.Field

end
```
## calculatePrice
Used to calculate the price of the field. 

**Must not return a negative number**
```laux
class Field extends XeninJC.Field
    calculatePrice(value = self:getValue())
        if (!self:isEnabled()) then return 0 end
        if (!value or value == 0) then return 0 end

        local price = tonumber(XeninJC.Config:get("my_field_price_increment"))

        return value * price
    end
end
```
## onConfigLoad
A static method used to inject config values into the config system for the addon.

This shows a quick example of how to do it taken from the default health field. A full guide with everything explained can be found in the [Config section](api/config.md)
```laux
class Field extends XeninJC.Field
    static onConfigLoad(config)
        config:addSetting("job_health_enabled", "Fields", "Health", "Purchase Health", "Can you purchase extra health?", false, "Checkbox")
        config:addSetting("job_health_max", "Fields", "Health", "Maximum health", "Description", 500, "SliderPad", {
            textWidth = 54,
            min = 100,
            max = 1000,
        })
    end
end
```