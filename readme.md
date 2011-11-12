Experimental Standards-Compliant File Saving for TiddlyWiki
-----------------------------------------------------------

This experiment is exploring one of the approaches to allow TiddlyWiki to be able to save changes on any standards-compliant browser, without needing the browser-specific hacks that we've relied on in the past.

The approach here is to encode the data to be saved as a base64 `data:` URI, and then simulating a click on a link to that URI. By carefully crafting the link, most modern browsers can be forced to automatically download the data as a file in the default download directory. It works better on some browsers than others; notably only Google Chrome allows the filename of the downloaded file to be specified. Some browsers also give security warnings when the saved file is reopened.

This means that the user experience would go something like this:

1. Load TiddlyWiki into the browser
2. Make changes and edits
3. Click the `save` command (or invoke it's keyboard shortcut)
4. The newly modified TiddlyWiki file will be downloaded to your `downloads` folder
5. Keep clicking `save` after each edit and each time a new copy of the file will be saved
6. Afterwards, the newest of the downloaded files will contain the latest content

It's really not a perfect experience, but it is very exciting that it works on more or less any browser. An adaptation of the technique can even work on iOS devices: on those devices it's possible to long click on the `data:` URI link and select to save it as a bookmark. Subsequently invoking that bookmark will reload the modified file.
