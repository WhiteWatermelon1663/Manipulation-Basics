Sup! 

Finding signatures is easy!

But some information about the signatures before we start.

People often say sig(s), patterns or signatures.

Signatures are specific patterns in code. You can imagine it like as morse code. If you would have a word in morse code, it has a specific pattern.
For example, the word "megaballs" in morse is "-- . --. .- -... .- .-.. .-.. ..." each character has it's own pattern, 
and all of the characters make up a bigger pattern, with signatures, it's basically the same.
When the developers write code, and compiles their code. We can see the patterns of the code. If we get these patterns of the code, we can refrence back to it.
But if the developers code changes, so does the patter, so you need to update patters aswell.
There are wildcards in patterns aswell, a wildcard is basically a section of a patter, that can change its value. A wildcard
is normally represented as a question mark in the pattern, e.g. "E8 ? ? ? ? 83 25 ? ? ? ? ? F3 0F".
All of those question marks can change its value.
Luckily the plugin we are about to use detects the wildcards and does the job for us.

If a signature is too short, then it could be found elsewhere in the game,
and too long of signatures might get broken more often after game updates.

You need to have a analyzed dump of the game, if you don't, then follow:
https://github.com/WhiteWatermelon1663/Manipulation-Basics/blob/main/Guides/Setting%20up%20IDA%20and%20Analyzing%20the%20dump%20with%20it.md

Open up the dump and lets try to find the signature to the game build and online version.

We can find strings by pressing Alt + T.

The only bad thing about searching for strings, it is very slow.

But lets still find the game build and online version.

So press Alt + T and search for "GAME_BUILD".

![image](https://user-images.githubusercontent.com/132128937/235351157-dc45e6ac-582d-4e6e-88f1-dbd797d68746.png)

Now you gotta wait a while.

When its done it should look something like this

![image](https://user-images.githubusercontent.com/132128937/235351813-442436a0-082b-4cc2-8e37-827367cd0c93.png)

We can see that the one that has a function actually does something with the game build,
whilst the second entry is just basically assigning the string "GAME_BUILD" to a variable called `aGameBuild`

![image](https://user-images.githubusercontent.com/132128937/235351873-4a93c0ac-628f-46e1-86f0-d3c7d2c2846c.png)

Now click on the first entry twice.

![image](https://user-images.githubusercontent.com/132128937/235352016-a58e4ee2-ed60-4280-9d04-297de2773325.png)

And it should bring you to some assembly code like this:

![image](https://user-images.githubusercontent.com/132128937/235352800-7484aced-d978-40f9-988f-c3273611a3cc.png)

Here you can actually see the game build and online version as strings.

The jz, lea, mov, call, xor ... are operation codes (opcodes), theese are basically instructions for the computer to do certain tasks with the data we provide it.

You can find all the opcode refreces here: http://ref.x86asm.net/coder64.html

The "E8 96 84 51 01" and "48 8D 15 67 20 71 01" are basically patterns of the code.

![image](https://user-images.githubusercontent.com/132128937/235352986-bbb080b0-b8d0-4cf3-b8d2-b833a1170289.png)

"4C 8D 0D 74 3B C4 01" loads the effective address of the memory location of a2845 into the r9 register.

![image](https://user-images.githubusercontent.com/132128937/235354251-bb2aaa33-eb5f-4380-b17b-b0b621cb3d61.png)

So this time I will show you how to get the pattern manually.

I started at "44 8B C3", because they cannot be wildcards,

and ended at "44 24 20", because the it cant change either.

With most of the Lua API's, when scanning for a pattern, it will return the starting address of the pattern
so if you scan for the pattern "44 8B C3 33 D2 C6 44 24 20", then it will return the address of "44" (the start of the pattern).

To calculate the hex you can use: https://www.unitconverters.net/numbers/decimal-to-hex.htm
If you use this, just add "0x" before the hexadecimal number, or it will be wrong.

Or if you dont like visiting websites, you can do it with the Windows calculator too:

Set the calculator to "Programmer" mode.

![image](https://user-images.githubusercontent.com/132128937/235355006-20fafa90-89b6-40c3-b783-61f2dbb32b3d.png)

Selected the "Dec" mode.

![image](https://user-images.githubusercontent.com/132128937/235355045-e18ab9c9-556b-43a5-a64c-85d398df27b6.png)

And type 37, to get the hex number 25

![image](https://user-images.githubusercontent.com/132128937/235355103-accd8932-65b9-4e98-824b-1edad03b10f7.png)

Then you add 0x25 or 37 (it does not really matter, but I personally like the hex more) do the scanned pattern, because the scan returns the
address of the patterns beginning. And then you rip it out, because rip an offset from the instruction and returns the resulting address.
And then you can read it as a string.

Here I will show an example with the Cherax Lua API.

```lua
local a = g_memory.scan_pattern("44 8B C3 33 D2 C6 44 24 20")
g_logger.log_info(a)
local b = g_memory.rip(a + 0x25)
g_logger.log_info(b)
local gameBuild = g_memory.read_string(b)
g_logger.log_info(gameBuild)
```
That was how you make a sig manually, but now lets do it with the plugin.

Select some bytes:

![image](https://user-images.githubusercontent.com/132128937/235361498-462cc14b-11ac-4782-9a55-ea174e208ee7.png)

Open up the sigmaker plugin.

![image](https://user-images.githubusercontent.com/132128937/235361529-fdc66b13-d346-4325-b5a1-27e5d71c0335.png)

And press Auto create ida pattern.

![image](https://user-images.githubusercontent.com/132128937/235361567-cdfdd82a-8000-4165-b84c-ad888651a585.png)

For me it created this long signature, with a offset. I dont recomend using this long signature, because its so long, and the offset is big.
The.

![image](https://user-images.githubusercontent.com/132128937/235361756-ac6bf188-3cf6-4d9d-beb9-ea062de753f2.png)

So select a bigger area, and make a signature again.

Now it created a even shorted signature, with no offset even.

![image](https://user-images.githubusercontent.com/132128937/235361888-129ceedf-351c-4a9a-9d18-9096af7576f1.png)

But the trick is, you need to calculate your own offset. Because I said that the pattern scanner returns the start address of a pattern.
Then you will need to calculate the offset. I will show you the easiest way with IDA pro.

![image](https://user-images.githubusercontent.com/132128937/235361420-59427e63-bf2c-4f74-b4a8-cf8a36ae7f05.png)

Get the Y part of the address, here it is 7FF686FE1F4D,
Get the X part of the address, here it is 7FF686FE1F13,
Get the Z part of bytes, here it is 3 (because "4C 8D 0D" is 3 bytes)

Subract Y - X in hex, wich is 7FF686FE1F4D - 7FF686FE1F13 = 3A

and add decimal 3 to hex 3A, wich is 3 + 3A = 3D

If the number of bytes is bigger than 9, then you will need to convert the decimal number of bytes to the hexidecimal value.

3D = 61

So the distance between the pattern start address and the end of the address is 61 bytes.

So now you can add the 61 to the scanned pattern.

```lua
local a = g_memory.scan_pattern("48 8D 0D ? ? ? ? B2 01 E8 ? ? ? ? BB ? ? ? ? ")
g_logger.log_info(a)
local b = g_memory.rip(a + 0x3D)
g_logger.log_info(b)
local gameBuild = g_memory.read_string(b)
g_logger.log_info(gameBuild)
```

That is the basics of pattern scanning.
