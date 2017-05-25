# YouPHPTube

This is a docker implementation of [YouPHPTube](https://github.com/DanielnetoDotCom/YouPHPTube).

## Database

This container requires a separate container for the MySQL database.  Further instructions will be added for those who don't know how to accomplish this.

## Running

```
docker run --name=youphptube --link mysql:mysql -d -p 80:80 -v $PWD/videos:/var/www/html/videos furiousgeorge/youphptube
```

### Description of parameters

#### Name
```--name=youphptube```

This is the name that identifies your docker container - you can choose any name.

#### Link
```--link mysql:mysql```

The first "mysql" before the colon is the name of your already running mysql container.  The second "mysql" after the colon is the database hostname that you will use during the install process.

#### Detatch
```-d```

This will cause the docker container to run in the background

#### Port
```-p 80:80```

This will map port 80 inside the container to port 80 on your docker host server.  If you wish to use a different port, do something like ```-p 8888:80```

#### Volume
```-v $PWD/videos:/var/www/html/videos```

This parameter is important.  This will provide a way for the container to save all videos on your docker host machine so they are available when this docker container is restarted.  YouPHPTube also stores its configuration in this directory

## Installing

Once you have the container running as described in the "running" step above, you will browse to your host server at the port you specified.  This should take you to the install screen for YouPHPTube.  Fill in all of the parameters.  For the Database host, make sure to fill in what you used in the --link paremeter for your container.  If you followed the above example, the Database host will be "mysql".


## Notes

### Videos directory

If you get a note on the install page that your videos directory must be writable, this is because you should be running the application in docker, but mounting a directory from your host into the application container.  Make sure the directory on your host has open permissions by using the following command (on your docker host machine):

```
chmod 777 /path/to/videos
```

