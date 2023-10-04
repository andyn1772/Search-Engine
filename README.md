ABOUT
-------------------------
This is the base implementation of a full crawler that uses a spacetime
cache server to receive requests.

EXECUTION
-------------------------

To execute the crawler run the launch.py command.
```python3 launch.py```

You can restart the crawler from the seed url
(all current progress will be deleted) using the command
```python3 launch.py --restart```

You can specify a different config file to use by using the command with the option
```python3 launch.py --config_file path/to/config```

ARCHITECTURE
-------------------------

### FLOW

The crawler receives a cache host and port from the spacetime servers
and instantiates the config.

It launches a crawler (defined in crawler/\_\_init\_\_.py L5) which creates a 
Frontier and Worker(s) using the optional parameters frontier_factory, and
worker_factory.

When the crawler in started, workers are created that pick up an
undownloaded link from the frontier, download it from our cache server, and
pass the response to your scraper function. The links that are received by
the scraper is added to the list of undownloaded links in the frontier and
the url that was downloaded is marked as complete. The cycle continues until
there are no more urls to be downloaded in the frontier.
