> Dockerfile

```
FROM node:17

WORKDIR  /home/ubuntu/rating/actions-runner/_work/rating/rating

COPY package*.json ./

RUN npm install 

COPY . .

EXPOSE 3000

CMD [ "node", "index.js" ]
```

> pipeline

```yml
name: build-time-project


on:
  push:
    branches: [ "main" ]
  pull_request:
    branches: [ "main" ]


jobs:
  build:
    runs-on: self-hosted

    steps:
    
      - uses: AutoModality/action-clean@v1   
      
      - uses: actions/checkout@v2
      
#       - name: Stop container
#         run:  |
#           docker container stop nodejs-image-demo
          
#       - name: Remove container
#         run:  |
#           docker container rm nodejs-image-demo
          
#       - name: Remove an image
#         run:  |
#           docker rmi testdemo12/nodejs_image-demo
          
      - name: Build an image
        run: |
          docker build -t testdemo12/nodejs_image-demo .
      
      
      - name: Run the container
        run: |
          docker run --name nodejs-image-demo -p 3000:8080 -d testdemo12/nodejs_image-demo

```

```js
'use strict';

const express = require('express');

// константы
const port = 8080;
const host = '0.0.0.0';

// приложение
const app = express();
app.get('/', (req, res) => {
  res.send('Hello World');
});

app.listen(PORT, HOST, () => {
  console.log(`Running on http://${HOST}:${PORT}`);
});
```
