SublimeText2-FTPSync
====================

Simple and free plugin for FTP syncing. Just hit the _save_ as usual and it's upped.

Recently:
* Started [Wiki](https://github.com/NoxArt/SublimeText2-FTPSync/wiki/_pages)
* FTPSync checks upon opening a file whether there's a new version of this file on a server
(checks only on file load, not when the file is loaded from cache)
* You can also check manually by *FTPSync: Check current file* command
* Fixed [issue #13](https://github.com/NoxArt/SublimeText2-FTPSync/issues/13)

What's there for you?
* Multiple named upload targets
* Ignored file regex patterns
* Secure transfer using TLS
* Manual multiple file & folder uploading (sidebar context menu)
* Manual multiple file & folder downloading (sidebar context menu)
* Progress bar for multiple up/download

Current focus:
* Remote vs local file _last\_updated_ detection
* Resolving downloading from more locations
* SFTP support



How to use
----------

To mark a folder and descendants for upload insert *ftpsync.settings* file in following format. Don't worry - the skeleton can be simply inserted using *Preferences > Package Settings > FTPSync > Setup FTPSync in this folder* or using context menu in Side bar or using Control/CMD+Shift+P.

Format:

    {
    	<connection_name>: {
    		host: {string},

    		username: {null|string=null}, // null means anonymous manipulation
    		password: {null|string=""},

    		path: {string="/"}, // remote root for these files

            upload_on_save: true, // whether upload on save or manually
            download_on_open: false // whether to check upon openning a file whether there's a new version on the server and offer download

    		port: {int=21}, // remote port, pretty much always 21, unless SFTP
    		tls: {bool=false}, // set true to use secured transfer, recommended! (server needs to support)
            passive: {bool=true}, // whether to use passive or active connection
    		timeout: {int=30}, // seconds to invalidate the cached connection
    		ignore: {null|string} // regular expression, matched against file path - not applied for downloading
    	} //,
        // <connection2_name>: { ... }
    }

Files are automatically uploaded **on save** (unless disabled by _upload\_on\_save_=false setting).



About
-----

Done by **@NoxArt** ~ [Twitter](https://twitter.com/#!/NoxArt)

Released under MIT licence.

Feel free to add issues, ideas, pull requests...

Thanks to [castus](https://github.com/castus), [tommymarshall](https://github.com/tommymarshall), [TotallyInformation](https://github.com/TotallyInformation), [saiori](https://github.com/saiori), [vnabet](https://github.com/vnabet) and [Jcrs](https://github.com/Jcrs), [ItayXD](https://github.com/ItayXD), [bibimij](https://github.com/bibimij), [digitalmaster](https://github.com/digitalmaster) for reporting issues, ideas and fixing!



Tips
----

* **Working from more places? Or in team?**
You can either use *download_on_open=true* to check files upon openning or *FTPSync: Check current file* command to see whether you have the same version as is on all servers.

* **Upload different language versions to different servers of paths**

        {
        	<connection_name>: {
        		host: "ftp.host.en.com",
        		ignore: "/locale/(?!fr)\\w+/.*"
        	},
        	<connection2_name>: {
        		host: "ftp.host.cz.com",
        		ignore: "/locale/(?!cz)\\w+/.*"
        	}
        }