Sup!

Analyzing the dump with IDA is easy.

If you dont have a game dump then follow the guide:
https://github.com/WhiteWatermelon1663/Manipulation-Basics/blob/main/Guides/Dumping%20the%20game.md

For this you will need IDA. Luckily IDA Freeware is a thing, and you probably do not need IDA Pro yet.

Go and download IDA Freeware.

IDA Freeware: https://hex-rays.com/ida-free/#download

And download the sigmaker plugins. (you will need this later, but in this guide)

Sigmaker: https://github.com/WhiteWatermelon1663/Manipulation-Basics/tree/main/Guide%20Resources/Sigmaker

Download both sigmaker.dll and sigmaker64.dll

Now that you have downloaded IDA and the dlls, go to IDA's file directory (where you download IDA to)

and drag the two sigmaker dlls into the plugins folder.

![image](https://user-images.githubusercontent.com/132128937/235344268-66c12fbb-ae50-4371-8308-ebbec44e07a5.png)

Now if you have set up IDA. Open it as administrator.

WARNING: IDA CAN CRASH YOU COMPUTER, AND IT COULD BLUE SCREEN. DONT BE ALARMED. IT IS NORMAL.

Now disassemble a new file.

![image](https://user-images.githubusercontent.com/132128937/235343527-899867dc-37c0-4027-9bbf-e90923ada74f.png)

Then open the dump, that you saved of the game. Should be named "GTA5_dump.exe", open it with IDA. And press Ok

![image](https://user-images.githubusercontent.com/132128937/235343951-707223d2-19ab-4ec2-97ad-c2657369330e.png)

Now IDA will take some time analyzing the dump, this takes some time, depending on how powerful your computer is.
If you have a computer with shit hardware, then its gonna take some time, but if you have high end stuff then it will be analyzed faster.

But we can still do things while its analyzing, so lets do some stuff.

If you have the goofy aah white theme, then you can change it to gigachad dark theme at Options > Colors... > Current theme

![image](https://user-images.githubusercontent.com/132128937/235344144-bc9ae2cf-33e2-47ae-b6f3-f6ef877a1716.png)

And turn that to "dark"

![image](https://user-images.githubusercontent.com/132128937/235344171-a2c8a05c-e983-4483-991f-ef9b8f65471d.png)

And press "Apply" and "Ok"

Now you got rid of the cringe white theme, you can check if you have the sigmaker plugin installed, 
by goind to Edit > Plugins > SigMaker.

![image](https://user-images.githubusercontent.com/132128937/235344494-e914dc40-48fd-4a75-90ff-eb52f188d004.png)

Now click on "SigMaker" and a window like this should pop up:

![image](https://user-images.githubusercontent.com/132128937/235344532-dc7726b0-ca5b-44d0-a763-d2f6b7b55bdf.png)

And if you have this goofy ahh "Graph Mode" then you can go to "Text View" by right clicking somewhere and pressing "Text view",
because text view is simply better.

![image](https://user-images.githubusercontent.com/132128937/235345045-35b25f19-f0ac-4100-9848-0f6461b48d28.png)

Now lets make the opcodes visible, by going to Options > General... > Disassembly > Number of opcode bytes (non-graph) and set it to 10

![image](https://user-images.githubusercontent.com/132128937/235348915-88bbbe84-cadc-4d9e-941a-fe4dbf061a04.png)

![image](https://user-images.githubusercontent.com/132128937/235348979-b8f4e23e-83f3-4c00-9054-251d2f015119.png)

Now wait until this says Idle.

![image](https://user-images.githubusercontent.com/132128937/235344733-4499c26d-3ffc-424e-9d70-3b22e31c33b1.png)

It should look like this

![image](https://user-images.githubusercontent.com/132128937/235348657-4579888f-9d53-4d36-b4a3-94246019d1c1.png)

Then press Ctrl + W to save the database.

And if you exit IDA, then always pack the database, like this:

![image](https://user-images.githubusercontent.com/132128937/235348698-c9ceeb7e-e292-4474-b539-46251a30e47c.png)

And if you want to open the dump again in IDA, then open it from the "GTA5_dump.exe.i64" file.

![image](https://user-images.githubusercontent.com/132128937/235348794-7346ed03-4132-4648-8b66-cfea0ac586fa.png)

So that is the basics of analyzing the game dump.
