<template>
  <div id="app" class="container">
    <div class="jumbotron">
        <h4 class="display-4">
            My Location
        </h4>
        <p class="lead">Enter your latitude and longitude to display your location on a Google Map</p>
        <hr>
        <form @submit.prevent="handleSubmit">
            <div class="form-row">
                <div class="col">
                    <input v-model="geoLat" type="text" name="lat" id="lat" placeholder="Latitude" class="form-control">
                </div>
                <div class="col">
                    <input v-model="geoLong" type="text" name="lon" id="lon" placeholder="Longitude" class="form-control">
                </div>
                <div class="col">
                  <button type="button" @click="getUsersGeo()"><img class="icon-button" src="https://cdn2.iconfinder.com/data/icons/freecns-cumulus/32/519777-89_Compass-512.png"></button>
                </div>
            </div>
            <div class="form-row">
                <div class="col">
                    <button type="submit" class="btn btn-primary mt-4">Show My Location</button>
                </div>
            </div>
        </form>
    </div>
    <my-map name="map" v-if="!isHidden" :lat="latitude" :lon="longitude" msg="oh no"></my-map>
  </div>
</template>

<script>
import MyMap from './components/my-map.vue'

export default {
  
  data: function () {
    return {
      isHidden: true,
      lati:String,
      long:String,
      geoLat:"",
      geoLong:""
    }
  },
  name: 'app',
  components: {
    MyMap
  },
  computed: {
    latitude: function () {
      return this.lati
    },
    longitude: function () {
      return this.long
    }
  },
  methods: {
    handleSubmit(submitEvent) {
      this.isHidden = false
      this.lati = submitEvent.target.elements.lat.value
      this.long = submitEvent.target.elements.lon.value
    },
    getUsersGeo() {		
      if(navigator.geolocation){
        navigator.geolocation.getCurrentPosition(this.autoEnterCoords);
      }else{
        this.error = "Geolocation is not supported."; 
      }
    },
    autoEnterCoords(position) {	
      this.geoLat= position.coords.latitude;
      this.geoLong = position.coords.longitude;
    }
  }
}
</script>

<style>
#app {
  font-family: 'Avenir', Helvetica, Arial, sans-serif;
  -webkit-font-smoothing: antialiased;
  -moz-osx-font-smoothing: grayscale;
  text-align: center;
  color: #2c3e50;
  margin-top: 60px;
}
.icon-button{
  height: 35px;
  width: 35px;
}
</style>
