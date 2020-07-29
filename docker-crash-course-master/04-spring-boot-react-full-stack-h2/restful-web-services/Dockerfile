##### Stage 1 - Lets build the "deployable package"

FROM maven:3.6.1-jdk-8-alpine as backend-build
WORKDIR /fullstack/backend

### Step 1 - Copy pom.xml and download project dependencies

# Dividing copy into two steps to ensure that we download dependencies 
# only when pom.xml changes
COPY pom.xml .
# dependency:go-offline - Goal that resolves all project dependencies, 
# including plugins and reports and their dependencies. -B -> Batch mode
# dependency:go-offline ==> to ensure you have all of your dependencies installed locally before you begin to work offline
RUN mvn dependency:go-offline -B

### Step 2 - Copy source and build "deployable package"
COPY src src
RUN mvn install -DskipTests

# Unzip
RUN mkdir -p target/dependency && (cd target/dependency; jar -xf ../*.jar)

##### Stage 2 - Let's build a minimal image with the "deployable package"
FROM openjdk:8-jdk-alpine
VOLUME /tmp
ARG DEPENDENCY=/fullstack/backend/target/dependency
COPY --from=backend-build ${DEPENDENCY}/BOOT-INF/lib /app/lib
COPY --from=backend-build ${DEPENDENCY}/META-INF /app/META-INF
COPY --from=backend-build ${DEPENDENCY}/BOOT-INF/classes /app
ENTRYPOINT ["java","-cp","app:app/lib/*","com.in28minutes.rest.webservices.restfulwebservices.RestfulWebServicesApplication"]

# simple build proccess [ all proccess is not in local machine]
# in stage 1  Lets build the "deployable package"
#       Step 1 - Copy pom.xml and download project dependencies
#       Step 2 - Copy source and build "deployable package"
#       unzip
#    Stage 2 - Let's build a minimal image with the "deployable package"
#    
# to create image 
# before remove maven-dependency-plugin  and spotify  from pom.xml
# docker build . 
# add tag to image 
# docker tag 1251dd21 rest-api-full-stack
