---
title: Loading Spinner is Bad
date: 2022-11-13 18:00:00 +0800
categories: [Blogging, Technology, Software Development]
tags: [programming]
---
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

1. [Stop Using A Loading Spinner There’s Something Better by Suleiman Ali Shakir, UX Collective](https://uxdesign.cc/stop-using-a-loading-spinner-theres-something-better-d186194f771e)
