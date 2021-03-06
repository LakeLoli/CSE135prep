CSE135prep
==========

This repository is to help UCSD CSE 135 Spring 2014 students for their project. 
What follows is a walkthrough for students that explains how to get started with the CSE 135 project, including how to install all the required libraries and frameworks and example application. 
Only the following technologies are required for the project :

 - Apache Tomcat Server
 - PostgreSQL DBMS
 - Java/JSP development
 
The other technologies are personal suggestions that I believe will make your life easier. 
For example, I will be able to help those who follow my suggestions much better :).

### Install a Ubuntu Virtual Machine

I suggest you use a Ubuntu virtual machine to build your project. 

There are several reasons for this suggestion :
 
 - You have no risk on crashing your computer while doing the project.
 - Linux Ubuntu is probably the best platform to develop open source software.
 - It will make grading for us easier ( I know, that's selfish :p). 
 - I don't want to write a cross platform guide.

The only part of this guide that will be cross platform will be how to obtain and install the Ubuntu VM. The rest of the guide will assume that you will be using Ubuntu.

 - The best way to obtain a free VM is to use Oracle's [Virtual Box](https://www.virtualbox.org/wiki/Downloads). On this page you will see download links available for all major platforms, as well as a platform dependent installation guide.
 - You can find a download link for Ubuntu [here](http://www.ubuntu.com/download/desktop). Please choose version 12.04 (not 13.10).
 
You should now have a Ubuntu .iso file and Virtual Box installed. Follow these steps to create a Ubuntu VM :

 - Start Virtual Box and select the *New* tab. You will be asked the type and the version for the operating system of the VM. Make sure to select Linux (type) Ubuntu(64 bit) (version).
 - You may want to allocate at least 512MB of RAM (although probably more), it should be sufficient for our purposes, but you can increase it if you want.
 - The next page should ask you if you want to create a virtual disk. You should select option *Create a virtual disk now*.
 - When asked which format for the virtual disk, select `.vdi`.
 - On the next pane you will be asked to specify the disk storage. Make sure to choose *dynamically allocated*.
 - Choose how much space you want your virtual disk to use (I chose 8GB) and select *Create*. Congrats, you now have a new VM!
 - You know have to install Ubuntu on your VM. You should be on the VM manager page of Virtual Box. Select the VM you just created and select the *Configuration* tab. A new window will pop up.
 - In the new window, select the *Storage* tab. On the left hand side of the window, you should see a pane with a field called *Controller : IDE*. On the right side of that field a little disk icon should be visible. Select it, and choose the option *Choose Disk*. This will ask you to choose an `.iso` file and you can use the Ubuntu version you downloaded. 
 - You can now start your VM on the main menu and it should boot ubuntu on a seperate window!
 - It will take you through the installation process.


#### Install Git

One personal suggestion is that you use a revision control system to manage the program such as [Git](http://git-scm.com/) to build your project.
I also suggest building your project as a private repository on [Github](https://github.com/) and add members of your group as collaborators.
In case you didn't know, you have up to 5 free private GitHub repositories as long as you are a student, see this [link](https://education.github.com/).

It is very easy to install git on ubuntu. Just type the following command on the terminal :

   sudo apt-get install git

#### Setup Java + Tomcat

I have written a script called `tomcat_setup.sh` that should be included in this git repository. You can execute this script on your machine.
It will install java (v1.6) and Tomcat (v7.0.53) on your VM, move them to appropriate directories and setup your `$CATALINA_HOME` and `$JAVA_HOME` variables.

The only thing this script does not do is setup your tomcat users :
 - copy the file `Tomcat/tomcat_users.xml` from this repository into `$CATALINA_HOME/conf`.

#### Install Eclipse

You can download eclipse by going on the Ubuntu Software Center and looking for Eclipse.

#### Setup Postgres

Issue the following command on your terminal (you need admin privileges) :

        sudo apt-get install postgresql postgresql-contrib

This way, you should get a recent version of PostgreSQL.
The PostgreSQL installation creates a unix user called `postgres` which is the only one allowed (at first) to create databases. 
It would be better if you could do that yourself :
 - Enter the command `sudo passwd postgres` on your terminal. This lets you create a new password for the postgres user (for some reason, the postgres user does not have a default password).
 - Enter the command `su postgres` and use the password to login into the postgres user.
 - Enter the following commands :

        createuser -s YOUR_UNIX_USERNAME
        createdb cse135

 - Log out from the postgres user and enter the command `psql -d cse135`. This connects you to the database, from here you can issue SQL statements.
 - To quit psql, just issue the command `\q1`.

#### Setup A Tomcat server on Eclipse

  - 1. Configure the run time server :
    - Go to Eclipse > Preferences > Server > Run Time Environments
    - Add...
    - Choose Apache Tomcat 7.0, then next.
    - Make sure Tomcat installation path is the one you get when you execute `echo $CATALINA_HOME` on a terminal.
    - Click on Finish 
  - 2. Add a new server :
    - Go on Window > Show View > Servers
    - Open new server wizard from the servers window pane (should be on the bottom of your screen).
    - Make sure Server Host Name is `localhost` and Server Runtime Environment `Apache Tomcat v7.0` then select Finish.
    - The server should now appear in the server window. Right-click and the server and press start. You should know be able to see the tomcat main page on http://localhost:8080.
    - Some people (including I) may see a 404 page error at this step. Don't worry, your tomcat is running. We just need to do an extra configuration.
    - Back on Eclipse, double-click on the server name and a server configuration window should appear. Make sure the radio button `User Tomcat Installation` is ticked. Verify that the *Server Path* is also set to `/usr/local/apache-tomcat-70.0.52`.
    - Restart the server. You should know see the Tomcat server normally.
    - If you have done the tomcat user setup (see Setup Java+Tomcat section), then you should be able to logon onto the Tomcat manager app and see all your current applications. The username and password are both "admin". The manager app will allow you to access your app more easily in the future from the Tomcat main page.

#### Write your first Tomcat web application
You can follow this [tutorial](http://www.srccodes.com/p/article/2/JSP-Hello-World-Program-using-Eclipse-IDE-and-Tomcat-web-server)
You now have a working HelloWorld simple JSP web app. However, if go on http://localhost:8080/HelloWorldJSP/, you will get a 404 error. 
This is because the `web.xml` file which manages your web app did not include your HelloWorld.jsp file as a welcome file.
You can fix this the following way : 
 - I have included the `web.xml` you want in this repository under `HelloWorldJSP/web.xml`. 
 - You should put this file in the WEBINF directory of your application. 
 - If you restart the application using Eclipse (as described in the tutorial for this section), you can now access http://localhost:8080/HelloWorldJSP/ and get the correct output.

#### Write your first JSP program
Coming soon...

#### Write your first Java JDBC app    
Coming soon...