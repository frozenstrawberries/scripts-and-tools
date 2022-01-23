
# Trigger a cron job by file creation events

Incron can help here which uses native inotify events from linux.

Follow the steps below to set up incron
- Add Repo to the sources list
	- Open sources list using vi or nano:
		`/etc/apt/sources.list`
	- Append following line at the end and save:
`deb [trusted=yes] http://archive.ubuntu.com/ubuntu/ bionic main restricted universe multiverse`
	- Run following command to update repo list:
`sudo apt update`
- Install incron
	- Run following command to install incron:
`sudo apt-get install incron -y`
- Add your user in the allow list
	- Open following file and add your username in order to allow it to create new cron jobs:
`sudo nano /etc/incron.allow`
- Create a script and place it in the logs folder
	- Create a new file in the logs folder and add following text(change the LOGPATH to the actual path):
`#!bin/bash`
`cat LOGPATH/$1 > LOGPATH/temp_upload.cef`
	- Save it as script.sh
	- Add execution permissions by running the following:
`chmod +x script.sh`
- Create a cron job
	- Run the following command to add a new cron job:
`incrontab -e`
	- add following job and save(change the LOGPATH to actual path):
`LOGPATH IN_CREATE LOGPATH/script.sh $#`