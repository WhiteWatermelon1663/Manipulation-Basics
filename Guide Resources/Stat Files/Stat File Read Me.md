This is from mpstatssetup(1).xml

I have removed the fluff and the useless data that you dont need.
0 to 255
0 to 65,535
0 and 18,446,744,073,709,551,615
```text
Name                - The string name of the stat value. Has to be unique. Max Size - 32 characters.
Type                - The type of this stat. Possible values are:
                        .. Possible values are:
                           .. Type = "float"  - C++ Float. (1.175494351*10^-38	3.402823466*10^38)
                           .. Type = "int"    - C++ Integer. (-2147483648 to 2147483647)
                           .. Type = "bool"   - C++ Boolean. (0 or 1 / false or true)
                           .. Type = "label"  - C++ Integer. (-2147483648 to 2147483647)
                           .. Type = "string" - C++ String. (string)
                           .. Type = "u8"     - C++ Unsigned Integer 8. (0 to 255)
                           .. Type = "u16"    - C++ Unsigned Integer 16. (0 to 65,535)
                           .. Type = "u32"    - C++ Unsigned Integer 32. (0 to 4,294,967,295)
                           .. Type = "u64"    - C++ Unsigned Integer 64. (0 to 18,446,744,073,709,551,615)
                           .. Type = "date"   - C++ Unsigned Integer 64 used in script for dates. (-2147483648 to 2147483647)
                           .. Type = "pos"    - C++ Unsigned Integer 64 used in script for map positions. (-2147483648 to 2147483647)
                           .. Type = "userid" - C++ String. (string)
online              - "true" if the stat is a multiplayer stat. "false" if it is a single player stat.
profile             - "true" if the stat is a Profile Stat.
community           - "true" if the stat is a community stats (Stock Market Stat).
Min                 - A minimum value of any submitted values. If a submitted value is less than this value then the submitters gamerhandle will be 
                        logged as a violator. If not provided the default is no minimum.
Max                 - A maximum value of any submitted values. If a submitted value is greater than this value then the submitters gamerhandle will be 
                        logged as a violator. If not provided the default is no maximum.
MaxVelocitySeconds  - Used in conjunction with the MaxVelocityDelta value for stat velocity (rate of change) cheat detection. To define the maximum rate 
                        of change possible for a stat, set this value to the the number of seconds to use in a (delta / seconds) rate calculation.
MaxVelocityDelta    - Used in conjunction with the MaxVelocitySeconds value for stat velocity (rate of change) cheat detection. To define the maximum rate 
                        of change possible for a stat, set this value to the the delta to use in a (delta / seconds) rate calculation.
Owner               - Owner of the stat.
                        .. Possible values are:
                          .. "system" - System stats are those that every game should report for players; 
                                        and are used for spotting trends in hardware and preferences among our player base.
                          .. "coder"  - Game Stat values are changed in C++ code.
                          .. "script" - Game Stat values are maintained in level design.
Comment             - A string which will appear only when the Config CSV downloaded.
Label               - A String that holds the text gxt label (optional)
Denominator         - And int that holds the award denominator for that stat. (optional)
ReadPriority        - Profile stats that have priority set to 1 or 2 will be downloaded during multiplayer game for the remote players.
FlushPriority       - Profile stats need to have flush priorities to that the most important take precenede
ServerAuthoritative - Profile stats that have this to true are synched with the value on ROS server.
```
