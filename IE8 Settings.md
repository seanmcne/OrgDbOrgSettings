Also See: [CRM Disable IE Compatibility Mode](CRM-Disable-IE-Compatibility-Mode)

This utility is intended for use in IE8 and higher as well as Chrome, Firefox, and Safari on the Mac. If your CRM Server URL is in the intranet zone in IE8 or 9 you may see a warning about automatic update failing.  This is due to IE forcing your browser into Compatibility Mode for various sites (which most likely includes your CRM Server).  Without getting into the deep technical details - if you wish to have update checking and you're on IE8 or 9 here is how you can enable it: 

#### Options: 
# Disable Automatic Compatibility Mode in IE. 
	* Open Internet Explorer 8 or 9 (does not apply to IE10)
	* Click the "Tools" button (if you don't see this - press your "Alt" key to show the menus) 
	* Click Compatibility View Settings
	* Remove the CRM URL from the compatibility view list if it is there 
	* Uncheck "Display intranet sites in compatibility view" NOTE: This may impact intranet sites other than CRM. 
	* Uncheck "Display all websites in compatibility view"
# Upgrade to IE10 for Windows 7 or Windows 8 
	* IE10 now natively supports CORS!  To take advantage of this download [IE 10 here](http://ie.microsoft.com/testdrive/Info/Downloads/Default.html)
	* NOTE: I've been using IE10 on Windows 7 since the earlier betas and have had very few issues, I highly recommend it :) 
# Force the standards mode 
	* Once the page is opened in IE press F12 to open the debugger tools (this has to be done 
	* In the top menu set the **Browser Mode** to: IE8 Standards mode 
	* this settings is not 'sticky' and will have to be done every time you browse the page 
# Ignore the error and frequently check back [here](https://orgdborgsettings.codeplex.com/releases) for updates. 
# Last resort and not recommended :)
	* If you wish to use FireFox, Chrome, or Safari on the Mac you'll need to be on **CRM UR12 or higher** and you'll have to **disable HTC's** (done via your system settings or via OrgDbOrgSettings using this utility). 
