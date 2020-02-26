<template>
  <div id="app" class="container">
    <div class="page-header">
      <h1>Smarthome</h1>
    </div>
    <div class="panel panel-default">
      <div class="panel-header">
        <h3>Device List</h3>
      </div>
      <ul class="device-list">
        <ul v-for="device in devices" :key="device['.key']">
          <h2>{{ device.name }}</h2>
          <li>LED Status</li>
          <li v-bind:class="device.led_status">
          <li>
            <button v-on:click="updateSetting(device)">Switch Off</button>
          </li>
        </ul>
      </ul>
    </div>
  </div>
</template>

<script>
import HelloWorld from './components/HelloWorld'
import Firebase from 'firebase'

let config = {
  apiKey: "AIzaSyDrcxqjj24d8KiTyyjv-sRf2OpUM8H7_GU",
  authDomain: "smarthome-bc05a.firebaseapp.com",
  databaseURL: "https://smarthome-bc05a.firebaseio.com",
  projectId: "smarthome-bc05a",
  storageBucket: "smarthome-bc05a.appspot.com",
  messagingSenderId: "725898910711"
}

let app = Firebase.initializeApp(config);
let db = app.database();

let devicesRef = db.ref('devices')

export default {
  name: 'App',
  data () {
    return {
      devices: [],
    }
  },
  methods: {
    updateSetting: function(device) {
      const childKey = device['.key'];

      if(device.led_status == "FALSE") {
        let new_led_status = "TRUE";
        devicesRef.child(childKey).child("led_status").set(new_led_status);
      }
      else if(device.led_status == "TRUE") {
        let new_led_status = "FALSE";
        devicesRef.child(childKey).child("led_status").set(new_led_status);
      }
    },
  },
  firebase: {
    devices: devicesRef
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

th,
tr td {
  text-align: center;
}

h2 {
  text-align: left;
  border-bottom: 2px solid #000;
}


.device-list,
.device-list ul {
  list-style: none;
  padding: 0;
  margin: 0;
}


.device-list {
  padding: 60px 30px;
  width: 100%;
}

.device-list ul {
  display: inline-flex;
  width: 100%;
}

.FALSE {
  background-color: red;
}

.TRUE {
  background-color: green;
}

</style>
