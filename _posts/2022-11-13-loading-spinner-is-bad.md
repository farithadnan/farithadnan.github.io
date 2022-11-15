---
title: Loading Spinner is Bad
date: 2022-11-13 18:00:00 +0800
categories: [Blogging, Technology, Software Development]
tags: [programming]
---

>During the development of my Angular project, I stumble upon a problem that are related to the loader spinner. For my project the loader spinner will popup only if there's a [HTTP Request] which took more than one second to load its data and for this to work I have to use Angular's HTTP interceptors to fetch request. In my project I also have a generic dialog/modal services that can be use by any components in the application. On the 'reusability' standpoint it look great but when it comes to implementing your application to work alongside the loading spinner it can become quite hard to execute.
>
>I got an issue whenever the dialog/modal is  popup to the screen the loading spinner will also got loaded as well, the loading spinner will appear  overlapping behind the dialog for a while before disappearing, when I tried to work on the solution for this issue, I stumble into an article ([[Stop Using A Loading Spinner, There’s Something Better | by Suleiman Ali Shakir | UX Collective](https://uxdesign.cc/stop-using-a-loading-spinner-theres-something-better-d186194f771e)]) that explain about why the loading spinner is bad for user's experiences.  
{: .prompt-info }


## Why loading spinner is a no-no

Below is my own interpretation on why the loading spinner is bad for the user's experiences. It maybe look cool with all the animating affect provided by the loading spinner but it actually  have its own disadvantages as well.

- Loading spinner doesn't tell you how long will it keep spinning to load the content for the user. By having the detail information about the duration of the load, user can feel at ease and will prevent them from exiting your website because of load duration is uncertain.
- Because of the uncertainty and not having any information about the loading process, user will think that the app is slower or have any issues with the server connection etc.
- A good practice to have is to let user know what content that the app will load beforehand.

## Alternative option

- **Finite loading spinner/progress bar** to give user information when the spinner will finish loading.
- **Skeleton Screen** will display the base UI all at once and will display it content gradually which is great for user experiences.

---

## Sources

1. [Stop Using A Loading Spinner, There’s Something Better | by Suleiman Ali Shakir | UX Collective](https://uxdesign.cc/stop-using-a-loading-spinner-theres-something-better-d186194f771e)
