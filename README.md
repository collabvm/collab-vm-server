# collab-vm-server
This repository contains all the necessary source files to compile the collab-vm-server. The collab-vm-server powers Collab VM, and it is what you use to host it. You can either download already compiled binaries or compile it yourself. Compilation instructions are below. 

Collab VM was coded and written by Cosmic Sans, Dartz, and Geodude.

# How to use
To start collab-vm-server make sure it has executable permissions and type ./collab-vm-server (port) (HTTP Directory (optional)). For instance, if you want to start collab-vm-server on port 6004 with the directory for the HTML files in a folder called "collabvm" you'd type ./collab-vm-server 6004 collabvm 

The HTTP Directory is optional, by default, it looks and will use a folder called http.

When you start the server you'll receive a message that a new database was created. The first thing you will want to do is configure the admin panel javascript to make sure it works properly. Go into the http directory, admin, open admin.min.js with a text editor, replace any instance of 127.0.0.1:6004 with your server's IP (or you can keep it localhost if you really want to). Afterwards, go to http://(your localhost):6004/admin/ and login with either the password "collabvm". The first thing we recommend is changing this password immediately because it is highly insecure. Type in the QEMU parameters, choose your snapshot mode, and make sure auto start is checked! 

By default when you download a pre-configured copy of collab-vm-server it will have a database and a micro Linux distribution that starts up automatically. Pre-configured copies will have the password collabvm. 

# Compilation
Compilation is semi-complicated as this was intended for personal use only, sorry. In the future there will probably be easier compilation methods.

## Windows
You need Visual Studio 2015 to compile the server on Windows. Community (the free version) will work just fine.

To compile on Microsoft Windows you need the dependencies for Guacamole. You can compile these yourself but it's easier to find already compiled libraries for Guacamole on Windows since they were designed for Linux.

Open the collab-vm-server.sln file and make sure before anything you go to Project > collab-vm-server Properties > C/C++ > Additional Include Directories then make sure to select the location of the header files. Next go to Project > collab-vm-server Properties > Linker > General and change the Additional Library Directories to include the location of the .dll and .lib files.

To compile the database files you need ODB, available here: http://www.codesynthesis.com/products/odb/download.xhtml When you have downloaded it go to src/Database and type this command in:

odb -d sqlite -s -q Config.h VMSettings.h

And everything should work after that.

## Linux
This is specifically for Debian-based distributions like Ubuntu but it really should work in most distributions of Linux. Like Windows the dependencies for Guacamole are required. You can download these from the Ubuntu package manager. 

When you've got all the dependencies for Guacamole you need to get ODB. Again it is available in the link above. This requires GCC 6.

Go into source/collab-vm-server and type the following commands

aclocal

automake --add-missing

autoconf

./configure

To compile the databases the same instructions for Windows applies, get ODB for Ubuntu or whatever distribution you are using and type in the following command:

odb -d sqlite -s -q Config.h VMSettings.h

If you cannot compile open src/Makefile.am and make sure the library paths are correct.

## Macintosh
I do not have a Macintosh computer so I don't know how to compile it nor do I know if it's possible, but it should be relatively the same as the Linux instructions. If anyone can write compilation instructions for the Mac, let me know.

# License
Collab VM Server, as well as the Web App and Admin Web App are licensed under the [Apache License](https://www.apache.org/licenses/LICENSE-2.0).
