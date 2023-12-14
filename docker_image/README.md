# Context Free

Docker image for building and running the command line UNIX verion of [context-free](https://github.com/MtnViewJohn/context-free) art program.

## Build Docker Image

```bash
docker build -t context-free .
```

## Creating an image

Change into the directory with the Context-free file.

```bash
docker run --rm -v ${PWD}:/mnt context-free -s1024 input_file.cfdg output.png
```

Output file will be written to the same folder.
