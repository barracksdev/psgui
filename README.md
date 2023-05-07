![psguisample](https://user-images.githubusercontent.com/132730427/236600874-23b1b6dc-8009-4f64-b31a-f618f6441c21.png)

# PSGui

This PowerShell script creates a GUI for launching your custom PowerShell scripts.  It was created through prompts given to ChatGPT-4.

# Usage
Launch `.\PSGui.ps1` from PowerShell, and it will load the configuration found in `config.json`.

This configuration file is used by the script to create the buttons for launching other pre-existing PowerShell scripts defined and created by the user.

Alternate configuration files can by loaded using the `-jsonconfig` parameter.
* For example: `PSGui.ps1 -jsonconfig altconfig.json`

A sample script file is included in the `Scripts` folder. This is included to show script launching functionality.  The script simply lists the files found in `C:\Windows\` using `Get-ChildItem C:\Windows`.

# Configuration and Layout
Tabs, buttons, and settings are defined using a JSON file named `config.json`.

Each tab object contains its own array of button objects, and each button objects contains several key value pairs.

Current button settings used are:
* `Content` Label text displayed on the button
* `ScriptPath` Path to the PowerShell script to be executed
* `ToolTip` Tooltip text displayed when hovering over the button
* `Group` Group name the button belongs to, used to organize buttons within a tab

The organization of GUI elements is ordered by:
1. Tabs in the the order they're defined in the configuration file
2. Button Groups alphabetically by the `Group` values found within in each button
3. Buttons alphabetically by their `Content` values

If a button does not have a `Group` value assigned, it will default to a `General Scripts` group.

The script will also try to verify the path of each `ScriptPath` value for every button.  If it cannot find the referenced file, the button will color will change to light red and show an error message in the button tooltip.  If a red button is clicked, it will return a Windows message stating the file cannot be found along with the path is trying to verify.

# config.json tree structure view
This is a tree view showing the general layout of the default configuration file.

This example has two tabs.  The first tab contains three buttons organized into two groups.  The second tab has buttons organized into two groups.  Since Button 5 does not have a `Group` name value, it will automatically be placed into a group named `General Scripts`.

- Tabs
  - Tab 1 // Name of the tab in the GUI
    - Buttons
      - Button 1 
        - Content: "Button 1" // Label text displayed on the button
        - ScriptPath: ".\\Path\\To\\Your\\Script1.ps1" // Path to the PowerShell script to be executed
        - ToolTip: "Description for Button 1" // Tooltip text displayed when hovering over the button
        - Group: "Group Name 1" // Group name the button belongs to, used to organize buttons within a tab
      - Button 2
        - Content: "Button 2"
        - ScriptPath: ".\\Path\\To\\Your\\Script2.ps1"
        - ToolTip: "Description for Button 2"
        - Group: "Group Name 1"
      - Button 3
        - Content: "Button 3"
        - ScriptPath: ".\\Path\\To\\Your\\Script3.ps1"
        - ToolTip: "Description for Button 3"
        - Group: "Group Name 2"
  - Tab 2
    - Buttons
      - Button 4
        - Content: "Button 4"
        - ScriptPath: ".\\Path\\To\\Your\\Script4.ps1"
        - ToolTip: "Description for Button 4"
        - Group: "Group Name 1"
      - Button 5
        - Content: "Button 5"
        - ScriptPath: ".\\Path\\To\\Your\\Script5.ps1"
        - ToolTip: "Description for Button 5"
        - Group: ""

# Other Details
While there are "Username" and "Password" boxes along with a "Use Modern Auth" checkbox, these do not do anything yet and can be ignored.
