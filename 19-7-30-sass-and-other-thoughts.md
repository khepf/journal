- Looks like the dart sass converter, when converting from .sass to .scss, expands all the selectors and removes all comments. How could anyone think this is acceptable. I am on the lookout for a sass converter that maintains formatting, which, I wouldn't think should be that big of a deal considering foth formats support nesting, and, comments.

- Spent almost 3 hours last night debugging the TeamSkipper backend while implementing environment variables. server.ts was the only file that was recognizing the env variables. Turns out the issue was dotenv wasn't required high enough in the server.ts code, so when the db tried to call the variable, it was undefined, which in turn , did not make typescript happy. Console.logging to the rescue!

