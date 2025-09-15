---
tags:
  - script
  - macro
resource_link: "https://www.redguides.com/community/resources/tradeskill-recipes-max-out-artisans-prize.1281/"
support_link: "https://www.redguides.com/community/threads/tradeskill-recipes-max-out-artisans-prize.70361/"
authors: "jande"
tagline: "Learn all recipes needed to evolve Artisan’s Prize augment."
---

# Artisan's Prize

<!--desc-start-->
Artisan's Prize is a macro that helps you learn all the recipes needed to evolve Artisan's Prize augment.
<!--desc-end-->
## Getting Started

### Installing
Preferably download through redfetch or download and unzip into the macro folder. If you used the MQ2->MQ migrator remove the config/ts folder for now.

### Setup
!!! note "Read the Tradeskill Books"  
    Before you start doing anything read these [Tradeskill Books](https://www.redguides.com/community/threads/anyone-have-a-way-to-automate-tradeskilling-301-350.68984/#post-386591).  
    !!! warning "Scribe all the books mentioned"
    !!! tip "Yes, it's irritating to visit all the zones/vendors, such is tradeskills."
    !!! danger "Every main inventory slot needs a bag."

---

## Settings

These are the settings you can configure in the `ts/tradesman.ini` file.

???+ example "tradesman.ini"
    ```ini
    [setting]
    debug=0
    subcombine=5
    bagopen=0
    staycontainer=0
    shopping=1
    useStaticLoc=1
    move2container=1
    MoveSuccess=10
    mayDestroy=5
    waitDestroy=5
    delayMissing=0
    recipeFarm=30
    endBeep=1
    tsTrophy=2
    nodestroy=conflagrant muhbis faded velious velium velious faded restea cloudberry
    beep=0
    ```

**beep** `0 (default) | 1`
: Turn use of beep on or off.

**shopping** `0 (default) | 1`
: Generate a shopping list, use with ts/finditem.

**subcombine** `5 (default) | number`
: When an ingredient is missing should a subcombine be attempted, if subcombine is missing an ingredient should it be attempted, until the level set is reached.

**staycontainer** `0 (default) | 1`
: During subcombines should recipes in different container be considered.

**debug** `0 (default) | number`
: Mess with this setting if you can read the macro code.

**movesuccess** `10 (default) | bag number/0 (disable)`
: Items to bag.

**mayDestroy** `5 (default) | platinum/0 (disable)`
: Destroy items under this limit.

**waitDestroy** `30 (default) | seconds/0 (disable)`
: Wait before destroying (0 to disable).

**nodestroy** `conflagrant muhbis faded velious (default) | words`
: Search itemname for these keywords, dont destroy them.

**delayMissing** `0 (default) | seconds/0 (disable)`
: Wait if a detecting recipe needs a farmed item.

**recipeFarm** `30 (default) | number/0 (do not stop)`
: Stop after detecting number of recipes needs ingredients.

**endBeep** `0 (default) | 1`
: Alert when macro ends.

**tsBags** `extraplanar trade satchel (default) | bagnames`
: Cleanup will check the following bags.
    ```ini
    tsBags=|extraplanar trade satchel|
    ```

**tsTrophy** `2 (default) | 0=unload/1=load/2=ignore/X=seconds`
: Wait seconds after automatically opening a new tradeskill container for trophy switch.

**SharedBank** `0 (default) | 1`
: Pull items from shared bank.

## Blocking recipes

Add it to the `[block]` section of the `ts/tradesman-block.ini` file.  

!!! example "tradesman-block.ini"
    ```ini
    [block]
    ;never ever attempt making this so set it to BLOCK
    2235131=BLOCK
    2235130=BLOCK
    ; list of recipes attempted/result
    ; tracking what was done/busy with
    [skill_character]
    20911=gofarm
    20913=gofarm
    20912=learn
    ```

## Operation

### Tradesman

???+ note "When skill is referred to, it is one of the following:"

    - :material-flask: **alchemy**
    - :material-bread-slice: **baking** 
    - :material-beer: **brewing**
    - :material-fish: **fishing**
    - :material-bow-arrow: **fletching**
    - :material-diamond-stone: **jewelcraft**
    - :material-pot: **pottery**
    - :material-book-open-page-variant: **research**
    - :material-hammer: **smithing**
    - :material-scissors-cutting: **tailoring**
    - :material-skull: **poison**
    - :material-wrench: **tinkering**

**Learn**  `"filter"`
: To learn a subset of known recipes.  

    syntax:
    ```eqcommand
    /mac ts/tradesman <skill> learn "filter"
    ```

    !!! example "e.g If you want to only learn ink recipes. "
        ```bash
        /mac ts/tradesman research learn "Ink of"
        ``` 
        (Note the use of quotes for recipes with spaces)

**Dryrun**
: Does not attempt to make any combines, it notes every single ingredient that you are missing, only check in inventory (not bank) to see what is needed. May check `ts/character-shop.ini` during or after to see what was logged.

    syntax:
    ```eqcommand
    /mac ts/tradesman <skill> dryrun
    ```

**Make** `"recipename"`
: Will attempt to make the specified recipe. A shopping list will be generated if set as allowed in `tradesman.ini`.

    syntax:
    ```eqcommand
    /mac ts/tradesman <skill> make "recipename"
    /mac ts/tradesman <skill> make "recipename" <quantity>
    ```

    !!! example "Examples"
        ```bash
        /mac ts/tradesman <skill> make "Wolf Steaks"
        ```
        Will attempt to make Wolf Steaks
        
        ```bash
        /mac ts/tradesman <skill> make "Wolf Steaks" 20
        ```
        Will attempt to make 20x Wolf Steaks

    !!! note "Use quotes if there are spaces in the recipe name."

**Filters** `"filter" ingredient`
: Check if the recipe uses the filter ingredient (note the use of quotes).

    syntax:
    ```eqcommand
    /mac ts/tradesman <skill> learn "filter" ingredient
    ```

    !!! example "e.g if you have a stack of vellum parchments"
        ```bash
        /mac ts/tradesman research learn "vellum parchment" ingredient
        ```

### Slash Commands

Most of these slash commands are not used as people find it easier to edit settings and restart the macro.

| Command | Description |
|---------|-------------|
| `/tradesman learn` | Start learning recipes again |
| `/tradesman restart` | Restart from the last known recipe |
| `/tradesman reset` | Restart from beginning |
| `/tradesman stop` | Stop learning/combining |
| `/tradesman end` | End the macro |
| `/tradesman list` | Show shopping list |
| `/tradesman learned` | Show recipes learned |
| `/tradesman subcombine` | Toggle making subcombines |
| `/tradesman subcombine 3` | Set allowed subcombine 3 levels deep |
| `/tradesman container` | Ignore subcombines not in same container |
| `/tradesman shop toggle` | Shopping list entries |
| `/tradesman beep` | Toggle beep |
| `/tradesman debug` | Toggle debug |

### Finditem
: Reads the `ts/character-shop.ini` then checks if you have any of the items in your inventory or bank. If so, it takes items out and puts them in your last bag (slot10). Does NOT check if there is space.

    - If you have the banker open it pulls from banker and does `/autoinventory`
    - If you have a merchant open it buys from the merchant  
    - If the character you are on is not the tradeskiller it checks the inventory and drops items in your last bag

    syntax:
    ```eqcommand
    /mac ts/finditem <charactername>
    ```

    !!! note "All inventory/banker slots need to have a container."

    !!! tip "Usage"
        After you run finditem against your bank/inventory, you can then open a merchant and run it again - it will buy the items it finds.

### Merchant
: Adds the vendor content to the `ts_merchants.ini`. Only unlimited items (stock they do not run out of, indicated by '--') will be added.

    syntax:
    ```eqcommand
    /mac ts/merchant
    ```

### Cleanup
: A way to clean up your bags after you reach 350 skill. Goes through your inventory, picks up every merchant sold item and does `/autoinventory`. 

    syntax:
    ```eqcommand
    /mac ts/cleanup
    ```

    !!! tip "Have an empty bag in first slot then you can just sell bag content."

    !!! warning "It will only move vendor sold items from an extraplanar trade satchel."

### Make Items in a list

**makelist** `b<skillname>`
: `trophy.ini` is a good example of how to setup this functionality.

    syntax:
    ```eqcommand
    /mac ts/tradesman <listname> makelist b<skillname>
    ```

    !!! example "Trophy makelist examples"
        ```bash
        /mac ts/tradesman trophy makelist bsmithing
        /mac ts/tradesman trophy makelist btailoring
        /mac ts/tradesman trophy makelist bpottery
        ```

    !!! note "For skill, start with "b" (for beginner) followed by the skillname."

## Example Workflow

!!! tip "Setup reminders"
    - Make a hotbutton `/mac ts/tradesman <skill> learn` as you will be running this macro a few times per skill
    - Do not destroy any items that are created and marked tradeskill - you will need them later
    - Did you remember to read the tradeskill books first?
    - Read the FAQ before asking questions already covered

### Main Learning Loop

Using fishing as an example, here's how the process works:

1. **Start learning recipes**
    ```bash
    /mac ts/tradesman fishing learn
    ```

2. **Let it run or stop when ready**  
    Wait for it to end or if you feel you saw enough recipes scroll by:
    ```bash
    /tradesman end
    ```

3. **Gather ingredients from the shopping list**  
    Farm/bazaar/merchant buy items listed in `ts/charactername-shop.ini`
    
    - You can buy/locate items in your bank/housing
    - Open up the vendor/bank/housing window and run:
        ```bash
        /mac ts/finditem charactername
        ```
    - You can run this on other characters and the found ingredients will be dropped into bag 10
    - Once you bought/located some items go back to step 1

!!! note "Iterative process"
    You may need to repeat steps 1-3 multiple times: get ingredients → learn recipes → buy vendor items → learn more recipes. After repeating this cycle you will reach 350 skill or your inventory will fill up with vendor bought items. Try to put them in the bank so you can pull them out with step 3 if needed again.

### When the macro adds to shopping list

The macro adds items to the shopping list when:

- It's a farmed ingredient
- It's vendor bought and you have all the farmed ingredients  
- All ingredients are vendor bought

### Cleanup Process

When your bags fill up with vendor items:

1. **Prepare for cleanup**
    - Have an empty bag in slot 1
    - Run: `/mac ts/cleanup`
    - It picks up each vendor item and does an `/autoinventory`
    - Items will end up in bag 1

2. **Sell the items**
    - Stop the macro with `/endm`
    - Check that no tools are in the bag
    - Open vendor window
    - Select bag 1 and click sell
    - Nice clean bag!

3. **Repeat** step 1 until no more vendor ingredients are found

---

!!! abstract "Contact the author"
    If you send me a private message tell me you removed the red jellybeans (This is a [Van Halen](https://www.insider.com/van-halen-brown-m-ms-contract-2016-9) check).

## FAQ

!!! question "Learn with a filter does not work?"
    Probably used the next migrator and it moved files to `config/ts` - remove that whole directory and it should start working.

!!! question "It appears to be making already learned recipes!"
    Remove the `config/ts` directory, it is a conflict between mqnext/migrator and the macro itself expecting files in certain places.

!!! question "Why do I want this?"
    You need to learn a certain amount of recipes to max out the Artisan's Prize, this will allow you to do it. Up to you if you take a skill to 350 or not.

!!! question "Does it work on TLP?"
    Not supported at all on TLP, difference is too big. Recipes/inventory/ingredients all differ or exist on TLP and not live or live but not TLP. Some things from that era auto learned on live or does not count towards the 350 goal then they are not included in recipe list e.g Banded. Most TLP are truebox and MQ should not be used on them anyway.

!!! question "It stops after 30 recipes and do not run through the whole list?"
    That is the default, adjust it to how many you want to try or the whole list by setting the value to 0:
    ```ini
    recipeFarm=0
    ```

!!! question "It does not take items from the shared bank?"
    Is your setting turned off?
    ```ini
    SharedBank=1
    ```

!!! question "What is the difference between tradesman / tradesmanv1 / tradesmanv2?"
    No difference at all, it is a leftover from when the macro started and there was experiments for people to try out before a middle road was chosen. It is precisely the same code. Names live on so as not to break people's hotbuttons.

!!! question "Which expansions are supported?"
    Up to Laurion's Song

!!! question "What is the easiest skill to start with?"
    Depending on your definition of easy it varies, all of the skills have a lot of required tedious farming (no the bazaar will not be a real option. You are not close to rich enough)

    **Easiest with least amount of farming and recipes is in order:**

    1. fishing, brewing, baking, jewelcraft, pottery, smithing, tailoring, research
    2. tinkering/alchemy/poison - lucky you get more recipes to max out the artisans prize
    - alchemy is mostly vendor bought
    - tinkering is a lot of tedious farming
    - poison some farming in ldon zones

    | Skill | Recipes per point |
    |-------|-------------------|
    | Alchemy | 11 |
    | Baking | 14 |
    | Blacksmithing | 39 |
    | Brewing | 6 |
    | Fishing | 2 |
    | Fletching | 18 |
    | Jewelry Making | 26 |
    | Poisonmaking | 11 |
    | Pottery | 40 |
    | Research | 51 |
    | Tailoring | 42 |
    | Tinkering | 16 |

!!! question "It does not work, environ1 not found!"
    You need to use static containers, e.g ones in Plane of Knowledge. I have no plans to support more containers that you carry around (a few very select recipes can only be made in some, those are supported)

!!! question "It is stuck making one recipe over and over! or I cannot make a recipe (class/race restriction)"
    ```bash
    /tradesman stop
    ```
    Add recipe ID to `ts/tradesman-block.ini` [BLOCK] section

!!! question "I cannot seem to learn XXX recipe?"
    Probably as it is learned through a book or you have not done the beginning tradeskill recipes (Crescent Reach / Abysmal Sea tradeskill quests). Use EQRecipe to find your free skillups

!!! question "Does it do all the tradeskills?"
    It works on all of them.

!!! question "Does it make all combines or just the ones I do not know?"
    It uses the output from EQ client `/outputfile recipes <tradeskill>` compares it against a master list of known 350 masters and the difference is what gets made. In short only those you do not know.

!!! question "I run out of bag space!"
    There is no easy solution to this, I have 2 other characters standing around ready to accept 32 slot Extraplanar bags when they fill up or when I think I don't need what is in them anymore (easy to get back just the items needed with `/mac ts/finditem <character>`)

    I used 3x32slot tradeskill and 3x 40slot all-purpose bags. Still did not have enough bagspace. After finishing fishing, brewing and some of baking the extra components took up 21x32slot tradeskill bags!

!!! question "Why did you rewrite?"
    It was easier taking the good parts and rewriting than trying to fix what a mess the v0x became. The v0x did not suit my future plans.

!!! question "Why was shop removed?"
    Frankly it is a waste of time running it, you now may as well try and make a few items as you go along building up a shopping list as it is not limited to 50 items anymore. It will stop when it either runs out of recipes or when you issue a slash command `/tradesman end`

!!! question "I need to imbue/enchanter does this macro do it?"
    It does not but there is Macro to cast Enchant or Imbue... or other spell to help

!!! question "There is something wrong, it does not do that combine and I have all of the items?"
    Make sure that in `tradesman.ini` your subcombine is set to 5 or greater. I had a default value of 1 which is just basic combines

!!! question "Inventory slot 11 and 12 from perks do not work?"
    I will not be supporting it unless it becomes accessible to everyone gold/f2p

!!! question "Item sold by merchant is not marked as such?"
    I am a slacker probably never thought to dump that merchant's inventory.

    Submit an update: with merchant open `/mac ts/merchant` then send me your `ts/ts_merchant.ini`

!!! question "How to skip recipes?"
    Add recipe ID to `ts/tradesman-block.ini`, in the [BLOCK] section. It may not exist yet.

!!! question "What do you do for 1-300?"
    Tradeskills is not cheap, it's not quick either.  

    **Pottery**  
    : - [Unfired Spherical Bottle (302)](http://www.eqtraders.com/items/show_item.php?item=17425)  

    **Baking**  
    : - [Patty Melt (181)](http://www.eqtraders.com/items/show_item.php?item=3009)  
    - [Broiled Raxil Fish (415)](http://www.eqtraders.com/items/show_item.php?item=38047)  

    **Fishing**  
    : - Probably max out fishing for raxil fish / CoV fish  

    **Brewing**  
    : - [Fetid Essence (122)](http://www.eqtraders.com/items/show_item.php?item=2975)  
    - [Brut Champagne (335)](http://www.eqtraders.com/items/show_item.php?item=3893)  
    - [Crowberry Juice (466)](http://www.eqtraders.com/items/show_item.php?item=66599)  

    **Research**  
    : - EQ Traders: search for binding powders   
    - [Elementary Enchanted Spell Parchment (118)](http://www.eqtraders.com/items/show_item.php?item=29914)  
    - [Simple Enchanted Spell Parchment (192)](http://www.eqtraders.com/items/show_item.php?item=29924)  
    - [Enchanted Spell Parchment (232)](http://www.eqtraders.com/items/show_item.php?item=29915)  
    - [Intricate Enchanted Spell Parchment (312)](http://www.eqtraders.com/items/show_item.php?item=28897)  
    - [Elaborate Enchanted Spell Parchment (352)](http://www.eqtraders.com/items/show_item.php?item=29913)  
    - [Guidestone (402)](http://www.eqtraders.com/items/show_item.php?item=5991)  

    **Fletching**  
    : - [CLASS 5 Bone Point Arrow (large nock) (162)](http://www.eqtraders.com/items/show_item.php?item=4248)  
    - [Rough Shadewood Recurve Bow (Linen) (255)](http://www.eqtraders.com/items/show_item.php?item=4397)  
    - [Rough Shadewood Compound Bow (hemp) (282)](http://www.eqtraders.com/items/show_item.php?item=4414)  
    - [Ethernere Arrow (308)](http://www.eqtraders.com/items/show_item.php?item=41093)  
    - [CLASS 9 Steel Fearbone Arrow (Small Nock) (308)](http://www.eqtraders.com/items/show_item.php?item=39620)  
    - [CLASS 9 Steel Fearbone Arrow (Large Nock) (322)](http://www.eqtraders.com/items/show_item.php?item=39625)  
    - [Primordial Driftwood Compound Bow (335)](http://www.eqtraders.com/items/show_item.php?item=6397)  
    - [Auspicious Elder Wood Plank (423)](http://www.eqtraders.com/items/show_item.php?item=63025)  
    - [Velium Infused Plank (423)](http://www.eqtraders.com/items/show_item.php?item=64565)  
    - [Restless Velium Plank (423)](http://www.eqtraders.com/items/show_item.php?item=66393)  

    **Blacksmithing**  
    : - Barbs: various ores + file (search eqtraders)  
            - Trivial 112 = 06. Fulginate Ore  
            - Trivial XXX = 07. Rubicite Ore  
            - Trivial XXX = 08. Indium Ore  
            - Trivial 184 = 09. Rhenium Ore  
            - Trivial XXX = 10. Tungsten Ore  
            - Trivial 222 = 11. Cobalt Ore  
            - Trivial 242 = 12. Titanium Ore  
            - Trivial 255 = 13. Tantalum Ore  
            - Trivial 268 = 14. Vanadium Ore  
            - Trivial 282 = 15. Osmium Ore  
            - Trivial 282 = 16. Paladium Ore  
    - [Velium Chainmail Rings (423)](http://www.eqtraders.com/items/show_item.php?item=64557)  
    - [Velium Sheet (423)](http://www.eqtraders.com/items/show_item.php?item=64555)  
    - [Restless Velium Chainmail Rings (423)](http://www.eqtraders.com/items/show_item.php?item=66385)  
    - [Restless Velium Sheet (423)](http://www.eqtraders.com/items/show_item.php?item=66382)  

    **Tailoring**  
    : - [Woven Mandrake (66)](http://www.eqtraders.com/items/show_item.php?item=1136)  
    - Hilt Wraps  
        - 112 Rough Hilt Wrap  
        - 184 Fine Hilt Wrap  
        - 222 Superb Hilt Wrap  
        - 242 Flawless Hilt Wrap  
        - 255 Exquisite Hilt Wrap  
        - 268 Immaculate Hilt Wrap  
        - 202 Fantastic Hilt Wrap  
        - 282 Exotic Hilt Wrap  
        - 282 Befouled Hilt Wrap  
    - [Velium Heavy Cloth (423)](http://www.eqtraders.com/items/show_item.php?item=64563)   
    - [Velium Infused Leather (423)](http://www.eqtraders.com/items/show_item.php?item=64558)    
    - [Restless Velium Heavy Cloth (423)](http://www.eqtraders.com/items/show_item.php?item=66392)    
    - [Restless Velium Leather (423)](http://www.eqtraders.com/items/show_item.php?item=66388)  

    **Jewelcraft**  
    : - Uncut Gems  
            - ..60 Rnd. Malachite (5s2c)
            - [Champagne Magnum (196)](http://www.eqtraders.com/items/show_item.php?item=1649)
            - 218 Oval Demantoid
            - 234 Tril Amethyst
            - 234 Marq Crimson Nihilite
            - 235 Marq Alexandrite
            - 252 H-Mn Goshenite
            - 259 Marq Indigo Nihilite
            - 267 Tril Combine Star
            - 270 Rnd. Morganite
            - 284 Marq Amber Nihilite
            - 284 H-Mn Staurolite
            - 287 Rnd. Jacinth
            - 300 Sqar Black Sapphire
            - 304 Pear Rubellite
            - 310 Tril Shimmering Nihilite

    **Alchemy**  
    : - [Deepwater Ink](http://www.eqtraders.com/search/reverse_recipe_search.php?item=6667)
    - [Distillate of Celestial Healing IX (302)](http://www.eqtraders.com/items/show_item.php?item=20721)

    **Poisonmaking**
    : - Look at eqtraders. Make what you have
    - [Make Poison](http://www.eqtraders.com/recipes/recipe_quicklist.php?rsa=Make%20Poison)

    **Tinkering**
    : - EQTraders: Perpetual Mana Battery: RoS/TBL/ToV/CoV variants

!!! question "I dislike you intensely!"
    I know, Happy farming.

## Known Bugs

!!! bug "Bugs"
    - **mq2live: no bag in slot X:** It's a live problem that has gone unfixed. Put something in all bags like a collection item.  
    - **mqnext: deprecated navigation to a ground item:** Will update the code when next becomes Redguides fully supported.  
    - **mqnext: recipes do not seem to update:** When using the migrator it moves the `ts/*.ini` to the config folder. Delete that `config/ts` folder.  
    - **fish scale combine bugs out:** Wait till it learns the recipe then use the autocombine button on tradeskill container.  
    - **ore/clay combines bug out:** Do it manually.  

## Acknowledgements

kaen01, Sic, ChatWithThisName thank you for answering silly questions. Without you this would not have being possible.
