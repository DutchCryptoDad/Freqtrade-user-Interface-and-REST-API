Use the REST API interface if you do not want to use the web interface but still want to check on the bot from another computer or want to use the output in another program.

The activation of the REST API is similar to the activation of the Web UI interface.

## Enable the API

This time we keep it simple and stay close to the configuration on the Freqtrade website.

Edit config.json and enable the API:

```
    "api_server": {
        "enabled": true,
        // Enable the bot to listen on all interfaces with 0.0.0.0
        // To stay on the local machine, use 127.0.0.1
        "listen_ip_address": "0.0.0.0",
        "listen_port": 8080,
        "verbosity": "error",
        "username": "dcd",
        "password": "dcdpass"
    },
```

Then start the bot.

## Create a client configuration

{
    "api_server": {
        "enabled": true,
        "listen_ip_address": "0.0.0.0",
        "listen_port": 8080,
        "username": "dcd",
        "password": "dcdpass",
        //...
    }
}

## Use the rest_client script

To get information from the bot through the REST API, use the rest_client.py file in the scripts/ directory.

In the example below we are checking if the bot is alive with a ping on the Freqtrade server itself:

```
cd scripts/

python3 rest_client.py --config rest_config.json ping

{"status": "pong"}
```

The command structure for the rest client is:

``python3 scripts/rest_client.py --config rest_config.json <command> [optional parameters]``

## Use the rest_client script from another computer

To use the rest_client from another computer, you must first instal the Python3 ``requests`` module.

Copy the [rest_client.py](https://github.com/freqtrade/freqtrade/blob/develop/scripts/rest_client.py) script from the Freqtrade site. Then create a client configuration pointing to the IP address and port on the server.

```
nano rest_config.json

# enter the lines below
{
    "api_server": {
        "enabled": true,
        // IP address of the listening Freqtrade server here
        "listen_ip_address": "191.1.1.16",
        "listen_port": 8080,
        "username": "dcd",
        "password": "dcdpass",
        //...
    }
}
```

Make sure that the firewall on the server is configured to allow traffic to this port!

## Other commands u can use

See the [Freqtrade site](https://www.freqtrade.io/en/stable/rest-api/#available-endpoints) for the other commands you can use.

To see which options are available, use the help switch after the command

```
python3 rest_client.py --config rest_config.json help
```

THe list below comes from the Freqtrade site and will not be updated:

|  Command | Description |
|----------|-------------|
| `ping` | Simple command testing the API Readiness - requires no authentication.
| `start` | Starts the trader.
| `stop` | Stops the trader.
| `stopbuy` | Stops the trader from opening new trades. Gracefully closes open trades according to their rules.
| `reload_config` | Reloads the configuration file.
| `trades` | List last trades. Limited to 500 trades per call.
| `trade/<tradeid>` | Get specific trade.
| `delete_trade <trade_id>` | Remove trade from the database. Tries to close open orders. Requires manual handling of this trade on the exchange.
| `show_config` | Shows part of the current configuration with relevant settings to operation.
| `logs` | Shows last log messages.
| `status` | Lists all open trades.
| `count` | Displays number of trades used and available.
| `locks` | Displays currently locked pairs.
| `delete_lock <lock_id>` | Deletes (disables) the lock by id.
| `profit` | Display a summary of your profit/loss from close trades and some stats about your performance.
| `forcesell <trade_id>` | Instantly sells the given trade  (Ignoring `minimum_roi`).
| `forcesell all` | Instantly sells all open trades (Ignoring `minimum_roi`).
| `forcebuy <pair> [rate]` | Instantly buys the given pair. Rate is optional. (`forcebuy_enable` must be set to True)
| `performance` | Show performance of each finished trade grouped by pair.
| `balance` | Show account balance per currency.
| `daily <n>` | Shows profit or loss per day, over the last n days (n defaults to 7).
| `stats` | Display a summary of profit / loss reasons as well as average holding times.
| `whitelist` | Show the current whitelist.
| `blacklist [pair]` | Show the current blacklist, or adds a pair to the blacklist.
| `edge` | Show validated pairs by Edge if it is enabled.
| `pair_candles` | Returns dataframe for a pair / timeframe combination while the bot is running. **Alpha**
| `pair_history` | Returns an analyzed dataframe for a given timerange, analyzed by a given strategy. **Alpha**
| `plot_config` | Get plot config from the strategy (or nothing if not configured). **Alpha**
| `strategies` | List strategies in strategy directory. **Alpha**
| `strategy <strategy>` | Get specific Strategy content. **Alpha**
| `available_pairs` | List available backtest data. **Alpha**
| `version` | Show version.

!!! Warning "Alpha status"
    Endpoints labeled with *Alpha status* above may change at any time without notice.




