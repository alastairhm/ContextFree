# Context Free

Docker image for building and running the command line UNIX verion of [context-free](https://github.com/MtnViewJohn/context-free) art program.

## Build Docker Image

```bash
docker build -t contextfree .
```

## Creating an image

Change into the directory with the Context-free file.

```bash
docker run --rm -v ${PWD}:/mnt alastairhm/contextfree -s1024 input_file.cfdg output.png
```

Output file will be written to the same folder.

```text
          _    _ __  __
    /\   | |  | |  \/  | Email    : alastair@montgomery.me.uk
   /  \  | |__| | \  / | Web      : https://blog.0x32.co.uk/
  / /\ \ |  __  | |\/| | Twitter  : @alastair_hm
 / ____ \| |  | | |  | | Mastodon : @Alastair@mastodon.me.uk
/_/    \_\_|  |_|_|  |_| (c) 2021
```
