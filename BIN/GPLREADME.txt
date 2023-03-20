File:       GPLREADME
Program:    GPL/TIMODE Interpreter for Geneve OS(MDOS) 2.0 and above
Version:    7.40 compiled 12 March 2023
Copyright:  (c)1994-2023 by 9640News and Contributors
Contact:    InsaneMultitasker or 9640News, at AtariAge.com
=====================================================================

GPL is a TIMODE (/4a) interpreter that allows the Geneve user to emulate
most functionality of the /4A.  This includes using 'dumped' cartridge
files (in GRAM Kracker format) and most existing /4a software

LIMITATIONS:
------------
GPL does not and cannot replace special TI cartridges such as the FinalROM,
FinalGROM, UberGROM, Superspace II.  Some device functionality requires a
mode called 'rompage' that exposes the peripheral expansion bus for programs
needing direct access to the card. Hardware that might benefit from this
mode includes the Myarc HFDC, SCSI, IDE, TIPI, SIDBlaster, and MBP cards.

Programs that require direct scan of the /4a keyboard will not function as
there is no mechanism to emulate the 9901 direct scan process.


PREPARATION:
------------
To use this update, you must first copy the program "GPL" over your
existing file. Files GPM, GPN, GPO, GPP,etc contain the /4a ROM and GROMs
for your particular configuration.  You do NOT need to copy GPM,N,O,P though
they are provided here for convenience and initial setup.

There are two typical variants of the GPL,M,N,O,P setup:

       1. GPL   - 80 Column menu replaces BASIC GROMs and title screen
       2. MYGPL - Standard title screen w/BASIC GROMs

Variant #1 has been the more commonly used option, unless BASIC is desired

**NOTE: In all cases, the "GPL" file is the same (just renamed)


USAGE:
=======
GPL can only be run via the Geneve OS command line or batch file.

To invoke GPL, one must first tell the OS to enable the TI mode interpreter
This is done with a batch file and one of the following commands:

       TIMODE   - Compatible with all OS versions; reserves the most memory
                  and is a necessity to run MyWord.
       TIMODE2  - Secondary mode in MDOS 7.xx and above; does not reserve
                  the extra 64K required for MyWord. Suitable for most
                  users. RECOMMENED for most usage.

This command may be placed in your AUTOEXEC file to be run at startup or
more commonly, in its own batch file that you execute with the prefix "&"

Create a DV80 file called TI2:
       TIMODE2
       A:GPL

Execute from the command line:
       &TI2

The above will perform a warm restart, execute batch file TI2, which will
then enable TI Mode and launch GPL from A:

You may also start a cartridge by appending the cartridge filename after
the GPL program name as follows:

       GPL A:XB          Would load GPL which in turn would load and start XB

Starting a cartridge in this manner bypasses the GPL Title Screen and its
options.  To return to the GPL title screen, press SHIFT-SHIFT-CTRL.


================
GPL TITLE SCREEN
================

Once GPL is loaded (provided you did not auto-start a cartridge) you will be
presented with the GPL title screen: version and copyright information and
available configuration options.

The special key combination SHIFT-SHIFT-CTRL is used to return to this title
screen once you enter /4A mode. This key sequence does NOT close open files
and is analagous to turning off the /4A. (Note: this sequence will reset the
Geneve if used from the command line mode)

Press <ENTER> to start the TI mode interpreter or ESCAPE to return to the OS.


1. Load a cartridge
Type the path and filename of a cartridge you wish to load. TI and Geneve OS
style paths are acceptable. The interpreter will show the load process and
inform you of an incorrect/unsupported file.

2. Protect/Unprotect 6000 and 7000 memory banks.
F1 and F2 allow you to protect and unprotect the simulated ROM/RAM at 6000/7000

3. Clear cartridge space
F3 allows you to reset the memory in preparation for loading another cartridge

4. GPL Speed
The GPL interpreter runs at Geneve speed, 5, which is faster than the TI. You
can slow down the interpreter by selecting speeds 1,2,3,4,5. The effect is
not linear and depends on where programs load and how they operate.  Speed 5
is usually acceptable (and desired) however, games and programs that rely
upon timed loops often need to be slowed down.

