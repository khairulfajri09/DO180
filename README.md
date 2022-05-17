# DO180
Courses DO180
Guided Exercise: Configuring the Classroom Environment
In this exercise, you will configure the workstation to access all infrastructure used by this course.

Outcomes

You should be able to:

Configure the workstation machine to access an OpenShift cluster, a container image registry, and a Git repository used throughout the course.

Fork this course's sample applications repository to your personal GitHub account.

Clone this course's sample applications repository from your personal GitHub account to the workstation machine.

To perform this exercise, ensure you have:

Access to the DO180 course in the Red Hat Training's Online Learning Environment.

The connection parameters and a developer user account to access an OpenShift cluster managed by Red Hat Training.

A personal, free GitHub account. If you need to register to GitHub, see the instructions in Appendix B, Creating a GitHub Account.

A personal, free Quay.io account. If you need to register to Quay.io, see the instructions in Appendix C, Creating a Quay Account.

A personal, GitHub access token.

Procedure 1.1. Instructions

Before starting any exercise, ensure you have:

Prepare your Github access token.

Navigate to https://github.com using a web browser and authenticate.

On the top of the page, click your profile icon, select the Settings menu, and then select Developer settings in the left pane of the page.


Figure 1.2: User menu

Figure 1.3: Settings menu

Figure 1.4: Developer settings
Select the Personal access token section on the left pane. On the next page, create your new token by clicking Generate new token, you are then prompted to enter your password.


Figure 1.5: Personal access token pane
Write a short description about your new access token on the Note field.

Select the public_repo option and leave the other options unchecked. Create your new access token by clicking Generate token.


Figure 1.6: Personal access token configuration
Your new personal access token is displayed in the output. Using your preferred text editor, create a new file in student's home directory named token and ensure you paste in your generated personal access token. The personal access token can not be displayed again in GitHub.


Figure 1.7: Generated access token
On workstation execute the git config command with the credential.helper cache parameters to store in cache memory your credentials for future use. The --global parameter applies the configuration to all of your repositories.

[student@workstation ~]$ git config --global credential.helper cache
Important
During this course, if you are prompted for a password while using Git operations on the command line, use your access token as the password.

Prepare your Quay.io password.

Configure a password for your Quay.io account. On the Account Settings page, click the Change password link. See Appendix C, Creating a Quay Account for further details.

Configure the workstation machine.

For the following steps, use the values the Red Hat Training Online Learning environment provides when you provision your online lab environment:


Open a terminal on the workstation machine and execute the following command. Answer the interactive prompts before starting any other exercise in this course.

If you make a mistake, you can interrupt the command at any time using Ctrl+C and start over.

[student@workstation ~]$ lab-configure
The lab-configure command starts by displaying a series of interactive prompts and uses sensible defaults when they are available.

This script configures the connection parameters to access the OpenShift cluster for your lab scripts.

 · Enter the API Endpoint: `https://api._cluster.domain.example.com_:6443`  1
 · Enter the Username: `_youruser_`  2
 · Enter the Password: `_yourpassword_`  3
 · Enter the GitHub Account Name: `_yourgituser_` 4
 · Enter the Quay.io Account Name: `_yourquayuser_` 5

...output omitted...
1

The URL to your OpenShift cluster's Master API. Type the URL as a single line, without spaces or line breaks. Red Hat Training provides this information to you when you provision your lab environment. You need this information to log in to the cluster and also to deploy containerized applications.

2 3

Your OpenShift developer user name and password. Red Hat Training provides this information to you when you provision your lab environment. You need to use this user name and password to log in to OpenShift. You will also use your user name as part of the identifiers, such as route host names and project names, to avoid collision with identifiers from other students who share the same OpenShift cluster with you.

4 5

Your personal GitHub and Quay.io account names. You need valid, free accounts on these online services to perform this course's exercises. If you have never used any of these online services, refer to Appendix B, Creating a GitHub Account and Appendix C, Creating a Quay Account for instructions about how to register.

The lab-configure command prints all the information that you entered and attempts to connect to your OpenShift cluster.

...output omitted...

You entered:
 · API Endpoint:            https://api.cluster.domain.example.com:6443
 · Username:                youruser
 · Password:                yourpassword
 · GitHub Account Name:     yourgituser
 · Quay.io Account Name:    yourquayuser

...output omitted...
If lab-configure finds any issues, it displays an error message and exits. You will need to verify your information and run the lab-configure command again. The following listing shows an example of a verification error.

