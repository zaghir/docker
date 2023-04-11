# build image
docker build .

# console 
get ref of image created 
=> writing image sha256:8cf1f171c1c5cbfa3760523a0bb4589ec4c066a54f9920906c099174bd51489c

## docker  images
REPOSITORY   TAG       IMAGE ID       CREATED              SIZE
<none>       <none>    823ecbc1271e   About a minute ago   916MB

# run container 
-d detache mode 
docker run -d -p 3000:3000 823ecbc1271e 

# list des contener   ps = process
docker ps 

docker stop 8cf1f171
