summary: How to setup Maxcess database
id: how-to-setup-maxcess
categories: Sample
status: Published
authors: Andy
Feedback Link: https://andy.io

#How to Setup Maxcess System

## Overview
Duration: 1

Scrapes franchise data from franchise.ftc.go.kr and inserts it into a MySQL database.

### What To Be Installed (or Upgraded)
- python3.6
- python3-venv
- pip


## Prerequisites
Duration: 1

fcscraper needs at least Python 3.6 to run.

### python3.6
```python3.6
  sudo apt-get install python3.6``
```

## Installation
Duration: 10

- Locate and enter the root folder of the source distribution. E.g.
```
  cd ~/fcscraper/``

  // Install Python virtual environment
  sudo apt-get install python3-venv``
```

- Create a new Python virtual environment
```
  sudo python3 -m venv .venv``
```

- Activate the virtual environment
```
  source .venv/bin/activate
```

- Upgrade pip to the latest version
```
  sudo pip install --upgrade pip
```

- Install fcscraper
```
   sudo python3 setup.py install
```

- Give fscraper your database credentials in ``config.yaml``

- Run fcscraper
```
  fcscraper
```

(Optional) Copy and paste your entire .scrapy folder to the running folder to import previous cache storage.  
Your directory should look similar to this:
```

  fcscraper/
      .scrapy/
          httpcache/
      src/
      README.rst
```

## Usage
Duration: 3

```
fcscraper [options] URLs

URLs            The URLs to start crawling from, separated by space.
--clear-cache   Clear cache and run. Not recommended. Scrapy automatically 
                compares cached versions to the live pages and fetches the most
                recent anyway.
--concurrent    Set a max number of concurrent requests
--config        Specify the configuration file to use   
--debug         Run in debug mode. Only affects what gets output to logs.
--delay         Set a delay between http requests (in seconds)
--file          Path to custom configuration file
--help          Display help
--json          Output scraped items in json instead of updating the db
--limit         Set the max number of requests to send before exiting
--lines         If --json is also set, output a jsonlines file
--version       Display version
--offline       Run the program in offline mode. Note: this does not prevent 
                new requests to the server. You should disable your network 
                adapter as well.
--version       Show version.
-c              Shorthand for --config
-d              Shorthand for --delay
-h              Shorthand for --help
-j              Shorthand for --json
-l              Shorthand for --limit
-n              Shorthand for --concurrent
-v              Shorthand for --version
```

## Examples
Duration: 2
```
.. csv-table::
   :header: "Command", "Description"
   :widths: 20, 59

   "``fcscraper``", "Scrape all franchises"
   "``fcscraper --clear-cache``", "Clear cache and scrape all"
   "``fcscraper -d 3``", "Scrape with a delay of 3 seconds between requests"
   "``fcscraper --offline -n 32``", "Scrape with a maximum of 32 concurrent connections to the domain in offline mode (useful when exclusively using cached pages)"
   "``fcscraper -c custom_configs.yml``", "Scrape using configurations stored in ``custom_configs.yml``"
   "``fcscraper -l 5 -j``", "Scrape 5 and output as JSON"
   "``fcscraper -l 50 -j --lines``", "Scrape 50 and output as JSONlines"
   "``fcscraper -l 10``", "Scrape 10"
   "``fcscraper -j https://franchise.ftc.go.kr/user/extra/main/62/firMst/view/jsp/LayOutPage.do?dataIdx=75545``", "Scrape the given page and output as JSON"
   "``fcscraper -j 75506``", "Shorthand for above command"
```
