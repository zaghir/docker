create image for fronted 
# docker build -t gols-react .

run a container 
# docker run --name gols-fronted --rm -d -p 80:80 --env-file ./.env  -it gols-react


run in network 
# docker run --name gols-fronted --rm -d -p 3000:3000  -it gols-react