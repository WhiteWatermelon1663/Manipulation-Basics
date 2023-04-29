Sup!

You will need a code editor for this, I suggest Visual Studio: https://code.visualstudio.com/

Let me show you how to edit and read script globals and script locals.

First you need to know what are script globals and script locals.

You can imagine a script global and a script local to be an address, if you go to the address it will point you to a value.

The value of a script global or script local can only be an integer (1234), float (69.420) or a boolean (true).

These script globals and script locals control a lot of things: clothing item prices, vehicle trade price value, duration of effects.

These script globals and locals can change if the game updates, but its not that often. 

Script globals have 2 types of globals. Tunable globals and normal globals

Tunable globals look like: `Global_262145.f_26154`, because they have the `262145` prefix, this prefix can change with updates as well.

To find those script globals or locals you would need to get the game scripts.

For now you can download the scripts from: https://github.com/root-cause/v-decompiled-scripts

A script global is shared across game scripts, a script local is not.

Keep in mind, that these game scipts update. So you would need to download the scripts for a newer version of the game.

Now that you have the decompiled scripts, you can open up freemode.c.

You can search for script globals with the "Global_" prefix before numbers, like: `Global_2657589[PLAYER::PLAYER_ID() /*466*/].f_321`

For this example, I will be using the Cherax Lua API: https://docs.cherax.vip/lua-documentation/api-reference/natives/script

Since you cannot just paste `Global_2657589[PLAYER::PLAYER_ID() /*466*/].f_321` into the API function, you will need to convert it.

The `PLAYER::PLAYER_ID()` has to be for the Lua API that you are working with, for Cherax it is `PLAYER.PLAYER_ID()`, for Stand it is `players.user()`

Converting globals goes like this:

![image](https://user-images.githubusercontent.com/132128937/235306087-1a2dd8a8-c784-4c04-abfd-eaa0610d4413.png)
  
 So it would look something like this:
 
  2657589 + 1 + PLAYER.PLAYER_ID() * 466 + 321
  
In conclusion:

<ul>
  <li>"Global_", remove it</li>
  <li>"[", add one (x + 1 + y)</li>
  <li>"/*" = multiply it (x * y)</li>
  <li>"*/]" = remove it</li>
  <li>"PLAYER::PLAYER_ID()" = Appropriate for API</li>
</ul>

So now you can edit that global to whatever value you desire, editing for Cherax goes like this:

`SCRIPT.SET_GLOBAL_I(int global, int value)` <br>
`SCRIPT.SET_GLOBAL_I(2657589 + 1 + PLAYER.PLAYER_ID() * 466 + 321, 69)`

For Cherax Lua API, <br>
&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;I stands for Integer (SCRIPT.SET_GLOBAL_I) <br>
&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;F stands for Float (SCRIPT.SET_GLOBAL_F) <br>
&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;B stands for Boolean (SCRIPT.SET_GLOBAL_B) <br>

And to read a global it is even easier:

`SCRIPT.GET_GLOBAL_I(int global)` <br>
`local valueOfGlobal = SCRIPT.GET_GLOBAL_I(2657589 + 1 + PLAYER.PLAYER_ID() * 466 + 321)`

Now lets move onto script locals. Script locals are only readable and writable in a game script.
Each game script has its own script locals. For example I will be using freemode.c's script local `uLocal_69`
It is not used anywhere in the script so it is useless.

Converting a script local is the same as converting a script global, you just need to remove the `uLocal_` or `iLocal_`. 
You just need to remove the prefix and follow the script global conversion.

To read a script local, the script needs to be running.

So for Cherax Lua API, I can read script local like this:

`SCRIPT.SET_LOCAL_I(Hash script, int local, int value)` <br>
`SCRIPT.SET_LOCAL_I(g_util.joaat("freemode"), 69, 420)`

For Cherax Lua API you need to joaat (jenkins one at a time) the string first with `g_util.joaat(string)`, but with other Lua API's you might not.

To read a script local is same as reading a script global:

`SCRIPT.GET_LOCAL_I(Hash script, int local` <br>
`local valueOfLocal = SCRIPT.GET_LOCAL_I(g_util.joaat("freemode"), 69)`

Thats the basics of script global and script local reading and editing.
