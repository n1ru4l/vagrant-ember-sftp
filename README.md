# vagrant-ember-sftp

## Why
Using ember-cli under windows is pain. 
Using ember-cli in a vagrant box with a shared folder is pain.
Using ember-cli in a vagrant box with a samba drive is pain.
For me this is the most convenient way to work with the ember-cli under windows by using the PhpStorm SFTP and Git integration.

## What

node 6.9.1 (LTS)
npm 3.10.8
ember-cli

## Setup

`git clone https://github.com/n1ru4l/vagrant-ember-sftp.git`
`vagrant up`

Wait for the provisioning to finish
Now your vagrant box is running.

## Configuring phpStorm

1. Open the folder of your ember-application in PhpStorm (I assume you already did your checkout)
2. Choose the `Tools/Deployment/Configuration` tab
3. Add a new server of type `SFTP`
4. Set `SFTP host` to `10.42.42.42`
5. Set `User name` and Password to `vagrant`
6. Change the Root Path to the path where you want to upload your ember-application (e.g. `/home/vagrant/projects/my-ember-app`)
7. Test your connection
8. Switch to tab Mappings
9. Set `Deployment path on server` to `/`
10. Save your configuration by clicking on the `OK` Button

Should look like this:
![Deployment 1](/img/deployment-1.jpg)
![Deployment 2](/img/deployment-2.jpg)


Now you can confugure your upload settings in the `Tools/Deployment/Options` tab
My recommended settings:
![Recommended Settings](/img/options.jpg)

Also make sure to check `Tools/Deployment/Automatic Upload`

## Connection to the vagrant box

Since phpStorm has a built in vagrant detection you can use `Tools/Deployment/Start SSH Sessions`. 
Choose your vagrant box, change to the path you configured in the upload settings and you are ready to go!
