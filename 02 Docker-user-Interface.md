The User Interface is installed by default when using Docker image. 

## Activation in config file

Change the config:

```
    "api_server": {
        "enabled": true,
        "listen_ip_address": "0.0.0.0",
        "listen_port": 8080,
        "username": "dcd",
        // Use a good password here!!!
        "password": "dcd"
    },

```

Take care that you use a good password, otherwise you could be hacked and your funds might be stolen.


## Activation in Docker compose file

Open the ``docker-compose.yml`` file and uncomment the following lines if necessary:

```
    ports:
      - "127.0.0.1:8080:8080"
```

Use 127.0.0.1 if you only want to reach your bot from the local computer.

You can also make your Freqtrade UI port more obscure by using the following line:

```
    ports:
      - "127.0.0.1:3333:8080"
```

Now the website is only reachable by port 3333

## Start the bot with UI

Start the bot with:

```
docker-compose up -d
```

## Check for workings and enter the UI

To check if the UI is working, enter the following in your browser:

```
http://127.0.0.1:3333/api/v1/ping
```

It should give you a 'pong' reaction: ``{"status":"pong"}``.

If you want to enter the Freqtrade user interface, use ``http://127.0.0.1:3333/`` in your browser.

Login with the name of the bot, user name and user password from the config file.

Now you can see how your bot performs through a graphical UI.
