Welcome to WolfRPG CLI System made by SaltfishAmi.
Current version is built upon Wolf ver2.10




This common event series can provide a CLI-like experience, including:
(Many commands are not yet implemented. See below)
- Basic commands:
     - Standard I/O commands: echo, msgbox (with selectable options), getchar, getline, etc.
     - File I/O commands: fread, fgetline, fwrite, etc. - TO BE DONE
     - File system directory tree: cd, ls, md
     - Variable manipulation: 3+2, a+b, c=a+b, etc.
     - String manipulation: concat, pushline, popline, substr, pos etc. - TO BE DONE
     - Calling native events: ev(500223,1)  - TO BE DONE
     - Command aliasing: alias("refresh(","common(223,")  - NOT IN CURRENT PLANS
     - Directly run script files by path and use parameters: start.wcs "test" - TO BE DONE
- A command line interface that let you type in commands (or just prints text, you can specify that)
- Understanding multi-line strings containing a series of commands, just like a shell interpreting a script
- Named variables, independent of WolfRPG native variables, like a="test"
- R/W access to WolfRPG native variables, like _s_3000000 means string variable S[0], _i_1600001 means integer variable CSelf[01].
- Reading configuration files for game-specific native variable locations, and achieve direct modification through command. - TO BE DONE
     - For example, specify the player HP database location and the status update common event usage in a configuration file, - the former is achievable at current stage, latter is TO BE DONE
     - then you can directly type "HP=9999" and "refresh" to set HP and see the results. - the former is achievable at current stage, latter is TO BE DONE
- Basic flow control commands like "if-else-endif" and "loop-break-next" available to multi-line scripts.
- Access to local file system and internet. - TO BE DONE

########Notice: Many commands are not yet implemented. For now, this is the list of all possible commands:
assign, break, cat, cd, cls, cmd, concat, dl, echo, else, endif, exit, getchar, getline, help, if, int, loop, ls, length, lines, md, msgbox, next, return, str
break, else, endif, if, loop, next and return could only be used in a script file.
You can also type a script file name and run it.

For other instructions like grammar, please refer to the sample script file "startup.wcs" and "move.wcs". You can view them with any text editor.

With this system, you can implement advanced debugging and/or cheating system in your game,
or host your malicious script on your server, change it every day, let your game load them and see the players' frightened faces. (Don't actually do it!)

This system is currently incomplete and very buggy, but is already useful to some extent.
I hope you can enjoy this, and bug reports and feature suggestions are welcome!

I appreciate bug reports and feature suggestions, but I can't guarantee to process them quickly.
Please mail: aaabbb1112221575@gmail.com
You can write in English, Chinese or Japanese.

In the first common event "■WolfRPG CLI System", there are some configurations that needs manual adjustment.
There're also some detailed instructions in that common event. Please read them after updating to a new version.
Besides this, please make sure to call "■WolfRPG CLI System" before you use any part of this system for the first time.
I recommend to call this event in the title screen event.

You can test the sample script file like this:
 |■Insert event： CommonXXX：[ 0■WolfRPG CLI System ]
 |■String manipulation：S0[[Sample]TemporaryString] =<Read file content> "startup.wcs"
 |■Insert event： S0[[Sample]TemporaryString] = CommonXXX：[ 2├■MultiLineParser ] / S0[[Sample]TemporaryString]
The return value will be saved in S0[[Sample]TemporaryString].

You can also call the command prompt event like:
 |■Insert event： CommonXXX：[ 9├■CmdMode ]
and then type the script file name to test it.

ChangeLog:
2019/06/12 First release
2019/06/12 Bug fix
2019/06/14
New command implemented: getchar getline
Calculating string length in BYTES implemented
(Input cursor will display correctly even if the path contains Japanese)
Implemented script line counting, and internal fixes accordingly
Implemented nesting of loop-break-next
Update readme file
Added new sample script to demonstrate new features
Bug fix
2019/07/07
ls - fixed bug: directorys doesn't change color.
getline - fixed: automatically make a new line if used when the screen is full
2019/12/10
ls - changed the way of distinguishing a folder from a file, from "file.read()==<NoFile>" to "folder.itemlist()==<<ERROR>>"