---
layout: post
title: Some useful Keyboard Shortcuts for Developers on Mac
---

At Bluespark we use [KnowYourCompany.com](https://knowyourcompany.com) to ask interesting questions of team members every week.

This week's internal team question was a particularly interesting one for me so I decided to share it more widely:

> # What are some of your most-used keyboard shortcuts (Mac or Windows)?    

I use keyboard shortcuts on Mac a lot so prepare yourself for my very liberal
interpretation of "*some*" because most of these I do use on a daily basis.

## macOS/OSX Standard shortcuts:

These shortcuts come standard on all Apple Macintosh machines running OSX or macOS.

Shortcut | Description
----- | -----
`⌘⇧3` | Take a fullscreen screenshot (I have screenshots setup to save to a custom folder in Bluespark Dropbox). 
`⌘⇧4` | Cross-hairs to select a screen area for a non-fullscreen screenshot. 
`⌘SPACE` | Open Spotlight; used as an app launcher. 
`⌥⌘SPACE` | Open Finder search. 
`⌥⌘→/←` | Depends on application, but usually switches tabs within an application. 
`⌘TAB` | Switch applications (I hide my dock and use this to switch between apps). 
`^⇧↓` | Show all windows of current app, then use right/left arrows to navigate through and select a window with space bar. 
`^⇧↑` | Shows all windows on current desktop. 
`⌘Q` | Quit current app. 
`⌘W` | Close current window (or tab) without quitting app. 
`⌘N` | Open new item (depends on app). 
`⌘T` | Open new tab (depends on app; works on Finder, Chrome, Terminal). 
`⌘,` | Open current app preferences.

## macOS/OSX custom curated shortcuts:

Custom global shortcuts can be added via  › System Preferences › Keyboard › Shortcuts ›
App Shortcuts › All Applications.  You need to save the title of the menu item. More information
can be found in [this KB article on support.apple.com](https://support.apple.com/kb/PH25372).

Shortcut | Description
----- | -----
`⌥⌘,` | Open System Preferences. Store the menu item as `System Preferences...`
`^⇧SPACE` | Change keyboard language. 🇺🇸🇪🇸🇫🇷
`⌥⌘V` | Paste from [Flycut](https://itunes.apple.com/us/app/flycut-clipboard-manager/id442160987?mt=12) clipboard manager. (Configured directly in app).

## Word processing (standard macOS/OSX shortcuts): 

Note these work in any word processing app, including Terminal, Notes, Mail, Evernote, Chrome, etc. 

Shortcut | Description
----- | -----
`^A` | Goto beginning of current line. (`⌥↑` sometimes also works).
`^E` | Goto end of current line. (`⌥↓` sometimes also works).
`^⇧A` | Select text from current position to beginning of line. 
`^⇧E` | Select text from current position to end of line.
`⇧↑` | Select the line above. 
`⇧↓` | Select the line below.
`⌥→/←` | Goto start/end of current word. (Doesn't work consistently in all applications).
`⌥⇧→/←` | Select text from current position to start/end of current word. (Doesn't work consistently in all applications).
`⌫` | Delete previous letter.
`fn⌫` | Delete next letter.
`⌥⌫` | Delete text from current position to beginning of line.
`^K` | Delete text from current position to end of line.

## Google Chrome (standard shortcuts): 

Shortcut | Description
----- | -----
`⌘⇧⌫` | Delete browser cache.
`⌥⌘I` | Open Chrome Developer Tools panel, then once launched, Fn+F1 opens settings panel to disable Javascript.
`⌘⇧N` | Open Private Browsing window; useful for testing unauthenticated version of sites while logged in on normal browser session.

## Google Chrome (custom URL bar shortcodes):

Add/edit these in Settings › Manage search engines.  The `%s` in URLs will be used as substitution for the search string in `<CODE>`.

Keycode |  Description / Query URL
---------- | ---------------------
`j <ISSUE_ID>` | Goto JIRA Issue page. <br> `https://<yourcompany>.atlassian.net/browse/%s`
`j <PROJECT_ID>` | Goto JIRA Issues listing for project. <br> `https://<yourcompany>.atlassian.net/browse/%s`
`jpi <PROJECT_ID> <some string>` | Execute a JIRA contextual project text string search. <br> `https://<yourcompany>.atlassian.net/secure/QuickSearch.jspa?searchString=%s`
`c <PROJECT_ID>` | Open Confluence space for specified project. <br> `https://<yourorg>.atlassian.net/wiki/display/%s`
`dn <ISSUE_ID>` | Open the specified Issue on drupal.org. <br> `https://www.drupal.org/node/%s`
`da <FUNCTION>` | Search for function name on api.drupal.org. <br>  `https://api.drupal.org/%s`
`dp <MODULE>` | Goto module page on Drupal.org. <br> `https://www.drupal.org/project/%s`
`dpi <MODULE>` | Goto issue queue on Drupal.org. <br> `https://www.drupal.org/project/issues/%s`
`ghb <REPO>` | Open Repo on your organization's Github account. <br> `https://github.com/<yourorg>/%s`
