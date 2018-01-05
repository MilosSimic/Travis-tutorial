# Travis CD [![Built with Spacemacs](https://cdn.rawgit.com/syl20bnr/spacemacs/442d025779da2f62fc86c2082703697714db6514/assets/spacemacs-badge.svg)](http://spacemacs.org)

## Setup
* To deploy your project to custom server using Travis we need to have installed travis cli tool ```gem install travis```, or you can use [Docker image](https://github.com/MilosSimic/mytravis).

* Before using this tool, positionate in directory where ```.travis.yml``` file is.
* To encrypt your secrets use ```encrypt```command:
```
travis  encrypt DOCKER_HUB_EMAIL=<email> --add
travis  encrypt DOCKER_HUB_USERNAME=<username> --add
travis  encrypt DOCKER_HUB_PASSWORD=<password> --add
``` 
**Note: these secrets will be stores as envariement variables, and we can use them during our build process (eg. ```$DOCKER_HUB_EMAIL```) in your ```.travis.yml``` file. For more details see [docs](https://docs.travis-ci.com/user/encryption-keys/)**

## More links
