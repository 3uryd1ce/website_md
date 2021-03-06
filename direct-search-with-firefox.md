# Search sites directly with Firefox

Many people use a search engine to navigate the Internet. However, not
everyone knows that Firefox's[^1] "add keyword" feature allows one to
directly search any website with an input field.

[^1]: Anything based on Firefox, such as Tor Browser, can also make use
  of this feature (assuming the fork is sufficiently up to date).

As for why this is useful:

1. Searching directly is more private since it cuts out the
   middleman (default search engine).
1. It saves time.

Let's take [Wiktionary](https://www.wiktionary.org/) as an example,
a multilingual dictionary.

Navigate to Wiktionary and right click Wiktionary's input field. A menu
will pop up.

[![In a Firefox window displaying Wiktionary, the cursor is highlighting
the "Add a Keyword for this Search" option in a
menu.](/images/add-keyword-1.png)](/images/add-keyword-1.png)

Click the "Add a Keyword for this Search..." option. Firefox will now
present a dialog box asking for the name of the bookmark, the folder to
save the bookmark in, and a keyword (I chose `wkt`).

[![A dialog box that asks for the name of the bookmark, the folder to
save it in, and the
keyword.](/images/add-keyword-2.png)](/images/add-keyword-2.png)

Now, it's possible to type in `wkt` (or whatever was chosen as a
keyword) into Firefox's search bar followed by a word and find its
definition. Here is an exercise to test it: figure out what the difference
between somnambulism and funambulism is, and why the two probably
wouldn't go well together.

The ArchWiki, Wikipedia, and many other websites can be searched in this
fashion. In addition, keywords work with ordinary bookmarks too (for
instance, `awl` is mapped to the ["List of applications" ArchWiki
entry](https://wiki.archlinux.org/index.php/List_of_applications) on my
computer). The main difference with regular bookmarks is that nothing is
typed except the keyword since a query is no longer being performed.

I prefer the bookmark method over adding a site as a search engine for
two reasons:

1. Firefox doesn't present the "Add Search Engine" option as
   consistently as expected.
1. Using keywords minimizes mouse usage, which translates to searching
   faster.
