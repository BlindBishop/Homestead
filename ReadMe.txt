documentation found at laravel.com/docs/5.4/homestead

/----------------------------------------------------\
|		   Getting Started		     |
\----------------------------------------------------/
Step 1) Install git bash
	https://git-scm.com/downloads

Step 2) Install VirtualBox
	https://www.virtualbox.org/wiki/Download_Old_Builds_5_1
	download VirtualBox 5.1.14 (released January 17th 2017)
		for windows, download Windows hosts
		for mac, download OS X hosts
	Run the installation file that you just downloaded.

Step 3) Install Vagrant
	https://releases.hashicorp.com/vagrant/1.9.1/
	download and run "vagrant_1.9.1.msi" for windows
	-or-
	download and run "vagrant_1.9.1.dmg" for mac

	*it will ask you to reboot. Do this.*
	
Step 4) Launch git bash and run the command:
-->	git clone github.com/BlindBishop/Homestead.git
	*you just downloaded all of the files you will need*
	*they are all in your home directory :: "C:/users/your user name/"*
	
	***from now on 'home directory' will be denoted as ~/

Step 5) Launch Vagrant
	-Go to your home directory ~/
	-Right click in the Homestead directory > Open git bash
	-Execute the following command
--> 	vagrant up
	*if it does not work please see the troubleshooting tips at the bottom of this guide!*

Step 6) Connect sites to the ngix engine in your Vagrant instance
	-For Windows
	-Run notepad as administrator
	- press ctrl + O; or file> open
	- browse to C:\Windows\System32\drivers\etc for windows
	- change file type to All
	- open the hosts file
	-> Insert the following line at the bottom, or anywhere on its own line really
		-  192.168.10.10 Capstone.app
		-  192.168.10.10 Lab4.app
* note you can set new ones up in ~/Homestead/Homestead.yaml* (~ == home directory)
* further information below (under Using Vagrant) *
	-or-
	- for mac : browse to your root directory ( should be 3 directories up from home and is designated by '/' )
		- then go to /etc and open hosts file.
		- I usually do this with the command line: 
			--> cd ../../../
			--> cd etc
			--> vi hosts
			-> Insert the following lines at the bottom, or anywhere on its own line really
				192.168.10.10 Capstone.app
				192.168.10.10 Lab4.app
			to save --> :x
			to quit without saving --> :q!
Step 7) Test
	1) go to chrome
	2) url = 'Lab4.app'

Hurray, you have a working server on your computer!



When you're done working, always shut down your vagrant instance:
	1) open git bash
	2)-> cd Homestead
	3)-> vagrant halt





documentation found at laravel.com/docs/5.4/homestead
----------------------------------------------------------------------------------------------------------

/----------------------------------------------------\
|		    Using Vagrant		     |
\----------------------------------------------------/
VagrantFile (found in ~/Homestead/VagrantFile)
	- this is the configuration for your server
	- I have configured the basics but if you want something more custom, this is where to do it.
Homestead.yaml (found in ~/Homestead/Homestead.yaml)
	This is where you will map your sites to urls
	To add a new site
		- go into ~/Projects and add a new folder called 'myNewSite'
		- go to your hosts file (see step 6)
		- add the following line
			192.168.10.10 myNewSite.app
		- open the homestead.yaml file
		- copy a map with the same structure and paste it below another site map, like so:

|			sites:
|		    		- map: Capstone.app
|		      		  to: /home/vagrant/Projects/484Project/views
|
|		    		- map: Lab4.app
|    				  to: /home/vagrant/Projects/Lab4
|		
|    				- map: myNewSite.app
|    				  to: /home/vagrant/Projects/myNewSite
		
		*note Projects/484Project/views is the root directory for that application*
		*we are telling our server where to find the application source and the index.html or index.php*
		*if you find tutorials, many will use the root directory of /src -or- /public instead of views*
	Save the file
	if vagrant is already running :: restart vagrant
	--> vagrant provision
	else if vagrant is not running :: just launch vagrant as usual
	--> vagrant up

*All vagrant commands are run from ~/Homestead*
launch vagrant
	--> vagrant up 

