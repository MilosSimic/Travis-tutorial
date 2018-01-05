# Travis CI
Here will be shown how to connect travis with your github project, run tests, add languange, connect Docker and few building steps.

## Connect Travis
* Go to [travis page](http://travis-ci.org/) and sign in with github
* Allow travis to see informations about your profile and projects
* Go to your profile (if travis don't do that), and in list of all public repos choose which repo to connect to Travis CI

![Allow build project](/images/allow_build.png)

*Now, on every push Travis will be triggered*

## Add build strategy
* Add to root of your repository ```.travis.yml``` file. This file will contain build strategy
* Goto project you've connected and click on *More Options > Settings* and in section _General_ click on _Build only if .travis.yml is present_
* In section _Environment Variables_ we can store Key-Value pairs (eg. username, password for Dockerhub) to access them add _$_ sign in front of variable name in ```.travis.yml```

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

You can [customize your build](https://docs.travis-ci.com/user/customizing-the-build) even more.
