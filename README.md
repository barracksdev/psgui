# PSGui

This Powershell script will create a GUI for launching your own custom Powershell scripts.  It was created primarily through prompts via ChatGPT-4.

# Usage
Launch PSGui.ps1 from Powershell and it will load the configuration found in "config.json".

This configuration file is what the script uses to create the buttons for launching other Powershell scripts.

You can additionally launch an alternate config file using the "-load" command.
* For example: PSGui.ps1 -load altconfig.json

# config.json
Tabs and Buttons are defined in this configuration file.

Each Tab object contains its own array of Buttons objects, and each Button contains a list of settings.

Button settings listed in the config file are:
* "Content": "Button Label Text"
* "ScriptPath": ".\\Path\\To\\Your\\Script.ps1"
* "ToolTip": "Additional details that can be provided when hovering over the button."
* "Group": "Group Name 1"
* "CreatesFiles": false --- NOT USED YET
* "ModifiesExistingData": false --- NOT USED YET

The organization of GUI elements is ordered by:
1. Tabs by their "Name" values
2. Buttons by their "Group" values
3. Buttons by their "Content" values within their Group

If a Button does not have a Group value assigned, it will default to a "General Scripts" group.

# Other Details
While there are "Username" and "Password" boxes along with a "Use Modern Auth" checkbox, these do not do anything yet and can be ignored.

The script will verify the path of each ScriptPath value in every button.  If it cannot find the referenced file, the button will appear red and show an error message in the hover tooltip.  If a red button is clicked, it will return an Windows message stating the file cannot be found along with the path is checking.


