<template>
  <div>
    <h1>{{lat}},{{lon}}</h1>
    <img :src="`http://maps.googleapis.com/maps/api/staticmap?center=${lat},${lon}&markers=${lat},${lon}&zoom=14&size=400x400&key=AIzaSyC0MAKJQQaF2SY2iaZjSQULtuCCN3QzLiM`">
  </div>
</template>

<script>
export default {
  name: 'my-map',
  props: {
    lat: String,
    lon: String
  }
}
</script>

<!-- Add "scoped" attribute to limit CSS to this component only -->
<style scoped>
h3 {
  margin: 40px 0 0;
}
ul {
  list-style-type: none;
  padding: 0;
}
li {
  display: inline-block;
  margin: 0 10px;
}
a {
  color: #42b983;
}
</style>