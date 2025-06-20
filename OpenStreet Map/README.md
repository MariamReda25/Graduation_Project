# OpenStreet Map 

## Main Flask Application (server.py):

  - Creates a Flask web server that:

     ◾️ Accepts POST requests at /api/add to record road damage reports (latitude, longitude, type, description)

     ◾️ Serves a map view at / that displays all reported damages

  - Uses SQLite database (damages.db) to store reports

  - Runs on port 5000 with debug mode enabled

## Client Script (request.py):

  - Appears to be a client that reads from:

      ◾️ ai.txt (contains damage type like "Pothole")

      ◾️ gps.txt (contains latitude,longitude coordinates)

  - Processes these files and sends the data to the Flask server

## Database Initialization (intialize_db.py):

   - Creates the SQLite database with a road_damage table

   - Includes a UNIQUE constraint to prevent duplicate entries for the same location and damage type

To make this system work properly, you would need to:

First run the database script to create the SQLite database

Then run the Flask application (app.py) to start the server

Finally, the client script can be run to submit damage reports

## Needed Packages :

 pip3 install flask

## Want to Test with Real Devices?
If you're running this on a Raspberry Pi or want to access the app from another phone/device on the same network:
Replace 127.0.0.1 with your local IP address in both app.py and request.py


  

