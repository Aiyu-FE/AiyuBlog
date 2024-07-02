---
标题: 如何在批处理模式下运行 SKILL --- How to run SKILL in batch mode
地址: https://support.cadence.com/apex/ArticleAttachmentPortal?id=a1O3w000009lXVoEAM&pageName=ArticleContent
时间: 2024-05-30 01:44:10
标签: #SKILL
附件:
---


# 如何在批处理模式下运行 SKILL --- How to run SKILL in batch mode

  

  

# Problem 问题

  

I am unable to find a way to automate Allegro using SKILL scripts without launching the tool.  
我无法找到在不启动工具的情况下使用 SKILL 脚本自动运行 Allegro 的方法。

  

# Solution 解决方案

  

Allegro provides two different ways of automation, one using the Allegro scripts and the other using SKILL language, the second one being Turing complete and thus allowing more flexibility. Both languages provide a way to store the code recorded or created in a file to source and run it later.  
Allegro 提供了两种不同的自动化方式，一种是使用 Allegro 脚本，另一种是使用 SKILL 语言，其中第二种语言是图灵完备的，因此具有更大的灵活性。两种语言都提供了一种将记录或创建的代码存储到文件中的方法，以便以后进行源代码和运行。

*   Allegro scripts are stored in .scr files and executed in the Allegro terminal using replay <file path>.scr.  
    Allegro 脚本存储在 .scr 文件中，并在 Allegro 终端中使用重放 <文件路径>.scr 执行。

*   SKILL scripts are stored in .il files and executed in the Allegro terminal using skill load("<file path>.il").  
    SKILL 脚本存储在 .il 文件中，并通过 skill load("<file path>.il") 在 Allegro 终端中执行。

![](assets/rtaImage.png)

  
A SKILL script allows you to define functions. If the algorithm is defined inside one or more functions, and you want to use them, it would be necessary to call the function in the Allegro terminal.  
SKILL 脚本允许您定义函数。如果算法是在一个或多个函数中定义的，而您又想使用这些函数，则必须在 Allegro 终端中调用函数。

skill <function name>(<function parameters>)  
skill <函数名>(<函数参数>)

Allegro allows automation in batch mode only using Allegro scripts by calling the following in your preferable shell terminal (batch, bash, cshell, etc):  
Allegro 只允许在批处理模式下使用 Allegro 脚本进行自动化，方法是在您喜欢的 shell 终端（batch、bash、cshell 等）中调用以下脚本：

allegro -s <path to the allegro script> -nograph <allegro board>  
allegro -s <allegro脚本路径> -nograph <allegro电路板

Here, \-nograph is an option to prevent the Allegro GUI from showing up. The board is also optional.  
在这里，-nograph 是一个选项，用于防止 Allegro 图形用户界面显示出来。电路板也是可选项。

Although you cannot directly call the SKILL script using the Allegro CLI, you can do it indirectly by creating a simple Allegro script, such as **tmp.scr**, which would call a SKILL script file, for instance, **script.il**, like the following:  
虽然无法使用 Allegro CLI 直接调用 SKILL 脚本，但可以通过创建一个简单的 Allegro 脚本（如 tmp.scr）来间接调用 SKILL 脚本文件（如 script.il），如下所示：

skill load("script.il")  
skill <function name>(<function parameters>)  
skill <函数名>（<函数参数>）。  
exit 退出

Then run it, for example:  
然后运行它，例如

allegro -s tmp.scr -nograph

Considering both files are in the same folder, this folder is currently open in the shell terminal. You must add an explicit exit command or the tool will not exit, even if it is launched in nograph mode.  
考虑到两个文件都在同一个文件夹中，该文件夹目前在 shell 终端中打开。您必须添加明确的退出命令，否则即使在 nograph 模式下启动，工具也不会退出。

This flow can be improved in many different ways: you can fully embed all the SKILL code in the .scr file by adding skill in the front of any command, you can call exit from the SKILL script instead, and so on.  
这个流程可以通过多种不同方式进行改进：可以在任何命令前添加 skill 将所有 SKILL 代码完全嵌入 .scr 文件，也可以从 SKILL 脚本中调用退出，等等。

  
**Note:** Apart from all the functionality of OrCAD/Allegro, their X platforms (OrCAD X/Allegro X) offer additional features and flexibility.  
注：除了 OrCAD/Allegro 的所有功能外，它们的 X 平台（OrCAD X/Allegro X）还提供额外的功能和灵活性。

[↓↓↓](#top)  
  
Return to the top of the page  
返回页面顶部  
  
[↑↑↑](#top)