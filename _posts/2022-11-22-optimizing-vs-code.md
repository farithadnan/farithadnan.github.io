---
title: Optimizing VS Code
date: 2022-09-30 14:57:00 +0800
categories: [Blogging, Technology, VS Code]
tags: [application]
---

I stumbled into an issue where my VS Code took longer than is should be during the initial startup, after some checked up I come to conclusion that this issue is related to my installed extension. So, I decided to disable or uninstall any unused extensions and it actually help boost my VS Code performance quite a lot.

I decided to look other people's opinion about the VS code's performance issue and I stumbled upon a good article about [VS Code Performance – How to Optimize Visual Studio Code and Choose the "Best" Extensions](https://www.freecodecamp.org/news/optimize-vscode-performance-best-extensions/) I recommend you to read it if you're facing any performance issue with your VS Code.
the author of this article explains about what makes the VS Code's performance slower and the main factor of this issue is because of the installed extension.

What intrigue me the most is the fact that VS code's default features can actually operates/has mechanism similar with the extension itself, instead of installing the extension, you only need to find and tweak the setting a bit to get the same result as the extension, which is really useful!, for more info about this, you can visit [VS Code: You don't need that extension](https://www.roboleary.net/vscode/2020/08/05/dont-need-extensions.html) and [Documentation for Visual Studio Code](https://code.visualstudio.com/Docs)

>The author also suggested to use several useful command to audit VS Code's performance:
>
> - Display startup performance of your VS Code by running `Developer: Startup Performance` command.
> - Display Running Extension of your VS Code by running `Developer: Running Extensions` command.

I will summarize the things that I learned from the article on how to boost the performance of my VS Code:

- Run audit to check the performance when starting up the IDE and also check for the running extension via built in command that been stated above.
- Uninstall any unwanted extension.
- Disable any unused extension for the project.
- Find alternative extension that is not resources heavy.
- Minify/edit the extension's code. can visit [Is Your VS Code Extension Slow? Here's How to Speed it Up! - DEV Community 👩‍💻👨‍💻](https://dev.to/azure/is-your-vs-code-extension-slow-heres-how-to-speed-it-up-4d66) for more details.
- Disable few settings in VS Code that are related to restoring project state from the previous state.

---

## Sources

1. [VS Code Performance – How to Optimize Visual Studio Code and Choose the "Best" Extensions](https://www.freecodecamp.org/news/optimize-vscode-performance-best-extensions/)
2. [Is Your VS Code Extension Slow? Here's How to Speed it Up! - DEV Community 👩‍💻👨‍💻](https://dev.to/azure/is-your-vs-code-extension-slow-heres-how-to-speed-it-up-4d66)
3. [VS Code: You don't need that extension](https://www.roboleary.net/vscode/2020/08/05/dont-need-extensions.html)
4. [Documentation for Visual Studio Code](https://code.visualstudio.com/Docs)
