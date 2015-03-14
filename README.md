#Description#

Many text editors have a 'Find in Files' function which shows exactly where in each file some text occurs. Then you can select each instance and jump to that location in the file(s) you are interested in.
ROX Edit does not have this feature. So rather than add it to ROX Edit, I figured it would be better as a standalone utility - then you could use it with your favorite editor.

#Instructions, etc.#

Find is simply a shell for find|grep or equivalent. It comes pre-installed with typical settings for these command line apps that should work for most people. If you have different needs, or have different find|search utilities, you can probably (possibly?) edit the standard settings to work.

To start a search you must enter a Path to search in (using '~' for your home directory works), a Pattern of text to search for (either plain text, or a regular expression, or whatever your custom find utility wants), and finally a Files specification to describe what files to search in and which to ignore (e.g. **.txt).

NOTE: You cannot execute a Find until all 3 text fields have some data in them. This is because just searching for files without specifying content is not what this application is all about.

![http://rox-find.googlecode.com/files/find.png](http://rox-find.googlecode.com/files/find.png)

Clicking the Find button will execute the find|grep command in the background and capture its output in the results window. While the Find is running, the Find button will be slightly grayed out and effectively becomes the Cancel button. The search results window is NOT cleared after each search, so that search results can be combined and reviewed later. Each set of results is headed by a row that shows the search criteria for that search, and allows that section to be collapsed/expanded.

If you double-click on the results in the Text or Line columns, your editor will open the file at the selected line (depending on which editor you are using). If you double-click on the Filename column, a ROX Filer window will open showing the location of that file.

Each of the Path | Pattern | Files fields will store up to the 10 most recently used entries.

There are options to Match or ignore text case (the Pattern, not the Files), Match whole words or not, Ignore binary files and search only the specified path or all of its subdirectories too. Each of these is configurable in the Preferences dialog.

The Find Command is defined in the Preferences dialog in the first text box that appears.

By default the following is used:

    'find "$P" $R -name "$F" -exec grep -Hn $C $B "$T" "{}" \;'


This can be modified to do things like ignore certain directories. For example to ignore all Subversion (or CVS?) hidden folders, use the following:

    'find "$P" $R -name "$F" \! -path "*.svn*" -exec grep -Hn $C $B $W "$T" "{}" \;'


If you know how to use find and grep well, you can customize this to suit your needs. If not, the default should work for most cases.

![http://rox-find.googlecode.com/files/options.png](http://rox-find.googlecode.com/files/options.png)

The find command contains several optional items that are replaced at runtime with different content as specified in the preferences dialog and controlled by the options checkboxes in the main UI window.

For each checkbox state, there is a text field that specifies what to add to the find command string. If the text field is empty, then nothing is added (but the replacement key is removed). Again, the defaults are chosen to work with standard (GNU?) find and grep, but these can be changed to suit.

So, the original find command:

    'find "$P" $R -name "$F" -exec grep -Hn $C $B "$T" "{}" \;'


is changed at runtime, in a typical case, to something like:

    'find "/home/user/textfiles" -name "*.txt" -exec grep -Hn -I "money" "{}" \;'


Finally, the Edit command allows you to specify your favorite editor to open the files and (hopefully) jump to the location of the found text.

By default the Edit command is blank. In this case, Find uses ROX' built-in 'text/plain' file handler to open the files. However, in this case the editor will not jump to the site of the found text. If you use ROX Edit, you can use the following command to enable this:

    /path/to/ROX-apps/Edit/AppRun $File -l $Line


Where $File is replaced with the filename, and $Line is the location of the found text. Many other text editors can also be made to function in this manner.

#Release History#

007 (2005-11-27)

  * Bugfixes for Cancel and Close
  * Switched to TreeView and add search section headers (collapse/expand)
  * Suppress error output from find/grep in results window
  * Increasingly non-blank README file

006 (2005-11-26)

  * UI redesign by Thomas Leonard
  * History items added to top of list (most recent at top)
  * Support '~' in Path field for home directory
  * non-blank README file :)

005 (2005-05-31)

  * It finally works with gtk < 2.4
  * works with certain other versions of gtk ??
  * Support for command line options
  * New 'Match Whole Words' feature.

004 (2005-05-29)

  * New options: Ignore binary files, Match case, Recurse Subdirectories
  * key executes Find
  * More gtk < 2.4 support

003 (2005-05-26)

  * Text entry fields are combo-boxes with history
  * Bug fixes

002 (2005-05-23)

  * Added toolbar button sensitivity
  * Bug fixes

001 (2005-05-22)
ToDo:

  * Right-click menu to perform other actions on found files
  * Support for multiple file patterns (e.g '**.c **.cpp **.h')
  * See the TODO file for more

Share and enjoy!
