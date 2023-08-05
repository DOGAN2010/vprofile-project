FROM tomcat:8-jre11
LABEL "Project"="Vprofile"
LABEL "Author"="Abdurrahman Dogan"
RUN rm -rf /usr/local/tomcat/webapps/*
COPY target/vprofile-v2.war /usr/local/tomcat/webapps/ROOT.war
EXPOSE 8080
CMD ["catalina.sh", "run"]
WORKDIR /usr/local/tomcat/
VOLUME /usr/local/tomcat/webapps



FROM openjdk:8 AS BUILD_IMAGE
RUN apt update && apt install maven -y
RUN git clone https://github.com/DOGAN2010/vprofile-project.git
RUN cd vprofile-project && git checkout ci-cd-jenkins && mvn test  
#  && git checkout ci-cd-jenkins  -b ci-cd-jenkins

FROM tomcat:8-jre11
RUN rm -rf /usr/local/tomcat/webapps/*
COPY --from=BUILD_IMAGE vprofile-project/target/vprofile-v2.war /usr/local/tomcat/webapps/ROOT.war
EXPOSE 8080
CMD ["catalina.sh", "run"]
