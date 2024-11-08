# Dockerised LIGSIFT 

In the directory containing the Dockerfile use the following command to build the image and tag as `kuano/ligsift`:
```
docker image build -t kuano/ligsift .
```

## Running (and limitations)

To check this works run:
```
docker container run kuano/ligsift
```
This should produce the ligsift usage instructions.

You can now run this image using the test molecules in this directory using:
```
docker container run --rm -v ${PWD}:/share kuano/ligsift -q mol1.mol2 -db mol2.mol2 -o alignment_scores.txt -s superposed.mol2
```

The `-rm` flag removes the stopped container after a run.

To break this down, the most important thing to notice is the`-v` option, this maps the present working directory (`$PWD`) to a directory used by the ligsift command in the container (`/share`). This needs to map to `/share` specifically.

The options after the tag for the image are those for the LIGSIFT tool itself (in Docker terminology this is the default 'entrypoint').

*Limitation*: Unfortunately this means the input and output must be in the present working directtory of the host machine.

*Note*: Output files are write protected.

