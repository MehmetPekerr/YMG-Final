FROM payara/server-full:5.2022.2-jdk11

# Root kullanıcısına geç
USER root

# Gerekli dizinleri oluştur
RUN mkdir -p /tmp/app/WEB-INF/classes

# Önce kaynak dosyalarını kopyala
COPY src /tmp/app/src
COPY WEB-INF /tmp/app/WEB-INF
COPY *.xhtml /tmp/app/

# Java dosyalarını derle
WORKDIR /tmp/app
RUN javac -d WEB-INF/classes -cp /opt/payara/appserver/glassfish/modules/jakarta.faces.jar:WEB-INF/lib/* src/java/com/opiframe/managed/*.java

# WAR dosyasını oluştur
RUN jar cvf jsf-exercise-1.war *.xhtml WEB-INF/

# WAR dosyasını autodeploy dizinine kopyala
RUN cp jsf-exercise-1.war /opt/payara/appserver/glassfish/domains/domain1/autodeploy/

# Payara kullanıcısına geri dön
USER payara

# Portları aç
EXPOSE 8080 4848

# Payara'yı başlat
CMD ["asadmin", "start-domain", "--verbose"]
