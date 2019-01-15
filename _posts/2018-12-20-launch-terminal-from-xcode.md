

##### Add New Behavior
1. Launch Xcode > Preferences > Behaviors
2. `+` to add
3. Rename "New Behavior" to something more meaningful "Launch Terminal"

##### Key Binding
1. Tap on ⌘ opposite to Behavior name
2. Choose a handy (non-conflicting) key binding. I use Control + Command + t (`⌃⌘T`)

##### Configure the run action
1. Save the _LaunchProjectInTerminal.sh_ so somewhere safe and accessible.
1. In the details panel of the new behavior, look for the checkmark `Run` and check it.
2. Select "Choose Script" and provide the path to the _LaunchProjectInTerminal.sh_ file

##### Done



What this script does.
1. Takes the current project path.
2. Launches Terminal.
3. `cd` to current project path.

```bash
#!/bin/sh

set -e

if [ -n "$XcodeProjectPath" ]; then
  open -a Terminal "$XcodeProjectPath"/..
else
  open -a Terminal "$XcodeWorkspacePath"/..
fi
```
