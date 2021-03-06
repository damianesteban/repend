# Express Yourself

https://www.youtube.com/watch?v=u31FO_4d9TY

Add a dependency to express in package.json.

```json
"dependencies": {
    "express": "^4.14.0"
}
```

Adjust the dockerfile to install the dependencies and expose the port.

```Dockerfile
FROM node:latest
RUN mkdir /app
WORKDIR /app
COPY ./package.json /app/package.json
RUN npm install
COPY ./index.js /app/index.js
EXPOSE 3000
CMD ["npm", "start"]
```

Map the port in the docker-compose.yml file.

```yml
version: '2'

services:
  repend:
    build: .
    ports:
      - "3000:3000" 
```

Create a simple express api in the index.js file.

```js
(function () {
    const express = require('express')
    const app = express();

    app.get('/', function (req, res) {
        res.send('I\'m droppin\' flavor, my behavior is hereditary. But my technique is very necessary.');
    });

    app.listen(3000, function () {
        console.log('express yourself');
    });
})();
```

Now start the docker container and browse to the api.

```shell
docker-compose up
```

Browse to [http://localhost:3000/](http://localhost:3000/)