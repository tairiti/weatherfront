<template>
  <h1>Ilm</h1>


  <div class="container text-center">
    <div class="row">
      <div class="col">
        Sisesta linna nimi:
      </div>

      <div class="col">
        <input v-model="cityName">
      </div>
      <br>
      <div class="col">
        <button @click="getWeatherInfo">Küsi ilma andmeid</button>
      </div>
      <br>
      <div class="col">
       Temperatuur: {{weatherResponse.temperature}} °C
      </div>
      <div class="col">
       Tuulekiirus: {{weatherResponse.windSpeed}} m/s
      </div>
      <div class="col">
       Õhuniiskus {{weatherResponse.humidity}} %
      </div>
      <br>

      <div class="col">
       Kustuta linn ja andmed {{cityName }}
        <br>

        <button @click="deleteCityAndWeatherInfo">Kustuta</button>
      </div>


    </div>
  </div>


</template>

<script>

export default {
  name: 'HomeView',
  data() {
    return {
      cityName: '',
      weatherResponse: {
        temperature: 0,
        windSpeed: 0,
        humidity: 0
      }
    }
  },
  methods: {

    getWeatherInfo() {
      this.$http.get("/weather", {
            params: {
              cityName: this.cityName
            }
          }
      ).then(response => {
        this.weatherResponse = response.data
      }).catch(error => {
        const errorResponseBody = error.response.data
      })
    },
    deleteCityAndWeatherInfo() {
      this.$http.delete("/weather", {
            params: {
              cityName: this.cityName
            }
          }
      ).then(response => {
       alert("Linn ja ilmaandmed andmebaasist kustutatud")
        this.resetAllFields();
      }).catch(error => {
        const errorResponseBody = error.response.data
      })
    },
    resetAllFields() {
      this.cityName = ''
      this.weatherResponse.temperature = 0
      this.weatherResponse.windSpeed = 0
      this.weatherResponse.humidity = 0
    },
  }
}
</script>