shut vagrant down
	--> vagrant halt
	*do this every time you shut your computer down; don't shut down with active connections*

restart vagrant
	--> vagrant provision
	*do this every time you make a change to your homestead.yaml*

MOST IMPORTANT FUNCTION :: go into your vagrant box to run commands on your project files
	--> vagrant ssh
	*don't be intimidated by this. This particular vagrant box comes preconfigured with really useful resources*
	*comes with php, mysql, node package manager (npm), and 10 other useful tools*
	- for instance :: you can create and modify your mysql database
		--> mysql -uhomestead -p
		it asks for a password
		--> secret
		--> show databases; create database newDatabase; use newDatabase; show tables;
	*you can also download MySql Workbench as a GUI (like sql server management studio for mysql)*
	
	-run the command :: 'exit' to exit mysql or the vagrant ssh session

kill your vagrant box forever
	--> vagrant destroy --force
	*do this if you messed up somewhere along the way and you need to start over*

Share your vagrant box with a teammate
	--> vagrant share
Connect to a teammate's box that has been shared
	--> vagrant connect
-------------------------------------------------------------------------------------------------

/----------------------------------------------------\
|	        Troubleshooting Vagrant		     |
\----------------------------------------------------/
1) you need to have hardware virtualization (or intel-VTX) enabled in the BIOS of your computer
	-if you don't know how to enter the bios of your particular computer, google it
2) you may not have permissions to modify files in your Temp folder (vagrant needs to be able to modify your files)
	-easy fix:
		C:\Users\your user name\AppData\Local\Temp
		-delete all files
		-delete the Temp folder itself and manually recreate it
3) repair vagrant
	-if a vagrant box was created, you may want to destroy it before running the repair command
		--> vagrant destroy --force
	-go to ~/VagrantTroubleshooting
	-run vagrant_1.9.1.msi -or- vagrant_1.9.1.dmg (for mac)
	-click repair
	-it will ask you to reboot and you will want to reboot.
4) enviornment variables
	-go to ~/VagrantTroubleshooting
	-open "System Variables.png" and "User Variables.png"
	-Make sure your enviornment variables look like mine.

------------------------------------------------------------------------------------------------
/----------------------------------------------------\
|	          Recommended Tools		     |
\----------------------------------------------------/
Version Control: github.com
php IDE: PhpStorm or Sublime. I use PhpStorm, but both are free to students
mySql client: mysql Workbench
remote collaboration tool: Lync
Videos and tutorials : 
	- general stuff :: Lynda.com
	- modern web dev :: egghead.io
	- IDE setup :: Laracasts.com
		- they have videos for both phpstorm and sublime text editor

For the Microsoft side it's all Microsoft Services. All can be found on Dreamspark.
	-> VisualStudio (Enterprise if you have space; express if you don't) -VS is a HUGE program
	-> TFS plugin -> you will want to create a remote code repository at visualstudio.com



  _   _       _        ____      ____      __   __                         
 |'| |'|  U  /"\  u  U|  _"\ u U|  _"\ u   \ \ / /                         
/| |_| |\  \/ _ \/   \| |_) |/ \| |_) |/    \ V /                          
U|  _  |u  / ___ \    |  __/    |  __/     U_|"|_u                         
 |_| |_|  /_/   \_\   |_|       |_|          |_|                           
 //   \\   \\    >>   ||>>_     ||>>_    .-,//|(_                          
(_") ("_) (__)  (__) (__)__)   (__)__)    \_) (__)                         
           ____     U  ___ u   ____                    _   _        ____   
        U /"___|     \/"_ \/  |  _"\        ___       | \ |"|    U /"___|u 
        \| | u       | | | | /| | | |      |_"_|     <|  \| |>   \| |  _ / 
         | |/__  .-,_| |_| | U| |_| |\      | |      U| |\  |u    | |_| |  
          \____|  \_)-\___/   |____/ u    U/| |\u     |_| \_|      \____|  
         _// \\        \\      |||_    .-,_|___|_,-.  ||   \\,-.   _)(|_   
        (__)(__)      (__)    (__)_)    \_)-' '-(_/   (_")  (_/   (__)__) 

~Hunter Hough



