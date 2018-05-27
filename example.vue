<template>
  <v-map :zoom=10 :center="center">
    <v-tilelayer url="http://{s}.tile.osm.org/{z}/{x}/{y}.png"></v-tilelayer>
    <v-editablecirclemarker :latLng.sync="ll" :options="{icon:icon}"></v-editablecirclemarker>
  </v-map>
</template>

<script>
  import { Vue, Component } from 'vue-property-decorator'
  import L from 'leaflet'
  import * as Vue2Leaflet from 'vue2-leaflet'
  import Vue2LeafletEditablecirclemarker from './Vue2LeafletEditablecirclemarker'
  import iconUrl from 'leaflet/dist/images/marker-icon.png'
  import shadowUrl from 'leaflet/dist/images/marker-shadow.png'

  const x = -35.15;
  const y = -58.2;
  let llvar = L.latLng(x, y)

  @Component({
    components: {
      'v-map': Vue2Leaflet.LMap,
      'v-tilelayer': Vue2Leaflet.LTileLayer,
      'v-editablecirclemarker': Vue2LeafletEditablecirclemarker
    },
  })
  export default class Map extends Vue {
    icon = L.icon(Object.assign({},
      L.Icon.Default.prototype.options,
      {iconUrl, shadowUrl},
    ))
    center = L.latLng(x, y)
    get ll() {
      return llvar
    }
    set ll(val) {
      console.log('setll', val)
      llvar = val
    }
  }
</script>

<style>
  @import "~leaflet/dist/leaflet.css";
  html, body {
    height: 100%;
    margin: 0;
  }
</style>