Hi!

You will need a code editor for this, I suggest Visual Studio: https://code.visualstudio.com/

Let me show you how to edit and read script globals and script locals.

First you need to know what are script globals and script locals.

You can imagine a script global and a script local to be a address, if you go to the address it will point you to a value.

The value of a script global or script local can only be a integer (1234), float (69.420) or a boolean (true).

Theese script globals and script locals control alot of things: clothing item prices, vehicle trade price value, duration of effects.

Theese script globals and locals can change if the game updates, but its not that often. 

Script globals have 2 types of globals. Tunable globals and normal globals

Tunable globals look like: "Global_262145.f_26154", because they have the "262145" prefix, this prefix can change with updates aswell.

To find those script globals or locals you would need to get the game scripts. For now you can download the scripts at:

https://github.com/root-cause/v-decompiled-scripts

Keep in mind, that theese game scipts update. So you would need to download the scripts for a newer version of the game.

Now that you have the decompiled scripts, you can open up freemode.c.

You can search for script globals with the "Global_" prefix before numbers, like: "Global_2657589[PLAYER::PLAYER_ID() /*466*/].f_321"

For this example I will be using the Cherax LUA engine.

Since you cannot just paste "Global_2657589[PLAYER::PLAYER_ID() /*466*/].f_321" into the API function, you will need to convert it.

The PLAYER::PLAYER_ID() has to be for the Lua API that you are working with, for Cherax it is PLAYER.PLAYER_ID(), for Stand it is players.user()

Converting globals goes like this:

![image](https://user-images.githubusercontent.com/132128937/235295118-cacc2930-4759-4f62-81ed-b60e3fe06868.png)
  
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
