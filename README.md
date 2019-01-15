### **For support, development, shenanigans: check out the [Discord](https://discord.gg/skUAWKg).**

# Description
This is a small script which uses adb to send touch and key events to your phone, in combination with Calcy IV it can automatically rename all of your pokemon. This script doesn't login to the pokemon go servers using the "unofficial API" and only relies on an Android phone (sorry, iPhone users). The upside to this is that you're very unlikely to get banned for using it. The downside is that it's a lot slower, and that you can't use your phone while it's running.

## Warnings
This script essentially blindly sends touch events to your phone. If a popup appears over where the script thinks a button is, or if your phone lags, it can do unintended things. Please keep an eye on your phone while it is running. If it transfers your shiny 100% dragonite, it's because you weren't watching it.

# Usage
- Download the files from this repository
- Install adb, make sure it's on your systems PATH, alternatively you can place adb in the same folder as main.py
- Install [clipper](https://github.com/majido/clipper) and start the service
- Install Python >=3.7 (older versions will not work)
- Run pip install -r requirements.txt
- Change your Calcy IV renaming scheme to `$IV%Range$$MoveTypes$$AttIV$$DefIV$$HpIV$$Appraised$` or if you're used to regular expressions, change your `iv_regexes` setting to match your renaming scheme.
    - Alternatively, if you want to keep your renaming string without too much fuss, check [question 5](#user-content-now-a-decent-faq) in the FAQ.
- Edit config.yaml locations for your phone (The defaults are for a oneplus 3T and should work with any 1080p phone that does not have soft buttons). Each setting is an X,Y location. You can turn on Settings > Developer options > Pointer location to assist you in gathering X,Y locations. Each location setting has a corresponding screenshot in docs/locations.
- Once you've done all that, run `python ivcheck.py`

## Actions and rules
Actions allow you to define new ways of renaming your pokemon, outside of the usual Calcy IV renaming scheme. Actions are processed from first to last, and the first one to have all its conditions pass is used.

**Conditions:**
- name - The Pokemons name
- iv - The exact IV (note: this will only be set if Calcy IV has discovered an exact IV
- iv_min - The minimum possible IV (This will be set even if Calcy IV pulls an exact IV)
- iv_max - The maximum possible IV (This will be set even if Calcy IV pulls an exact IV)
- success - Whether the calcy IV scan succeeded (true/false) (Note: Will be false if pokemon is blacklisted)
- blacklist - Whether the pokemon is in the blacklist
- appraised - Whether the pokemon has been appraised or not (true/false)
- id - The pokemons pokedex ID
- cp - The pokemons CP
- max_hp - The pokemons max hp
- dust_cost - The dust cost to power up
- level - The pokemons level (1-40)
- fast_move - The pokemons fast move (usually only visible on fully evolved pokemon)
- special_move - The pokemons special/charged move (usually only visible on fully evolved pokemon)
- gender - The pokemons gender (1 = male, 2 = female)

_Conditions also support the following operators:_
- lt - Less than
- le - Less than or equal to
- eq - Equal to
- ne - Not equal to
- ge - Greater than or equal to
- gt - Greater than
- in - In list
- not_in - Not in list

**Actions:**
- rename - Allows you to specify your own name for the pokemon. You can also use any of the above conditions as variables. For example `{name} {iv}`. In addition, there is also a {calcy} variable, which contains Calcys suggested name.
- favorite - Favorite the pokemon
- appraise - Appraise the pokemon

### Actions examples
Faster rename run by skipping rename on Pokemon with <90% IVs. Rename any pokemon that failed to scan as ".FAILED" so you know which ones failed to scan, and which ones are skipped as trash.

```
actions:
  - conditions:
      success: false
    actions:
      rename: ".FAILED"
  - conditions:
      iv_max__ge: 90
    actions:
      rename: "{calcy}"
```

Rename bad IV Abra, Gastly and Machop to ".TRADE" so you can trade them later.
```
    - conditions:
        name__in:
          - Abra
          - Gastly
          - Machop
        iv_max__lt: 90
      actions:
        rename: ".TRADE"
```

# _(now, a decent)_ FAQ
1. It taps in the wrong locations / doesn't work / automatically called my mother:

    You probably need to edit the `locations:` in config.yaml, the defaults are for a 1080p phone. **You can find where the spots are supposed to be in [docs/locations](docs/locations)!**

    To find out the coordinates, enable *Pointer Location* in your phone's *Developer Settings*. If you're lazy like me, just type the code below with your phone connected:

    - To enable:
                adb shell content insert --uri content://settings/system --bind name:s:pointer_location --bind value:i:1
                    If that doesn't work, use this:
                adb shell settings put system pointer_location 1

    - To disable

        adb shell content insert --uri content://settings/system --bind name:s:pointer_location --bind value:i:0
            If that doesn't work, use this:
        adb shell settings put system pointer_location 0

2. It's not pasting the pokémon's name

    Unfortunately, the paste key event doesn't work on older versions of Android. Use the `--nopaste` argument to paste it by tapping (make sure you edit the `locations:` accordingly).

3. It's going too fast for my phone! :O

    This is being developed and tested on a OnePlus 3T and a Google Pixel, so the script runs quite fast _(until the phone gets hot, that is)_. You can slow it down by increasing the `waits:` in config.yaml.

4. Can it do multiple phones at the same time

    Sure, you just have to run multiple instances. Run `adb devices` to get the device ids for your phones, then run multiple instances of the script with --device_id=XXXXX

5. _I don't even know what a regular expression is!_ How can I keep my Calcy string *and* use the script, without needing to ask for help on the [Discord](https://discord.gg/skUAWKg)?

    **TL;DR: there's a GIF below, run the command from step 4 and follow the image.**

    There's a neat trick in which you add a lot of spaces to the end of Calcy's string followed by `IV%Range$`. This make it so whenever you paste the pokémon's name in the game, you don't see anything after the spacesbecause of 12-char limitation. If you want to try it out, do as follow:

    1. Connect your phone to your computer (check with `adb devices`)

    2. Make sure `clipper` service is running on your phone (check with `adb shell am broadcast -a clipper.get`)

    3. Open CalcyIV, go to the *Renaming* section and click at the end of your string.

    4. Run the following commands (if the latter doesn't work, just paste manually):
            adb shell am broadcast -a clipper.set -e text $'\u2003\u2003\u2003\u2003\u2003'
            adb shell input keyevent KEYCODE_PASTE

    6. Add *IV% RANGE* after the spaces. Repeat the process for the *Not fully evolved:* section as well.

    7. Change your `iv_regexes:` to the following:
            iv_regexes:
                - ^.+  +(?P<iv>\d+)$
                - ^.+  +(?P<iv_min>\d+)\-(?P<iv_max>\d+)$

    8. Done! Oh no, wait, there's a GIF as well! :)
    ![](docs/tutorial_spaces.gif?raw=true)