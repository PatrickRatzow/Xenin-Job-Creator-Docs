# Jobs
To manipulate a job you have to interact with a XeninJC.JobBuilder

XeninJC.JobBuilder utilises the [Builder Pattern](https://en.wikipedia.org/wiki/Builder_pattern), which means all operations returns the object, allowing method chaining as seen in the example below.
```laux
XeninJC.API:createJob()
    :setName("My Job Name")
    :setSalary(45)
    :setColor(Color(255, 127, 0))
    :build(function(err, job) end) -- Build is a finishing operation
```
# Methods
All the methods that can be called on the XeninJC.API namespace that directly has to do with job management.
## createJob
```laux
XeninJC.API:createJob(): XeninJC.JobBuilder
```
## updateJob
```laux
XeninJC.API:updateJob(existingJob: number|XeninJC.Job): XeninJC.JobBuilder
```
**Arguments**
1. If number it must be a job id, otherwise supply the actual job object.

## deleteJob
```laux
XeninJC.API:deleteJob(existingJob: number|XeninJC.Job): Promise<boolean>
```
**Arguments**
1. If number it must be a job id, otherwise supply the actual job object.

# XeninJC.JobBuilder
All write operations to build the object is available here.

## setName
**Required.**
Used to set the name of the job.
```laux
:setName(name: string)
```
**Arguments**
1. What name the job should have

## setSalary
**Required.**
Used to set the salary of the job
```laux
:setSalary(salary: number)
```
**Arguments**
1. How much the salary should be set to

## setColor
**Required.**
Used to set the name of the job. 

If the input is a string, it must be a 3/6 digit hexadecimal with a # prefixed.
```laux
:setColor(color: Color|string)
```
**Arguments**
1. What colour the job should have

## setField
Sets a fields value. It does not check any types, or if the field even exists.
```laux
:setField(key: string, value: any)
```
**Arguments**
1. The id of the field
2. The value you wish to set it to

## setPrimaryOwner
Used to set the primary owner. The primary owner has extra privilieges, and are capable of fully editing the job + deleting it.
```laux
:setPrimaryOwner(sid64: string)
``` 
**Arguments**
1. The SteamID64 of the player that should be the primary owner.

## addWeapon
Used to add a single weapon to the job.
```laux
:addWeapon(weapon: string)
```
## addModel
Used to add a single local model
```laux
:addModel(path: string)
```
## addWorkshopModel
Used to add a workshop model.

Path **must** be in the workshop addon, or it'll cause an error when building.
```laux
:addWorkshopModel({
    path = "model/path", -- model path
    workshop = "123456789", -- id
    bodygroups = {
        [1] = 1, -- bodygroup id = bodygroup value
        [2] = 0
    }
})
```
## addSecondaryOwner
Used to add an owner to the job. Must be a SteamID64
```laux
:addOwner(sid64: string)
```
## finish
Finishes the action currently in the works.
```laux
:finish([ callback: function(err: string, job: XeninJC.Job) ])
```
**Arguments**
1. A callback for when the action has been finished. If err is nil, it means the action went through.

# Example
A full example of :createJob() + XeninJC.JobBuilder usage.
```laux
XeninJC.API:createJob()
    :setName("My Job")
    :setSalary(45)
    :setColor("#ffffff")
    :setField("health", 150)
    :setField("armor", 25)
    :setPrimaryOwner("76561198202328247")
    :addSecondaryOwner("76561198058042338")
    :addModel("player/alyx.mdl")
    :addModel("player/bean.mdl")
    :addWorkshopModel({
        path = "player/dewobedil/maid_dragon/lucoa/default_p.mdl",
        workshop = "974221698",
        bodygroups = {
            [1] = 3,
            [2] = 1,
            [4] = 1
        }
    })
    :finish(function(err, job)
        if (err) then return end

        -- Do something
    end)
```