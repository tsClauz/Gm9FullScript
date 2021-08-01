# Gm9FullScript
3DS GodMode9 script that does nearly everything you can do with GodMode9

IMPORTANT: Some of this script's functions, are inspired from other scripts.

I recommend reading this before using the script.


First, I'll explain some script's special functions that make it more safe and noob-friendly

----------------------------------------------------------------------------------------------------------------------------------------------------------------------

CONFIRMATION

Before running some functions that are particulary delicate, the script asks another confirmations by pressing START, to avoid user to casually pressing A fast and running the function without being sure of what he is exactly going to do

----------------------------------------------------------------------------------------------------------------------------------------------------------------------

WARNING WHEN DOING DELICATE STEPS

When the script is editing crucial files in the NAND, it warns the user saying "Please do not turn off the power now" in the upper screen.
As soon as the script cleared the delicate step, that will disappear.
With this, user knows exactly when the scripts is doing delicate steps.

----------------------------------------------------------------------------------------------------------------------------------------------------------------------

EMERCENCY ROUTINES

This should not happen, but if the script enters emercency mode, says "Emercency Mode is Active.
DO NOT TURN OFF THE CONSOLE NOW" in the upper screen to make the user know that something went really, really wrong.


Now, let's see what the script does when launched.

----------------------------------------------------------------------------------------------------------------------------------------------------------------------

CONSOLE'S TYPE CHECK

When launched, the script checks if the console is a devkit, if yes, it prevents itself from running because this script is retail consoles only.

----------------------------------------------------------------------------------------------------------------------------------------------------------------------

GODMODE9 VERSION CHECK:

When launched, the script checks if the running GodMode9 Version is 1.9.1 or higher, if not, it prevents itself from runnning to avoid unexpected errors due to missing commands, the script also explains to user how to update GodMode9 to use the script.

----------------------------------------------------------------------------------------------------------------------------------------------------------------------

Now, i'll explain all the script functions.
I'll explain the function in order to make it understandable to everyone, and then i'll give a little bit more in-depth explanation.

----------------------------------------------------------------------------------------------------------------------------------------------------------------------

SYSNAND BACKUP

Creates a NAND backup.

This makes a copy of sysNAND's nand_minsize.bin in the gm9/out folder called "(DATESTAMP)_(SERIAL)_sysnand_00.bin"

----------------------------------------------------------------------------------------------------------------------------------------------------------------------

EMUNAND BACKUP 

Creates and emuNAND backup

This makes a copy of emuNAND's nand_minsize.bin in the gm9/out folder called "(DATESTAMP)_(SERIAL)_emunand_00.bin"

----------------------------------------------------------------------------------------------------------------------------------------------------------------------

SAFE SYSNAND RESTORE

Restores a NAND backup with 0 brick risk (if NCSD is intact)

A safe restore has a high chance of bricking a non exploited console. 
Because of this, the script prevents the function from running if the console is not exploited or if it is running from ntrboot entrypoint. (when in ntrboot, there is absolutely no way of knowing if the console is exploited or not).

The safe restore, makes the user select the NAND backup they would like to restore, it mountes the NAND backup, then it checks if the NAND's NCSD differs beetwen image and local, if yes, it injects the backup's "nand_hdr.bin" to sysNAND's "nand_hdr.bin" (requires higher permissions due to crucial parts being touched). Then injects these parts of the NAND backup to sysNAND:

ctrnand_full.bin (the CTRNAND partition)

