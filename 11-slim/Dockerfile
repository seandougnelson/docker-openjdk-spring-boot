FROM openjdk:11-slim

# Use APR based Apache Tomcat Native library for optimal performance
COPY /tomcat-native-1.2.21-src.tar.gz /tomcat-native-1.2.21-src.tar.gz
RUN apt-get -y update && apt-get -y install libapr1-dev libssl-dev gcc make \
  && tar xzf /tomcat-native-1.2.21-src.tar.gz \
  && cd /tomcat-native-1.2.21-src/native \
  && ./configure --with-apr=/usr/bin/apr-1-config --with-java-home=$JAVA_HOME --with-ssl=yes --prefix=$JAVA_HOME \
  && make && make install \
  && LD_LIBRARY_PATH=$LD_LIBRARY_PATH:$JAVA_HOME/lib && export LD_LIBRARY_PATH \
  && apt-get -y remove gcc make && apt-get -y autoremove && rm -rf /var/lib/apt/lists/* \
  && rm -rf /tomcat-native-1.2.21-src && rm /tomcat-native-1.2.21-src.tar.gz
