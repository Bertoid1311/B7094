B7094 is a Windows-based emulator for the IBM 7094 mainframe computer from the 1960s.

## Basic usage

If you're a "casual" user, and running Windows, just:

- Download the B7094V34A.zip distribution archive

- Extract it into a new folder

- Run either B7094.32.exe or B7094.64.exe in the created "Bin" sub-folder

- Click on the options displayed to select from the many demonstrations available.

B7094 makes no changes to the Windows registry or any other part of the system other than its install folder. Deleting the distribution archive and the install folder will completely remove B7094 from your system.

There is a YouTube video [here](https://www.youtube.com/watch?v=4xaBS6pWrG0) that shows the use and operation of B7094 (an earlier release, but the basic operation is the same).

There is also more documentation in the "Docs" sub-folder of the install folder, in the following files:

- **B7094SourceReadMe.txt** lists the source files in the ..\Build\Source sub-folder of the install folder. Describes each window file in some detail, making it something of a "user's manual". Describes how to install and configure Lazarus/Free Pascal and rebuild the B7094 executables.

- **B7094ScripterSyntax.txt** describes in detail the command syntax of the EC7 script language.

- **B7094SuggestedManuals.txt** gives links to some useful manuals on bitsavers and elsewhere.

- **B7094DebuggingExamples.txt** gives a couple of simple illustrations of how the facililties in B7094 can be used to perform some (admittedly rudimentary) debugging of programs running on the emulated machine.

- **B7094ReadMe.txt** is similar to the information in this section of the GitHub README.

- **B7094WhatsNew.txt** describes the current status and history of the emulator (including its very earliest history).

## Additional details

This emulator has a graphical interface with separate windows for the main console with all its flashing lights, the card reader, the line printer and all the tape drives, as well as several other specialized windows. The console is not, alas, a faithful recreation of an IBM 7094 in photo-realistic detail; it's a schematic representation modelled loosely on the console of an [IBM 7044](https://www.gettyimages.com/detail/news-photo/woman-at-a-design-model-of-the-operators-console-of-the-new-news-photo/107644558).  If you want photo-realism, check out Roberto Sancho Villa's work [here](https://github.com/rsanchovilla/SimH_cpanel).

B7094 can run two different preserved versions of the IBSYS operating system, and can compile and execute programs written in FORTRAN II and the Fortran Assembly Program (FAP) under the FORTRAN II subsystem; as well as FORTRAN IV, COBOL, and a Macro Assembly Program (MAP) under the IBJOB subsystem.  All the required IBM 7094 software to do that is included in the distribution.

The source of B7094 is included in the distribution, to allow you to modify or enhance the program and rebuild it. You'll need to install Lazarus/Free Pascal to do this, the 32-bit and/or 64-bit versions. The current B7094 v3.4A release was built using the newest (as of September 2023) releases of these development tools (Lazarus 2.2.6, 05 March 2023; Free Pascal 3.2.2, 20 May 2021).

There is another YouTube video [here](https://www.youtube.com/watch?v=W5Blz5-chSU) that shows how to compile B7094 from the sources.

The 32-bit executable will still run on Windows XP, and both executables will run on any 64-bit version of Windows from Vista up through the present. There are Windows dependencies "baked in" to the code, but the program can be run on Linux using Wine (with a few non-fatal quirks), and even under Wine 8.x on x86 MacOS (the 64-bit executable has been tested on 'Catalina' in a VM). The B7094V34A.tgz archive is provided solely for the convenience of the Linux user; its contents are the same as B7094V34A.zip.

The second set of archives here (labelled "reloc_scripts_*") are packages containing bash shell scripts and other supporting utilities (hence requiring a Unix-y environment to run, either Linux or something like Msys2 or Cygwin under Windows) that can process Peripheral Punch tapes generated by the IBSYS compilers and extract and format the data required to create relocatable binary jobs (i.e., programs that can be re-run without recompiling them every time).  There are instructions on how to do this in the included README.txt file.  But note that these are provided for **advanced** users.  The relocatable jobs in the demo scripts have already been processed with these tools.

## Changes since the last (v3.3B) release

B7094 is now hosted at GitHub; the earlier release was hosted at FossHub.

This new version fixes some long-standing bugs in the user interface:

- The Editor is more useful than before; you can now 'Save' and 'SaveAs' files in addition to just 'Open'-ing and 'Run'-ning them. It is also possible to just type script commands into a 'New' Editor window and 'Run' them immediately, without having to explicitly save the file.

  This is not new, but it's worth pointing out here: if you're running the demo suite and at any point you click the 'End Demonstration Script' on a Scripter window, you can of course restart the demo suite by powering off the emulator and restarting it. But you can also, after having ended the demo, simply click the 'Editor' button on the Control Panel window to display the Text Editor window, click the 'Open' button on the Text Editor, navigate to the ..\Files\Scripts directory in the Open File dialog, select 'B7Demo.EC7' and click 'Open'. Then click 'Run' in the Text Editor to restart the demo suite. You could also 'Open' and 'Run' any other *.EC7 script (such as one of the "Xample_xxx.EC7' scripts in the same directory).

  Note: the Text Editor will "remember" that a file is open even after the emulator is powered off (the information is saved in the ..\Bin\B7094.INI file). If you want the Text Editor to "forget" a file, you have to explicitly 'Close' it.

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

## Additional advanced details

A scripting language (in files with extension .EC7 -- "Execute Commands for the B7094") serves to configure the emulator, load IBSYS, and submit programs (in a job stream including the necessary IBSYS control cards) via the emulated card reader or a designated tape drive. These scripts serve the same function as the "do_ibsys.txt" and ".job" files used by the SimH-based i7090 and i7094, but they do not require typing a command line.  The canned demos in the Scripts directory are implemented by means of the EC7 scripting language (and utilize script commands to display text, display option menus, advance to and return from a succession of screens, and call EC7 subroutines defined in the same script file). However, a user can run their own programs by embedding them (by means of an Include command) in a suitable EC7 file, which can then be opened and run from the built-in Editor.  Some simple, in-line "Xample_xxx.EC7" files are provided as models for doing this.  More sophisticated jobs (such as running relocatable binaries) can be constructed by examining the demo scripts (and utilizing the tools provided in a "reloc_scripts_*" archive).

Like Rich Cornwell's SimH-based i7090, B7094 expects to "see" the correct parity on tapes (odd for binary records, even for BCD ones). This is in fact necessary to be able to run relocatable binary jobs in FORTRAN II (with the KSYS61 version of IBSYS only). Tapes created on other emulators can be used with B7094 provided they are:

- in P7B format (originated by Paul Pierce: this is the default with Dave Pitt's s709, with SimH format being optional; while Rich Cornwell's i7090 and Bob Supnik's i7094 are the other way around, with SimH format the default, but P7B available as an option),

- have the correct parity (i7090 creates tapes with correct parity, and I believe i7094 and s709 do as well, and 3) use the "alternate" BCD coding for BCD records (the default for i7090 and i7094, optional for s709).

Likewise, tapes created by B7094 can be used on other emulators (whether or not the other emulators expect to "see" parity; i7090 does, I believe i7094 and s709 do not), if those emulators can:

- utilize tapes in P7B format tapes, either by default (s709) or optionally (i7090, i7094), 

- interpret BCD records using "alternate" coding (i7090 and i7094 do this by default; s709 can optionally do so).

B7094's "Tape Viewer" is a useful tool for examining the contents of any P7B tape: a small script can be created and run in the Editor to mount the tape; then clicking on the tape in the Tape Drives window will bring it up in the Tape Viewer. But here's another way to do it with just the mouse:

(1) Start the emulator, and in the first demo window click 'End Demonstration Script'.

(2) In the Control Panel window, click the 'TapeDrives' checkbox. The Tape Drives window will appear, but not show any configured Tape Units.

(3) On the Tape Drives window, click the 'All' radiobutton (this deselects 'Used').

(4) On the Tape Drives window, click the 'Add Drive' button. Tape Unit 'A1' will appear. (You could continue to click and add additional Tape Units from 'A2'-'A0' and 'B1'-'B0' if you wanted to.)

(5) On one of the added Tape Units, click the 'Opn' button and browse to any tape image file in the Open Dialog window. Any P7B file can be attached to the drive -- a SysIn.BCD or SysOut.BCD from a previous run (from the ..\Output directory), or any other tape.

(6) Now click on the channel-letter+decimal-unit-number of the Tape Unit with your attached tape image file. The Tape Viewer window will appear, displaying the tape in whatever mode matches the image file extension (BCD mode for *.BCD, Binary mode for any other extension).

You can attach any file, with any name, to a tape drive -- either via a Tape Unit's 'Opn' button or via an EC7 script's 'Mount' command. But any file you expect to be usable with IBSYS must have a filename extension of either '.BCD' or '.BIN' (upper- or lower-case, doesn't matter). This is true even if the file is otherwise a properly-formatted P7B image containing "real" data. Further, any file intended for use with IBSYS that contains BCD records (with even parity), or **begins** with BCD records in the case of a "hybrid" tape (such as a job input tape) must have the '.BCD' extension. And a file which contains binary records (with odd parity), such as an operating system or stand-alone diagnostic tape, must have the '.BIN' extension.

You can also save the text in the Tape Viewer window by clicking the 'Save' pushbutton at the top left of the window. There won't be any acknowledgment of the button press, but you'll get a "dump" file in the ..\Output directory with the extension '.DMP', named according to the tape image file that was being displayed (e.g., 'SYSOUT.BCD.DMP' or 'SYSIN.BCD.DMP').  The dump file name will always reflect the format (and hence the extension) of the tape image that was being displayed in the Tape Viewer (either '.BCD' or '.BIN') but in fact the text in the Tape Viewer window will be saved in whatever mode the Tape Viewer is currently displaying: either 'BCD' or 'Binary'.

## Writing and running your own programs

The EC7 script files comprising B7094's demo suite are a **bit** convoluted at first glance; so a number of simple, in-line script files (named ..\Files\Scripts\Xample_xxx.EC7) are provided as models for anybody who actually wants to write and run IBM 7090/7094 programs in any of the supported languages (FORTRAN II, FAP; FORTRAN IV, COBOL, MAP). These "Xample" scripts should make it possible to just concentrate on your own program and not have to worry about the "envelope" of IBSYS control cards or EC7 configuration commands. You can basically just copy one of the Xample scripts and make a very small alteration to have it run your own code.

To start, here's the procedure for **running** one of the Xample scripts. We'll exhibit one that assembles and runs a very short FAP assembly-language program, under IBSYS's FORTRAN II subsystem, to request IBSYS to generate a core dump.

(1) Start the emulator, and in the first demo window click 'End Demonstration Script'.

(2) In the Control Panel window, click the 'Editor' button (or the 'Editor' checkbox, they do the same thing). The Text Editor window will appear. It'll likely be blank, but if it's not, click the 'Close' button and close any editing sessions that might currently be open.

(3) Click the 'Open' button, and navigate to ..\Files\Scripts and open the file "Xample_Sysdmp.Fap.KSYS.EC7" (there's also an ASYS version of this file, but we're sticking with the KSYS version for reasons that will explained below).

(4) Now just click the 'Run' button on the Editor window, and the job will run. You could then 'Close' the file in the Editor, if you want; otherwise it will be kept open even if you 'Power Off' and restart the emulator. (Editor sessions are saved in the ..\Bin\B7094.INI file in the [EditFiles] section.)  But don't close the example script file just yet.

Scroll down a bit in the Editor, past the mounting of all the SCRATCH tape drives, and you'll see a line:

####
    Include File='Sysdmp.Fap'    // Insert the source text

"Sysdmp.Fap" is the actual Fortran Assembly Program code:

####
    *     FAP                                                               SYSDMP00
    *      FORCE IBSYS TO DUMP CORE                                         SYSDMP01
    *      SEE IBM 7090/7094 IBSYS OPERATING SYSTEM VERSION 13 MANUAL       SYSDMP02
    *      C28-6248-7 DEC. 1966                                             SYSDMP03
    *      SYSTEM CORE-STORAGE DUMP PROGRAM, P. 18                          SYSDMP04
           COUNT   14                                                       SYSDMP05
    *      SST IS A PSEUDO-OPERATION THAT LOADS THE SYSTEM SYMBOL TABLE     SYSDMP06
    *      IT MAKES THE LOCATION OF SYSDMP (115 OCTAL) AVAILABLE HERE       SYSDMP07
    *      SEE IBM 7090/7094 FORTRAN II ASSEMBLY PROGRAM (FAP) MANUAL       SYSDMP08
    *      GC28-6235-5 APRIL 1965                                           SYSDMP09
    *      APPENDIX C: SYSTEM SYMBOL TABLE, FORTRAN MONITOR, P. 69          SYSDMP10
           SST                                                              SYSDMP11
           TRA     SYSDMP                                                   SYSDMP12
           END                                                              SYSDMP13

Note that the "Include File=" command in the script is surrounded by text constituting the IBSYS and FORTRAN control cards that precede and follow the actual user-program source code. Without the single quotes required by the EC7 script interpreter, the first cards in the "job deck" would look like:

####
    $LIST
    $DATE
    $UNITS
    $JOB           SYSDMP
    $EXECUTE       FORTRAN
    *     ID       SYSDMP
    *     XEQ
    
The cards beginning with '$' are IBSYS control cards; note that any "argument" on such a card must begin in column 16. All the IBSYS control cards are all documented in the "IBM 7090/7094 IBSYS Operating System Version 13 Operator's Guide", section "Control Cards", p. 12., at bitsavers.org/pdf/ibm/7090/C28-6355-4_7090oper_Jun65.pdf .

$LIST causes **all** control cards to be listed on the lineprinter as well as the System Output Unit (SYSOU1 -- in our case, tape drive A3; image file SysOut.BCD). Normally, only a subset of control cards is also listed on the lineprinter.

$DATE sets the system date (the argument is provided by the scripter).

$UNITS causes all the "System Unit function names" to be listed on the output tape (and in our case the lineprinter as well). These are symbolic names for various functions served (mainly, and exclusively in our case apart from the card reader) by tape drives. SYSIN1 (or SYSIN2) means "system input"; SYSOU1 (or SYSOU2) means "system output" (think stdin and stdout in a Unix system); SYSPP1 (or SYSPP2) means "peripheral punch" (mainly for object code, to be punched on cards offline on another computer); SYSUT1, SYSUT2, ..., SYSUT9 ("system utility") are essentially "temp files" used for various things by various programs; etc.  Each System Unit in use has to be associated with a physical tape drive, designated by its "channel letter" and (decimal) "unit number": A1, A2, ..., A0 ("A0" comes at the end because you should think of it as being "A10"); B1, B2, ..., B0.  (A 7094 system could have up to 8 channels, designated by A, B, C, ..., H; we don't ever have to deal with more than 2 (A and B).  The $UNITS control card is not **required** here; it's just there to document what's going on. It's present in all the demo jobs (and in the case of the ASYS demos, it shows the list before and after System Unit reassignments via the "$ATTACH . . .", "$AS . . ." control cards -- refer to the IBM manual). One other physical device specification you'll see in the scripts, in addition to the physical tape drive designations, is "RDA" -- "card reader on channel A", which also has the System Unit function name "SYSCRD".

The $JOB card marks the beginning of a "job" -- a unit of work in IBSYS. It must always be present.

The $EXECUTE card causes IBSYS to invoke one of its major "subsystems" -- in this case, the FORTRAN processor. (But the IBJOB processor is also invoked by means of the $EXECUTE card.)

The cards beginning with '*' are FORTRAN processor control cards, and the FORTRAN control-card commands must begin in column 7. All the Fortran Processor control cards are all documented in the "IBM 7090/7094 Programming Systems FORTRAN II Programming" manual, Chapter 14 "FORTRAN II Monitor Control Cards", p. 37 at bitsavers.org/pdf/ibm/7090/C28-6054-5_FORTRANII_Apr64.pdf and the "IBM 7090/7094 Programming Systems FORTRAN II Operations" manual, Chapter 13 "FORTRAN II Monitor Control Cards and Utility Cards", p. 30 at bitsavers.org/pdf/ibm/7090/C28-6066-6_FORTRANII_oper.pdf

The 'XEQ' control card is supposed to mean "execute immediately" rather than "just compile or assemble, but do not execute", but our two IBSYS versions' FORTRAN processors are idiosyncratic with regard to "honoring" this -- ASYS respects the absence of an XEQ card; KSYS does **not**, and will go ahead with immediate execution whether or not it's there. Of course, in all cases, attempting to execute the program is denied if there are errors reported by the compiler or assembler ("EXECUTION DELETED" is the usual message).

The cards following the inserted source code are:

####
    ~
    $IBSYS
    $STOP

The '~' character is just our convention to represent an End-Of-File card. '$IBSYS' tells the FORTRAN processor to return control to the IBSYS monitor. '$STOP' tells the system to print some final statistics and halt the CPU.

Strictly speaking, the first "card" in "..\Files\Cards\Sysdmp.Fap" is actually a FORTRAN processor control card, not part of the assembly-language source and **certainly** not a comment -- note that the 'F' in "FAP" is aligned with column 7; the rest of the lines beginning with asterisks **are** comments. The first actual comment is used by the Assembler as the text of page headings on the SYSOU1 tape. In a similar example script that could have been shown here, "..\Files\Scripts\Xample_MatrixInv05.Ftn.KSYS.EC7", the Include file "..\Files\Cards\MatrixInvO5.Ftn" **is** pure FORTRAN II source code (though the initial line of that is also a comment whose text is used for page headings in the compiler report). But the core dump is more entertaining. Oh and by the way, there's a convention in the "..\Files\Cards" directory that source "decks" with ".Ftn" in the file names are FORTRAN II, whereas decks with ".For" in the names are IBJOB/FORTRAN IV. And of course ".Cob" indicates IBJOB/COBOL. There's no file that's pure IBJOB/MAP, but the source code for one of the demo jobs -- "..\Files\Cards\Lsqrs.For" -- is a very large deck with multiple "Control Sections" (as they're called in the native lingo of this machine), and some of them are MAP subroutines (and the multiple sections also necessitate the embedding of some IBJOB control cards ($IBFTC, $IBMAP) in that particular file. Similarly, "..\Files\Cards\StressIII.Ftn" is a large multi-section file with embedded FORTRAN control cards.

If no path is given, the scripter's "Include File=" command will find the file of that name in the ..\Files\Cards directory. This is the default directory where B7094 keeps source-code "decks" for all the included demo programs. This is true even if, as is the case here, the program and its enclosing control cards must be converted to a tape before the job can run (which is required here because the FORTRAN II subsystem does not permit job input from cards. This conversion occurs slightly further on in the "Xample_Sysdmp.Fap.KSYS.EC7" script file you currently have open in the Editor.) The ..\Files\Tapes directory is where the IBSYS tapes live, in addition to some other binary files that are used to create relocatable binary jobs for input on tape. Most of the files in ..\Files\Cards are text files -- either source code or input data for a demo program -- though there are also some binary files in that directory, used to create relocatable binary jobs for input via the card reader.

There are two alternatives if you want to keep your own files elsewhere than in the expected directories: a) use the full path name in the "Include File" command or b) add to or change the list of default search paths on the B7094 "Configuration" window (click the "Config" checkbox on the Control Panel to bring it up). You might in fact want to create ..\Files\MyScripts and ..\Files\MyCards directories underneath your B7094 installation directory, and add these directories to the list of search paths on the Configuration window.

(4) Now just click the 'Run' button on the Editor window, and the job will run. You could then 'Close' the file in the Editor, if you want; otherwise it will be kept open even if you 'Power Off' and restart the emulator (Editor sessions are saved in the ..\Bin\B7094.INI file in the [EditFiles] section).

You could copy"Xample_Sysdmp.Fap.KSYS.EC7" and only have to change a single line to run your own FORTRAN II or FAP program. Alternatively, you could copy one of the other Xample scripts, say "Xample_Primes.For.EC7" or "Xample_Primes.Cob.EC7", and make fairly minimal changes to be able to use one of the IBJOB languages (FORTRAN IV or COBOL, in those scripts).

Note: it's mentioned above that KSYS (the Aerojet-General KSYS61.BIN single-tape version of IBSYS) is slightly easier to work with than the ASYS1.BIN/ASYS8.BIN two-tape version of IBSYS. The reason is somewhat obscure. The ASYS1/ASYS8 duo included with B7094 are the **original** images of the tapes recovered by Paul Pierce in the late 90s. But this system has a quirk: it was built by default with System Units SYSIN1 and SYSOU1 pointing to the same tape drive (B1). This is not a problem when jobs are coming from the card reader (via the Sense Switch 1 "on" setting), but if a job has to come from tape (as with FORTRAN II), it requires a bit of fancy footwork to switch the SYSOU1 System Unit assignment so the SYSIN1 tape doesn't get clobbered as soon as a job starts to run (it was a bit surprising to discover that this was possible at all). The EC7 scripts included here **do** perform that little dance, but it adds an additional layer of obscurity to everything else that's going on. The other emulators (i7090, i7094, s709) seem to be using (in their provided software kits) a rebuilt version of the ASYS1 system (presumably created from IBSYS source with Dave Pitt's "asm7090" and "lnk7090" cross-assembler and cross-linker) that eliminated this problem (and also only requires a single channel's-worth of tape drives).

The methods described above will take care of compile-and-go (or assemble-and-go) jobs, which will probably be sufficient for the vast majority of users.  It is possible, though, to compile a program from source and then create and submit a relocatable binary version of the program whenever it needs to be re-run.  This is, however, as the Emerald City cabbie said to Dorothy, "a horse of a different color".  See the README.txt file included with the reloc_scripts.* archives for more details about that.

## Acknowledgments

Grateful acknowledgment is due to Richard Cornwell for providing some of the sample demo jobs, and for providing technical assistance in getting this new release operational. And of course to Al Kossow et al. for the bitsavers archive, without which many retro-emulators couldn't exist; to Bob Supnik, Dave Pitts, and Richard Cornwell for their work getting **really**-working IBM 709x emulators operational in the mid-late 2000s.  And to Paul Pierce, who got the ball rolling with his collection of tapes, without which there would be nothing to run on such emulators (well, apart from the CTSS software from MIT).

## Gotchas

Screen "real estate" and the large number of display windows:

- Initial window positions are read from the ..\Bin\B7094.INI file when the emulator starts up, and saved back to B7094.INI when the emulator shuts down (thus recording a changed window position if any window is moved while the emulator is running).  It is possible, for certain monitors, that a window might end up being "out of sight" for a given INI file.  In that case, you'd have to edit the INI file manually to bring the "lost" window back within range.

- There's no way to avoid a "cramped" window layout with a single monitor, with windows potentially obscuring other windows.  A partial remedy for this is that it's possible, from the Control Panel, to de-select (and re-select) windows for display by checking and unchecking the 12 checkboxes
corresponding to the windows.  For the canned demos, the script files normally control when windows are displayed and hidden -- for example, by bringing up the Tape Viewer when a job completes, and then automatically hiding it when you click 'Continue' (on the Scripter window that says
"Click 'Continue' to dismiss the tape viewer and redisplay the demo list.") But if you wanted, for example, to see the whole Operator Console window at the point when a job completes, you could de-select both the Tape Viewer and the Script Dialog windows.  Then you could re-select one (or both) of those windows and click 'Continue' on the Scripter window to resume the demo suite.

There are some things that can make the emulator seem to hang, but are just **very** slow:

- When the Tape Viewer is being displayed after finishing a job with a **lot** of output. (You'll encounter this when building 'STRESS III' from source. Be patient.)

- When you switch the Tape Viewer from BCD mode to BIN mode, when there's a lot of data on the tape.

- When you use the Tape Viewer on a system tape (KSYS61.BIN, for example). Especially if you load the system tape into the Tape Viewer in BCD mode and then realize you actually wanted BIN mode. You'll have to wait a while!

- When you're using B7094's tracing facilities. There are lots of things that can be traced: device accesses, register stores, core writes, instruction execution, etc.  These are all selected on the Log/Trace screen (that you can display by clicking the 'Trace' checkbox on the Control Panel window). But be careful how you use this, if you don't want to slow things down unacceptably (either during the running of a program in the emulator or while waiting for the results of an already-recorded list of traced events to be displayed in the Log/Trace window).  The most efficient way to use this is, in the Log/Trace window, to:

  (1) Check the boxes in the 'Trace Record filters' section on the left to select the classes of items you want traced (the fewer the "better", if you can narrow things down);

  (2) When the job finishes either 'Power Off' the emulator or click the 'Clear' pushbutton in the Log/Trace window.  You'll then be prompted to 'Save current trace data?'. Click 'Yes' and a file ..\Output\B7094.TRC will be written (overwriting one that's already there, if there is one). The saving of the trace file can itself take a **bit** of time.

  But the Log/Trace window also has a 'Trace Display filters' section on the right, and this allows you to filter and display in the window anything that's been recorded as a result of making the selections on the left (you check the desired checkboxes on the right, and then click the 'Display' pushbutton). But this can be a big annoyance if there's a lot of trace data to be filtered for display (examine the 'Lines:' counter above the 'Display' pushbutton to see if this might be the case). This process of filtering for "on-line" display can take a **long** time if there's a lot of trace data -- much longer than just saving all the trace data to a file and then using a text editor to view it.

- If you've activated the Core Plot window. This is a graphical display of core usage, with memory locations represented by blocks of colored pixels. Pixels in a block are black initially; a write to a location turns them blue, a read from a location turns them green, a (pending) instruction fetch flashes a pixel block white (before the actual fetch turns it green). This can be entertaining (and one of the canned demos features it), but it **really** slows down the emulator.

Sometimes, the emulator really can get hung. This can happen if you try to 'Power Off' while a job is running (it's "safer" to click the 'Stop' button on the Operator Console window and **then** click 'Power Off').

By the way, if you **are** running a demo job and don't want to wait for it to finish, you can click the 'Stop' button on the Operator Console window at any time. The Scripter will treat the job as having completed normally, and both the Tape Viewer window (albeit with truncated contents, of course) and the Script Dialog window that says "Click 'Continue' to dismiss the tape viewer and redisplay the demo list." will come up. Just click 'Continue' at that point, and the demo suite will continue normally.

If the emulator hangs, or if something is just taking more time than you care to wait for, I'm afraid there's nothing for it but to kill the process in the Task Manager.

## Known bugs

- If line numbering is turned on in the Editor window, the numbers in the parallel list box on the left side of the window will not update automatically as text is typed in. But they will be updated if the 'Line Numbers' checkbox is unchecked and then checked again, or if a file is loaded (the latter creates an additional editing box within the same Editor window; multiple text boxes are accessed via the file name tabs near the top of the window).  If text is entered (or loaded from a file) that's long enough to activate the scroll bar for the edit box, a scroll bar for the list box containing the line numbers will also be activated, but the scrolling will not be synchronized.  It will be up to the user to synchronize the line numbers with the text -- such as, by moving both bars to the beginning (or the end), and then scrolling downward (or upward) in discrete steps.

- Neither of the included stand-alone diagnostic programs (the '9M21A' card diagnostic, or the '9M71B' tape diagnostic) will run completely without errors.

## About the mainframe

The IBM 7094 computer was a commercial 36-bit (6-bit byte) "scientific" computer (with 15-bit addresses, encompassing 32K words) that was produced (beginning as the model 7090; the 7094 was a slightly enhanced version) starting in 1959, and withdrawn from sale in 1969.  While a few installations (e.g., at MIT) remained in service into the 1970s, by the late 60s many customers were switching over to the System/360 series (a 32-bit, 8-bit-byte architecture touted as being "universally" applicable to both commercial and scientific tasks, with a greatly expanded address space).  The 7094 was a member of the "7000 series", which also included commercial machines such as the 7070 and 7074 (architecturally dissimilar to the 7090 and 7094, but sharing manufacturing technology and peripherals) and the quasi-experimental 7030 "STRETCH" supercomputer.  The 7090/7094 was preceded by the vacuum-tube "700 series", an architecturally-similar line of 36-bit machines beginning with the 704 in 1954 (on which both Fortran and Lisp were developed) up through the 709 in 1958).  The machines introduced in 1959 featured IBM's first generation of discrete-transistor circuitry.

While the machine supported random-access storage devices (disk and drum), and some installations utilized these (e.g., MIT's CTSS timesharing system), the more common "IBSYS" operating system made heavy use of magnetic tape and punched cards.

You can read some amusing anecdotes about the IBM 7094 by clicking on the last option of B7094's initial demo window.
