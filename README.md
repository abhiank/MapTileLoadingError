# MapTileLoadingError
A sample app to show the tile loading error happening in Google Maps.

The error which I'm facing in this app is that while the map is tracking a live location (which has been simulated here using a fixed route), the map tiles do not load. This happens both for vector and raster map tiles. This repo only has the vector tiles, but the issue is visible on this as well. 

### More details :

1. In this sample app, I've preloaded latitude and longitudes of a route in Perth, Australia.

2. To simulate a real live tracking of current location, I'm creating a new cameraPosition object every 1000 milliseconds and then animating the camera to the new location. 

```
val cameraPosition = CameraPosition.Builder()
    .target(newPos)
    .zoom(navCurrentLocationMapZoomLevel!!)
    .tilt(navCurrentLocationMapTilt!!)
    .bearing(mapBearing)
    .build()

mMap.animateCamera(CameraUpdateFactory.newCameraPosition(cameraPosition))
```

The tracking works fine. The only problem is that new tiles do not get loaded while the map follows the current location. If however, I touch the screen while map is following the location, then the tiles for the visible area starts loading.

#### A new observation I made was that if the duration between new location updates was set to anything above 1100 milliseconds then the map starts loading. 

Here's a gif showing this - The gif is showing that the camera is moving to an area where tiles of that zoom level have not been loaded and despite coming into the view, they do not load. Only when I touch the screen do the tiles load.

![Alt Text](https://i.stack.imgur.com/VljaY.gif)
