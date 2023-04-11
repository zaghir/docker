# copy files from local to container
docker cp dummy/. <container>:/test 


# copy files from container to local
docker cp <container>:/test/test.txt dummy 
