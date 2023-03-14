[Source](https://medium.com/@kevinwilliams.dev/building-a-flutter-web-container-3b13f4b2bd0c)

```yml


name: flutter


on:
  push:
    branches: [ "main" ]
  pull_request:
    branches: [ "main" ]
 

jobs:
  build:
    runs-on: self-hosted

    steps:
          
      - uses: actions/checkout@v2
    
    
      - name: Stop main container
        run: | 
          docker stop flutter-web
      - name: Delete the container
        run: |
          docker rm flutter-web
          
          
      - name: Build an image
        run: |
          docker build -t flutter-web .
      
      
      - name: Run the container
        run: |
          docker run -d -p 3000:80 --name flutter-web flutter-web
          
```
> Dockerfile

```

FROM debian:latest AS build-env

RUN apt-get update
RUN apt-get install -y curl git wget unzip libgconf-2-4 gdb libstdc++6 libglu1-mesa fonts-droid-fallback lib32stdc++6 python3 sed
RUN apt-get clean

RUN git clone https://github.com/flutter/flutter.git /usr/local/flutter

ENV PATH="${PATH}:/usr/local/flutter/bin:/usr/local/flutter/bin/cache/dart-sdk/bin"

RUN flutter doctor -v
RUN flutter channel master
RUN flutter upgrade
 
RUN mkdir /app/
COPY . /app/
WORKDIR /app/

RUN flutter build web

FROM nginx:1.21.1-alpine
COPY --from=build-env /app/build/web /usr/share/nginx/html
```
