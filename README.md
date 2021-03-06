# Sponsorship API
> DEPRECATED: The previously active mongo instance supporting data to this API has been shut down. If you would like to run this project, you will need to provide a viable datastore. 

![coverage][coverage]
[![made-with-python](https://img.shields.io/badge/Made%20with-Python-1f425f.svg)](https://www.python.org/)

> A proof of concept sponsorship matching API which takes a community sports league and matches is with a potential sponsor. 



## Project Features

#### ADD A LEAGUE TO THE SYSTEM
In this example API, a League refers to a collection of, at the very least:

1. A league name.
2. A latitude/longitude pair.
3. A single price to purchase their sponsorship opportunity.

#### FIND LEAGUES TO SPONSOR
This endpoint should accept a few arguments:

1. A latitude/longitude pair around which to focus the search.
2. A radius in miles in which to search around that central point.
3. A total budget to spend on leagues.


## Running development server

Make sure to initialize a new MongoDB instance for testing. 
Start by creating a directory for your MongoDB data.

Eg: `/data/db`

#### Mac OSX install
```sh
brew tap mongodb/brew
brew services start mongodb
mongod --port 27017 --dbpath <path_to_directory>
```

Instructions for how to install on other machines can be found in the [MongoDB docs](https://docs.mongodb.com/v3.2/tutorial/install-mongodb-on-os-x/).

```sh
$ pip install -r requirements.txt
$ export MONGO_HOST=<host>
$ python app.py
 * Serving Flask app "app" (lazy loading)
 * Environment: production
   WARNING: Do not use the development server in a production environment.
   Use a production WSGI server instead.
 * Debug mode: off
 * Running on http://127.0.0.1:5000/ (Press CTRL+C to quit)
```

## Run Tests
```
$ pytest
================================ test session starts ================================
platform darwin -- Python 3.7.2, pytest-4.4.2, py-1.8.0, pluggy-0.11.0
plugins: cov-2.7.1
collected 22 items                                                                                                                                              

tests/test_mongo_interface.py ......................                                                                                                              [100%]

================================ 22 passed in 0.18 seconds ================================
```

## [API Endpoints](https://documenter.getpostman.com/view/6396321/S1LySmdN)
_-- Follow the link for Auto generated Postman Docs_
<hr>

#### GET Check Server
_-- This confirms that the server is active._

`http://localhost:5000/health`

<hr>

#### GET MongoDB Health
_-- This checks that the MongoDB instance is running and accessible by the server._

`http://localhost:5000/database_health`

<hr>

#### POST Create New League
_-- This creates a new league and stores it in the database._

`http://localhost:5000/leagues`


##### HEADERS
```
{
	"league_name": "The Red Sox",
	"price": 2400,
	"coordinates": [40.03423242143, -75.13485]
}
```

##### SAMPLE OUTPUT
```
"The Red Sox -- Price: 2400, Coordinates(latitude=40.03423242143, longitude=-75.13485)"
```

<hr>

#### GET Get Leagues to Sponsor

_-- This returns enough leagues to spend up to the budget, sponsoring as many leagues as possible without going over it. Also returns the remaining budget._

`http://localhost:5000/leagues`



##### HEADERS
```
{
    "total_budget": 7500, 
    "search_radius": 7, 
    "central_location": [40.0274622857143, -75.0562142]
}
```
##### SAMPLE OUTPUT
```
{
    "leagues_to_sponsor": [
        {
            "coordinates": [
                40.0276523242143,
                -75.0132142
            ],
            "name": "The Fighting Irish",
            "price": 1300
        },
        {
            "coordinates": [
                40.0274622852143,
                -75.0564142
            ],
            "name": "The Zoomers",
            "price": 1500
        },
        {
            "coordinates": [
                40.0274622852143,
                -75.0564142
            ],
            "name": "Team 8",
            "price": 1620
        },
        {
            "coordinates": [
                40.0274622851143,
                -75.0552142
            ],
            "name": "Team 7",
            "price": 2130
        }
    ],
    "remaining_budget": 950
}
```

[coverage]: ./coverage.svg
