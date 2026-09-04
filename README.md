MoveText
========

Select text and move it around using the keyboard, or setup a text "tunnel" to move code from one location to another.


## Installation

### By Package Control

1. Download & Install **`Sublime Text 3`** (https://www.sublimetext.com/3)
1. Go to the menu **`Tools -> Install Package Control`**, then,
    wait few seconds until the installation finishes up
1. Now,
    Go to the menu **`Preferences -> Package Control`**
1. Type **`Add Channel`** on the opened quick panel and press <kbd>Enter</kbd>
1. Then,
    input the following address and press <kbd>Enter</kbd>
    ```
    https://raw.githubusercontent.com/evandrocoan/StudioChannel/master/channel.json
    ```
1. Go to the menu **`Tools -> Command Palette...
    (Ctrl+Shift+P)`**
1. Type **`Preferences:
    Package Control Settings – User`** on the opened quick panel and press <kbd>Enter</kbd>
1. Then,
    find the following setting on your **`Package Control.sublime-settings`** file:
    ```js
    "channels":
    [
        "https://packagecontrol.io/channel_v3.json",
        "https://raw.githubusercontent.com/evandrocoan/StudioChannel/master/channel.json",
    ],
    ```
1. And,
    change it to the following, i.e.,
    put the **`https://raw.githubusercontent...`** line as first:
    ```js
    "channels":
    [
        "https://raw.githubusercontent.com/evandrocoan/StudioChannel/master/channel.json",
        "https://packagecontrol.io/channel_v3.json",
    ],
    ```
    * The **`https://raw.githubusercontent...`** line must to be added before the **`https://packagecontrol.io...`** one, otherwise,
      you will not install this forked version of the package,
      but the original available on the Package Control default channel **`https://packagecontrol.io...`**
    > [!WARNING]
    > Placing this custom channel before the default channel changes Package Control's resolution globally. Packages from this channel with the same name will override versions from the default channel.
    >
    > You can review the channel contents here:
    > https://raw.githubusercontent.com/evandrocoan/StudioChannel/master/channel.json
1. Now,
    go to the menu **`Preferences -> Package Control`**
1. Type **`Install Package`** on the opened quick panel and press <kbd>Enter</kbd>
1. Then,
    search for **`MoveText`** and press <kbd>Enter</kbd>
1. Install keymaps for the commands (see Example.sublime-keymap for my preferred keys)

See also:

1. [ITE - Integrated Toolset Environment](https://github.com/evandrocoan/ITE)
1. [Package control docs](https://packagecontrol.io/docs/usage) for details.


Commands
--------

`move_text_left`: Moves the selected text one character to the left

`move_text_right`: Moves the selected text one character to the right

`move_text_up`: Moves the selected text one line up

`move_text_down`: Moves the selected text one line down

When moving text up and down, funny things happen when the destination line doesn't have enough preceding characters.  An attempt *is made* to keep the text on the same column, but the mechanism for this uses `sublime.View.command_history`, which doesn't update after every movement.  It updates in between "Undo" events, so if you move the text in the opposite direction, or if you pause long enough for an "undo" to register, the text will move correctly.  It looks like this:

    1. one*dragme*  1. one          1. one       1. one
    2. two          2. two*dragme*  2. two       2. two
    3.              3.              3. *dragme*  3.
    4. four         4. four         4. four      4. *dragme*four

But if you move the text *up* first, it will move correctly:

    1. one          1. one*dragme*  1. one          1. one       1. one
    2. two*dragme*  2. two          2. two*dragme*  2. two       2. two
    3.              3.              3.              3. *dragme*  3.
    4. four         4. four         4. four         4. four      4. fou*dragme*r
