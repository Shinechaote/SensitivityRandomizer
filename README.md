# Sensitivity Randomizer

**By: Whisper & El Bad**

**Note** - Known issue: If you click *within* the Sensitivity Randomizer window when open, this can sometimes freeze your mouse until potentially a manual restart. A fix for this issue can be found in [4) Fix for Mouse Freeze Issue](#fix-for-mouse-freeze-issue).

## Overview

This tool generates smooth or step-like, randomized sensitivity multiplier curves around a baseline value using [Interception](http://www.oblita.com/interception.html) and [Armadillo](http://arma.sourceforge.net/) in C++. The goal of this tool is to begin to understand the effects of varying mouse sensitivities while aim training.

Ideally, this is something to occasionally **_train_** with, but not to have active during actual gameplay. While there's no concrete proof to back this up, we feel smoothly varying sensitivity might increase reactivity and help train fine motor movements in a way that's superior to keeping with a single sensitivity. Thus, the target audience will be people who play aim trainers such as [Kovaak's FPS Aim Trainer](https://store.steampowered.com/app/824270/KovaaKs_FPS_Aim_Trainer/).

## Instructions

### *1) Download the program*

* Clicking the download link below will give you access to **_all_** the files needed to successfully run this tool.

| [Download Here!](https://github.com/Whisperrr/SensitivityChanger/releases/download/v0.5/SensitivityRandomizer-v0.5.zip)|     
| ------------- |

* You may also download the *SensitivityRandomizer.zip* file directly from my [releases](https://github.com/Whisperrr/SensitivityRandomizer/releases).  
* Or clone/download the repo from my [GitHub](https://github.com/Whisperrr/SensitivityRandomizer).

### *2) Install Interception*

Once you extract the ZIP file, you must first install Interception. More on what that is in the _Details_ section if you care.

The process is _very_ similar to Kovaak and Povohat's [InterAccel](http://mouseaccel.blogspot.com/2015/12/new-method-for-mouse-acceleration.html), thus some of the installation code/executables are borrowed from them.

1) Double click the *driver_install.bat* file from the extracted ZIP file (It will ask for Admin priviledges).
2) Install the Visual C++ Redistributable for Visual Studio 2015 from https://www.microsoft.com/en-us/download/details.aspx?id=48145 if you don't have it.
3) **Reboot**. Yes, you actually need to reboot because of first step, or it won't work.

Once this is done, you should be able to run the tool.

### *3) Run the program*

* Run the **_SensitivityRandomizer.exe_** file located in your extracted ZIP folder.
* Optional, although highly recommended: [Fix Mouse Freeze Issue](#fix-for-mouse-freeze-issue)

**Note:** The program will begin to generate a complete sensitivity curve. Your mouse may initially freeze for a few seconds while generating this curve. If you want to stop randomizing your sensitivity at any time, either press **Control+C** or exit the application manually. 

This program will look for a _settings.ini_ file that contains several key pieces of information that you can modify. If no settings file is found, it will use default values I've chosen. These components are:

* Type
* Baseline_Sensitivity
* Min_Sensitivity
* Max_Sensitivity
* Spread
* Smoothing
* Timestep (seconds)
* Runtime (minutes)
* Visualize
* Debug

The *Type* value determines whether you want your generated sensitivities to be *step-like* or *smooth*. It takes on two values: **0** (step-like) or **1** (smooth). Setting Type = **1** will result in a sensitivity curve similar to this **and behave exactly as previous iterations of the randomizer (v0.1-v0.4)**:
![](./Source/SmoothGraph.png)

whereas setting Type = **0** will result in something like this:
![](./Source/StepGraph.png)

The *Baseline_Sensitivity* value determines determines where you'd like to vary your sensitivity multiplier around. **This should almost always be set to 1**, as this means you'll vary your sensitivity around a value *1x* your current sensitivity value (aka still your current sensitivity).

The *Min_Sensitivity* and *Max_Sensitivity* values determine the largest and smallest multipliers that you want your sensitivity to reach. I usually keep Min_Sensitivity = **0.50** (half your default sensitivity), and Max_Sensitivity = **2** (twice your default sensitivity).

_Spread_ determines how fast/wide swings in sensitivities can happen. Counterintuitively, increasing the spread value will not _always_ increase how crazy your generated sensitivity curve is. Because we're attempting to create smooth curves, too much noise (no apparent patterns) will often not produce large variations around the baseline value. We'll be tweaking this in the future, but for now, I keep it at **0.6**. If you don't feel this is enough. I'd recommend actually _decreasing_ the value to, say, 0.1 to test.

_Smoothing_ (added in v0.3) determines, well, how smooth you'd like your randomization to be (given that you choose a *smooth* graph rather than *step-like*). The smoothing parameter can take on several values:

* 0: No smoothing performed (interesting option to say the least)
* 1: Low amount of smoothing
* 2: Medium amount of smoothing
* 3: High amount of smoothing
* 4: Very high amount of smoothing
* 5: [This smooth](https://www.youtube.com/watch?v=ZMByI4s-D-Y)

I have this value set to **2** by default.

*Timestep* (added in v0.5) allows you to control how **often** your sensitivity changes when using the **step-like** sensitivity randomization option. By default, I have this set to **10**, meaning your sensitivity will change once every *ten* seconds.

**Note:** If you set _Type = 1_ (generating a smooth curve), you **won't** be able to modify the timestep variable. It will be forced at a very small value (0.001) to ensure the generated sensitivity curve is actually _smooth_. To be able to modify this variable, you'll need to first have _Type = 0_ set above to specify you no longer want a smooth sensitivity curve.

*Runtime (minutes)* - Determines how long you want your program to run for before you need to restart. I keep this value at **30** (for 30 minutes).

*Visualize* allows you to visualize the sensitivity curve the tool generates. By default, this is set to **0** (so no visualization), however setting it to 1 will generate a .txt file called "sens_list.txt". For now, I've included a script called _visualize.py_ that can be run to visualize this output.

**Note:** You'll need to first have [Python](https://realpython.com/installing-python/) _and_ [matplotlib](https://matplotlib.org/3.1.1/users/installing.html) installed.

*Debug* lets you see a live value of your current sensitivity multiplier and a live percentage of time left before needing to restart. By default this is set to **1**, however if you're experiencing any performance issues, I'd recommend setting this to 0.

***

Also, you can press __"P"__ on your keyboard to pause/unpause the program (toggle). So if you find a particular sensitivity you like (or hate for that matter), you can now pause to practice it for a while. With the "Debug" option set to 1, you'll be able to see a _PAUSE_ icon appear.

***

## Fix for Mouse Freeze Issue

Until a better solution can be found, I've created a [YouTube video](https://youtu.be/0Gg1Gep0CK8) that walks you through a fix for this issue (disabling QuickEdit mode in the console). You can also follow the steps below:

1. Double-click SensitivityRandomizer.exe
2. Right-click the title bar at the top of the window (can be seen in the video)
3. Navigate to *Defaults*
4. Uncheck  *QuickEdit Mode*
5. Restart the program

***
***

## Details

If you'd like to know more about how the program actually works, please see [this Reddit post](https://www.reddit.com/r/FPSAimTrainer/comments/cve6oi/tool_for_smoothly_randomizing_sensitivity/) where I describe exactly that! If you have any issues running the program, you can:
* Message **El Bad#5788** or **Whisper#4442** on Discord.
* Join the official [FPS Aim Trainer Discord](https://discordapp.com/invite/Z8hGxnM).
