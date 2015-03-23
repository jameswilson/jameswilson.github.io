---
layout: post
title: Customize the Drupal 6 Comment Form
---

Originally I found this site that said this could be done within the theme, but
I ended up going for a hook_form_alter.

http://pastebin.com/DJ47XUMy

{% highlight php %}
// Put this in mymodule.module

/**
 * Implementation of hook_form_alter().
 */
function mymodule_form_alter(&$form, $form_state, $form_id) {
  switch ($form_id) {
    case 'comment_form':
      // Rename some of the form element labels.
      $form['name']['#title'] = t('Name');
      $form['homepage']['#title'] = t('Website (optional)');

      // Add some help text to the homepage field.
      $form['homepage']['#description'] = t('If you have your own website, enter its address here and we will link to it for you. (please include http://).');
      $form['homepage']['#description'] .= '<br/>'. t('eg. http://www.mysite.com');

      // Remove the preview button
       $form['preview'] = NULL;
      break;
  }
}
{% endhighlight %}
