<template>
  <div id="app" class="container">
    <div class="page-header">
      <h1>Vue.js 2 &amp; Firebase Sample Application</h1>
    </div>
    <div class="panel panel-default">
      <div class="panel-header">
        <h3>Books Lists</h3>
      </div>
      <div class="panel-body">
        <table class="table table-striped">
          <thead>
            <tr>
              <th>
                Title
              </th>
              <th>
                Author
              </th>
            </tr>
          </thead>
          <tbody>
            <tr v-for="book in books">
              <td>
                <a v-bind:href="book.url">{{book.title}}</a>
              </td>
              <td>
                {{book.author}}
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

let booksRef = db.ref('books')

export default {
  name: 'App',
  data () {
    return {
      books: [],
    }
  },
  firebase: {
    books: booksRef
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
