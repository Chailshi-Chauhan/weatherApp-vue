<template>
<div id="weather-app">
  <main>
    <div class="search-box">
      <input type="text" v-model="searchText" class="search-bar" placeholder="Search here.." @keypress="Weatherfetch($event)"/>
    </div>
    <div class="second-box" v-if="typeof weather.main != 'undefined'">
      <div class="location">{{ weather.name }}</div>
    </div>
    <div class="weather-temp">
      <div class="temp">{{ Math.round(weather.main.temp) }}°c</div>
      <div class="weather">{{ weather.weather[0].main }}</div>
    </div>
  </main>
</div>
</template>
<script >
export default {
  data () {
    return {
      api: '653ad8aa09eae6b9017765031c3873f2',
      url: 'https://api.openweathermap.org/data/2.5/',
      searchText: '',
      weather: {}
    }
  },
  methods: {
    Weatherfetch (e) {
       if (e.key == "Enter") {
        let res =  fetch(`${this.url}weather?q=${this.searchText}&units=metric&APPID=${this.api}`);
        this.weatherResults(res.data);
       }
    },
    weatherResults (weatherResult) {
      this.weather = weatherResult;
    }
  }
}
</script>
<style scoped>
* {
  margin: 0;
  padding: 0;
  box-sizing: border-box;
  font-family: 'Segoe UI', Tahoma, Geneva, Verdana, sans-serif;
}

#weather-app {
  background-image: url('https://encrypted-tbn0.gstatic.com/images?q=tbn:ANd9GcTQh-ADNW7J3GKKTp3X3W97dQEG1VrbJ8dcrQ&usqp=CAU');
  background-size: cover;
  background-position: bottom;
  transition: 0.4s;
}

main {
  min-height: 100%;
  padding: 25px;
  background-image: linear-gradient(to bottom, rgba(0, 0, 0, 0.25), rgba(0, 0, 0, 0.75));
}

.search-box .search-bar {
  width: 100%;
  padding: 15px;
  font-size: 20px;
  appearance: none;
  border:none;
  outline: none;
  background: none;
  background-color: rgba(255, 255, 255, 0.5);
  border-radius: 0px 16px 0px 16px;
}
.search-box .search-bar:focus {
  background-color: rgba(255, 255, 255, 0.75);
  border-radius: 16px 0px 16px 0px;
}
.location {
  color: #FFF;
  font-size: 32px;
  font-weight: 500;
  text-align: center;
}
.weather-temp {
  text-align: center;
}
.weather-temp .temp {
  display: inline-block;
  padding: 10px 25px;
  color: #FFF;
  font-size: 102px;
  font-weight: 900;
  background-color:rgba(255, 255, 255, 0.25);
  border-radius: 16px;
  margin: 30px 0px;
}
.weather-temp .weather {
  color: #FFF;
  font-size: 48px;
  font-weight: 700;
  font-style: italic;
}
</style>
