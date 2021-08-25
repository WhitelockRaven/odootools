# odootools for Ubuntu 20.04

Tools to help install and manage an Odoo installation.

## Prerequisites

The installation scripts assume the host OS is Ubuntu 20.04. Usage on other 
systems might require tweaking to work.

Odoo 14 require `init-system-helpers 1.57` or later. This rules out usage of
Ubuntu 18.04 or older.

## Install

Installation of Odoo and Odootools.

1 Ensure you are using the version (eg branch 14.0 for Odoo 14) you want to install.

2 The command below will download and execute the installation script:
```
wget -O- https://raw.githubusercontent.com/vertelab/odootools/14.0/install | bash
```
3 To install all repos in the repos-directory follow these steps
```
git clone -b 14.0 git@github.com:vertelab/odootools.git

cd odootools/repos

./cloneall

./allrequirements

```
4 Follow the instruction in: /themes/README.md to copy the themes to the server.

5 If you want to add additional customer unique repositories to the server
git clone -b 14 https://git.vertel.se/vertelab/odoo-customer-addons.git or any other repository where there is a copy of a similar odootools/repos-folder with a list of repos in one of the folders. When done, run this command to add the repos to odoo.conf
```
odooaddons
```

6 restart the server with this command.
```
odoorestart
```


## Uninstall

Use the command below to uninstall your Odoo installation.

*this drops your databases and all your data related to Odoo*
```
wget -O- https://raw.githubusercontent.com/vertelab/odootools/14.0/uninstall | bash
```

## Odoo-tools commands

Odoo-tools command |Description
--- | ---
 alldbs                    | Lists all databases             
 allprojects               | Lists all projects              
 cdb                       | change database                 
 cdo                       | change directory to Odoo core   
 cdp                       | change directory to project     
 odooaddons                | Updates addons_path with all project according to ODOOADDONS defined in odoo.tools (or is it odootools/repos/MAINTAINER_repo)
 odooadminpw               | view master password
 odoocheckmodule   <module>        | lists databases that use a module (eg odoocheckmodule sale)
 odoocreatetestdb <database name> <input file or stdin> | Creates new database without e-mail-settings for outgoing mail
 odoofind *pattern*        | find patterns in odoo-core source code                     
 odoogitclone *project*    | clones and installs projects from githuh (vertel-projects)   
 odoogitpull    | does a *git pull* for every project in ODOOADDONS  
 [odoolangexport](https://github.com/vertelab/odootools/blob/14.0/odoolangexport.pdf)    | export po/pot file for a module, -m <module> -d <database> -l <language>. To export a pot-file exclude "-l"
 odoopatch                 | Implements patches from the directory /etc/odoo/patch.d        
 odoorestart               | Restarts odoo and apache/varnish or other systems that have to be restarted (configure in odoo.tools)
 odoosetperm               | Sets permissions for all projects and modules
 odoosyncall -h *host*     | Syncs all projects and modules
 odoosync -h *host* -p *project* | Syncs a project to a server without git meta data           
 odootail                  | Views odoo-log live, you can use the one-liner *odoorestart ; odootail* to restart and monitor odoo
odooupd -h/--host, -P/--port, -d/--database, -m/--module, -p/--password, -l/--list, -i/--install, -u/--uninstall | Modifies Odoo-instanses; -m/--module=	comma separated  module list, -i/--install	install or upgrade modules  -u, --uninstall	uninstall modules, -c/--check coma separeted module list
odooupdm *database* *modulelist*      | Installs/updates modules in single user mode                
 odoovilog                 | Opens Odoo log file in vi       
