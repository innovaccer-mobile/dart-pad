FROM dart:2.16.1
#FROM cirrusci/flutter:2.10.3
WORKDIR /app/dart-services

# protoc installation

RUN export PROTOC_ZIP=protoc-3.19.4-linux-x86_64.zip
RUN curl -OL https://github.com/protocolbuffers/protobuf/releases/download/v3.19.4/protoc-3.19.4-linux-x86_64.zip
RUN unzip -o protoc-3.19.4-linux-x86_64.zip -d /usr/local bin/protoc
RUN unzip -o protoc-3.19.4-linux-x86_64.zip -d /usr/local 'include/*'
RUN rm -f protoc-3.19.4-linux-x86_64.zip

# node installation

RUN rm /bin/sh && ln -s /bin/bash /bin/sh
RUN curl -sL https://deb.nodesource.com/setup_16.x -o nodesource_setup.sh
RUN bash nodesource_setup.sh
RUN apt install nodejs


RUN npm install -g vulcanize
RUN pub global activate protoc_plugin
RUN export PATH="$PATH":"$HOME/.pub-cache/bin"


COPY . /app/dart-services
RUN dart pub global activate grinder
RUN dart pub install
RUN rm -rf flutter-sdks
RUN dart run tool/update_sdk.dart stable


CMD export PATH="$PATH":"$HOME/.pub-cache/bin" && grind serve
#CMD echo "$(uname -s)"
#CMD cat /etc/os-release
#CMD lscpu
#CMD dart --version
#CMD flutter doctor -v
#CMD protoc --version
#CMD export PATH="$PATH":"$HOME/.pub-cache/bin" && grind --version
#CMD getconf LONG_BIT