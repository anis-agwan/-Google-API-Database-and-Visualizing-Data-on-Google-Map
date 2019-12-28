# -Google-API-Database-and-Visualizing-Data-on-Google-Map
Using the Google Places API with a Database and
Visualizing Data on Google Map

In this project, we are using the Google geocoding API
to clean up some user-entered geographic locations of
Places names and then placing the data on a Google
Map.

Note: Windows has difficulty in displaying UTF-8 characters
in the console so for each command window we open, we may need
to type the following command before running this code:

    chcp 65001

http://stackoverflow.com/questions/388490/unicode-characters-in-windows-command-line-how


we should install the SQLite browser to view and modify
the databases from:

http://sqlitebrowser.org/

The first problem to solve is that the Google geocoding
API is rate limited to a fixed number of requests per day.
So if we have a lot of data we might need to stop and
restart the lookup process several times.  So we break
the problem into two phases.

In the first phase we take our input data in the file
(where.data) and read it one line at a time, and retrieve the
geocoded response and store it in a database (geodata.sqlite).
Before we use the geocoding API, we simply check to see if
we already have the data for that particular line of input.

we can re-start the process at any time by removing the file
geodata.sqlite

Run the geoload.py program.   This program will read the input
lines in where.data and for each line check to see if it is already
in the database and if we don't have the data for the location,
call the geocoding API to retrieve the data and store it in
the database.

As of December 2016, the Google Geocoding APIs changed dramatically.
They moved some functionality that we use from the Geocoding API
into the Places API.  Also all the Google Geo-related APIs require an
API key. To complete this assignment without a Google account,
without an API key, or from a country that blocks
access to Google, we can use a subset of that data which is
available at:

http://py4e-data.dr-chuck.net/json

To use this, simply leave the api_key set to False in 
geoload.py.

This URL only has a subset of the data but it has no rate limit so
it is good for testing.

If we want to try this with the API key, follow the
instructions at:

https://developers.google.com/maps/documentation/geocoding/intro

and put the API key in the code.

Here is a sample run after there is already some data in the
database:

Mac: python3 geoload.py
Win: geoload.py

The geoload.py can be stopped at any time, and there is a counter
that we can use to limit the number of calls to the geocoding
API for each run.

Once we have some data loaded into geodata.sqlite, we can
visualize the data using the (geodump.py) program.  This
program reads the database and writes tile file (where.js)
with the location, latitude, and longitude in the form of
executable JavaScript code.

A run of the geodump.py program is as follows:

Mac: python3 geodump.py
Win: geodump.py

12 records written to where.js
Open where.html to view the data in a browser

The file (where.html) consists of HTML and JavaScript to visualize
a Google Map.  It reads the most recent data in where.js to get
the data to be visualized.  Here is the format of the where.js file:


This is a JavaScript list of lists.  The syntax for JavaScript
list constants is very similar to Python so the syntax should
be familiar to us.

Simply open where.html in a browser to see the locations.  we
can hover over each map pin to find the location that the
gecoding API returned for the user-entered input.  If we
cannot see any data when we open the where.html file, we might
want to check the JavaScript or developer console for ourr browser.
