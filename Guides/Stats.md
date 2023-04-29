Sup!

Stats are alot like script globals and locals, but they never get updated.

You can get most of the stats at: https://gist.github.com/1337Nexo/945fe9724b9dd20d33e7afeabd2746dc

You can also extract all of the stats yourself, by using OpenIV to extract the stats in a .xml format.

Stats can hold strings ("ballsman"), booleans (true), integers (1337), labels ("HUD_JOINING"), floats (4.20), 
positions (x = 1.1, y = 2.2, z = 3.3), and other other data types (https://en.wikipedia.org/wiki/C_data_types)

There are packed stats, wich hold up to 64 of one type of stat, so if there is a packed int stat,
then it can hold up to 64 regural integer values.

Certain stats need a prefix of "MP0_" or "MP1_" (further on will be called "MPx_"). Depending on wich character slot you are on.
Only stats that dont containt the "MPPLY_" prefix dont need the "MPx_" prefix, because a "MPPLY_" prefixed stat is basically shared between character slots.

To get the current character slot you are playing in, you can get the integer value of the stat "MPPLY_LAST_MP_CHAR":

`local characterSlot = STATS.STAT_GET_INT(g_util.joaat("MPPLY_LAST_MP_CHAR"))` <br>

To set a normal integer stat with the Cherax Lua API, you will use
`STATS.STAT_SET_INT(Hash statName, int value, bool save)`

but this will only return you the character slot, not the entire prefix of "MPx_".

For that you can make a wrapper function to set stats, so you dont need to get the character slot each time.

For this example I will use the Cherax Lua API: https://docs.cherax.vip/lua-documentation/api-reference/natives/stats

```lua
local function statSetInt(statName, value)
    local statWithPrefix = string.format("%s%s%s%s", "MP", STATS.STAT_GET_INT(g_util.joaat("MPPLY_LAST_MP_CHAR")), "_", statName)
    return STATS.STAT_SET_INT(g_util.joaat(statWithPrefix), value, true)
end
```
or 
```lua
local function statSetInt(statName, value)
    return STATS.STAT_SET_INT(g_util.joaat(string.format("%s%s%s%s", "MP", STATS.STAT_GET_INT(g_util.joaat("MPPLY_LAST_MP_CHAR")), "_", statName)), value, true)
end
```
Theese just return if the setting of the stat was successful or not

Mind that theese cant set stats, that have the prefix "MPPLY_" because the wrapper function will always add the prefix "MPx_" infront of the string that is passed in the function.

You can make a wrapper function, that detects if the passed statName contains "MPPLY", and if it does then it does not add the prefix "MPx_"

Some stats are srver authoritative, that means you cannot edit them, but you can read from them.

Thats the basics of stat reading and writing.
