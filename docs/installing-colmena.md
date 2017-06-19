# Setup a Colmena development environment

### Download Colmena.

Create a Colmena workspace in the `colmena-base` folder.

```
$ cd ~/workspace/ngatl
$ git clone https://github.com/colmena/colmena.git colmena-base
```

### Install dependencies

Move into the `colmeba-base` folder and run `npm install`

```
$ cd colmena-base
$ npm install
```

### Start development servers

Colmena comes with a MongoDB and Mailhog development server that run inside Docker.

> When MongoDB is not configured Colmena will use the in-memory database. This means that all the data is gone each time the API server restarts, and in order to be useful you'd have to run Colmena with `initdb` mode on, which slows down API start significantly. This is why it's recommended to run the development setup on MongoDB. 

If you prefer to run these servers in anohter way you can skip this step and configure your mongo url in the next step.

```
$ npm run servers:start
```

### Edit configuration to use mongodb and MailHog

Create a copy of the default configuration

```
$ cp apps/api/config/default.yaml apps/api/config/local.yaml
```

Update `apps/api/config/local.yaml` to define the development database- and mailserver.

```
mongodb:
  url: mongodb://localhost/ngatl

smtp:
  host: localhost
  port: 1025
```


### Seed DB with sample data

In order to get some sample data in the database we run the initdb command:

```
$ npm run initdb
```

### Start Colmena in Development mode

```
$ npm run dev
```

You should now see the server starting. 

The API will listen on [http://127.0.0.1:3000](http://127.0.0.1:3000) and the API explorer is found here [http://127.0.0.1:3000/explorer](http://127.0.0.1:3000/explorer)

When the admin is built it can be accessed on [http://127.0.0.1:9000](http://127.0.0.1:9000).

## PLease make sure Colmena is working 

When there are no build errors in the log, and you see the message `Webpack: Compiled successfully.` you should be able to log in on [http://127.0.0.1:9000](http://127.0.0.1:9000). Because the server is running in development mode, the default credentials will be displayed. 

After logging in you should see the sample content like pages, files, etc that are all part of the default 'domain'. 