twln.bin (3DS' TWL mode)

twlp.bin (TWL photo)

bonus.bin (bonus drive) 

----------------------------------------------------------------------------------------------------------------------------------------------------------------------

FULL SYSNAND RESTORE

Restores a NAND backup by fully injecting it to sysNAND, it's more risky, but needed in some cases.

A full restore is risky, if done with a corrupted NAND backup or with an emuNAND backup image, it can brick the console.
For safety reasons, the script will prevent the function from running if the console isn't running from ntrboot entrypoint, as it is the only way to unbrick the console in case of a brick (excluding hardmod, which in 2021 is a pretty died method).
Then the script makes the user select a NAND backup, verify it to check if it's corrupted, mounts it, and then injects the backup's "nand_minsize.bin" to sysNAND's "nand.bin"

----------------------------------------------------------------------------------------------------------------------------------------------------------------------

EMUNAND RESTORE

Restores an emuNAND backup, emuNAND is not vital, so no brick risk here.

The script makes the user select a NAND backup, mounts it, and then injects the backup's "nand_minsize.bin" to emuNAND's "nand.bin".
No checks here, as the emuNAND is not vital.

----------------------------------------------------------------------------------------------------------------------------------------------------------------------

TRANSFER SYSNAND TO EMUNAND
EmuNAND restore, but we use as backup image the sysNAND.

The script injects the sysNAND's "nand_minsize.bin" to emuNAND's "nand.bin"

----------------------------------------------------------------------------------------------------------------------------------------------------------------------

TRANSFER EMUNAND TO SYSNAND

SysNAND safe restore, but we use as backup image the emuNAND.

This function has the some effect of a Safe sysNAND restore, but we use as NAND backup the emuNAND.

A safe restore has a high chance of bricking a non exploited console. 
Because of this, the script prevents the function from running if the console is not exploited or if it is running from ntrboot entrypoint. (when in ntrboot, there is absolutely no way of knowing if the console is exploited or not).

Then, the script injects this parts of emuNAND to sysNAND:

ctrnand_full.bin (the CTRNAND partition)

twln.bin (3DS' TWL mode)

twlp.bin (TWL photo)

----------------------------------------------------------------------------------------------------------------------------------------------------------------------

CHECK EMMC STATUS

Checks the EMMC status for hardware problems. Use this only in emercency cases.

This function is mode for unbrick purposes, it is not for the faint of hearth
This function does some write tests to sysNAND's "nand.bin" and checks it for hardware problems.
This function is the most delicate in the script.
Please use this only if every other unbrick attemp failed or didn't fix your console.
To make sure user knows what he is doing, the script asks to insert a security code before proceeding (the the konami code)

----------------------------------------------------------------------------------------------------------------------------------------------------------------------

CTRTransfer

Performs a CTRTransfer to sysNAND by using a prefabbrcated backup image.

First of all, the script asks to user to select a CTRTransfer image, it mounts it and it checks if CTRNAND image is corrupted or incomplete, is yes, the scripts prevents the CTRTransfer from being performed.
Then the script checks if the CTRTransfer image's type (O3DS or N3DS) is the some type of the console, if not, the scripts prevents the CTRTransfer from being performed.
Then the script makes a backup of the console's tickets (ticket.db) named "ticket.bak" to the RAMDRIVE
Then the script deletes these folders in the CTRNAND 

dbs

title

Then the script injects these parts of the CTRTransfer image to CTRNAND

dbs/* (everything inside the dbs folder)

title/* (everything inside the title folder)

Then the scripts moves the "ticket.bak" file from the RAMDRIVE to the "dbs" folder.

----------------------------------------------------------------------------------------------------------------------------------------------------------------------

CTRTRANSFER D9 TYPE

Performs a CTRTransfer to sysNAND using a method inspired by the old Decrypt9 method of flashing the entire partition, the script tries also to preserve important user informations.

This function is inspired by the old Decrypt9 CTRTransfer method that flashes the entire ctrnand_full.bin and restores only the essential files.
This script try to preserve as much as user files as it can
First of all, the script checks if the essential files backup exists, if not, it prevents the function from running.
Then the script checks if the CTRTransfer image's type (O3DS or N3DS) is the some type of the console, if not, the scripts prevents the CTRTransfer from being performed.
Then the script copies these files and folders to RAMDRIVE:

data (folder)

movable.sed

LocalFriendCodeSeed_B


Then the scripts injects the entire CTRTransfer image to sysNAND's ctrnand_full.bin
Then the script restores this files from the backup that has been made

data (folder)

movable.sed

LocalFriendCodeSeed_B

----------------------------------------------------------------------------------------------------------------------------------------------------------------------

MAKE CTRNAND TRANSFERABLE IMAGE

Makes a .bin image wich can be used to perform a CTRTransfer.

This function copies the "ctrnand_full.bin" file to gm9/out calling it "(REGION)_ctrtransfer_(OLD/NEW)3ds.bin", mountes it, and removes from the image useless Luma3DS files.

----------------------------------------------------------------------------------------------------------------------------------------------------------------------

INSTALL BOOT9STRAP

Installs Boot9Strap to sysNAND safely, security checks and emercency routine included.

First, this function checks is the sha value of the B9S FIRM is the .sha file, then it checks if the B9S FIRM sha is precisely 79C68585B4BA1D7C4A91B858861553E768C6576B92E303810B33219736B3598B, to avoid user blindly installing old B9S FIRMS; if one of these checks fails, the operation is cancelled.

Then the script checks if the console is an N3DS, if yes, it checks if the Sector0x96 is corrupted, if yes, it searchs for a clean secret_sector.bin in the boot9strap folder, if it doesn't find it, the process is aborted to avoid a brick.

Then the script backs up FIRM0, FIRM1 and Sector0x96, if one of this backing up process fails, the operation is cancelled.

Then the script copies the B9S FIRM to FIRM0 and FIRM1, if one of these operation fails, the script jumps to the emercency routine.

If the console is an O3DS, it copies the Sector0x96 to boot9strap folder because we need it there for the next step.

Then the script copies the secret_sector.bin to Sector0x96, if the process fails the script checks if the console is an N3DS, if yes it jumps to the emercency routine

Then the script checks the sha of the newly installed files, if one of the checks fails, the script jumps to emercency routine.

The emercency routine, if triggered, restores the FIRM0, FIRM1, and Sector0x96 backups to sysNAND, reverting it at it's earlier state to avoid a brick; if this process fails, the script tells to user what to do.

----------------------------------------------------------------------------------------------------------------------------------------------------------------------

CHECK BOOT9STRAP VERSION

Shows wich Boot9Strap version does the console have

This function mountes FIRM0 and checks the sha of the header.bin file, wich determines the Boot9Strap version

----------------------------------------------------------------------------------------------------------------------------------------------------------------------

SAFETY CHECK

Boots the console stock mode to see if it will work properly after B9S uninstall

This function mountes the NATIVE_FIRM NCCH (nand/title/00040138/?0000002/????????.app), and boots the .firm file booting the stock mode 

----------------------------------------------------------------------------------------------------------------------------------------------------------------------

UNINSTALL BOOT9STRAP

Removes Boot9Strap and deletes Luma3DS related files in the NAND

Then the script checks if the console is an N3DS, if yes, it checks if the Sector0x96 is corrupted, if yes, it searchs for a clean secret_sector.bin in the boot9strap folder, if it doesn't find it, the process is aborted to avoid a brick.

Then the script mountes the NATIVE_FIRM NCCH (nand/title/00040138/?0000002/????????.app), and copies the .firm to gm9/out

Then the script copies the NATIVE_FIRM to FIRM0 and FIRM1 uninstalling cfw

If the console is an O3DS, it copies the Sector0x96 to boot9strap folder because we need it there for the next step.

Then the script copies the secret_sector.bin to Sector0x96.

Then the script deletes Luma3DS files in the CTRNAND.

----------------------------------------------------------------------------------------------------------------------------------------------------------------------

DUMP CARTRIDGE TO .CIA

Dumps the title in the cartridge that is inserted as a .cia file, ready to be installed.

This function builds a .cia file on the .trim.3ds file found in the cartridge drive to gm9/out.

----------------------------------------------------------------------------------------------------------------------------------------------------------------------

DUMP CARTRIDGE TO .3DS

Dumps the title in the cartridge that is inserted as a .3ds encrypted file, wich can be installed with GodMode9, or converted as .cia file with 3dsconv or GodMode9.

This function copies the .3ds file found in the cartridge drive to gm9/out

----------------------------------------------------------------------------------------------------------------------------------------------------------------------

DUMP CARTRIDGE TO .NDS

Dumps the title in the cartridge that is inserted as a .nds file

This function copies the .nds file found in the cartridge drive to gm9/out

----------------------------------------------------------------------------------------------------------------------------------------------------------------------

DUMP FIRM0.BIN

Dumps the FIRM0.bin file to gm9/out

----------------------------------------------------------------------------------------------------------------------------------------------------------------------

DUMP FIRM1.BIN

Dumps the FIRM1.bin file to gm9/out

----------------------------------------------------------------------------------------------------------------------------------------------------------------------

DUMP ESSENTIAL.EXEFS

Dumps the essential.exefs file is it exists to gm9/out

----------------------------------------------------------------------------------------------------------------------------------------------------------------------

DUMP SECUREINFO_A

Dumps the SecureInfo_A file to gm9/out

----------------------------------------------------------------------------------------------------------------------------------------------------------------------

DUMP MOVABLE.SED

Dumps the movable.sed file to gm9/out

----------------------------------------------------------------------------------------------------------------------------------------------------------------------

DUMP BOOT9.BIN

Dumps the boot9.bin file to gm9/out

----------------------------------------------------------------------------------------------------------------------------------------------------------------------

DUMP OTP.BIN

Dumps the otp.bin file to gm9/out

----------------------------------------------------------------------------------------------------------------------------------------------------------------------

DUMP LOCALFRIENDCODESEED_B

Dumps the LocalFriendCodeSeed_B file to gm9/out

----------------------------------------------------------------------------------------------------------------------------------------------------------------------

DUMP AGBSAVE.BIN

Dumps the agbsave.bin file to gm9/out

----------------------------------------------------------------------------------------------------------------------------------------------------------------------

DUMP NNID.BIN

Dumps the nnid.bin file to gm9/out

This function dump the nnid management file in CTRNAND (nand:/data/(SYSID0)/sysdata/?0010038/00000000) to gm9/out renaming it to "nnid.bin"

----------------------------------------------------------------------------------------------------------------------------------------------------------------------

INJECT FBI TO H&S

Injects the fbi.cia file to Health & Safety app.

First, the script makes the user select the fbi.cia file.

Then, the script checks the console's region to know where to find the H&S .app.

Then, the script makes two backups of the H&S .app (one to the inject, one to restore it when needed)

Then, the script mountes the fbi.cia file, and inject some parts of it to the H&S .app backup

Then the script encrypts the H&S .app backup and injects it to the real H&S backup

----------------------------------------------------------------------------------------------------------------------------------------------------------------------

RESTORE H&S

Restores the H&S app from the fbi injection

First, the script checks the console's region to know where to find the H$S .app.

Then the script injects the H&S backup made at the time of injection, and injects it to the H&S .app.

----------------------------------------------------------------------------------------------------------------------------------------------------------------------

SETUP LUMA3DS TO CTRNAND
