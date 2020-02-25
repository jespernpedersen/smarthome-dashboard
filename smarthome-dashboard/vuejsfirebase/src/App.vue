<template>
  <div id="app" class="container">
    <div class="page-header">
      <h1>Smarthome</h1>
    </div>
    <div class="panel panel-default">
      <div class="panel-header">
        <h3>Device Lists</h3>
      </div>
      <div class="panel-body">
        <table class="table table-striped">
          <thead>
            <tr>
              <th>
                Setting
              </th>
              <th>
                Status
              </th>
            </tr>
          </thead>
          <tbody>
            <tr v-for="device in devices">
              <td style="text-align: left">
                LED Status
              </td>
              <td style="text-align: left">
                {{device.led_status}}
              </td>
            </tr>
          </tbody>
        </table>
      </div>
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
</style>
