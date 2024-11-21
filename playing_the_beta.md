# How to play the beta on sc2-next
## Install tools
You'll need:
* git (see [the installation notes in the guide](git.md#installation))
* Python 3.10 ~ 3.12 ([download here](https://www.python.org/downloads/))
  * Note Python should be installed from the installer, not from winget
  * I recommend doing a system-wide installation, and future instructions will largely assume that's the case
* You can use a GUI git tool like GitHub for Desktop or SourceTree instead of baseline git; I will give command-line instructions as they're easier to type

### Verifying git installation
* Open a command prompt (start menu, type "cmd" and hit enter)
* Enter commands by typing them out and hitting enter
  * `where git` -- should print a path to some git.exe somewhere; doesn't matter where

### Verifying Python installations
* Open a command prompt (start menu, type "cmd" and hit enter)
* Enter commands by typing them out and hitting enter
  1. `where python`
     * should return a path in `C:/Program Files/Python312` (or `Python311` for 3.11, `Python310` for 3.10, etc)
     * **OR** can return a path in `C:/Users` (user installation), unless it's in `AppData/Local/Microsoft/WindowsApps` -- that's the winget version and it breaks
     * If multiple paths appear, we only care about the first one; ie if the winget version is installed but second in the list, we don't care.
  2. `python --version` should print the version -- make sure it's 3.10, 3.11, or 3.12
* Check the path for Python -- it's broken for a lot of people for some reason
  1. In the start menu, type "env" to click on the option "Modify the System Environment Variables" (Fig. 1)
  2. In the "System Properties" popup, click "Environment Variables" (Fig. 2)
  3. If you installed Python system-wide, look in the bottom box; if you installed it just for your user, look in the top box
  4. Find the "Path" Variable and double-click it to edit it
  5. Verify these two paths are in the list: (These are for 3.12, and assume system-wide installation) (Fig. 3)
     * `C:\Program Files\Python312\`
     * `C:\Program Files\Python312\Scripts\`
     * Make sure these appear _before_ any other python installation directory if you have multiple
  6. If any path is missing, you can add it (and verify Python exists in that directory). *If you make updates, be sure to restart command-prompt before continuing*
  7. Check `where python` and `python --version` again if you made changes

![Environment](./images/environment_variables_start.png)

Figure 1: Opening the environment variables window

![Variables](./images/environment_variables_panel.png)

Figure 2: The variables to edit

![Paths](./images/entering_path_variables.png)

Figure 3: Adding the variables near the top of the list

## Downloading from git
* The sc2 beta fork is here: https://github.com/Ziktofel/Archipelago.git
* Decide what folder you want to put your installation in. I will use `D:/example` for an example
* Open command-prompt (type `cmd` in the start menu and hit enter)
* Navigate to the desired folder
  * Change drives by typing the drive name (e.g. `d:` will change to the D:/ drive)
  * See what folders you can go to by typing `dir`
  * Change folders by typing `cd <foldername>` (e.g. `cd example` will change directory to example)
    * "cd" is short for "change directory"
    * `cd ..` will go up one folder level (e.g. from `D:/example/subfolder` to `D:/example`)
    * auto-complete a folder name by hitting tab
  * run `git clone https://github.com/Ziktofel/Archipelago.git` to clone (download) the repository
    * This may take several seconds
    * This will create a new folder called `Archipelago/`; you can check it exists with `dir`
  * `cd` into the new `Archipelago/` folder
* run `git status` to verify the git repository is initialized correctly
  * This should say what branch you're on; if you're not on `sc2-next`, change to it with `git checkout sc2-next`
* In future, you can get the latest updates by just running `git pull` from this location

## Running
It is recommended that the first time you run from source, you run from a command-prompt. This is because if there is an error, the command prompt will stay open so you can read it and ask for help. You can run by double-clicking files in the explorer, but the terminal will close instantly on error.

* Open or an Administrator command-prompt in `D:/example/Archipelago`
  * You can get an administrator terminal when you start cmd by right-clicking it and selecting "run as administrator"
* run `python setup.py` in the administrator command prompt
  * This should ask to download all third party-libraries; hit enter to proceed
  * We expect this to error with "error: no commands supplied"
  * If there is some other error (usually complaining about cx_freeze), something went wrong with installing libraries.
    * Share the error message in the discord to get help (and we can update this guide, hopefully)
  * Otherwise, we should be ready to go; command-prompt is optional from here on
* Close the administrator command-prompt -- we shouldn't need it anymore, and it's not secure to leave administrator command-prompts open for long periods in general
* Run `Launcher.py` to get your template yamls
* Run `Generate.py` to generate a game with yamls in the Players/ folder
* Run `MultiServer.py` to locally-host a generated world
  * Tip: on command-line, you can run `MultiServer.py <output_zip_name>` to instantly start the server without going through a file-selection screen
* Run `Starcraft2Client.py` to start up the sc2 client
  * [Update the map and mod files](#updating-the-mod-files) by running `/download_data`
* Report issues to the github at https://github.com/Ziktofel/Archipelago/issues
* Have fun!

## Updating the mod files
The simplest way to get the latest files is to run `/download_data` in the client. This fetches and installs the files from the [ap-sc2-data releases page](https://github.com/Ziktofel/Archipelago-SC2-data/releases).

### Installing manually from the releases page
You generally shouldn't have to do this, but you can just do what `/download_data` does manually by going to the [releases page](https://github.com/Ziktofel/Archipelago-SC2-data/releases), selecting the Archipelago-SC2Data.zip artifact of the API version you want, unzipping, and putting the contents of the Maps/ and Mods/ folders into the corresponding folders of your sc2 install.

### Installing manually from the actions page
This also generally shouldn't be necessary, though it does allow selecting the mod files from a particular branch or push. So if you want to get the files for a feature which is still in PR (say, to assist in testing a new unit), you can follow these steps.
* Sign into a github account. Make one if you don't have one
* Go to the [Github Actions page for the map/mod repository](https://github.com/Ziktofel/Archipelago-SC2-data/actions)
* Click the build (white text) for the latest build labeled with the desired branch
* Click the "Archipelago-SC2Data" link in the Artifacts section, near the bottom of the page. This requires being signed into github. This should download a .zip file
* Unpack the .zip; it should contain folders named `Maps/` and `Mods/`. Paste the contents of these folders into the Maps/ and Mods/ folders of your sc2 install

### Building locally
This is an alternate way to get the maps, more useful for developers.
* Clone the archipelago-sc2-data repository or your fork of it. Fork from [Ziktofel's fork](https://github.com/Ziktofel/Archipelago-SC2-data) or clone his fork directly
* For windows users:
  * Open `build_release_package.sh` and `Maps/ArchipelagoCampaign/build.sh` in an editor like vscode or Notepad++. Change the line ending to Unix-style (LF)
    * In vscode, this is done by clicking the little "CRLF" in the bottom-bar or running the "Change End of Line Sequence" task, and selecting LF
    * In Notepad++, this is done with Edit -> EOL Conversion -> LF
  * Ensure you have WSL (Windows Subsystem for Linux) enabled. Use the WSL terminal to execute .sh scripts
* Run `./build_release_package.sh` in a terminal. This should build the maps, and will take a minute or two
* The result should appear in the target/ directory. Get the contained Maps/ and Mods/ folders to your sc2 install
  * A neat trick is to create a symlink from `<sc2 install>/Maps/ArchipelagoCampaign` to `<repo clone>/target/Maps/ArchipelagoCampaign` (and similar for mods)

## Troubleshooting
### Uninstalling all libraries
* This hopefully shouldn't be necessary, but might be if things got installed in user installs when Python / Archipelago wants it in at the system-level
* in cmd, run:
  * `python -m pip freeze > reqs.txt` to list all currently installed Python libraries in reqs.txt
  * `python -m pip uninstall -r reqs.txt` to uninstall everything in reqs.txt
  * `del reqs.txt` to delete the reqs.txt file

## Details / other ways of running for technical users
Some people have extra requirements for maintaining their system or running the code
* If you're debugging, get set up with an IDE
  * I recommend vscode with the pylance extension (Visual Studio Code, not the same as Visual Studio)
  * Many developers use PyCharm, which is a Python-specific but high-quality IDE
  * If you're more technical than I'd expect any reader of this guide to be, Vim and Emacs are also options
  * For the love of god, do not use Visual Studio
* If you need to keep your system Python libraries clean (ie don't want Archipelago 3rd party libraries interfering with other Python projects), you can use `python venv` to make a project-specific Python install
