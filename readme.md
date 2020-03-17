**Where to find the releases?**
The link to the releases is somewhat hidden in plain sight - to help with this, you can just click this link to get to the releases page: https://github.com/seanmcne/OrgDbOrgSettings/releases 

**Project Description**
This is a utility allowing admins of Dynamics CRM Online & onPrem (2016) to edit  organization database settings otherwise known as OrgDBOrgSettings

This utility allows you to edit your settings without the use of the command line utility in the KB article documenting "OrgDBOrgSettings."  The utility is written using the CRM SDK as a reference and currently all changes and retrieval of settings are done via the CRM's OData Endpoint.  The utility is provided as a managed webresource that can easily be installed and uninstalled from your CRM environment.  

**Where to I find it after installing?**
The OrgDBSettings utility is installed as a managed CRM solution. As a result I have decided to keep it out of the sitemap and leave it as a Configuration Page in the solution.  To find the editor, go to "Settings", then "Solutions", within the solutions double click on "Organization Settings Editor" this will launch the solution configuration automatically. 
_Note: During beta testing I received feedback asking for the utility to have it's own place in the sitemap however, after discussing with some partners and developers they suggested leaving it out due to possible dependency conflicts._

Browser Supportability: 
- CRM v9.0 and higher in Edge (Chromium), Edge, Chrome, Firefox, and Safari on Mac.
- NOTE: Some browser configurations block XDR's (cross domain requests) and thus will not get the benefit of update warnings - if you're impacted by this you can disable any addins that block these requests, alternatively keep checking back on this site for updates. 
- If you must use IE, please use another browser such as Edge https://aka.ms/GetEdge - for folks who are stuck with IE talk to your IT Department about using modern browsers, if you are absolutely stuck you can read this article on [CRM Disable IE Compatibility Mode](CRM-Disable-IE-Compatibility-Mode) however, I'm not planning on making changes to accomidate IE at this point in time given that most have moved on to modern browsers now. 

![](Home_OrgDbOrgSettings2013UR1.png)

The importing of this managed solution will include the following components: 
- JQuery [http://jquery.com/](http://jquery.com/)
- JSON2 [http://www.json.org/](http://www.json.org/)
- OrgDBOrgSettings.html [How to use the editor](How-to-use-the-editor)
- settings.xml [What is Settings.xml](What-is-Settings.xml)
- Azure Mobile Apps [Azure Portal](http://portal.azure.com), MSDN [AzureMobile Services](https://azure.microsoft.com/en-us/services/app-service/mobile/) - this service is used for the browser to call back and check for any new updates of the editor solution (and prompt you to download an update, if one is available). 

**How do I install just the zip file from this site?**
- Go to the releases page https://github.com/seanmcne/OrgDbOrgSettings/releases 
- Download the zip release - *do not download the source, make sure to download the solution zip file* 
![](Home_OrgDbOrgSettingsDownload1.png)
- Once you download the zip file upload this solution into your CRM/CE/CDS instance by navigating to Settings | Solutions then click the Import button in the command bar. 
- Once completed you now can use the editor to alter any settings that need to be changed or viewed
