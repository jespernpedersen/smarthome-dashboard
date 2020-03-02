<template>
  <div id="app" class="container">
    <div class="page-header">
      <h1>Smarthome</h1>
    </div>
    <div class="panel panel-default">
      <div class="panel-header">
        <h3>Device List</h3>
      </div>
      <section v-for="device in devices" :key="device['.key']" class="device-list">
          <h2>{{ device.name }}</h2>
          <ul class="device-header">
            <li>Setting Name</li>
            <li>Status/Value</li>
            <li>Actions</li>
          </ul>
          <ul v-if="device.led_status" class="led-status">
            <li class="setting-name">LED Status</li>
            <li v-bind:class="device.led_status"></li>
            <li>
              <button v-on:click="updateSetting(device, 'led_status', 'boolean', device.led_status)">Toggle</button>
            </li>
          </ul><!-- end led_status -->
          <ul v-if="device.interactive" class="interactive">
            <li class="setting-name">Interactivity</li>
            <li v-bind:class="device.interactive">
            <li>
              <button v-on:click="updateSetting(device, 'interactive', 'boolean', device.interactive)">Toggle</button>
            </li>
          </ul>
      </section>
      </ul>
    </div>
  </div>
</template>

<script>
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

let devicesRef = db.ref('devices');

export default {
  name: 'App',
  data () {
    return {
      devices: [],
    }
  },
  methods: {
    updateSetting: function(device, setting_name, setting_type, setting_value) {
      // Set Key
      const childKey = device['.key'];

      // If Setting is a Boolean we will perform a toggle
      if(setting_type == "boolean") {
        if(setting_value == "FALSE") {
          devicesRef.child(childKey).child(setting_name).set("TRUE");
        }
        else if(setting_value == "TRUE") {
          devicesRef.child(childKey).child(setting_name).set("FALSE");
        }
      }
      else {
        console.log("Error in setting type");
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
  padding-bottom: 5px;
  margin-bottom: 0;
  padding-left: 15px;
  padding-right: 15px;
}

h2:first-letter {
  text-transform: uppercase;
}


.device-list,
.device-list ul {
  list-style: none;
  padding: 0;
  margin: 0;
  padding-bottom: 10px;
}

.device-list ul + ul {
  border-top: 3px solid #ccc;
  padding-top: 15px;
}

.setting-name {
  font-weight: bold;
}

.device-list {
  padding: 0px 30px 60px 30px;
  width: 100%;
}

.device-list ul {
  display: grid;
  grid-template-columns: 1fr 1fr 1fr;
  padding-left: 15px;
  padding-right: 15px;
}

.device-list ul li {
    text-align: left;
    display: inline-flex;
    align-items: center;
}

.device-list ul li:last-of-type {
  text-align: right;
  justify-content: flex-end;
}

html body .device-header {
  text-align: center;
  background-color: #ededed;
  padding-top: 12px;
  padding-bottom: 12px;
}

.device-header li {
  font-weight: bold;
}


.FALSE,
.TRUE {
  min-width: 350px;
  height: 30px;
}

.FALSE {
  background-color: red;
}

.TRUE {
  background-color: green;
}

</style>
