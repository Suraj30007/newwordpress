I have set up WordPress on VPS. Now, deploying the website using the GitHub
Actions workflow which includes below steps :

#Creating a GitHub Repository:

I created a New Github Repository. 
https://github.com/Suraj30007/newwordpress.git

#Initialize Repository:

*Cloning - Navigate to the root directory of your WordPress project, WordPress is installed in
 /var/www/html/mywordpress directory. 

I have cloned the repository and added project files using.

git clone https://github.com/Suraj30007/newwordpress.git 

*Copy WordPress Files (Excluding wp-config.php):
Copied all the WordPress project files and directories from the local WordPress installation directory and paste them into the cloned GitHub repository directory using

cp -r \
index.php \other files\
/var/www/html/wordpress/newwordpress

*Exclude wp-config.php from Git:

wp-config.php contains data related to username, and sensitive password.

In the cloned repository directory, I created a file named .gitignore by using the command

touch .gitignore

Edited .gitignore file in a text editor and mentioned below details

#Exclude wp-config.php
wp-config.php

*Commit Changes: Used the below commands to add and commit the changes
*Push Changes to GitHub: Pushed the changes to the GitHub repository

git add .
git commit -m "Add WordPress files and directories"
git push origin main

#Create a GitHub Actions Workflow:

Inside the GitHub repository, click on the "Actions" tab.
Click "Set up a workflow yourself" to create a custom workflow.

GitHub Actions workflow created in YAML file, I have attached the YAML file for your reference.


In the YAML file for your workflow (e.g., .github/workflows/deploy.yml), I have defined the steps needed for deploying WordPress website.


#GitHub Secrets:

To securely store sensitive information like server IP, username, and SSH private key, I set up GitHub secrets:

In the GitHub repository, go to "Settings" -> "Secrets" -> "New repository secret."

I have created secrets like SERVER_IP , SERVER_USERNAME, SSH_PRIVATE_KEY by entering the name and secret information that needs to be hidden.

#Permissions :

Check User Permissions: By Making sure that the user specified in ${{ secrets.SERVER_USERNAME }} (in your GitHub Actions workflow) has written permissions to the destination directory /var/www/html/wordpress/newwordpress on VPS. I have done this on VPS by running the following command

sudo chown -R ubuntu:ubuntu /var/www/html/wordpress/newwordpress


#Customize the Workflow:

Modify the workflow to match your specific project's build and deployment requirements. I need to install PHP, MySQL, and other dependencies on the server by 
sudo apt-get update
sudo apt-get install php-cli php-fpm php-mysql -y

#Commit and Push Changes:

Committed the changes to the GitHub repository and push them to the repository's main branch.

#Monitor Workflow Execution:

Go to the "Actions" tab in the GitHub repository to monitor the workflow's execution. GitHub Actions will run the workflow whenever changes are pushed to the main branch.
