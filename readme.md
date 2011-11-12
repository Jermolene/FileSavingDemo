# Experimental Standards-Compliant File Saving for TiddlyWiki

This experiment is exploring one of the approaches to allow TiddlyWiki to be able to save changes on any standards-compliant browser, without needing the browser-specific hacks that we've relied on in the past.

## Introduction

The approach here is to encode the data to be saved as a base64 `data:` URI, and then simulating a click on a link to that URI. By carefully crafting the link, most modern browsers can be forced to automatically download the data as a file in the default download directory. It works better on some browsers than others; notably only Google Chrome allows the filename of the downloaded file to be specified. Some browsers also give security warnings when the file is saved and/or reopened.

## User Experience

This means that the user experience goes something like this:

1. Load TiddlyWiki into the browser
2. Make changes and edits
3. Click the `save` command (or invoke it's keyboard shortcut)
4. The newly modified TiddlyWiki file will be downloaded to your `downloads` folder
5. Keep clicking `save` after each edit and each time a new copy of the file will be saved
6. Afterwards, the newest of the downloaded files will contain the latest content

It's really not a perfect experience, but it is very exciting that it works on more or less any browser.

## Browser Details

Here is a summary of testing the demo on various browsers.

### Safari OS X 5.1.1

* The file is downloaded under the name `Unknown` (or `Unknown-1`, `Unknown-2` etc if the file already exists)
* The first attempt to open the file causes OS X to display a warning dialogue about opening files downloaded from the Internet
* Once downloaded the file has to be manually renamed to have a `.html` extension before Safari will reopen it successfully

### Firefox OS X 6.0

* Firefox displays a prompt to open or save the file
* The file is saved under a random name with the extension `.part` (for example `IShr3ZJF(1).part`)
* Firefox will happily reopen the file without renaming it, and without displaying a warning dialogue

### Chrome OS X 16.0.912.36 beta

* Chrome displays a prompt saying "This type of file can harm your computer. Do you want to keep SavedFile.html anyway?", and the user must manually click `Keep`
* The saved file is called `SavedFile.html` (or `SaveFile (1).html`, `SavedFile (2).html` etc if the file already exists). The string "SavedFile" is hardcoded into the demo
* Chrome will happily reopen the downloaded file without displaying a further warning dialogue

### Opera OS X 11.52

* Opera displays a prompt to open or save the file
* Choosing to save the file brings up another dialogue for the filename to be specified
* Opera will happily reopen the downloaded file without displaying a further warning dialogue

### iOS

An adaptation of this technique can even work on iOS devices: on those devices it's possible to long click on the `data:` URI link and select to save it as a bookmark. Subsequently invoking that bookmark will reload the modified file.

