Also see: [IE8 Settings](IE8-Settings) 

Unfortunately the azure mobile update check can only function when IE is running in standards mode. To force standards mode in CRM, you can follow one of two options - both will result in the same outcome and ultimately are the same setting: 
* Use this editor to change the setting
	* find the **"disableIECompat"** setting in this organization settings editor.  
	* Add the value
	* Once added then Edit the value to **"True"**
	* Now press the F5 key in your editor or CRM browser window to inherit the new setting 

* Use CRM's setting admin page 
	* Click Settings, go to Administration, Open System Settings
	* in the system settings editor go to Customizations 
	* on the customizations tab **check** the checkbox value for **"Load pages in the most recent version of internet explorer."**
	* your browser window will now refresh to inherit the new setting 

Warning: After making this change you should test CRM for any impact to custom HTML pages, the biggest impact would most likely be to pages you're rendering in iFrames that violate browser standards.  If you're running cross browser already - this change should have no major negative impact. 