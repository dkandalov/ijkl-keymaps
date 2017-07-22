## Alt-ijkl keymaps

This project contains config files with `alt-ijkl` keyboard shortcuts.
This keymap was inspired by Vim and gaming keyboard layouts.
One of the main goals is to navigate and modify text without moving hands over keyboard too much.


### Differences compared to typical OS keymaps
Arrows are moved to `ijkl` and left/right arrows jump to next/previous word:
 - `alt-i` - line up
 - `alt-j` - move to previous word
 - `alt-k` - line down
 - `alt-l` - move to next word
 - `alt-n` - move left
 - `alt-m` - move right

Jump to start/end of line:
 - `alt-u` - move to start of line
 - `alt-o` - move to end of line

All of the above with selection:
 - `alt-shift-ijklmnuo` - navigate with selection

Delete/backspace:
 - `alt-d` - delete next word
 - `alt-;` - delete next character
 - `alt-shift-;` - delete previous character

Modes:
 - `alt-cmd-\` - toggle column mode
 - `alt-cmd-'` - toggle insert mode

Tabs:
 - `alt-q` - close tab
 - `cmd-shift-[` - previous tab
 - `cmd-shift-]` - next tab

### Installation in IJ
Copy file from `intellij` folder into `~/Library/Preferences/IntelliJIdea2017.1/keymaps/`.
Restart IntelliJ, switch to new keyboard layout.


### Custom OSX key layout

Issues with built-in OSX key layouts in IJ (most likely caused by JDK changes since java 7)
 - dead keys cannot be used as IDE shortcuts (e.g. alt+i in US layout).
   Solution: edit keyboard layout to remove dead keys. 
 - unmapped keys (i.e. keys with no output defined in key layout) cannot be used as IDE shortcuts.
   Solution: when editing key layout always map keys to some output. 
 - keys with certain output, when held down, trigger IDE action only once (e.g. alt+i with 'ˆ' output in US layout).
   Solution: disable sticky feature by executing this in a shell `defaults write -g ApplePressAndHoldEnabled -bool false`.
 - if alt+ik are mapped to some character, then Navigate to Class action handles alt+ik shortcuts as both navigation up/down and entering a character. 
   Solution: map alt+ijkl to produce the same output as up/left/down/right keys

IDE issues:
 - project view doesn't use alt+ijkl shortcuts for navigation. This problem existed in all IJ version.
   Solution unknown.
 - inspection/intention/create new file/import popups treat aly+ik keys as text instead of navigation up/down.
   The problem doesn't exist in older IJ version (e.g. IntelliJ IDEA 2016.2.4 Build #IU-162.2032.8 JRE: 1.8.0_40-release-b119 x86_64)
   Solution unknown.
 

How to edit OSX keyboard layout:
 - download and install Ukelele from http://scripts.sil.org/cms/scripts/page.php?site_id=nrsi&id=ukelele
 - in Ukelele "File -> New From Current Input Source"
 - remove dead keys from the layout:
    - press "alt" and click on one of the orange/red keys
    - (keep "alt" pressed) Main Menu -> Keyboard -> Edit Key
    - in the dialog
        - in "Dead Key" tab, copy terminator symbol and delete "the dead key state the key will initiate"
        - in "Output" tab, paste terminator symbol into "the new output for the key", press OK
 - (optional) click on "Info" button and change key layout name so that later it's easier to distinguish from built-in OSX layout 
 - use "File -> Save" to save layout in "Keyboard Layout Bundle" file format to "~/Library/Keyboard Layouts/";
   (layout can be saved in "Keyboard Layout" format as a single file, but it won't include layout flag)
 - (OSX will normally notice modified or added layout, especially if you change its name, but sometimes you might need to log out / log in)
 - in "Settings -> Keyboard -> Input" add new input source (it might appear in category "Other")

If you're happy with custom layout and want to hide built-in layout from input source list, 
follow these steps (https://apple.stackexchange.com/questions/44921/how-to-remove-or-disable-a-default-keyboard-layout):
 - Change the current input source to your custom keyboard layout
 - `open ~/Library/Preferences/com.apple.HIToolbox.plist` (requires XCode)
 - Remove the input source or input sources you want to disable from the AppleEnabledInputSources dictionary 
   If there is an AppleDefaultAsciiInputSource key, remove it
 - Restart
