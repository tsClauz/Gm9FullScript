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


Now, let's see what the script does when launched.


CONSOLE'S TYPE CHECK

When launched, the script checks if the console is a devkit, if yes, it prevents itself from running because this script is retail consoles only.


GODMODE9 VERSION CHECK:

When launched, the script checks if the running GodMode9 Version is 1.9.1 or higher, if not, it prevents itself from runnning to avoid unexpected errors due to missing commands, the script also explains to user how to update GodMode9 to use the script.


Now, i'll explain all the script functions


SYSNAND BACKUP

This makes a copy of sysNAND's nand_minsize.bin in the gm9/out folder called "$[DATESTAMP]_$[SERIAL]_sysnand_00.bin"


EMUNAND BACKUP 

This makes a copy of emuNAND's nand_minsize.bin in the gm9/out folder called "$[DATESTAMP]_$[SERIAL]_emunand_00.bin"


SAFE SYSNAND RESTORE

A safe restore has a high chance of bricking a non exploited console. 
Because of this, the script prevents the function from running if the console is not exploited or if it is running from ntrboot entrypoint. (when in ntrboot, there is absolutely no way of knowing if the console is exploited or not).

The safe restore, makes the user select the NAND backup they would like to restore, it mountes the NAND backup, then it checks if the NAND's NCSD differs beetwen image and local, if yes, it injects the backup's "nand_hdr.bin" to sysNAND's "nand_hdr.bin" (requires higher permissions due to crucial parts being touched). Then injects these parts of the NAND backup to sysNAND:

ctrnand_full.bin (the CTRNAND partition)

twln.bin (3DS' TWL mode)

twlp.bin (TWL photo)

bonus.bin (bonus drive) 


FULL SYSNAND RESTORE

A full restore is risky, if done with a corrupted NAND backup or with an emuNAND backup image, it can brick the console.
For safety reasons, the script will prevent the function from running if the console isn't running from ntrboot entrypoint, as it is the only way to unbrick the console in case of a brick (excluding hardmod, which in 2021 is a pretty died method).
Then the script makes the user select a NAND backup, verify it to check if it's corrupted, mounts it, and then injects the backup's "nand_minsize.bin" to sysNAND's "nand.bin"


EMUNAND RESTORE

The script makes the user select a NAND backup, mounts it, and then injects the backup's "nand_minsize.bin" to emuNAND's "nand.bin".
No checks here, as the emuNAND is not vital.

TRANSFER EMUNAND TO SYSNAND

The script injects the sysNAND's "nand_minsize.bin" to emuNAND's "nand.bin"


TRANSFER EMUNAND TO SYSNAND

This function has the some effect of a Safe sysNAND restore, but we use as NAND backup the emuNAND.

A safe restore has a high chance of bricking a non exploited console. 
Because of this, the script prevents the function from running if the console is not exploited or if it is running from ntrboot entrypoint. (when in ntrboot, there is absolutely no way of knowing if the console is exploited or not).

Then, the script injects this parts of emuNAND to sysNAND:

ctrnand_full.bin (the CTRNAND partition)

twln.bin (3DS' TWL mode)

twlp.bin (TWL photo)


