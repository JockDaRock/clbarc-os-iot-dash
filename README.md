# clbarc-os-iot-dash
Lab Guide for Building IoT Dashboards with OpenSource Technologies

## Building the apps we need to build our dashboard.

### First we need to download the main source code for our app with our terminal.

First, we need to open iTerm or the default terminal app to get started

Now, we are going to create our working directory and change our current working directory to our new directory.

```
$ mkdir dash-ws

$ cd dash-ws

```

Next, we need to download the source code from GitHub that we will be using to build our dashboards and other tools.

```

$ git clone https://github.com/JockDaRock/mqtt-docker-lab-code

$ git clone https://github.com/JockDaRock/freeboard-lab-code

```

### Now it is time to build the app from our source code

Change directories into our first code base

```
$ cd mqtt-docker-lab-code
```

Then, using the docker engine we will build our mqtt broker app.

```
$ docker build -t mqtt-brk:latest .
```

Once that is done building, we will run our application on our laptops.

```
$ docker run -d -p 1883:1883 -p 9001:9001 mqtt-brk:latest

$ docker ps
```

Next, we will build the dashboard application we will connect to for our MQTT application.

First, we need to get back out of our current directory and change into our freeboard app directory.

```
$ cd ..

$ cd freeboard-lab-code

```

Next, we need to build out freeboard image.

```
$ docker build -t barca-freeboard:latest .
```

Now, we are going to run our application on our laptop.

```
$ docker run -d -p 8585:80 barca-freeboard:latest

$ docker ps
```

Our applications are running! We can now start connecting our dashboard to our MQTT broker app.

### Now it is time to connect our dash and datasource together.

We need to open up our browser to a couple of sites.

Let's open our browser to `http://www.hivemq.com/demos/websocket-client/`.  We will use this a bit later.

Also, we will utilize the MQTT fx app as well.

Then, we will open an additional browser tab to `http://127.0.0.1:8585`.

#### Data Connections

* Now, in the Freeboard Dashboard app, under **Datasources**, click the add link.
* In the drop down menu, Select type **MQTT**
* Name your first pane of Data, **Engine Data**
* replace the default TOPIC with **devnet/dash**
* change the server variable to **127.0.0.1**
* change the port number to **9001**
* change _USE ENCRYPTION_ to **NO**
* then click save.

Our data source is now connected to our dashboard.

### Send a little bit of data

Using MQTT FX and our web based websockets client, we will use send a little bit of JSON data.

```
{"Data": {"RPM": 35}}
```

### Building our dashboard widgets

On the same dashboard site, click the **ADD PANE** button.

* Inside the pane, click the **+** button.
* For TYPE, select Text.
* For Title, type RPM Text.
* For value click DataSource, and then add the data source we connected.
* Click SAVE.

We have now created our first real-time widget on our dashboard. Let's practice a few more.

