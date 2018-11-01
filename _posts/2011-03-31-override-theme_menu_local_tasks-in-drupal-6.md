---
layout: post
title: Override Theme Menu Local Tasks in Drupal 6
---

Today I needed to hide the Signups tab on user profiles, but sadly, there
aren't any CSS classes to target the item I needed to hide. Because there is
no way to alter local menu tasks in Drupal 6, I had to write some logic in a
custom module to override the `theme_local_menu_tasks` function, and scrub the
link using a regular expression.

<!--more-->

```php
/**
 * Implementation of hook_theme_registry_alter().
 *
 * Hook our module in to the theme rendering chain.
 */
function mymodule_theme_registry_alter(&$theme_registry) {
  }
  if (!empty($theme_registry['menu_local_tasks'])) {
    $theme_registry['menu_local_tasks']['function'] = 'mymodule_menu_local_tasks';
  }
}

/**
 * Overrides theme_menu_local_tasks().
 */
function mymodule_menu_local_tasks() {

  // Remove the 'Signups' link on the user profile local tasks.
  $output = theme_menu_local_tasks();
  if (!user_access('sign up for content')) {
    $output = preg_replace('/<li[^>]*><a[^>]*>Signups<\/a><\/li>/', '', $output);
  }
  return $output;
}
```

That was enough to hide the Signups tab for users that are not allowed to
signup.  There is an issue in core Drupal 7 that tries to address the issue of
being able to alter the menu tasks: http://drupal.org/node/599706
