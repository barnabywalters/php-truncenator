php-truncenator
===============

~ THE TRUNCENATOR ~ is the ultimate clean syndication function (and supporting functions)

If you’re implementing [POSSE](http://indiewebcamp.com/POSSE) to syndicate your content out to services like Twitter or Facebook, odds are you want to pre-process anything you send out to deal with problems like:

* Length limits
* Lack of HTML display

~ THE TRUNCENATOR ~ is a highly–configurable solution to these problems. Give it a string and some parameters and it’ll spit out something perfect for syndication.

## Features

* Truncate text to the nearest word boundary
* Append a URL
* If truncation took place, append an ellipsis (customisable, defaults to …)
* If truncation didn’t take place, surround the URL with parens

## Usage

Typical usage: Syndicating a note out to Twitter.

<pre><code>&lt;?php

$raw_string = 'If you’re using Chome and you quit accidentally, losing important text forever, don’t panic! It can be found in /Application Support/Google/Chrome/Default/Last Session (on a Mac) with a bit of digging around.';
$uri = 'http://waterpigs.co.uk/notes/198'; // Real example

$truncated = text\truncate($raw_string, $length=140, $uri=$uri, $urilen=20);

echo $truncated;
// EOF</code> </pre>

Results in:

> If you’re using Chome and you quit accidentally, losing important text forever, don’t panic! It can be… http://waterpigs.co.uk/notes/198

See the docblock on the function for more details.

### Supporting Functions

If you want to expand <code><img></code> elements into just their <code>@href</code> instead of stripping them out completely, the <code>expand_img()</code> function handles that:

<pre><code>&lt;?php

$raw_string = 'Hah! IndieWebCamp group animated gif: &lt;img src="https://dl.dropbox.com/u/49437/share/2012-07/30-gif-oBpKA1/f/animated.gif" alt="animated gif"&gt;';
$uri = 'http://waterpigs.co.uk/notes/216'; // Another real example

$truncated = text\truncate($raw_string, $length=140, $uri=$uri, $urilen=20);

echo $truncated;
// EOF</code> </pre>

Results in:

> Hah! IndieWebCamp group animated gif: https://dl.dropbox.com/u/49437/share/2012-07/30-gif-oBpKA1/f/animated.gif (http://waterpigs.co.uk/notes/216)

## Testing

I have written a load of phpunit tests and will commit them to the github project soon.

## Roadmap

What’s here is an initial, scruffy implementation to cater for my immediate needs. I plan on heavily refactoring bits of the code out into multiple separate functions as this is a surprisingly tricky problem to deal with.

If you have any ideas for other things ~ THE TRUNCENATOR ~ should do/how it should work, let me know or submit a pull request :)

## TODO

* Write more+better tests
* Improve config options (some of them aren’t actually being used)
* Refactor different stages into multiple functions
* Add ability to preserve hashtags at the expense of text