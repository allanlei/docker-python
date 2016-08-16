# docker-python

## How to Use (2.7.12+, 3.5.2+)
## Python packages that require external libraries to **build**
Add the packages to ```requirements.build.txt```.  Keep in mind this is alpine based image.

## Python packages that require external libraries to **run**
* Automatically: Libraries automatically be detected and added to the ```.run-deps``` virtual package
* Manually: Add the packages to ```requirements.run.txt```.  Keep in mind this is alpine based image.

## TODOs
* During the build, docker will copy ```requirements*.txt```.  It would be better if the specific files are copied over, but the ```COPY``` command fails if the file does not exist
* Enabling extra Alpine repositories in conjunction with virtual packages