...output omitted...

Verifying your API Endpoint...

ERROR:
Cannot connect to an OpenShift 4.6 API using your URL.
Please verify your network connectivity and that the URL does not point to an OpenShift 3.x nor to a non-OpenShift Kubernetes API.
If everything is OK so far, the lab-configure attempts to access your public GitHub and Quay.io accounts.

...output omitted...

Verifying your GitHub account name...

Verifying your Quay.io account name...

...output omitted...
The lab-configure displays an error message and exits if it finds any issues. You must verify your information and run the lab-configure command again. The following listing shows an example of a verification error:

...output omitted...

Verifying your GitHub account name...

ERROR:
Cannot find a GitHub account named: invalidusername.
Finally, the lab-configure command verifies that your OpenShift cluster reports the expected wildcard domain.

...output omitted...

Verifying your cluster configuration...

...output omitted...
If all checks pass, the lab-configure command saves your configuration:

...output omitted...

Saving your lab configuration file...

All fine, lab config saved. You can now proceed with your exercises.

If you need to modify the configuration, rerun this or directly modify the values in /usr/local/etc/ocp4.config.
If there were no errors saving your configuration, you are almost ready to start any of this course's exercises. If there were any errors, do not try to start any exercise until you can execute the lab-configure command successfully.

Fork this course's sample applications into your personal GitHub account. Perform the following steps:

Open a web browser and navigate to https://github.com/RedHatTraining/DO180-apps. If you are not logged in to GitHub, click Sign in in the upper-right corner.


Log in to GitHub using your personal user name and password.


Navigate to the RedHatTraining/DO180-apps repository and click Fork in the top right corner.


In the Fork DO180-apps window, click yourgituser to select your personal GitHub project.


Important
While it is possible to rename your personal fork of the https://github.com/RedHatTraining/DO180-apps repository, grading scripts, helper scripts, and the example output in this course assume that you retain the name DO180-apps when your fork the repository.

After a few minutes, the GitHub web interface displays your new repository yourgituser/DO180-apps.


Clone this course's sample applications from your personal GitHub account to your workstation machine. Perform the following steps:

Run the following command to clone this course's sample applications repository. Replace yourgituser with the name of your personal GitHub account.

[student@workstation ~]$ git clone https://github.com/_yourgituser_/DO180-apps
Cloning into 'DO180-apps'...
...output omitted...
Verify that /home/user/DO180-apps is a Git repository.

[student@workstation ~]$ cd DO180-apps
[student@workstation DO180-apps]$ git status
# On branch master
nothing to commit, working directory clean
Create a new branch to test your new personal access token.

[student@workstation DO180-apps]$ git checkout -b testbranch
Switched to a new branch `testbranch`
Make a change to the TEST file and then commit it to Git.

[student@workstation DO180-apps]$ echo "DO180" > TEST
[student@workstation DO180-apps]$ git add .
[student@workstation DO180-apps]$ git commit -am "DO180"
...output omitted...
Push the changes to your recently created testing branch.

[student@workstation DO180-apps]$ git push --set-upstream origin testbranch
Username for `https://github.com`:  1
Password for `https://_yourgituser_@github.com`:  2
...output omitted...
1

Enter your GitHub username

2

Enter your personal access token

Make other change to a text file, commit it and push it. You will notice you are no longer asked to put your user and password. This is because the git config command you ran in step 1.7.

[student@workstation DO180-apps]$ echo "OCP4.6" > TEST
[student@workstation DO180-apps]$ git add .
[student@workstation DO180-apps]$ git commit -am "OCP4.6"
[student@workstation DO180-apps]$ git push
...output omitted...
Verify that /home/user/DO180-apps contains this course's sample applications, and change back to the user's home folder.

[student@workstation DO180-apps]$ head README.md
# DO180-apps
...output omitted...
[student@workstation DO180-apps]$ cd ~
[student@workstation ~]$
Now that you have a local clone of the DO180-apps repository on the workstation machine, and you have executed the lab-configure command successfully, you are ready to start this course's exercises.

During this course, all exercises that build applications from source start from the master branch of the DO180-apps Git repository. Exercises that make changes to source code require you to create new branches to host your changes so that the master branch always contains a known good starting point. If for some reason you need to pause or restart an exercise and need to either save or discard changes you make into your Git branches, refer to Appendix E, Useful Git Commands.

This concludes the guided exercise.
