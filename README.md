# touchosc-confirm-button

In some cases a TouchOSC button might perform a destructive or permanent action, such as initializing or saving a patch, or resetting a device to some initial state. In those cases, you might want to the user to confirm the action before proceeding. This can be accomplished by flipping to a hidden page to display a traditional "Are you sure?" message with OK/Cancel or Yes/No buttons but this is a tedious and heavy-handed approach.

This repo contains code for a 2-stage button. Touch/Click once to put the button into a confirmation mode, where it will flash the configured color. Touch/Click again to confirm and the action will proceed. If the user does not make the 2nd touch/click within the confirmation timeout period the button will stop flashing and return to idle.

There are two constant values within the code that the programmer can tweak:
```
local CONFIRM_TIMEOUT_SECS = 3
local FLASH_RATE_MS = 140
```

* **CONFIRM_TIMEOUT_SECS** - Number of seconds in the confirmation timeout period. This is the number of seconds the user has to make the 2nd touch/click before the button returns to idle state.
* **FLASH_RATE_MS** - Number of milliseconds between each flash cycle. The lower the number, the faster the flashing rate.

All Lua code is attached to the button control - _btnInit_ in the example.

The code position where the programmer should perform the confirmed action is here, located in the _onValueChanged()_ handler:
```
-- TODO: Do confirmed action here
    print('Do action')
```

Note that the example code disables the button before performing the action in order to prevent multiple touch/click events while the panel is "busy" performing the action. It is important to remember to re-enable the button after the action is completed. For example, if your button sends a MIDI sysex string to change the state of connected hardware, the button should be re-enabled after the hardware has confirmed processing is complete (if possible) or after the MIDI message send function has returned.

# Links
 * [Hexler TouchOSC](https://hexler.net/touchosc)
 * [TouchOSC Scripting API](https://hexler.net/pub/touchosc/scripting-api.html)
