B7094 is a Windows-based emulator for the IBM 7094 mainframe computer from the 1960s.

## Basic usage

If you're a "casual" user, and running Windows, just:

- Download the B7094V34A.zip distribution archive

- Extract it into a new folder

- Run either B7094.32.exe or B7094.64.exe in the created "Bin" sub-folder

- Click on the options displayed to select from the many demonstrations available.

B7094 makes no changes to the Windows registry or any other part of the system other than its install folder. Deleting the distribution archive and the install folder will completely remove B704 from your system.

There is a YouTube video [here](https://www.youtube.com/watch?v=4xaBS6pWrG0) that shows the use and operation of B7094 (an earlier release, but the basic operation is the same).

## Additional details

The source of B7094 is included in the distribution, to allow you to modify or enhance the program and rebuild it. You'll need to install Lazarus/Free Pascal to do this, the 32-bit and/or 64-bit versions. The current B7094 v3.4A release was built using the newest (as of the end of last year) releases of these development tools (Lazarus 2.2.4, 28 Sept 2022; Free Pascal 3.2.2, 20 May 2021).

There is another YouTube video [here](https://www.youtube.com/watch?v=4xaBS6pWrG0) that shows how to compile B7094 from the sources.

The 32-bit executable will still run on Windows XP, and both executables will run on any 64-bit version of Windows from Vista up through the present. There are Windows dependencies "baked in" to the code, but the program can be run on Linux using Wine (with a few non-fatal quirks), and even under Wine 8.x on x86 MacOS (the 64-bit executable has been tested on 'Catalina' in a VM). The B7094V34A.tgz archive is provided solely for the convenience of the Linux user; its contents are the same as B7094V34A.zip.