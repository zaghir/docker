docker images 

REPOSITORY   TAG       IMAGE ID       CREATED         SIZE
<none>       <none>    2eefdd26b64e   2 minutes ago   1.01GB

docker container run -d -p 3000:80 --rm --name golsapp 2eefdd26b64e

CONTAINER ID   IMAGE          COMMAND                  CREATED          STATUS         PORTS                  NAMES
bf22dcda7954   2eefdd26b64e   "docker-entrypoint.s…"   11 seconds ago   Up 9 seconds   0.0.0.0:3000->80/tcp   golsapp

# naming image 
name:tag 

docker build -t gols:latest .

docker images
REPOSITORY   TAG       IMAGE ID       CREATED          SIZE
gols         latest    2eefdd26b64e   14 minutes ago   1.01GB

docker container run -d -p 3000:80 --rm --name golsapp gols:latest




docker build --help

Usage:  docker build [OPTIONS] PATH | URL | -

Build an image from a Dockerfile

Options:
      --add-host list           Add a custom host-to-IP mapping (host:ip)
      --build-arg list          Set build-time variables
      --cache-from strings      Images to consider as cache sources
      --disable-content-trust   Skip image verification (default true)
  -f, --file string             Name of the Dockerfile (Default is 'PATH/Dockerfile')
      --iidfile string          Write the image ID to the file
      --isolation string        Container isolation technology
      --label list              Set metadata for an image
      --network string          Set the networking mode for the RUN  instructions during build (default "default")
      --no-cache                Do not use cache when building the image
  -o, --output stringArray      Output destination (format: type=local,dest=path)
      --platform string         Set platform if server is multi-platform capable
      --progress string         Set type of progress output (auto, plain, tty). Use plain to show container output  (default "auto")
      --pull                    Always attempt to pull a newer version of the image
  -q, --quiet                   Suppress the build output and print image  ID on success
      --secret stringArray      Secret file to expose to the build (only if BuildKit enabled): id=mysecret,src=/local/secret
      --ssh stringArray         SSH agent socket or keys to expose to the  build (only if BuildKit enabled) (format: default|<id> [=<socket>|<key>[,<key>]])
  -t, --tag list                Name and optionally a tag in the  'name:tag' format
      --target string           Set the target build stage to build.

