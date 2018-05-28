<template>
  <div style="display: none;">
    <slot v-if="ready"></slot>
  </div>
</template>

<script>
import L from 'leaflet'
import 'leaflet-editablecirclemarker'

import { findRealParent, propsBinder } from 'vue2-leaflet'

const props = {
  rad: {
    type: Number,
    custom: true,
  },
  latLng: {
    type: [Object, Array],
    custom: true,
  },
  visible: {
    type: Boolean,
    custom: true,
    default: true
  },
  options: {
    type: Object,
    default: () => ({}),
  },
};

export default {
  name: 'LEditablecirclemarker',
  props,
  data() {
    return {
      ready: false,
    }
  },
  mounted() {
    this.mapObject = L.editableCircleMarker(this.latLng, this.rad, this.options);
    this.mapObject.on('moveend', (e) => {
      this.$emit('update:latLng', e.target._latlng)
    })
    L.DomEvent.on(this.mapObject, this.$listeners);
    propsBinder(this, this.mapObject, props);
    this.ready = true;
    this.parentContainer = findRealParent(this.$parent);
    this.parentContainer.addLayer(this, !this.visible);
  },
  beforeDestroy() {
    this.parentContainer.removeLayer(this);
  },
  methods: {
    setVisible(newVal, oldVal) {
      if (newVal == oldVal) return;
      if (newVal) {
        this.parentContainer.addLayer(this);
      } else {
        this.parentContainer.removeLayer(this);
      }
    },
    setLatLng(value) {
      this.mapObject.setLatLng(value);
    },
    setRad(value) {
      this.mapObject.setRadius(value);
    }
  }
};
</script>
