FROM tomcat:8.0.51-jre8-alpine
EXPOSE 8080
# delete all webapps deployed  -r =recursive  -f =force
# Le r ça veut dire que ça supprime tous les fichiers et répertoires de manière récursive… et le f
# le f pour ne pas avoir de demande de confirmation à chaque fichier à supprimer [Yes][No]
RUN rm -rf /usr/local/tomcat/webapps/*
# copy war application to webapps folder where tomcat it s installed in docker image ==> /usr/local/tomcat/webapps
# ROOT.war it s the application 
COPY target/*.war /usr/local/tomcat/webapps/ROOT.war
# catalina.sh => shell file lunch tomcat
CMD ["catalina.sh","run"]


# run container
# docker container -p 8080:8080 in28min/todo-web-application-h2:0.0.1-SNAPSHOT
# url => localhost:8080/login
# user =in28minutes pass =dummy 