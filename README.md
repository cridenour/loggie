![Loggie Logo](addons/loggie/assets/logo.png)

Loggie is a basic logging utility for Godot 4.0+ for those who could use a couple of improvements and more control over how console and logfile output is styled and handled. 

It makes it a breeze to compose and print messages with all the extra data you need to have helpful logs.

Loggie takes care that your logs always look clean in release builds, while allowing you to use extra styling for console targeted output. ANSI-compatible, and friendly both for solo developers and developers in a team (externally loaded settings for each developer).

If you need something simple but effective, Loggie is your guy.

### [📚 User Guide](docs/USER_GUIDE.md)

### [💬 Loggie Discord - Support & Development](https://discord.gg/XPdxpMqmcs)

# Installation
*(Loggie is not yet available on the Godot AssetLib.)*
*(Loggie was developed for Godot 4.0+, therefore it may not work on older versions of Godot.)*

1. Clone or download this repository as a .zip.

2. Copy the `addons/loggie` folder and place it in your `res://addons/` directory in your Godot project (if you don't have that folder, create it first).

3. (Optional): Adjust the name of the Loggie singleton to something else if you don't want to use the default "Loggie" name. Read here how to do it: [📚 User Guide](docs/USER_GUIDE.md#using-a-custom-singleton-name). This is best done before first enabling the plugin.

4. In Godot, go to Project -> Project Settings -> Plugins, and enable Loggie:
![LoggieProjSettings](https://i.imgur.com/suO2Itm.png)

5. You're good to go. Have a peek at the [📚 User Guide](docs/USER_GUIDE.md) for more details.

# Features

### All Basic Settings in Project Settings
Loggie creates new Project Settings in your Godot when it's used, allowing you to modify your Loggie preferences from the comfort of the Project Settings GUI.

![gif](https://i.imgur.com/Nus0cpK.gif)

## Easy Message Composition and Customization

##### Step 1
Start composing a message with Loggie.msg(...):
```gdscript
Loggie.msg("Hello")
```
##### Step 2
Chain any other customizations you want onto it.
```gdscript
Loggie.msg("Hello").bold().color(Color.CYAN)
```
There is a variety of styling functions you can use, such as `bold()`, `italic()`, `color(color)`, `nl()`, `header()`, `box()`, etc.

##### Step 3
Call one of the output functions (`info`, `notice`, `warn`, `error`, `debug`) at the end of the chain to output the composed message at that debug level.

```gdscript
Loggie.msg("Hello").bold().color(Color.CYAN).info()
```

## BBCode/ANSI Terminal Compatibility
Loggie was made with different consoles in mind. As such, it can be configured so that your logs (and their stylings, including custom colors) appear properly in any terminal with ANSI support.

This is great for users who prefer to develop Godot projects with VSCode or some other external editor which displays logs in a non-godot console.

![Compatibility](screenshots/screenshot_1.png)

## Automatically makes clean plaintext logs in Release builds
Loggie can create some fancy looking output, but you don't want to open a .log file from an user who ran your project on release and realize your .log files are filled with BBCode or ANSI sequences, which were helpful during development... but now are simply creating a mess.

Loggie automatically switches to producing clean plaintext logs when it detects that your project is running in Release mode.

## Device Specs Output
The logger can be configured to log the specs of the device running your project at launch, giving you a neat overview of all the details you may be interested in for debugging purposes.

![SpecsLog](https://i.imgur.com/ZshsF9J.png "SpecsLog")

## Team Environment Support
Using Loggie as a solo developer is a smooth experience, but when working with teams, different teammates may desire to configure their logger (at least during local development) to use different features or styles of output.

To avoid pushing such changes to the Loggie plugin files directly, and to your repository, loggie allows you to boot a custom local settings file.

By gitignoring and using that file, each team member can use their own settings.

## Toggleable Message Domains (Channels)
Messages can be configured to belong to a domain, and domains can be easily enabled or disabled. Messages coming from a disabled domain won't be processed or output.
This makes it simple to create functions that can output verbose and advanced logs related to their behavior only when the domain is enabled by the developer.

For example, you may want to print out every detail about how your Loot generator rolls chances for items: which number it rolled, was it a success or not, etc. - but you only want to see these diagnostics when you specifically enable them in that function:

```gdscript
func generate_loot_for(recipient : Creature):
  var diagnostics_enabled = true
  Loggie.set_domain_enabled("LootDiag", diagnostics_enabled)

  Loggie.msg("Generating loot for %s" % recipient.name).domain("LootDiag").info()
  Loggie.msg("Rolling for rare items...").domain("LootDiag")..info()
```

## Class Name Extraction
A neat feature pulled I from [LogDuck](https://github.com/ZeeWeasel/LogDuck "LogDuck") *(also a cool logging library worth checking out)*, which allows you to see the names of the classes that prompted Loggie to output something.* This only works when the engine debugger is connected, therefore it does not work in Release mode, and won't be shown in those logs.*

![ClassNameExtraction](https://i.imgur.com/EWlcKnD.png)

## Dictionary Pretty-print
Loggie makes an extra step to pretty-print dictionaries, outputting them in a json-like format with newlines and tabs, instead of having them smushed into a single line, which makes reading printed dictionaries easier when dealing with larger ones.

![DictPrettyPrint](https://i.imgur.com/H3VAM1g.png)

## Detailed In-Engine Documentation
Loggie's classes, variables and methods are all well documented and browsable directly in your Godot engine.
Head to the 'Search Help' window in Godot and search for Loggie to check it out.

If you need help with anything, feel free to reach out on the [Loggie discord server](https://discord.gg/XPdxpMqmcs).

![LoggieDocs](https://i.imgur.com/7PIWXam.png)

# About the project

It was developed for private use on a small project, but I decided to open-source it as I think it can be a very useful tool for anyone with basic logging needs with some extra focus on style.

I find tremendous reading comprehension value in adequately stylized and subdivided log messages, however, others on the team may have different preferences. Therefore, the main problems I aimed at with Loggie were:

1. Intuitive and easy flow for composing stylized messages.
2. Preferences for Settings that can easily be configured by each developer on the team locally without modifying the plugin itself.
3. Regardless of which styling is used during local development, when switched into "Production/Release" mode (ideally by automatically detecting that), the logger should create clean plaintext output in the actual .log files.

For anyone else who finds those things on the forefront of what they want their logger to achieve, Loggie is a great starting point.

I'm looking to improve Loggie over time with more features, flexibility, stylings and so on. If you would like to Contribute, please read the Contributing section.

# Contributing
All valid improvements and feature contributions are welcome.

Feel free to open a PR directly, or if you wish to preemtively discuss your changes or ideas before working on them - talk to me on the [Loggie discord server](https://discord.gg/XPdxpMqmcs).
