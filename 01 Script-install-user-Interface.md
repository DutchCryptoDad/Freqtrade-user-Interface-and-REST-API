By default the User Interface is not installed when installing Freqtrade with the install.sh script.

## Installation

To install the UI, use the following command:

```
source ./.env/bin/activate
freqtrade install-ui
```

The UI will be installed in ``/freqtrade/freqtrade/rpc/api_server/ui``.

## Activation in config file

Change the config at several points.
Most important are the API server configuration lines:


```
    "api_server": {
        "enabled": true,
        // Listen to all interfaces for network requests
        "listen_ip_address": "0.0.0.0",
        // Use a obscure port for security measures
        "listen_port": 9487,
        "verbosity": "error",
        "enable_openapi": false,
        // USE A VERY GOOD SECRET KEY!!!
        "jwt_secret_key": "itsmysecret",
        "CORS_origins": [],
        // Username and password for web interface
        "username": "dcd",
        // USE A VERY GOOD PASSWORD!!!
        "password": "dcd"
    },
    "bot_name": "freqtrade bot",
    "user_data_dir": "/home/dcd/freqtrade/user_data/",
    "strategy_path": "/home/dcd/freqtrade/user_data/",
    "strategy": "SampleStrategy",
    "db_url": "sqlite:////home/dcd/freqtrade/user_data/trades_dryrun.sqlite",
```

Take care that you use good keys and passwords otherwise you could be hacked and your funds might be stolen.

Also, use 127.0.0.1 if you only want to reach your bot from the local computer.

Use 0.0.0.0 if your bot is on a server and you want to reacht the bot interface from another computer. 
You can also change your bot port from 8080 to a more obscure port so that the bot is not easily spotted by hackers.

Make sure the firewall port is also open to allow traffic to reach your bot UI.

## Start the bot with UI

Then start the bot with:

```
freqtrade trade --config config.json
```

You will see something like this in the logs of Freqtrade:

```
2021-11-26 10:12:05,660 - uvicorn.error - INFO - Started server process [5370]
2021-11-26 10:12:05,668 - uvicorn.error - INFO - Waiting for application startup.
2021-11-26 10:12:05,672 - uvicorn.error - INFO - Application startup complete.
2021-11-26 10:12:05,674 - uvicorn.error - INFO - Uvicorn running on http://0.0.0.0:9487 (Press CTRL+C to quit)
```

## Check for workings and enter the UI

To check if the UI is working, enter the following in your browser:

```
http://127.0.0.1:9487/api/v1/ping
```

It should give you a 'pong' reaction: ``{"status":"pong"}``.

If you want to enter the Freqtrade user interface, use ``http://127.0.0.1:9487/`` in your browser.

Login with the name of the bot, user name and user password from the config file.

Now you can see how your bot performs through a graphical UI.
