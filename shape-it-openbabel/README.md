# Dockerised Shape-it (OpenBabel Edition)

In the directory containing the Dockerfile use the following command to build the image and tag as `kuano/shapeitob`:
```
docker image build -t kuano/shapeitob .
```

Note this version of the program is built with OpenBabel and not RDKit so there are no Python bindings.

## Running (and limitations)

To check this works run:
```
docker container run kuano/shapeitob
```
This should produce the shapeitob usage instructions.

You can now run this image using the test molecules in this directory using:
```
docker container run --rm -v ${PWD}:/share kuano/shapeitob -r mol1.sdf -d mol2.sdf -s alignment_scores.txt -o output.sdf
```

The `-rm` flag removes the stopped container after a run.

To break this down, the most important thing to notice is the`-v` option, this maps the present working directory (`$PWD`) to a directory used by the shape-it command in the container (`/share`). This needs to map to `/share` specifically.

The options after the tag for the image are those for the shape-it tool itself (in Docker terminology this is the default 'entrypoint').

*Limitation*: Unfortunately this means the input and output must be in the present working directtory of the host machine.

*Note*: Output files are write protected.