5. GPL with ROMPAGE
Certain programs utilize features of peripheral cards that are not emulated
by the Geneve. This is mostly limited to "level 2" device routines, such as
used by Terminal Emulators and Disk Management Software

Using this option will allow you to access some peripherals as if they were
in a TI system.  GPL Speed sometimes needs to be reduced and some peripherals
will not work properly (TI Floppy controller, CorComp Floppy Controller) at
any speeds.

Some examples of software that might benefit from ROMPAGE:

  -- TIPI programs such as Telnet and TIPICFG must be run with ROMPAGE
  -- Hard drive device disk management software like DM2K, DU2K, MDM5
  -- Terminal Emulator upload/download functionality for hard drive devices
  -- Spell-It
  -- Programs requiring level 2 routines (>2x, >8x, >9X) for scsi/ide/tipi/etc

NOTE: The rompage function is in effect until you return to the GPL Title
      Screen with the special "shift-shift-ctrl" key combination. Once
      you return to this screen, rompage is disabled unless you select the
      option again.

6. HFDC DSK1 Emulation
The Myarc HFDC can emulate DSK1 via the hard drive DSK/DSK1 folder and via
the special EMULATE file. See the HFDC manual for more details.  The DSK1
emulate file may be REMAPped to devices 1-9, per the OS command



ENHANCEMENT LOG:
---------------
V7.40  12 March 2023
       - Added command line options GPL /R#V filename (CASE SENSITIVE)
         R - Rompage, with autostart or first entry
         # - speed 1-5
         V - 9938 Vr0 support for GPL VWTR (Scott Adam's Adventure 80 col)
         ? - help
       - Changed VR0 mask to support 80 column mode via GPL video routines
            use option V
       - Fixed speed issue identified by @mizapf; SPEED 1 did not work after
         starting the interpreter with either speed 4 or 5.
       - Cleanup in preparation for releasing the source code

V7.30  04 April 2021
       - Final cleanup and release

V7.22  28 February 2021
       - Added TIMODE to the title for continuity
       - Removed unsupported Winchester Personality code
       - Corrected the DSR powerup routines; master DSR is restored properly
         whenever the GPL title screen is invoked
       - Geneve mode maximum open file count is restored to 10 (from 3) upon
         exit to the OS. This only works with Geneve OS 7.xx and higher
       - GPL Title screen foreground/background colors now follow from the
         command prompt whenever started from 40 or 80 column TEXT modes.
       - Cleaned up GPLREADME
       - Identified future changes and items to review

V6.5   November 2002
       - Version number update only

V6.0   16 May 1998
       - Version number update only

V5.0   30 June 1996
       - DSK1 emulation is not F6 to make room for rompage
       - Added ROMPAGE option F5 for access to level 2/WDSx devices

N/A    1994-1996
       Programmers note:  The mapper page for GPL task page zero is stored
       at location >8100.  This was done to facilitate paging to Geneve
       mode for certain applications, such as the S&T BBS Geneve version of
       assembly which uses the master DSR for all file access.
       If you would like to learn how to do this please contact me for more
       information. This modification is also present in the GPL Cheater
       program.

V2.2   31 October 1994 <Halloween>
       - Copyright adjusted and updated to reflect 9640*News and Contributors
       - Added DSK1 emulation option F5
       - Updated keyscan per Jeff White's MDOS modifications
         (Note: also updated EXEC 2.11 with same routines)

V2.0   01 March 1994
       - Added ESCAPE key to exit from GPL to MDOS. Prior implementations
         only allowed for ctrl-alt-del, which had the habit of resetting the OS
       - Joystick line reversal corrected (Note: EXEC also updated)
       - Fire buttons are now independently processed
         GPL status bye was not being properly set/reset; Barrage and Tennis
         among programs that now work properly. Resolved issues with "missed"
         fire button activity.


V?.?   15 January 1994
       - Unified release for all MDOS versions
       - Enhanced GPL powerup routines
       - Clear/set V9938 registers to minimize problems with /4a programs
         that didn't "know" about registers beyond VR07. GPL now sets
         the color, sprite, and blink attribute registers

** End of file 28-Feb-2021, TT
