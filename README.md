# Apache2.4-PHP7-MySQL-and-phpMyAdmin-Configuration
This is a step-by-step configuration setup to create an environment for deploying applications on Apache server
and using phpMyAdmin to store data in database.


1. Download Apache, PHP, MySQL, phpMyAdmin...

•	Download Apache for Windows: https://www.apachelounge.com/download/

•	Download PHP 7 for Windows (select ‘Thread Safe’): http://windows.php.net/qa/

•	Download MySQL for Windows (select ZIP Archive): http://dev.mysql.com/downloads/mysql/

•	Download phpMyAdmin: https://www.phpmyadmin.net/

•	Download the latest C++ Redistributable Visual Studio 2017: (direct link to download the 64-bit version, a direct link to the 	         download of the 32-bit version).

•	Download Visual C++ Redistributable Packages for Visual Studio 2015: https://www.microsoft.com/ru-ru/download/details.aspx?             id=48145


You should have the following files :

•	httpd-2.4.29-Win64-VC15.zip

•	php-7.2.0-Win32-VC15-x64.zip

•	mysql-8.0.11-winx64.zip

•	phpMyAdmin-4.7.7-all-languages.zip

•	vc_redist.x64.exe

•	vcredist_x64.exe





![1-files](https://user-images.githubusercontent.com/20470279/60244809-3a71f880-9889-11e9-8199-cc14a33bdfb7.jpg)





First! you want to install the vc_redist.x64.exe and vcredist_x64.exe files for the platform to run apache, php, mySQL.

2. Create necessary folders...

On the drive C create a directory Server; inside that create the bin directory (where you will install Apache, PHP, and MySQL ) and data directory (where the apps and databases will be located).
In the data directory I created two folders:
	DB (for the database)
	htdocs (for the apps)


3. Install and configure Apache 2.4 on Windows...

Unpack the Apache files (archive httpd-2.4.25-win64-VC14.zip) to the C:\Server\bin\ directory (we are interested only in the Apache24 folder):


![3 0-apache](https://user-images.githubusercontent.com/20470279/60245038-b704d700-9889-11e9-806e-b25a53007b30.JPG)






3.1--> After unpacking, go to the “c:\Server\bin\Apache24\conf\” folder and open the “httpd.conf”  file with any text editor.





![3 0-bin-apache](https://user-images.githubusercontent.com/20470279/60245282-4a3e0c80-988a-11e9-81bd-dace7af2cc48.JPG)




Replace:  


Define SRVROOT "c:/Server/bin/Apache24 ” 


with  


Define SVROOT “c:/Apache24”



3.2-->Replace:    

“ #ServerName www.example.com:80”  


with


“ServerName localhost”


3.3-->Replace: 


DocumentRoot “${SRVROOT}/htdocs” 


with 


DocumentRoot “c:/Server/data/htdocs/”



The following picture displays how 3.2 and 3.3 should look after the correct changes have been made : 





![3 3-apache servr confg](https://user-images.githubusercontent.com/20470279/60245583-e5cf7d00-988a-11e9-8984-28877cfb5868.JPG)






3.4--> Replace :



“ DirectoryIndex index.html ”   



![3 4](https://user-images.githubusercontent.com/20470279/60245775-465eba00-988b-11e9-8216-d72c009ebe20.JPG)





with the following :



“ DirectoryIndex index.php index.html index.htm ”   



![3 4-replaced](https://user-images.githubusercontent.com/20470279/60245898-86be3800-988b-11e9-960a-e65ed624646e.JPG)



3.5--> Replace 



![3 5](https://user-images.githubusercontent.com/20470279/60246009-c7b64c80-988b-11e9-9027-616efd7aa7f7.JPG)




With the following :





![3 5 - replaced](https://user-images.githubusercontent.com/20470279/60246106-02b88000-988c-11e9-8867-0bf274442311.JPG)






3.6--> Replace :

“ #LoadModule rewrite_module modules/mod_rewrite.so ”

With 

“ LoadModule rewrite_module modules/mod_rewrite.so ”




3.7--> Save and close the file. Apache configuration is complete!




3.8--> Next! In windows, open the command prompt and make sure you run it as administrator! Copy-paste:


	c:\Server\bin\Apache24\bin\httpd.exe -k install
	

Then hit enter. If firewall prompt comes up just hit ‘Allow Access’.
Also, Copy-paste:


c:\Server\bin\Apache24\bin\httpd.exe -k start


![3 8-cmdprmpt-apcheInstall](https://user-images.githubusercontent.com/20470279/60246220-3e534a00-988c-11e9-89bf-b493155d9927.jpg)



3.9--> After Apache is started you need to follow the following link in your chrome browser :


“ http://localhost/ ”


you should see a windows page with a message that says the following : 


“ Index of / ”

![3 9](https://user-images.githubusercontent.com/20470279/60246756-655e4b80-988d-11e9-99b6-60f11af95fc4.JPG)




4.Installation and configuration MySQL 8.0 on Windows...


4.1-->	In the c:\Server\bin\ folder unpack MySQL archive (the mysql-8.0.11-winx64.zip file). Rename it to mysql-8.0 (just for short).

4.2-->	Go inside the mysql-8.0 folder and create my.ini file. Open this file with any text editor. Copy-paste the following lines:



![4-mySQL-ini](https://user-images.githubusercontent.com/20470279/60246996-d1d94a80-988d-11e9-97b6-9d9a3ee6919b.JPG)



4.3-->	Save and close it.


4.4-->	Configuration is complete! But you have to initiate and install mySQL 8.0 on your Windows so open the command prompt as Admin and run the following :


“ C:\Server\bin\mysql-8.0\bin\mysqld  --initialize-ins
  C:\Server\bin\mysql-8.0\bin\mysqld  --install
Net start mysql ”


When this process is done you should look inside the “ C:\Server\data\DB\data” folder and there should be automatically generated files that appear. You should see the following :


![4 2-MySQL-GeneratedFiles](https://user-images.githubusercontent.com/20470279/60247170-1ebd2100-988e-11e9-95a8-c4ce851c889c.JPG)




From here on out the MySQL service should start automatically with every Windows boot.



5.Installation PHP 7 on Windows...

5.1-->	In the c:\Server\bin\ create new PHP folder and copy there the contents of php-7.1.1RC1-Win32-VC14-x64.zip.

5.2-->	Again, open the c:\Server\bin\Apache24\conf\httpd.conf file and append it with lines you see inside of the red circle I made in the picture below (CORRECT php7 module you need to load on apache):


![5 1 -phpModules](https://user-images.githubusercontent.com/20470279/60247358-87a49900-988e-11e9-819d-ae39e0fab5f7.JPG)



5.3-->	Restart Apache using command prompt (run as administrator always!) :


“ C:\Server\bin\Apache24\bin\httpd.exe -k restart ” 


5.4-->	In the c:\Server\data\htdocs\ folder create i.php file and copy to there:


“<?php
phpinfo  ( ) ;”


5.5--> In a browser open the http://localhost/i.php address. If you see something like this,     it means PHP works:




![5 5-php7localhost](https://user-images.githubusercontent.com/20470279/60247685-19aca180-988f-11e9-8f07-bf23c10d865e.jpg)






6. Configuration PHP 7...

In the c:\Server\bin\PHP\ folder rename “ php.ini-development ” file to “ php.ini ”. Open it with a text editor. Find the following string : 



![6 0-extnsn_dir](https://user-images.githubusercontent.com/20470279/60247768-45c82280-988f-11e9-82f3-9acaf6194bf1.JPG)



and replace it with the following : 


![6 0-extnsn_replaced](https://user-images.githubusercontent.com/20470279/60247863-7b6d0b80-988f-11e9-88ad-e653e7268e6b.JPG)



6.1--> Now find the group of strings:


![6 1](https://user-images.githubusercontent.com/20470279/60247949-abb4aa00-988f-11e9-9e53-11c641cd09ca.JPG)



and replace it with the following :



![6 1-replaced](https://user-images.githubusercontent.com/20470279/60248281-5200af80-9890-11e9-86d5-08f064ec7478.JPG)




6.2--> Now uncomment this group of strings:



-	PICTURE 6.2 



They should look like:



-	PICTURE 6.2 replaced
	
  
  
6.3--> Save the file and restart Apache.





7. Installation and configuration phpMyAdmin on Windows...

To the “ c:\Server\data\htdocs\ folder ” copy the content of phpMyAdmin-4.6.5.2-all-languages.zip. 
Rename phpMyAdmin-4.6.5.2-all-languages to phpmyadmin (for brevity).
In the “ c:\Server\data\htdocs\phpmyadmin\ ” folder create config.inc.php file and copy there:



-	PICTURE 7.0 config-inc-php




7.1--> Open in your browser http://localhost/phpmyadmin/
Enter root as name, do not fill password. If everything is working it should look like this:

 
- PICTURE 






8. In case you can NOT login to phpMyAdmin without password...



-	PICTURE 8.0 aphp…




If for some reason you are still not able to get into phpmyadmin database what you can do is first, go to “C:\Server\data\htdocs\phpmyadmin”.

Then you want to type in the search box “ config.default.php ” :


-	PICTURE 8.0


8.1--> Once you are inside the file, you should scroll down to the section where it shows the following below and change where it says “ [‘AllowNoPassword’] = false; ” to “ [‘AllowNoPassword’] = true; ”


	PICTURE 8.1


8.2--> Next, go back to “ C:\Server\data\htdocs\phpmyadmin ” and type in the search box “config.inc.php ” and select the first file. Should look like the following below: 


	PICTURE 8.2 
              

8.3--> Once you are inside the file, make sure you make the following changes so the file looks EXACTLY like what you see in the picture below:



	PICTURE 8.2 pma confgNoPasswrd



Everything should be working now! 





9. If the phpMyAdmin is STILL NOT working!
		
 If for whatever reason you are still not able to login your phpmyadmin database you can do the following simple steps:
 



9.1-->	Find your MySQL Installer from your Windows search box or if your using Cortana in Windows 10.




9.2--> Open MySQL Installer and choose the option to reconfigure MySQL Server -Version 8.0.16 - Architecture X64.


				-	PICTURE 9.1 
        
        

9.3--> DO NOT CHANGE ANYTHING EXCEPT AUTHENTICATION METHOD. Once, you get to this step inside of MySQL Installer you need to choose the option that says, “ Use Legacy Authentication Method(Retain MySQL 5.x Compatibility) ”, click Next. Continue on until you reach Apply Configuration. Wait until everything is finished downloading and checked off. When complete, click the Finish button. 



        -	PICTURE 9.2



9.4-->   Next,  you need to login the phpMyAdmin with the SAME root username and root password you created when you installed MySQL onto your computer. This will allow you to access phpMyAdmin like you would the MySQL Database. (NOTE: always save your database passwords or ANY passwords in a secure place or folder)



        -	PICTURE 9.3




