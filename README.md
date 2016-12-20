# CoreBrowser

[![Build status](https://ci.appveyor.com/api/projects/status/2i85nqapq6i2ed0v?svg=true)](https://ci.appveyor.com/project/ollejacobsen/corebrowser)
[![Build Status](https://travis-ci.org/ollejacobsen/CoreBrowser.svg?branch=master)](https://travis-ci.org/ollejacobsen/CoreBrowser)

A simple web file system browser build with .NET Core and MVC6. 
Replacement for the standard web "directory browsing". Runs on Windows, Linux and OSX.

You can see a demo at [http://corebrowser20161026075844.azurewebsites.net/](http://corebrowser20161026075844.azurewebsites.net/)

## Features
The idea is that CoreBrowser will display the content of a directory.
A simple sort-by is implemented in the UI as well as file type icons and modal image browser.

## HeaderContent
If you place a file named "_headerContent.md" in a directory. 
This will get parsed and the content will be displayed in the top for that folder.

The header file is by default excluded from the directory listing.

You can configure the name of the file in `Startup.cs`  (see Configuration below).

## Exclude files
You can exclude files from the directory listing. Both by extension and a full file name.

This is done by modifying `Startup.cs` (see Configuration below)

## Appsettings
In the file appsettings.json there is a CoreBrowser section that you can tweak.

Example:
```
	"CoreBrowser": {
		"FilesRootFolder": "{wwwroot}/files",
		"GaTrackingUA": "",
		"TitleSuffix": "CoreBrowser"
	}
``` 
### FilesRootFolder
Used to set the root folder for the browser. Absolute path on disc or you can use the {wwwroot} placeholder to map a folder in the wwwroot.

### GaTrackingUA
Used for Google tracking.

### TitleSuffix
Used to build the `<title>` element.

## Configuration
Example:
```
    var conf = new FileSystemConfiguration(...)
                .AddExcludedFileNames("web.config")
                .AddExcludedFileExtensions(".hidden,.secret")
                .SetDirectoryHeaderFileName("myCustomHeaderFile.md")
                .Build();

    services.AddTransient<IFileSystemService>(x => new FileSystemService(conf));
``` 

### Security note
A user cannot download a file that are hidden from the directory listing. Even though the file path is supplied.
All downloads are passed though an Action that does some sanity checking before serving the files.


## License

MIT &copy; Olle Jacobsen