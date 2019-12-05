<template>
  <div class="container">
    <div class="jumbotron jumbotron-fluid">
      <div class="container">
        <h1 class="display-4 text-right bottom">HOROSCOPE</h1>
      </div>
    </div>
    <div class="row">
      <div class="col-xs-12 col-sm-6">
        <h4>Silahkan masukan nama dan tanggal lahir anda</h4>
        <br />
        <form>
          <div class="form-group text-left">
            <label>Nama</label>
            <input
              v-model="name"
              type="name"
              id="name"
              class="form-control"
              placeholder="Masukan Nama"
              required
              autofocus
            />
          </div>
          <div class="form-group text-left">
            <label>Tanggal Lahir</label>
            <br />
            <date-pick v-model="birthday" :format="'DD-MM-YYYY'"></date-pick>
          </div>
          <button
            v-on:click="prosesData()"
            type="submit"
            class="btn btn-primary"
          >
            Proses
          </button>
        </form>
      </div>
      <div class="col-xs-12 col-sm-6">
        <div class="card">
          <div class="card-body">
            <h5 class="card-title">{{jsonData.nama}}</h5>
            <p class="card-text">
              {{jsonData.lahir}}
            </p>
          </div>
          <ul class="list-group list-group-flush">
            <li class="list-group-item">Usia : {{jsonData.usia}}</li>
            <li class="list-group-item">Ultah : {{jsonData.ultah}}</li>
            <li class="list-group-item">Zodiak : {{jsonData.zodiak}}</li>
          </ul>
        </div>
      </div>
    </div>
  </div>
</template>

<script>
import DatePick from 'vue-date-pick'
import 'vue-date-pick/dist/vueDatePick.css'
import axios from 'axios'

export default {
  components: { DatePick },
  data() {
    return {
      name: '',
      birthday: '',
      response: '',
      jsonData:'',
    }
  },
  methods: {
    prosesData() {
      axios
        .get(
          'https://script.google.com/macros/exec?service=AKfycbw7gKzP-WYV2F5mc9RaR7yE3Ve1yN91Tjs91hp_jHSE02dSv9w&nama=' +
            this.name +
            '&tanggal=' +
            this.birthday
        )
        .then(response => (this.response = response))
        this.jsonData = this.response.data.data
    }
  }
}
</script>

<style>
.jumbotron {
  background-image: url('../assets/banner2.jpg');
}
h1 {
  font-size: 250px;
  color: red;
  font-family: 'Franklin Gothic Medium', 'Arial Narrow', Arial, sans-serif;
}
</style>
