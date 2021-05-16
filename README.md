# Gm9FullScript
3DS GodMode9 script that does nearly everything you can do with GodMode9

IMPORTANT: Some of this script's functions, are inspired from other scripts (GM9Megascript; CTRTransfer-Type D9).

I recommend reading this before using the script.

First, I'll explain some script's special functions that make it more safe and noob-friendly

CONFIRMATION

Before running some functions that are particulary delicate, the script asks another confirmations by pressing START, to avoid user to casually pressing A fast and running the function without being sure of what he is exactly going to do

WARNING WHEN DOING DELICATE STEPS

When the script is editing crucial files in the NAND, it warns the user saying "Please do not turn off the power now" in the upper screen.
As soon as the script cleared the delicate step, that will disappear.
With this, user knows exactly when the scripts is doing delicate steps.

EMERCENCY ROUTINES

This should not happen, but if the script enters emercency mode, says "Emercency Mode is Active.
DO NOT TURN OFF THE CONSOLE NOW" in the upper screen to make the user know that something went really, really wrong.


Now, let's see what the script actually does.

CONSOLE'S TYPE CHECK

When launched, the script checks if the console is a devkit, if yes, it prevents itself from running because this script is retail consoles only.

GODMODE9 VERSION CHECK:

When launched, the script checks if the running GodMode9 Version is 1.9.1 or higher, if not, it prevents itself from runnning to avoid unexpected errors due to missing commands, the script also explains to user how to update GodMode9 to use the script.

