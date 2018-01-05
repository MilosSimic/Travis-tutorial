# Travis CI [![Built with Spacemacs](https://cdn.rawgit.com/syl20bnr/spacemacs/442d025779da2f62fc86c2082703697714db6514/assets/spacemacs-badge.svg)](http://spacemacs.org)
Here will be shown how to connect travis with your github project, run tests, add languange, connect Docker and few building steps.

## Connect Travis
* Go to [travis page](http://travis-ci.org/) and sign in with github
* Allow travis to see informations about your profile and projects
* Go to your profile (if travis don't do that), and in list of all public repos choose which repo to connect to Travis CI

![Allow build project](/images/allow_build.png)

## Add build strategy
* Add to root of your repository ```.travis.yml``` file. This file will contain build strategy
* Goto project you've connected and click on *More Options > Settings*
![Allow build project](/images/options.png)

and in section _General_ click on _Build only if ```.travis.yml``` is present_
![Allow build project](/images/allowed_options.png)

**Note: we should not trigger builds for every branch, in ```.travis.yml``` we should [restrict which branch to build only](https://docs.travis-ci.com/user/customizing-the-build/#Building-Specific-Branches)**

* In section _Environment Variables_ we can store Key-Value pairs (eg. username, password for Dockerhub) to access them add _$_ sign in front of variable name in ```.travis.yml```
![Allow build project](/images/env.png)**

_We can also use [travis cli](https://docs.travis-ci.com/user/encryption-keys/) tool to encrypt all sensitive informations_ **But note that cli is written in ruby and it might cause problems with windows machines. We can use [Docker image](https://github.com/MilosSimic/mytravis) to solve that problem easy.**

## Define steps
* Now we need to fill in ```.travis.yml``` with langunage, usage of external services, etc.
* Example of simple defintion for Python projects:

```
language: python
python:
  - "2.7"
# command to install dependencies
install:
  - pip install -r requirements.txt
# command to run tests
script:
  - python tests.py
```

* Now, on every push travis will trigger build process. We can observe whole process in _Build History_

You can (and you should) [customize your build](https://docs.travis-ci.com/user/customizing-the-build) even more, to include Docker (build, tag, push) or to do some stuff only if everyting is successful.

## Other links
* Learn [travis-ci](https://github.com/dwyl/learn-travis/blob/master/README.md#environment-variables-travis.yml)
* [Travis and Django](https://godjango.com/25-travis-ci-and-coveralls/)
* Explore The [Travis-CI Configuration File](http://blog.tgrrtt.com/exploring-the-travisci-configuration-file)
