# Splunk® Enterprise Installation Manual

Splunk® Enterprise Installation Manual

Splunk Enterprise is a software product that enables you to search, analyze, and visualize the data gathered from the components of your IT infrastructure or business. Splunk Enterprise takes in data from websites, applications, sensors, devices, and so on. After you define the data source, Splunk Enterprise indexes the data stream and parses it into a series of individual events that you can view and search.

Most users connect to Splunk Enterprise with a web browser and use Splunk Web to administer their deployment, manage and create knowledge objects, run searches, create pivots and reports, and so on. You can also use the command-line interface to administer your Splunk Enterprise deployment.

You can extend the Splunk Enterprise environment to fit the specific needs of your organization by using apps. An app is a collection of configurations, knowledge objects, views, and dashboards that runs on the Splunk platform. A single Splunk Enterprise installation can run multiple apps simultaneously. Browse available apps on Splunkbase or build your own on the Splunk developer site.

# Tar file installation
What to know before installing with a tar file
Knowing the following items helps ensure a successful installation with a tar file:

Some non-GNU versions of tar might not have the -C argument available. In this case, to install in /opt/splunk, either cd to /opt or place the tar file in /opt before you run the tar command. This method works for any accessible directory on your host file system.
Splunk Enterprise does not create the splunk user. If you want Splunk Enterprise to run as a specific user, you must create the user manually before you install.
Confirm that the disk partition has enough space to hold the uncompressed volume of the data you plan to keep indexed.


# Installation procedure
Expand the tar file into an appropriate directory using the tar command:

```
tar xvzf splunk_package_name.tgz
The default installation directory is splunk in the current working directory. To install into /opt/splunk, use the following command:

tar xvzf splunk_package_name.tgz -C /opt

```

# RedHat RPM installation
RPM packages are available for Red Hat, CentOS, and similar versions of Linux.

The rpm package does not provide any safeguards when you use it to upgrade. While you can use the --prefix flag to install it into a different directory, upgrade problems can occur If the directory that you specified with the flag does not match the directory where you initially installed the software.

After installation, software package validation commands (such as rpm -Vp <rpm_file> might fail because of intermediate files that get deleted during the installation process. To verify your Splunk installation package, use the splunk validate files CLI command instead.

Confirm that the RPM package you want is available locally on the target machine.
Verify that the Splunk Enterprise user account that will run the Splunk services can read and access the file.
If needed, change permissions on the file.

```
chmod 644 splunk_package_name.rpm
Invoke the following command to install the Splunk Enterprise RPM in the default directory /opt/splunk.
rpm -i splunk_package_name.rpm
(Optional) To install Splunk in a different directory, use the --prefix argument.
rpm -i --prefix=/<new_directory_prefix> splunk_package_name.rpm

For example, if you want to install the files into /new_directory/splunk use the following command:
rpm -i --prefix=/new_directory splunk_package_name.rpm

# Replace an existing Splunk Enterprise installation with an RPM package
Run rpm with the --prefix flag and reference the existing Splunk Enterprise directory.
rpm -i --replacepkgs --prefix=/splunkdirectory/ splunk_package_name.rpm
```

# Automate RPM installation with Red Hat Linux Kickstart
If you want to automate an RPM install with Kickstart, edit the kickstart file and add the following.

```
./splunk start --accept-license
./splunk enable boot-start 
The enable boot-start line is optional.
```

# Debian .DEB installation
# Prerequisites to installation
You can install the Splunk Enterprise Debian package only into the default location, /opt/splunk.
This location must be a regular directory, and cannot be a symbolic link.
You must have access to the root user or have sudo permissions to install the package.
The package does not create environment variables to access the Splunk Enterprise installation directory. You must set those variables on your own.
If you need to install Splunk Enterprise somewhere else, or if you use a symbolic link for /opt/splunk, then use a tar file to install the software.

# Installation procedure
Run the dpkg installer with the Splunk Enterprise Debian package name as an argument.

```
dpkg -i splunk_package_name.deb
Debian commands for showing installation status
Splunk package status:

dpkg --status splunk
List all packages:

dpkg --list
```

# Information on expected default shell and caveats for Debian shells

On later versions of Debian Linux (for example, Debian Squeeze), the default non-interactive shell is the dash shell. Splunk Enterprise expects to run commands using the bash shell, and bash to be available from /bin/sh. Using the dash shell can result in zombie processes - processes that have completed execution, yet remain in the process table and cannot be killed or removed. If you run Debian Linux, consider changing your default shell to be bash.

# Start Splunk Enterprise for the first time
Before you begin using your new Splunk Enterprise upgrade or installation, take a few moments to make sure that the software and your data are secure.

As part of the initial startup process, Splunk Enterprise prompts you to create credentials for the administrator user. You can choose a username or use the default of admin. You can also enter a password. You must complete both steps for Splunk Enterprise to start and operate normally.



Accept the Splunk license automatically when starting for the first time

```
Add the --accept-license option to the start command:
$SPLUNK_HOME/bin/splunk start --accept-license
Create the Splunk Enterprise admin username. This is the user that you log into Splunk Enterprise with, not the user that you use to log into your machine or onto splunk.com. You can press Enter to use the default username of admin.
This appears to be your first time running this version of Splunk.

Splunk software must create an administrator account during startup. Otherwise, you cannot log in.
Create credentials for the administrator account.
Characters do not appear on the screen when you type in credentials.

Please enter an administrator username:
Create the password for the user that you just created. You use these credentials to log into Splunk Enterprise.
Password must contain at least:
* 8 total printable ASCII character(s).
Please enter a new password:
The startup sequence displays:
Splunk> 

Checking prerequisites...
	Checking http port [8000]: open
	Checking mgmt port [8089]: open
	Checking appserver port [127.0.0.1:8065]: open
	Checking kvstore port [8191]: open
	Checking configuration...  Done.
	Checking critical directories...	Done
	Checking indexes...
		Validated: _audit _blocksignature _internal _introspection _thefishbucket history main msad msexchange perfmon sf_food_health sos sos_summary_daily summary windows wineventlog winevents
	Done
	Checking filesystem compatibility...  Done
	Checking conf files for problems...
	Done
All preliminary checks passed.

Starting splunk server daemon (splunkd)...  
Done
                                                           [  OK  ]

Waiting for web server at http://127.0.0.1:8000 to be available... Done


If you get stuck, we're here to help.  
Look for answers here: http://docs.splunk.com

The Splunk web interface is at http://localhost:8000
```


# Launch Splunk Web
With a supported web browser, navigate to:

```
http://<host name or ip address>:8000
```

