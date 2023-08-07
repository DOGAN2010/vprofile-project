FROM openjdk:8 AS BUILD_IMAGE
RUN apt update && apt install maven -y
RUN git clone -b ci-cd-jenkins https://github.com/DOGAN2010/vprofile-repo.git
RUN cd vprofile-repo && mvn install 
#  && git checkout ci-cd-jenkins  -b ci-cd-jenkins
FROM tomcat:8-jre11
RUN rm -rf /usr/local/tomcat/webapps/*
COPY --from=BUILD_IMAGE vprofile-project/target/vprofile-v2.war /usr/local/tomcat/webapps/ROOT.war
EXPOSE 8080
CMD ["catalina.sh", "run"]
