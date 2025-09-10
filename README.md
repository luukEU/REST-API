# REST API
# Roermond Nominatim Client-Side Demo

Dit project toont hoe je coördinaten van een locatie (Roermond) kunt ophalen en visualiseren op een kaart met **Leaflet**. Het gebruikt de opgegeven coördinaten van Nominatim en toont een marker op de kaart.

---

## Bestand

* **index.html**:

  * Initialiseert een Leaflet-kaart.
  * Plaatst een marker op de opgegeven coördinaten van Roermond (`lat: 51.1933903`, `lon: 5.9882649`).
  * Toont de coördinaten boven de kaart.
  * Toont de raw JSON data van deze locatie onder de kaart.

---

## Hoe werkt het

1. **Coördinaten instellen**

   ```js
   const lat = 51.1933903;
   const lon = 5.9882649;
   document.getElementById('coords').textContent = lat + ', ' + lon;
   ```

   * De coördinaten worden gebruikt om de kaart te centreren en een marker te plaatsen.

2. **Kaart initialiseren**

   ```js
   const map = L.map('map').setView([lat, lon], 13);
   L.tileLayer('https://{s}.tile.openstreetmap.org/{z}/{x}/{y}.png', {
     maxZoom: 19,
     attribution: '&copy; OpenStreetMap contributors'
   }).addTo(map);
   ```

   * Maakt een Leaflet-kaart en laadt OpenStreetMap-tegels.

3. **Marker plaatsen**

   ```js
   const marker = L.marker([lat, lon]).addTo(map);
   marker.bindPopup(`Roermond<br>Lat: ${lat}<br>Lon: ${lon}`).openPopup();
   ```

   * Plaatst een marker op de kaart en toont een popup met de naam en coördinaten.

4. **Raw JSON tonen**

   ```js
   const rawData = {
     "place_id":101517446,
     "lat":"51.1933903",
     "lon":"5.9882649",
     "display_name":"Roermond, Limburg, Nederland"
   };
   document.getElementById('raw').textContent = JSON.stringify(rawData, null, 2);
   ```

   * Toont de basisinformatie van de locatie in JSON-formaat.

---

## Hoe te gebruiken

1. Open `index.html` in je browser.
2. Je ziet de kaart gecentreerd op Roermond met één marker.
3. De coördinaten worden boven de kaart weergegeven.
4. Onder de kaart zie je de raw JSON van de locatie.

> Tip: Als je problemen krijgt met het openen via `file://`, start een lokale server:
>
> ```bash
> python3 -m http.server 8000
> # Open http://localhost:8000 in je browser
> ```

---

## Dependencies

* [Leaflet](https://leafletjs.com/) voor interactieve kaarten
* OpenStreetMap-tegels als kaartbron

---

### Opmerking

Deze demo gebruikt **vast ingestelde coördinaten** en haalt geen live data meer op van Nominatim. De marker wordt altijd op dezelfde locatie geplaatst.
