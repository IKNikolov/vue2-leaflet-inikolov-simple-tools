# Leaflet simple tools for vue2

Simple vue2 package to be possible using of few packages in vue projects.

## PACKAGES (the big applause is for the creators of this packages)

[Leaflet.fullscreen](https://github.com/Leaflet/Leaflet.fullscreen)

[Map Print Plugin for Leaflet.js](https://github.com/Igor-Vladyka/leaflet.browser.print)

[Leaflet.PolylineMeasure](https://github.com/ppete2/Leaflet.PolylineMeasure)

[leaflet-measure](https://github.com/ljagis/leaflet-measure)

[Leaflet-History Control](https://github.com/cscott530/leaflet-history)

[Leaflet.GeoSearch](https://github.com/smeijer/leaflet-geosearch)

[leaflet.wms.js](https://www.npmjs.com/package/leaflet.wms) -> only overlay

[leaflet.ScaleFactor](https://github.com/MarcChasse/leaflet.ScaleFactor) 


## Usage

You can read the documentation of the packages above and use their options like in the example below.

### IMPORTANT FOR [Map Print Plugin for Leaflet.js](https://github.com/Igor-Vladyka/leaflet.browser.print)

I replaced the original print modes option from the documentation of the print plugin. Please see the printModes in the example below.

I added additional options to be possible to have [L.control.scale()](https://leafletjs.com/reference-1.7.1.html#control-scale) in the printed map. You can see the example below in printOptions.

### IMPORTANT FOR Leaflet.GeoSearch

I used only OpenStreetMapProvider for now. If someone wants to use this package and other Leaflet.GeoSearch provider just writes an issue.

```html
<template>
  <div style="height: 100%; width: 100%">
    <l-map
      style="height: 600px"
      :center="mapCentre"
      :zoom="mapZoom"
      ref="map"
    >
      <l-tile-layer
        :url="tileUrl"
        :attribution="tileAttribution"
      />
      <l-control-layers position="topright"  ></l-control-layers>
      <l-control-scale position="bottomleft" :imperial="false" :metric="true"></l-control-scale>
      <l-control-scale-factor :options="svaleFactorOptions" />
      
      <l-control-area-measure :options="areaMesureOptions" />
      <l-control-poly-line-measure :options="polylineOptions" />
      <l-control-fullscreen position="topleft" :options="fullscreenOptions" />
      <l-control-print :options="printOptions"  />
      <l-control-history :options="historyOptions"  />
      <l-control-geo-search :options="geoSearchOptions" :providerOptions="providerOptions"  />

      <l-layer-group
        layer-type="overlay"
        name="WMS Overlay"
      >
        <l-wms-overlay :url="WMSURL" :options="WMSOptions" />
      </l-layer-group>
    </l-map>
  </div>
</template>

<script>

import L from 'leaflet';
import {
  LMap,
  LTileLayer,
  LControlScale,
  LLayerGroup,
  LControlLayers
} from 'vue2-leaflet';
import { 
  LControlPrint, 
  LControlFullscreen, 
  LControlPolyLineMeasure, 
  LControlAreaMeasure, 
  LControlHistory,
  LWmsOverlay,
  LControlScaleFactor
} from 'vue2-leaflet-inikolov-simple-tools';
export default {
  components: {
    LMap,
    LTileLayer,
    LControlPrint,
    LControlFullscreen,
    LControlPolyLineMeasure,
    LControlAreaMeasure,
    LControlHistory,
    LControlGeoSearch,
    LControlScale,
    LWmsOverlay,
    LLayerGroup,
    LControlLayers,
    LControlScaleFactor
  },
  data() {
    return {
      mapCentre: [51, -114],
      mapZoom: 10,
      tileUrl: 'https://{s}.tile.openstreetmap.org/{z}/{x}/{y}.png',
      tileAttribution: '&copy; <a href="//osm.org/copyright">OpenStreetMap</a> contributors',


      fullscreenOptions: {
        title: {
          'false': 'Switch to full-screen view',
          'true': 'Exit full-screen mode',
        },
      },


      printOptions: {
        title: 'Just print me!',
        documentTitle: 'Map printed using leaflet.browser.print plugin',
        closePopupsOnPrint: false,
        printModes: [
          {"type": 'all', "name": 'All'},
          {"type": 'landscape', "name": 'Landscape'},
          {'type': 'portrait', 'name': 'Portrait'},
          {'type': 'custom', 'name': 'Select'}
        ],
        manualMode: false,
        showScale: true,
        scaleOptions: {
          metric: true,
          imperial: false,
          position: "bottomleft"
        }
      },


      polylineOptions: {
        position: 'topleft',
        showClearControl: true,
        showUnitControl: true
      },


      areaMesureOptions: {
        position: 'topleft'
      },


      historyOptions: {
        backText: 'Back',
        forwardText: 'Forward',
      },


      geoSearchOptions: {
        position: 'topright',
        style: 'bar',
      },

      
      providerOptions: {
        language: 'bg',
        region: 'bg',
      },

      WMSURL: 'https://mesonet.agron.iastate.edu/cgi-bin/wms/us/mrms.cgi?',
      WMSOptions: {
        layers: 'mrms_p72h',
        format: 'image/png',
        transparent: true,
        tiled: false,
        maxZoom: 12,
        pane: 'points'
      },
      
      svaleFactorOptions: {
        position: 'bottomright'
      }

    };
  },
  methods: {

  }
};
</script>

<style>
@import '~leaflet/dist/leaflet.css';
</style>

```