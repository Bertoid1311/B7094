B7094 is a Windows-based emulator for the IBM 7094 mainframe computer from the 1960s.

## Basic usage

If you're a "casual" user, and running Windows, just:

- Download the B7094V34A.zip distribution archive

- Extract it into a new folder

- Run either B7094.32.exe or B7094.64.exe in the created "Bin" sub-folder

- Click on the options displayed to select from the many demonstrations available.

B7094 makes no changes to the Windows registry or any other part of the system other than its install folder. Deleting the distribution archive and the install folder will completely remove B7094 from your system.

There is a YouTube video [here](https://www.youtube.com/watch?v=4xaBS6pWrG0) that shows the use and operation of B7094 (an earlier release, but the basic operation is the same).

## Additional details

This emulator has a graphical interface with separate windows for the main console with all its flashing lights, the card reader, the line printer and all the tape drives, as well as several other specialized windows. The console is not, alas, a faithful recreation of an IBM 7094 in photo-realistic detail; it's a schematic representation modelled loosely on the console of an [IBM 7044](https://www.gettyimages.com/detail/news-photo/woman-at-a-design-model-of-the-operators-console-of-the-new-news-photo/107644558).  If you want photo-realism, check out Roberto Sancho Villa's work [here](https://github.com/rsanchovilla/SimH_cpanel).

B7094 can run two different preserved versions of the IBSYS operating system, and can compile and execute programs written in FORTRAN II and the Fortran Assembly Program (FAP) under the FORTRAN II subsystem; as well as FORTRAN IV, COBOL, and a Macro Assembly Program (MAP) under the IBJOB subsystem.  All the required IBM 7094 software to do that is included in the distribution.

The source of B7094 is included in the distribution, to allow you to modify or enhance the program and rebuild it. You'll need to install Lazarus/Free Pascal to do this, the 32-bit and/or 64-bit versions. The current B7094 v3.4A release was built using the newest (as of the end of last year) releases of these development tools (Lazarus 2.2.4, 28 Sept 2022; Free Pascal 3.2.2, 20 May 2021).

There is another YouTube video [here](https://www.youtube.com/watch?v=W5Blz5-chSU) that shows how to compile B7094 from the sources.

The 32-bit executable will still run on Windows XP, and both executables will run on any 64-bit version of Windows from Vista up through the present. There are Windows dependencies "baked in" to the code, but the program can be run on Linux using Wine (with a few non-fatal quirks), and even under Wine 8.x on x86 MacOS (the 64-bit executable has been tested on 'Catalina' in a VM). The B7094V34A.tgz archive is provided solely for the convenience of the Linux user; its contents are the same as B7094V34A.zip.

The second set of archives here (labelled "reloc_scripts_*") are packages containing bash shell scripts and other supporting utilities (hence requiring a Unix-y environment to run, either Linux or something like Msys2 or Cygwin under Windows) that can process Peripheral Punch tapes generated by the IBSYS compilers and extract and format the data required to create relocatable binary jobs (i.e., programs that can be re-run without recompiling them every time).  There are instructions on how to do this in the included README.txt file.  But note that these are provided for **advanced** users.  The relocatable jobs in the demo scripts have already been processed with these tools.

## Changes since the last (v3.3B) release

B7094 is now hosted at GitHub; the earlier release was hosted at FossHub.

This new version fixes some long-standing bugs in the user interface:

- The Editor is more useful than before; you can now save files in addition to just opening and running them. It is also possible to just type script commands into a new Editor window and run them immediately, without having to explicitly save the file.

- The Stops and Core View windows are now fully functional, which provides some rudimentary debugging capabilities for programs being run on the emulated machine.

There are also some new capabilities in the emulation itself:

- The scripted demos have been expanded to allow choosing between two alternative versions of IBSYS: the originally-included two-tape ASYS1/ASYS8 system recovered by Paul Pierce a quarter-century ago, and the single-tape "Aerojet-General" KSYS61 version (also originally recovered by Paul Pierce).

- Using the KSYS61 system, FORTRAN II now supports "chaining", which allows the early-60s "Structural Engineering System Solver" program (STRESS III, from MIT, originally transcribed from a listing on bitsavers by Richard Cornwell and later further proofread by others), to build and run to completion with sample input data from the STRESS user's manual downloadable from MIT.

- Sample programs can now be run in relocatable binary form (for FORTRAN II, in KSYS61 only; for IBJOB languages, in either version of IBSYS). Instructions (and Unix-y utilities) for extracting a binary job from the "Peripheral Punch" tape generated by the compiler, are provided in the separate "reloc_scripts_*" archives. The "reloc_scripts_Msys2.zip" archive is specifically targeted for the Msys2 environment on Windows. The "reloc_scripts_Linux.tgz" archive is targeted for Linux, or for Cygwin on Windows. The bash scripts in the former contain DOS-style (CRLF) line endings, while those in the latter contain Unix-style line endings. Additionally, the contents of "reloc_scripts_Msys2.zip" are ready-to-use "out of the box", whereas "reloc_scripts_Linux.tgz" requires first running a script to rebuild a couple of "helper" utilities. See the included README.txt file for more information.

- The emulator demo scripts can be run either in "verbose" mode, which provides lots of explanation and references; or "silent" mode, which skips all the verbiage and just presents straightforward option menus on the minimum number of click-through screens.

- The demos have been reorganized into more logical groups by "subsystem" -- either FORTRAN II (which provides FORTRAN II and the Fortran Assembly Program) or IBJOB (which provides FORTRAN IV, COBOL, and a Macro Assembly Program).  A couple of the utility demos from the earlier release have been retained: the IBEDT editor used to maintain IBSYS itself (in the demo, used just to copy and list the contents of a system tape), and the IBJOB "Librarian" used to maintain the IBLIB subroutine library (here just used to list and cross-reference the contents of the library).  A couple of stand-alone diagnostic programs -- one loaded from the card reader the other from tape -- are still included (though neither one runs completely error-free).

- A number of new script commands have been added to support the creation of card deck and tape images for relocatable binary jobs.

- Since it doesn't really make any sense to display register and memory values using hexadecimal representations for a 36-bit machine using 6-bit bytes (whereas it makes perfect sense to do so for a machine whose registers are multiples of 8-bit bytes, such as the IBM System/360 and nearly all modern machines), the Oct/Hex toggle buttons previously present on the Console, Reader, and CoreView windows have been eliminated.

B7094 does not support the range of peripherals (and pass the array of diagnostics) that Rich Cornwell's SimH-based i7090 does; neither does it support the spectacular photo-realistic panels created by Roberto Sancho Villa. And it can't run CTSS.  But B7094's graphical interface still provides some visual entertainment, and it's possibly easier than the more sophisticated emulators for a newcomer to get started with, while still providing some significant capabilities.

## About the "Tape Viewer"

The Tape Viewer has been thoroughly re-worked:

- The hexadecimal column in the binary-mode display (that previously showed the P7B formatting of a tape image) has been eliminated, and replaced by a new character column showing machine words interpreted as if they contain six characters using internal BCD character codes, rather than the usual external (or "alternate") BCD character codes used on a BCD tape. This column always contains gibberish for a "pure" BCD tape, but on a hybrid BCD and binary tape (such as a job tape containing a program in relocatable binary form), or even on a "pure" binary tape (such as an IBSYS tape), this column sometimes shows human-readable text that can be of interest.

- There is now a "sliding window" in the Tape Viewer, where arbitrary "From Byte" and "To Byte" positions can be selected for display. The "Redisplay" button causes the chosen limits to take effect (if "From Byte" is blank, it defaults to 0; if "To Byte" is blank, it defaults to either the last position on the tape or to "From Byte" plus a maximum window size, whichever is lower). "Clear" clears "From Byte" and "To Byte". "Use Whole Tape" resets the limits from 0 up to either the actual size of the tape or the maximum window size, whichever is lower. The maximum window size is large enough to be able to see all of SYSOUT.BCD for 
all the demos without the user having to increase the "From Byte" and click "Redisplay" to see the end of the tape. All the labels and buttons having to do with the adjustable view window are colored purple, to visually group them together.  The Tape Viewer resynchronizes the word framing when starting the display from an arbitrary point on the tape.

- This is not new, but it's worth pointing out: you can save the text in the Tape Viewer window by clicking the 'Save' pushbutton at the top left of the window. There won't be any acknowledgment of the button press, but you'll get a "dump" file in the ..\Output directory with the extension '.DMP', named according to the tape image file that was being displayed (e.g., 'SYSOUT.BCD.DMP' or 'SYSIN.BCD.DMP').  The dump file name will always reflect the format (and hence the extension) of the tape image that was being displayed in the Tape Viewer (either '.BCD' or '.BIN') but in fact the text in the Tape Viewer window will be saved in whatever mode the Tape Viewer is currently displaying: either 'BCD' or 'Binary'.

## Additional advanced details

A scripting language (in files with extension .EC7 -- "Execute Commands for the B7094") serves to configure the emulator, load IBSYS, and submit programs (in a job stream including the necessary IBSYS control cards) via the emulated card reader or a designated tape drive. These scripts serve the same function as the "do_ibsys.txt" and ".job" files used by the SimH-based i7090 and i7094, but they do not require typing a command line.  The canned demos in the Scripts directory are implemented by means of the EC7 scripting language (and utilize script commands to display text, display option menus, advance to and return from a succession of screens, and call EC7 subroutines defined in the same script file). However, a user can run their own programs by embedding them (by means of an Include command) in a suitable EC7 file, which can then be opened and run from the built-in Editor.  Some simple, in-line "Xample_xxx.EC7" files are provided as models for doing this.  More sophisticated jobs (such as running relocatable binaries) can be constructed by examining the demo scripts (and utilizing the tools provided in a "reloc_scripts_*" archive).

Like Rich Cornwell's SimH-based i7090, B7094 expects to "see" the correct parity on tapes (odd for binary records, even for BCD ones). This is in fact necessary to be able to run relocatable binary jobs in FORTRAN II (with the KSYS61 version of IBSYS only). Tapes created on other emulators can be used with B7094 provided they are:

- in P7B format (originated by Paul Pierce: this is the default with Dave Pitt's s709, with SimH format being optional; while Rich Cornwell's i7090 and Bob Supnik's i7094 are the other way around, with SimH format the default, but P7B available as an option),

- have the correct parity (i7090 creates tapes with correct parity, and I believe i7094 and s709 do as well, and 3) use the "alternate" BCD coding for BCD records (the default for i7090 and i7094, optional for s709).

Likewise, tapes created by B7094 can be used on other emulators (whether or not the other emulators expect to "see" parity; i7090 does, I believe i7094 and s709 do not), if those emulators can:

- utilize tapes in P7B format tapes, either by default (s709) or optionally (i7090, i7094), 

- interpret BCD records using "alternate" coding (i7090 and i7094 do this by default; s709 can optionally do so).

B7094's "Tape Viewer" is a useful tool for examining the contents of any P7B tape: a small script can be created and run in the Editor to mount the tape, then clicking on the tape in the Tape Drives window will bring it up in the Tape Viewer.

Grateful acknowledgement is due to Richard Cornwell for providing some of the sample demo jobs, and for providing technical assistance in getting this new release operational. And of course to Al Kossow et al. for the bitsavers archive, without which many retro-emulators couldn't exist; to Bob Supnik, Dave Pitts, and Richard Cornwell for their work getting **really**-working IBM 709x emulators operational in the mid-late 2000s.  And to Paul Pierce, who got the ball rolling with his collection of tapes, without which there would be nothing to run on such emulators (well, apart from the CTSS software from MIT).

## Gotchas

Screen "real estate" and the large number of display windows.

- Initial window positions are read from the ..\Bin\B7094.INI file when the emulator starts up, and saved back to B7094.INI when the emulator shuts down (thus recording a changed window position if any window is moved while the emulator is running).  It is possible, for certain monitors, that a window might end up being "out of sight" for a given INI file.  In that case, you'd have to edit the INI file manually to bring the "lost" window back within range.

- There's no way to avoid a "cramped" window layout with a single monitor, with windows potentially obscuring other windows.  A partial remedy for this is that it's possible, from the Control Panel, to de-select (and re-select) windows for display by checking and unchecking the 12 checkboxes
corresponding to the windows.  For the canned demos, the script files normally control when windows are displayed and hidden -- for example, by bringing up the Tape Viewer when a job completes, and then automatically hiding it when you click 'Continue' (on the Scripter window that says
"Click 'Continue' to dismiss the tape viewer and redisplay the demo list.") But if you wanted, for example, to see the whole Operator Console window at the point when a job completes, you could de-select both the Tape Viewer and the Script Dialog windows.  Then you could re-select one (or both) of those windows and click 'Continue" on the Scripter window to resume the demo suite.

There are some things that can make the emulator seem to hang, but are just **very** slow:

- When the Tape Viewer is being displayed after finishing a job with a **lot** of output. (You'll encounter this when building 'STRESS III' from source. Be patient.)

- When you switch the Tape Viewer from BCD mode to BIN mode, when there's a lot of data on the tape.

- When you use the Tape Viewer on a system tape (KSYS61.BIN, for example). Especially if you load the system tape into the Tape Viewer in BCD mode and then realize you actually wanted BIN mode. You'll have to wait a while!

- When you're using B7094's tracing facilities. There are lots of things that can be traced: device accesses, register stores, core writes, instruction execution, etc.  These are all selected on the Log/Trace screen (that you can display by clicking the 'Trace' checkbox on the Control Panel window). But be careful how you use this, if you don't want to slow things down unacceptably (either during the running of a "guest" program in the emulator or while waiting for the results of the tracing).  The most efficient way to use this is, in the Log/Trace window, to: 1) check the boxes in the 'Trace Record filters' section on the left to select the classes of items you want traced -- the fewer the "better", if you can narrow things down; 2) when the job finishes either 'Power Off' the emulator or click the 'Clear' pushbutton in the Log/Trace window.  You'll then be prompted 'Save current trace data?'. Click 'Yes' and a file ..\Output\B7094.TRC will be written (overwriting one that's already there, if there is one). The saving of the trace file can itself take a **bit** of time.

  But the Log/Trace window also has a 'Trace Display filters' section on the right, and this allows you to filter and display in the window anything that's been recorded as a result of making the selections on the left (you check the desired checkboxes on the right, and then click the 'Display' pushbutton). But this can be a big annoyance if there's a lot of trace data to be filtered for display (examine the 'Lines:' counter above the 'Display' pushbutton to see if this might be the case). This process of filtering for "on-line" display can take a **long** time if there's a lot of trace data -- much longer than just saving all the trace data to a file and then using a text editor to view it.

Sometimes, the emulator really can get hung. This can happen if you try to 'Power Off' while a job is running (it's "safer" to click the 'Stop' button on the Operator Console window and **then** click 'Power Off'.

If the emulator hangs, or if something is just taking more time than you care to wait for, I'm afraid there's nothing for it but to kill the process in the Task Manager.

## About the mainframe

The IBM 7094 computer was a commercial 36-bit (6-bit byte) "scientific" computer (with 15-bit addresses, encompassing 32K words) that was produced (beginning as the model 7090; the 7094 was a slightly enhanced version) starting in 1959, and withdrawn from sale in 1969.  While a few installations (e.g., at MIT) remained in service into the 1970s, by the late 60s many customers were switching over to the System/360 series (a 32-bit, 8-bit-byte architecture touted as being "universally" applicable to both commercial and scientific tasks, with a greatly expanded address space).  The 7094 was a member of the "7000 series", which also included commercial machines such as the 7070 and 7074 (architecturally dissimilar to the 7090 and 7094, but sharing manufacturing technology and peripherals) and the quasi-experimental 7030 "STRETCH" supercomputer.  The 7090/7094 was preceded by the vacuum-tube "700 series", an architecturally-similar line of 36-bit machines beginning with the 704 in 1954 (on which both Fortran and Lisp were developed) up through the 709 in 1958).  The machines introduced in 1959 featured IBM's first generation of discrete-transistor circuitry.

While the machine supported random-access storage devices (disk and drum), and some installations utilized these (e.g., MIT's CTSS timesharing system), the more common "IBSYS" operating system made heavy use of magnetic tape and punched cards.

You can read some amusing anecdotes about the IBM 7094 by clicking on the last option of B7094's initial demo window.
