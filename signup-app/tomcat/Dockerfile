FROM openjdk:10-jdk
MAINTAINER jyson

# 환경 변수 및 작업 경로8
ENV CATALINA_HOME /usr/local/tomcat
ENV PATH $CATALINA_HOME/bin:$PATH
RUN mkdir -p "$CATALINA_HOME"
RUN mkdir -p /usr/local/tomcat/webapps/signup
WORKDIR ${CATALINA_HOME}


# 톰캣 설치 파일 다운로드 실행 및 압축해제
#RUN wget http://apache.mirror.cdnetworks.com/tomcat/tomcat-10/v10.0.20/bin/apache-tomcat-10.0.20.tar.gz;
RUN wget https://archive.apache.org/dist/tomcat/tomcat-10/v10.0.20/bin/apache-tomcat-10.0.20.tar.gz;
RUN tar -xf apache-tomcat-10.0.20.tar.gz  --strip-components=1;
RUN wget https://downloads.mysql.com/archives/get/p/3/file/mysql-connector-java-5.1.40.tar.gz
RUN tar -xf mysql-connector-java-5.1.40.tar.gz
RUN mv ./mysql-connector-java-5.1.40/mysql-connector-java-5.1.40-bin.jar /usr/local/tomcat/lib
RUN rm -rf mysql-connector-java-5.1.40.tar.gz
#RUN podman login 52.79.48.121:30002 --username admin --password Harbor12345 --tls-verify=false

# config 파일 복사
COPY CI-CD/signup-app/tomcat/config/server.xml /usr/local/tomcat/conf/server.xml
COPY CI-CD/signup-app/tomcat/config/context.xml /usr/local/tomcat/conf/context.xml

# JSP 파일 복사
COPY CI-CD/signup-app/tomcat/jsp/* /usr/local/tomcat/webapps/signup
#COPY jsp/index.jsp /usr/local/tomcat/webapps/
#COPY jsp/join.jsp /usr/local/tomcat/webapps/
#COPY jsp/input.jsp /usr/local/tomcat/webapps/
#COPY jsp/output.jsp /usr/local/tomcat/webapps/
#COPY jsp/delete_do.jsp /usr/local/tomcat/webapps/

# war 파일 복사
#COPY ./sample.war $CATALINA_HOME/webapps

# jdbc driver jar 복사
#COPY ./mysql-connector-java.jar ../openjdk-10/lib
#COPY ./mysql-connector-java.jar /usr/local/tomcat/lib/
#COPY ./mysql-connector-java-5.1.40-bin.jar ../openjdk-10/lib
#COPY ./mysql-connector-java-5.1.40-bin.jar /usr/local/tomcat/lib/

# 컨테이너에서 사용할 포트
EXPOSE 8080

# 설정 완료 후 실행
CMD ["catalina.sh", "run"]
