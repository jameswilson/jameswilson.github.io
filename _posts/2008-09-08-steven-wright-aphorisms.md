---
excerpt: 'A simple PHP script that wraps the linux fortune command to provide a random quote from american comedian Stephen Wright.'
categories:
    - Web development
layout: post
title: Steven Wright Aphorisms
created: 1220912923
---
For fun today I learned how to <strong>run a bash script from PHP</strong>, and implemented everybody's favorite command line utility:  <strong>fortune</strong>!  The script takes advantage of php's <code>exec()</code> command, and ended up looking something like this:

<pre lang="php" line="1">
<?php
exec ("/opt/local/bin/fortune -s", $lines_of_output, $error_code);
if (!$error_code) {
	foreach ($lines_of_output as $line) {
		print $line."\n";
	}
} else {
	print "script failed with exit code $error_code, see http://tldp.org/LDP/abs/html/exitcodes.html";
}
?>
</pre>

Check out the two beta versions I've created here (Hit refresh in your browser to get a new fortune).

<ul>
<li><a href="http://projects.elementalidad.com/fortune/" target="_blank">Your daily online fortune cookie.</a></li>
<li><a href="http://projects.elementalidad.com/fortune/steven-wright.php" target="_blank">Steven Wright aphorisms.</a></li>
</ul>

These are meant to be part of a larger project intended to expose these quotes via RSS to incorporate them into some dynamically created "signature" lines, which is part of some new Gmail functionality available from Google Labs.

