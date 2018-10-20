# starter-snake-node(js)

A simple [Battlesnake AI](https://battlesnake.io) written in Javascript for NodeJS.

To get started you'll need a working NodeJS development environment, and at least read the Heroku docs on [deploying a NodeJS app](https://devcenter.heroku.com/articles/getting-started-with-nodejs).

If you haven't setup a NodeJS development environment before, read [how to get started with NodeJS](http://nodejs.org/documentation/tutorials/). You'll also need [npm](https://www.npmjs.com/) for easy JS dependency management.

This client uses [Express4](http://expressjs.com/en/4x/api.html) for easy route management, read up on the docs to learn more about reading incoming JSON params, writing responses, etc.

[![Deploy](https://www.herokucdn.com/deploy/button.png)](https://heroku.com/deploy)


---

## Running the AI locally

Fork and clone this repo:

```shell
git clone git@github.com:battlesnakeio/starter-snake-node.git
cd battlesnake-node
```

Install the client dependencies:

```shell
npm install
```

Create an `.env` file in the root of the project and add your environment variables (optional).

Run the server with auto-reloading on file change:

```shell
npm start
```

Test the client in your browser at <http://localhost:5000>

---

## Deploying to Heroku

Click the Deploy to Heroku button at the top or use the command line commands below.

Create a new NodeJS Heroku app:

```shell
heroku create [APP_NAME]
```

Push code to Heroku servers:

```shell
git push heroku master
```

Open Heroku app in browser:

```shell
heroku open
```

Or go directly via <http://APP_NAME.herokuapp.com>

View/stream server logs:

```shell
heroku logs --tail
```

---
# Serverless

## Deploying a serverless snake to AWS Lambda

For deploying to AWS Lambda, we'd suggest using a framework. In this example we're recommending [Serveress](https://serverless.com) platform.

The steps are as follows:

1. [Install the Serverless framework](https://serverless.com/blog/anatomy-of-a-serverless-app/#setup)

    * Requires Python (or Python 3) to install the AWS CLI
    * Requires setting up an AWS account and setting up an IAM user

1. `sls deploy` to deploy to AWS Lambda.



---


### Making your own node snake serverless (with express)

If you have a snake written in node already, making it serverless is quite easy.

**- The assumption is that you're using Express as your application framework.**

**- We're using the [Serverless](https://serverless.com) framework (refer above)**



1. Install serverless-http:
```
    npm install --save serverless-http
```

2. Add the following to the top of your _index.js_ file:

```
    const serverless = require('serverless-http');
```

And to the bottom of your _index.js_:

```
    module.exports.handler = serverless(app);
```

where app is your express client.

3. Add the following to your main folder and name it `serverless.yml`

```
# serverless.yml

service: starter-snake-node

provider:
  name: aws
  runtime: nodejs6.10
  stage: dev
  region: us-east-1

functions:
  app:
    handler: index.handler
    events:
      - http: ANY /
      - http: 'ANY {proxy+}'
```

This yaml file matches any http endpoints you've defined in your express app.

4. You're done! deploy with `sls deploy`.

### Extra Resources

- [This tutorial](https://serverless.com/blog/serverless-express-rest-api/) is a good starting point.