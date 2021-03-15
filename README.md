# What is this?
Xenin Custom Jobs completely automates custom jobs for DarkRP. Players can easily create and preview their jobs within the limits set by the server administrator, all in real time.

As soon as a player has created their job, they will instantly have access to the job, no waiting around days for the owner to add it! And if that's undesirable due to a server theme, there's an option to have all jobs go into an approval queue for inspection. Admins online will then be notified, and if enabled a message will be posted to a Discord webhook.

# Features
There's a huge amount of features as this addon isn't your standard run-of-the-mill addon; it's an addon with incredibly depth and detail. This is most, but not all features.

- Automatic and instant job creation, synchronised for all players on the spot.
- Full in-game config, with everything visualised and explained.
- Automatic addon updates + opt-in beta versions.
- Built for MySQL, supports SQLite.
- Custom currency system by default, allowing users to donate money to gain it! Or use any other currency instead! The system can be linked to any currency system.
- Includes all the basic DarkRP job options, and allows you to customise the costs for all of it.
    - Name
        - Length min + max restrictions.
        - Word filter
    - Colour
    - Salary
    - Health
    - Armor
    - Gun License
    - Description
- Expandable field API, allowing anyone to create new options for a job with relative ease.
- Weapons list to choose from, by default includes FA:S 2 and M9K.
- Models list to choose from, by default includes all HL2 models.
- Allows multiple models if configurated so, and has different UI for 1 model or multiple models.
- Supports workshop models
    - Only downloads whats needed! It will not download workshop models for offline players, only downloading the models when the user comes onto the server.
    - Supports bodygroups, allowing the player to choose any combination.
    - Automatically detects player models in addons
    - Uses workshop addon size for price, and has an option to cap max workshop addon at a specific size, i.e 5 MB.
    - Has an option to limit 1 workshop addon to 1 job.
    - Has an option to not allow workshop addons uploaded by the same person that's creating a job.
    - Has automatic model size & hitbox restrictions
    - Protection against updating the workshop addon after the job has been creating, immediately disabling the job and putting it into an approval queue if too much has changed. Admins are notified of it too.
- Supports multiple owners for one job as an option, multiplying the entire jobs cost based off the amount of owners.
- Smooth UI with emphasis on the user experience; never overwhelming users with too much information at once.
- Can update a job post creation, allowing users to change at any time.
- Admins can disable a job, putting it back into an approval queue.
- Job Importer that can import Lua jobs into the system, allowing you to port your old custom jobs with relative ease!
- Well documented developer API, allowing developers to easily interact with the addon.

# DRM
This addon uses a custom DRM built specifically for it. This enables auto updating, meaning you will never have to update the addon yourself!

If you wish to get a DRM free version of the script, you can open a ticket, but be aware that DRM free versions are not given out lightly to anyone. Be prepared to extensively reason why you need a DRM free version.

