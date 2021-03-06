<h1 align="center"><img width="30px"> Geolocation </h1>

##  About Me:

<img  src="./programming.gif" height="290px" align="right" />
<br>

- All about me is at **[My Website](https://jompy31.github.io/)**

What is Geolocation?
=====================

Geolocation is a simple and clever application which uses google maps api.

1. Geocode Module allows you to easily and quickly get information about given location.

Geocode Module returns such information as: 
* country, 
* country short form,
* city, 
* route/street, 
* street number,
* postal code,
* formatted address,
* administrative areas,
* lat,
* lng


2. Distance Module allows you to get information about travel distance and time for a matrix of origins and destinations.

Distance Module returns such information as:
* origin address
* destination address
* duration
* distance
    - kilometers
    - meters
    - miles


What do You need?
-----------------
To use this application you need to have Google API key.
    [Google Maps Documentation](https://developers.google.com/maps/documentation/geocoding/) -- Geocoding

1. Open [APIs console](https://code.google.com/apis/console).


2. Turn On Geocode API.


3. Turn On Distance Matrix API.
  
4. Get your API Key.


How to install it?
-------------------
    pip install geolocation-python


How to use Geocode Module?
----------------------------

```python
# -*- coding: utf-8 -*-

from geolocation.main import GoogleMaps

address = "New York City Wall Street 12"

google_maps = GoogleMaps(api_key='your_google_maps_key') 

location = google_maps.search(location=address) # sends search to Google Maps.

print(location.all()) # returns all locations.

my_location = location.first() # returns only first location.

print(my_location.city)
print(my_location.route)
print(my_location.street_number)
print(my_location.postal_code)

for administrative_area in my_location.administrative_area:
    print("{}: {} ({})".format(administrative_area.area_type, 
                               administrative_area.name, 
                               administrative_area.short_name))

print(my_location.country)
print(my_location.country_shortcut)

print(my_location.formatted_address)

print(my_location.lat)
print(my_location.lng)

# reverse geocode

lat = 40.7060008
lng = -74.0088189

my_location = google_maps.search(lat=lat, lng=lng).first()

```

How to use Distance Module?
----------------------------
Mode parameter ??? specifies the mode of transport to use when calculating directions. 

Valid values are:
* driving (default) indicates standard driving directions using the road network.
* walking requests walking directions via pedestrian paths & sidewalks (where available).
* bicycling requests bicycling directions via bicycle paths & preferred streets (currently only available in the US and some Canadian cities).
* transit requests distance calculation via public transit routes (where available).

Avoid parameter -  Directions may be calculated that adhere to certain restrictions. Restrictions are indicated by use of the avoid parameter, and an argument to that parameter indicating the restriction to avoid.

The following restrictions are supported:
* avoid=tolls
* avoid=highways
* avoid=ferries
    
```python
# -*- coding: utf-8 -*-

from geolocation.main import GoogleMaps
from geolocation.distance_matrix.client import DistanceMatrixApiClient

origins = ['rybnik', 'oslo']
destinations = ['zagrzeb']

google_maps = GoogleMaps(api_key='your_google_maps_key')

items = google_maps.distance(origins, destinations).all()  # default mode parameter is DistanceMatrixApiClient.MODE_DRIVING.

for item in items:
    print('origin: %s' % item.origin)
    print('destination: %s' % item.destination)
    print('km: %s' % item.distance.kilometers)
    print('m: %s' % item.distance.meters)
    print('miles: %s' % item.distance.miles)
    print('duration: %s' % item.duration)  # returns string.
    print('duration datetime: %s' % item.duration.datetime)  # returns datetime.
    
    # you can also get items from duration, returns int() values.
    print('duration days: %s' % item.duration.days)
    print('duration hours: %s' % item.duration.hours)
    print('duration minutes: %s' % item.duration.minutes)
    print('duration seconds: %s' % item.duration.seconds)
```

Mode Bicycling:
```python
items = google_maps.distance(origins, destinations, DistanceMatrixApiClient.MODE_BICYCLING).all()

for item in items:
    print('origin: %s' % item.origin)
    print('destination: %s' % item.destination)
    print('km: %s' % item.distance.kilometers)
    print('m: %s' % item.distance.meters)
    print('miles: %s' % item.distance.miles)
    print('duration: %s' % item.duration)
```

Mode Walking:
```python
items = google_maps.distance(origins, destinations, DistanceMatrixApiClient.MODE_WALKING).all()

for item in items:
    print('origin: %s' % item.origin)
    print('destination: %s' % item.destination)
    print('km: %s' % item.distance.kilometers)
    print('m: %s' % item.distance.meters)
    print('miles: %s' % item.distance.miles)
    print('duration: %s' % item.duration)
```

Mode Transit:
```python
items = google_maps.distance(origins, destinations, DistanceMatrixApiClient.MODE_TRANSIT).all()

for item in items:
    print('origin: %s' % item.origin)
    print('destination: %s' % item.destination)
    print('km: %s' % item.distance.kilometers)
    print('m: %s' % item.distance.meters)
    print('miles: %s' % item.distance.miles)
    print('duration: %s' % item.duration)
```

Mode Highway:
```python
items = google_maps.distance(origins, destinations, avoid=DistanceMatrixApiClient.AVOID_HIGHWAYS).all()

for item in items:
    print('origin: %s' % item.origin)
    print('destination: %s' % item.destination)
    print('km: %s' % item.distance.kilometers)
    print('m: %s' % item.distance.meters)
    print('miles: %s' % item.distance.miles)
    print('duration: %s' % item.duration)
```

Avoid Ferries:
```python
items = google_maps.distance(origins, destinations, avoid=DistanceMatrixApiClient.AVOID_FERRIES).all()

for item in items:
    print('origin: %s' % item.origin)
    print('destination: %s' % item.destination)
    print('km: %s' % item.distance.kilometers)
    print('m: %s' % item.distance.meters)
    print('miles: %s' % item.distance.miles)
    print('duration: %s' % item.duration)
```

Avoid Tolls:
```python
items = google_maps.distance(origins, destinations, avoid=DistanceMatrixApiClient.AVOID_TOLLS).all()

for item in items:
    print('origin: %s' % item.origin)
    print('destination: %s' % item.destination)
    print('km: %s' % item.distance.kilometers)
    print('m: %s' % item.distance.meters)
    print('miles: %s' % item.distance.miles)
    print('duration: %s' % item.duration)
```

## ?????? Let's get connected:

<p>
  <a href="https://www.linkedin.com/in/jean-pierre-barnett-caruzo-452b9a1b1/" target="_blank"><img alt="LinkedIn" target="_blank" src="https://img.shields.io/badge/LinkedIn-0077B5?style=for-the-badge&logo=linkedin&logoColor=white"  height="30px"/></a>

</p>


## Activities and Information GITHUB:

<div align="center">
  <img align="center" src="https://github-readme-stats-anuraghazra1.vercel.app/api?username=jompy31&show_icons=true" />
  <img align="center" src="https://github-readme-streak-stats.herokuapp.com/?user=jompy31" alt="Jean_Pierre" />
  <img align="center" src="https://github-readme-stats.vercel.app/api/top-langs/?username=jompy31&show_icons=true&layout=compact&langs_count=10" alt="jorneylopez" />
</div>


  

