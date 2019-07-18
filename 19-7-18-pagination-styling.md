
The end goal is for the Pagination Buttons to have the same visual look and feel, statically and interactively, as the normal

Buttons.  This might be accomplished by just copy/pasting the Button Style Overrides directly, but given that in Vuetify the

Pagination Buttons have their own separate styles, the actual Pagination Style Overrides _implementation_ may very well be

different.

The Buttons Styleguide page gives you a handy reference for how the styles should look.  Take note, however, that there are

distinct Hover, Press, and Active styles.  These are represented in the Button Style Overrides, though, but due to how Vuetify

base styles are implemented, and thus how the Overrides are implemented, they can be a bit hairy to parse through. 

My recommendation is to keep both the Button Override Styles and the Pagination Base Styles open for reference.  For the Button Override Styles, I started by just copy/pasting the original Vuetify Button Base Styles because Stylus Braceless and SASS are actually almost identical, especially with nesting selectors.

Then, just comment out all the actual styles, leaving just the selectors themselves, and start putting in overrides as necessary.  Note that the way Vuetify implemented their theming will require its own little section of that overrides file, but we currently only need to worry about light theming, so you can probably just not worry about dark theming at all.

The actual implementation may be somewhat different, but you're trying to match the visual effects, not the implementations.  The implementation is just a vehicle to create the actual visual effects.




