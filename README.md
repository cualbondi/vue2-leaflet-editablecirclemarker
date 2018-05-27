# vue2-leaflet-editablecirclemarker

This is a [editable circle marker plugin](https://github.com/cualbondi/leaflet-editablecirclemarker) extension for [vue2-leaflet package](https://github.com/KoRiGaN/Vue2Leaflet)

## Install

    npm install --save vue2-leaflet-editablecirclemarker

## Demo

    git clone git@github.com:cualbondi/vue2-leaflet-editablecirclemarker.git
    cd vue2-leaflet-editablecirclemarker
    yarn
    yarn example

    # or alternatively using npm
    npm install
    npm run example

Then you should be able to navigate with your browser and see the demo in http://localhost:4000/

You can see the demo code in the file [example.vue](example.vue)

## Usage

### on &lt;template&gt; add

something like this

    <v-map :zoom=10 :center="initialLocation">
      <v-editablecirclemarker :paths="[latlngsarray, otherlatlngsarray]" :options="options"></v-editablecirclemarker>
    </v-map>

### on &lt;script&gt; add

#### option 1

In the same template file, at `<script>` part, this will make the component available only to the template in this file

    import Vue2LeafletEditablecirclemarker from 'vue2-leaflet-editablecirclemarker'
    ...
    export default {
      ...
      components: {
        'v-editablecirclemarker': Vue2LeafletEditablecirclemarker
        ...
      },
      ...
    }

#### option 2

At main Vue configuration, this will make the component available to all templates in your app

    import Vue from 'vue'
    import Vue2LeafletEditablecirclemarker from 'vue2-leaflet-editablecirclemarker'
    ...
    Vue.component('v-editablecirclemarker', Vue2LeafletEditablecirclemarker)

## Access editablecirclemarker layer directly

If you need to access other editableCircleMarker methods, you can do it with a ref on the editablecirclemarker vue element and using the `mapObject` property

    ...
    <v-editablecirclemarker ref="circlemarkerRef"></v-editablecirclemarker>
    ...

    ...
    this.$refs.circlemarkerRef.mapObject.setPaths()
    ...


## Develop and build

    npm install
    npm run build

## Author

[Julián Perelli](https://jperelli.com.ar/)

## License

MIT
