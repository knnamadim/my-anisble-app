FROM tomcat:9.0-jdk11
COPY target/myapp.war /usr/local/tomcat/webapps/myapp.war
EXPOSE 8080
HEALTHCHECK --interval=30s --timeout=3s CMD curl -f http://localhost:8080/myapp/ || exit 1
