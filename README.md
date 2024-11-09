# Dockerized compound similarity scorers

A repositroy to hold the recipes used to make versions of compound comparison (alignment and scoring) codes that are no longer easy to install.


## Possible wrappers to make more flexible

All of the Dockerfiles in this repo make images with the same setup - files specified on the commandline can be imported only from the present working directory. This is obviously an annoying limitation.
A way of making some improvement (based on this [blog](https://blog.smallsec.ca/dockerizing-cli-tools/) is to put a short wrapper into the `PATH` which enables directory selection, see below (`<IMAGETAG>` identifies the image that the container to be wrapped will be launched from).

```
#!/bin/bash

# Check whether our first positional argument is a directory
if [[ -d "$1" ]]; then
    # It is a directory. Store the argument in a variable.
    dir_name="$1"
    # Remove the first argument from our list of arguments
    shift
else
    # It's not a directory, just use the current working directory
    dir_name="$(pwd)"
fi

# Run the container:
#     - in interactive mode
#     - remove it when finished
#     - mount a shared volume
# and then pass the rest of the arguments ("$@") to our container
docker run --rm -i -v "$dir_name":/share <IMAGETAG> "$@"

```
