# Tweet Deletion Automation #
> Doing it the DIY way.

## Usage
1. Open the Page instructed in the [Action](#Actions) you intend to use.
2. Right Click and select Inspect (depending on your Browser, you might need to separately enable Developer Tools).
3. Open the Console (usually by selecting the Console tab at the top of the developer tools, if the console isn't already opened at the bottom of the developer tools)
4. Copy the action you intend to use, that is the bit that starts with `setInterval(() =>...` and ends with `...}, 1000);`
5. Paste the action you intend to use and press enter. Now might be a good time to look into the Notes Section below.
6. Wait until everything has been deleted.

## Notes
* Do not run multiple actions at once, you might run into issues with the Twitter API timing out.
* while an Action is running the tab **likely** needs to stay in the Foreground, you **might** need to put it in a window in the background instead of minimizing it or using a different Tab in the same window.
* if any of the actions spontaneously stop working, try reloading or come back in a while.
* Actions might or might not have issues with threads, reloading usually helps.
* if you get errors that say something like object not found, these actions might be broken. ([Maybe try this](#Selectors))
* if you get errors with page loading, try to readjust the [timing](#Timing).

## Modifications
### Selectors
* For this you will need to poke around Twitters HTML yourself, use the Element-picker (usually located in the top-right of the Developer Tools)
* from this point on you will need to go through the action of one deletion and find the right selectors for the buttons.
* replace or expand the actions for this you will need some javascript knowledge.

### Timing
Each of the `setInterval(())` and `setTimeout(())` functions end with `...}, 500);`
Example:
```
setInterval(() => { # A0
  # there will be code here in the example
  setTimeout(() => { # B0
    # this code will run after the timeout
  }, 500); # B1
}, 1000); # A1
```
A0 and A1 encapsulate the entire loop, so 1 loop is deleting 1 tweet.
B0 and B1 encapsulate one subroutine, for example, waiting for a menu to open.

Change the numbers on the lines A1 and B1 to change the pace of the respective encapsulating code, the values are the wait time in milliseconds (60000 is a minute; 1000 is a second).

## Actions
### Delete Tweets
> Open your Profile with the Tweets tab open.
```
setInterval(() => {
  let a = document.querySelector("div[data-testid=\"caret\"]:first-of-type");
  if (a) {
    a.scrollIntoView({block: 'center'});
    a.click();
  } else {
    window.scrollTo(0, document.body.scrollHeight);
  }
  setTimeout(() => {
    let b = document.querySelector("div[data-testid=\"Dropdown\"]:first-of-type > div:first-child");
    b.scrollIntoView({block: 'center'});
    b.click();
  }, 500);
  setTimeout(() => {
    let c = document.querySelector("div[data-testid=\"confirmationSheetConfirm\"]:first-of-type");
    c.scrollIntoView({block: 'center'});
    c.click();
  }, 500);
}, 1000);
```

### Delete Retweets
> Open your Profile with the Tweets tab open.
```
setInterval(() => {
  let a = document.querySelector("div[data-testid=\"unretweet\"]:first-of-type");
  if (a) {
    a.scrollIntoView({block: 'center'});
    a.click();
  } else {
    window.scrollTo(0, document.body.scrollHeight);
  }
  setTimeout(() => {
    let b = document.querySelector("div[data-testid=\"unretweetConfirm\"]:first-of-type");
    b.scrollIntoView({block: 'center'});
    b.click();
  }, 500);
}, 1000);
```

### Delete Likes
> Open your Profile and open the Likes tab.
```
setInterval(() => {
  let a = document.querySelector("div[data-testid=\"unlike\"]:first-of-type");
  if (a) {
    a.scrollIntoView({block: 'center'});
    a.click();
  } else {
    window.scrollTo(0, document.body.scrollHeight);
  }
}, 1000);
```
