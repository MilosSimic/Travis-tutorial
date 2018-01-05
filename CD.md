# Travis Deployment [![Built with Spacemacs](https://cdn.rawgit.com/syl20bnr/spacemacs/442d025779da2f62fc86c2082703697714db6514/assets/spacemacs-badge.svg)](http://spacemacs.org)

## Setup
* To deploy your project to custom server using Travis we need to have installed travis cli tool ```gem install travis```, or you can use [Docker image](https://github.com/MilosSimic/mytravis).
* Before using this tool, positionate in directory where ```.travis.yml``` file is.
* To encrypt your secrets use ```encrypt```command:
```
travis  encrypt DOCKER_HUB_EMAIL=<email> --add
travis  encrypt DOCKER_HUB_USERNAME=<username> --add
travis  encrypt DOCKER_HUB_PASSWORD=<password> --add
``` 
**Note: these secrets will be stored as environment variables, and we can use them during our build process** (eg. ```$DOCKER_HUB_EMAIL```) **in your** ```.travis.yml``` **file. For more details see [docs](https://docs.travis-ci.com/user/encryption-keys/)**

## Build Docker image and push to dockerhub
* To pack our application in docker image, first create ```Dockerfile``` in your project structure with all commands needed for your application.
* Then we need to add few things to ```.travis.yml``` :
```
sudo: required
language: python
services:
 - docker
before_install:
  - docker login -u "$DOCKER_HUB_USERNAME" -p "$DOCKER_HUB_PASSWORD";
after_success:
  - docker build -t $DOCKER_HUB_USERNAME/image_name .
  - docker push $DOCKER_HUB_USERNAME/image_name:your_tag
```

**Note: here we are missing steps for running tests, install dependencies explained [elsewhere](CI.md)**

* Create a deploy script, which will be called after Travis finish his work. We will use [Docker Compose](https://docs.docker.com/compose/) create ```docker-compose.yml``` file and add this content:
```
version: '2'
services:
 app:
   image: <your_docker_hub_id>/<your_project_name>:production
   ports: 
     - server_port:container_port
```

**Note, we can create** ```docker-compose.yml``` **file on server, or create localy than copy to server using** ```scp docker-compose.yml host@address:```

* And we need a little bit of bash :). Create a ```deploy.sh``` file with the following content (locally than copy to server, or create on server direcly):
```
docker-compose down
docker-compose pull
docker-compose up -d
```

* Make the file executable (and send it to your host if created localy using ```scp``` command):
```
chmod +x ./deploy.sh
```

## Security


## Automatic deployment
Here will be shown how to deploy new software version as new docker image



## More links
