
> The end goal is for the Pagination Buttons to have the same visual look and feel, statically and interactively, as the normal
Buttons.  This might be accomplished by just copy/pasting the Button Style Overrides directly, but given that in Vuetify the
Pagination Buttons have their own separate styles, the actual Pagination Style Overrides _implementation_ may very well be
different.

> The Buttons Styleguide page gives you a handy reference for how the styles should look.  Take note, however, that there are
distinct Hover, Press, and Active styles.  These are represented in the Button Style Overrides, though, but due to how Vuetify
base styles are implemented, and thus how the Overrides are implemented, they can be a bit hairy to parse through. 

> My recommendation is to keep both the Button Override Styles and the Pagination Base Styles open for reference.  For the Button Override Styles, I started by just copy/pasting the original Vuetify Button Base Styles because Stylus Braceless and SASS are actually almost identical, especially with nesting selectors.

> Then, just comment out all the actual styles, leaving just the selectors themselves, and start putting in overrides as necessary.  Note that the way Vuetify implemented their theming will require its own little section of that overrides file, but we currently only need to worry about light theming, so you can probably just not worry about dark theming at all.

> The actual implementation may be somewhat different, but you're trying to match the visual effects, not the implementations.  The implementation is just a vehicle to create the actual visual effects.

http://localhost:3000/styleguide/buttons

https://ge.invisionapp.com/

1. Make border disappear on click
2. make border appear on hover

> The :hover pseudo-class applies when a pointing device interacts with an element without necessarily activating it.

> The :focus pseudo-class applies when an element is in a state that is ready to be interacted with, i.e. it has the focus of the input device.

> The :active pseudo-class applies during the period in which the element is being activated. For example, if using a mouse it would be the time between when the mouse button is clicked and when it is released.

> The :not(selector) selector matches every element that is NOT the specified element/selector.

> The ::before selector inserts something before the content of each selected element(s).

# Pagination Button Formatting

- styles/vuetify-overrides/_button-defs.scss
- styles/vuetify-overrides/_buttons.scss
- styles/colors.sass
