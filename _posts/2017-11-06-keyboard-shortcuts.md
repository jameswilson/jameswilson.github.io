---
layout: post
title: '⚡️ Mac Keyboard Shortcuts for Web Developers'
description: >-
    Learning keyboard shortcuts are a quick-win with long-term advantages that
    reduce context switching between keypad input and mouse input navigation.
---

<p class="intro">Learning keyboard shortcuts are a quick-win with long-term advantages that reduce context switching between keypad input and mouse input navigation.</p>

<!--more-->

As a Mac power user, I employ keyboard shortcuts extensively in my daily grind. As a developer I'm hardwired to look for opportunities to automate repetetive tasks.

This is why when this week's team question came up in our Wednesday email from [Know Your Company](https://knowyourcompany.com) I was excited to discuss my setup.

Team question from Know Your Company:

> What are some of your most-used keyboard shortcuts?

Unfortunately these posts are internal only, so I'm sharing my notes here as well. These shortcuts will be most helpful for Web developers running OSX or macOS, however there is something for everybody here, if you're not a developer you may want to skip down to the [word processing shortcuts section](#word-processing-shortcuts)

## Mac system shortcuts

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

## Customizing Mac shortcuts

Custom global shortcuts can be added via  › System Preferences › Keyboard › Shortcuts › App Shortcuts › All Applications.  You need to save the title of the menu item. More information can be found in [this KB article on support.apple.com](https://support.apple.com/kb/PH25372).

Shortcut | Description
----- | -----
`⌥⌘,` | Open System Preferences. Store the menu item as `System Preferences...`
`^⇧SPACE` | Change keyboard language. 🇺🇸🇪🇸🇫🇷
`⌥⌘V` | Paste from [Flycut](https://itunes.apple.com/us/app/flycut-clipboard-manager/id442160987?mt=12) clipboard manager. (Configured directly in app).

## Word processing shortcuts

There are a number of standard system shortcuts to help with word processing tasks like moving the cursor around on the line and making text selections.

These work in any word processor application including TextEdit, Mail, Notes, Evernote, Chrome, Terminal, etc. Developers that use Emacs will already be familiar with some of these.

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

## Google Chrome shortcuts

Shortcut | Description
----- | -----
`⌘⇧⌫` | Delete browser cache.
`⌥⌘I` | Open Chrome Developer Tools panel, then once launched, Fn+F1 opens settings panel to disable Javascript.
`⌘⇧N` | Open Private Browsing window; useful for testing unauthenticated version of sites while logged in on normal browser session.

## Google Chrome shortcodes

Short codes let you create auto-expanding URLs, straight from Google Chrome's URL bar. They can be created/edited in Settings › Manage search engines.  The format is `<shortcode> <string>` whereby the `<shortcode>` is a brief (one or two character) code that will be expanded to a full URL. The `<string>` value will be substituted into the URL in place of the `%s` placeholder.

Shortcode |  Description / Query URL
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
