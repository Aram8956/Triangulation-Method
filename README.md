# Triangulation Method for Mobile Subscriber Localization

This project represents a mobile subscriber localization system developed in LabVIEW using the WebView2 library and OpenStreetMap visualization technologies. The main purpose of the project is to simulate and visualize the process of determining a mobile user’s location based on distances from multiple BTS (Base Transceiver Station) units.

The system combines numerical calculations performed in LabVIEW with real-time map visualization implemented using HTML, JavaScript, Leaflet.js, and OpenStreetMap. This approach allows the project to integrate engineering calculations with modern web-based geographic visualization technologies.

The application architecture consists of several interconnected modules:

```
LabVIEW → WebView2 → HTML/JavaScript → Leaflet.js → OpenStreetMap
```

LabVIEW is responsible for:

* signal processing calculations,
* distance estimation,
* subscriber coordinate calculation,
* BTS parameter processing,
* real-time data updates.

The HTML and JavaScript part is responsible for:

* displaying the map,
* rendering BTS markers,
* visualizing subscriber movement,
* drawing coverage areas,
* displaying trajectory lines,
* updating the map interface in real time.

To visualize the geographic environment, the project uses OpenStreetMap together with the Leaflet.js JavaScript library. OpenStreetMap was selected because it is a free and open-source mapping platform that does not require paid APIs or commercial licenses. Leaflet.js provides flexible tools for rendering markers, circles, trajectories, and dynamic map objects.

The HTML page containing the map is loaded directly inside LabVIEW using the WebView2 component. This allows JavaScript code execution and real-time interaction between LabVIEW and the web interface.

The localization algorithm is based on the triangulation principle. Several BTS stations are placed on the map, each having predefined coordinates:

```
(x0, y0)
```

For every base station, the following parameters are entered:

* `PL` — measured path loss,
* `PLm` — reference path loss at 1 meter,
* `n` — propagation attenuation coefficient,
* `(x0, y0)` — BTS coordinates.

Using these parameters, the approximate distance between the mobile subscriber and each BTS is calculated using the path loss propagation model:

```
d = 10 ^ ((PL - PLm) / (10 * n))
```

where:

* `d` is the estimated distance,
* `PL` is the measured path loss,
* `PLm` is the reference path loss,
* `n` is the environmental attenuation factor.

The calculated distances are then used to estimate the subscriber’s approximate location on the map. Each BTS coverage area is visualized as a circle whose radius corresponds to the calculated signal distance. By combining multiple BTS measurements, the system approximates the subscriber position using triangulation principles.

Communication between LabVIEW and JavaScript is implemented through the `ExecuteScriptAsync()` method provided by WebView2. LabVIEW dynamically generates JavaScript commands such as:

```
updatePosition(latitude, longitude);
```

and

```
addBaseStation(latitude, longitude, radius);
```

These functions update the map in real time by moving the subscriber marker and rendering BTS coverage zones.

Several graphical elements are used to improve visualization clarity:

* blue marker — mobile subscriber,
* red markers — BTS stations,
* transparent red circles — coverage areas,
* blue polyline — subscriber movement trajectory.

The system also implements real-time subscriber movement simulation. A While Loop inside LabVIEW periodically recalculates coordinates and sends updated values to the JavaScript map interface. This creates continuous real-time visualization of subscriber movement across the map.

The developed system provides the following capabilities:

* visualization of BTS positions,
* mobile subscriber tracking,
* distance estimation based on signal attenuation,
* real-time coordinate updates,
* movement trajectory visualization,
* BTS coverage area rendering,
* simulation of mobile communication network behavior,
* integration of LabVIEW with modern web technologies.

One of the main advantages of the project is the combination of engineering computation tools with modern GIS visualization technologies. The developed solution demonstrates how LabVIEW can be integrated with web-based geographic systems to create interactive and real-time monitoring applications.

The project can be further extended by implementing:

* accurate trilateration algorithms,
* RSSI-based signal strength visualization,
* dynamic signal quality indicators,
* handover simulation between BTS stations,
* heatmap generation,
* GPS integration,
* database logging,
* historical route analysis,
* multiple subscriber tracking.

Overall, the project demonstrates a practical implementation of mobile subscriber localization techniques and provides a flexible platform for studying triangulation methods, wireless signal propagation, and real-time geographic visualization systems.
