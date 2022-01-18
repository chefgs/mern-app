# "Property Bookings Catalog" web app developed using MERN Stack 

[![NodeJS CI Job](https://github.com/chefgs/mern-app/actions/workflows/node.js.yml/badge.svg)](https://github.com/chefgs/mern-app/actions/workflows/node.js.yml)  [![CodeQL](https://github.com/chefgs/mern-app/actions/workflows/codeql-analysis.yml/badge.svg)](https://github.com/chefgs/mern-app/actions/workflows/codeql-analysis.yml)

## Table of Contents
- [Introduction](#introduction)
- [MERN Architecture](#mern-architecture)
- [Steps to create the application](#steps-to-create-the-application)
  - [Create MongoDB Cluster and Get DB Connection String](#create-mongodb-cluster-and-get-db-connection-string)
  - [Setting up Application to connect with MongoDB](#setting-up-application-to-connect-with-mongodb)
  - [Start the Express server](#start-the-express-server)
    - [Method 1](#method-1)
    - [Method 2](#method-2)
  - [Start the React app](#start-the-react-app)
- [Testing Application and Accessing UI](#testing-application-and-accessing-ui)
- [GitHub Action Workflow Details](#gitHub-action-workflow-details)
- [Reference](#reference)

## Introduction
This application is developed for the submission of *__Dev community X  MongoDB Hackathon__*. This is a MERN stack based Web Application. 

MERN stands for MongoDB, Express, React, Node, which are making up the tech stack.

MongoDB - Popular NoSQL document database
ExpressJS - Node.js web framework
ReactJS - a client-side JavaScript framework
NodeJS - the JavaScript web server

Express and Node make up the middle (application) tier. Express.js is a server-side web framework, and Node.js the popular and powerful JavaScript server platform. Regardless of which variant you choose, ME(RVA)N is the ideal approach to working with JavaScript and JSON, all the way through.

## MERN Architecture
> As per the [documentation](https://www.mongodb.com/mern-stack)
The MERN architecture allows us to easily construct a `3-tier` architecture (frontend, backend, database) entirely using JavaScript and JSON.
![MERN Arch](https://webimages.mongodb.com/_com_assets/cms/mern-stack-b9q1kbudz0.png?auto=format%2Ccompress)

It is been a while I'm trying to create a Web App using MERN stack. Finally I'm able to create it. Thanks to the great [article by MongoDB team](https://www.mongodb.com/languages/express-mongodb-rest-api-tutorial). I took the inspiration from the MongoDB tutorial and created this application.

## Steps to create the application
### Create MongoDB Cluster and Get DB Connection String
- We choose MongoDB Atlas Managed Database Service provider by MongoDB
- We need to signup for an account in MongoDB portal
- After logging into account we need to create project and enable billing if needed. There is no billing required for Demo purposes.
- Rest of steps assuming that, we have created project in MongoDB account
  - Step 1: Create MongoDB cluster using Atlas UI. Refer the documentation [here](https://docs.atlas.mongodb.com/getting-started/?_ga=2.209539858.187869111.1641820485-130312989.1641820485)

![project](https://github.com/chefgs/repo_images/blob/master/mongo-create-project-cluster.png?auto=format%2Ccompress)

  - Step 2: After choosing the project to create the Cluster, click `create` button
  - Step 3: Choose the required Cloud Provider and dedicated or shared infrastructure to host the DB. This would take few minutes to create the Cluster. Move to next step after the Cluster creation is complete

![create_cluster](https://github.com/chefgs/repo_images/blob/master/mongo-create-cluster.png?auto=format%2Ccompress)  

  - Step 4: Select the database from Atlas UI and click on `connect` button available near the DB cluster
  - Step 5: Choose `Connect Your Application` and choose `NodeJS` from the option in next screen

![connect_string](https://github.com/chefgs/repo_images/blob/master/mongo-connect-dbstring.png?auto=format%2Ccompress)

- Step 6: Get the `connection string` for the database to use it in the `ATLAS_URI` config value in the file `server/config.env` later in this tutorial
- Step 7: We are choosing `sample_airbnb` database collection to implement the bookings catalog application
```
mongodb+srv://<admin_user>:<password>@democluster.aurnw.mongodb.net/myFirstDatabase?retryWrites=true&w=majority
```
Note: Replace `<password>` with the password for the `<admin_user>` user. Replace myFirstDatabase with the name of the database that connections will use by default.

### Setting up Application to connect with MongoDB
- We have `server/config.env` file in our repository, replace the values `db_user`, `db_user_pwd` and `mongodb_cluster_url` with the respective values that is set
Then, set the Atlas URI connection parameter in `server/config.env` to our Connection String:
```
ATLAS_URI=mongodb+srv://<db_user>:<db_user_pwd>@<mongodb_cluster_url>?retryWrites=true&w=majority
```
- We need to run the Express server and React app parallely in two different terminals
## Start the Express server
- Express server runs on `localhost:5000`
### Method 1
- In this method we use `nodemon` - Nodemon is a utility that will monitor for any changes in your source and automatically restart your server.
```
cd server
npm install
npm install -g nodemon
nodemon server
```

### Method 2
- In this method, we simply run `npm start` to run the server
```
cd server
npm install
npm start
```

## Start the React app
- React app runs on `localhost:3000`
```
cd app/listings/
npm install
npm start
```
## Testing Application and Accessing UI
- Once `Server` and `React App` are up and running, it opens the portal in default browser on `http://localhost:3000` URL (else we can use this URL to access the portal) and we should see our “Property Bookings Catalog” application.

> Application Accessible on Browser
> 
![mern app in browser](https://github.com/chefgs/repo_images/blob/master/mern_app.png?auto=format%2Ccompress)

> Application `See Details` response
> 
![mern see details](https://github.com/chefgs/repo_images/blob/master/mern-app-seedetails.png?auto=format%2Ccompress)

> Server response on console for various CRUD operations
> 
![server response](https://github.com/chefgs/repo_images/blob/master/mern-app-server-resp.png?auto=format%2Ccompress)

## GitHub Action Workflow Details
- This repo has GitHub action [CI workflow](https://github.com/chefgs/mern-app/blob/master/.github/workflows/node.js.yml) to perform Continuous integration process explained below,
  - Checks out the code into workspace root
  - Build the server and frontend app
  - Creates docker image build for server and frontend app
  - Pushes the docker image into docker hub registry

## Reference
- This repository contains the sample application for the [MongoDB and Express.js REST API tutorial](https://www.mongodb.com/languages/express-mongodb-rest-api-tutorial).

- [Getting Started with Atlas](https://docs.atlas.mongodb.com/getting-started/) guide, to learn how to create a free Atlas account, create your first cluster and get your Connection String to the database. 

- [MERN Stack documentation](https://www.mongodb.com/mern-stack)
