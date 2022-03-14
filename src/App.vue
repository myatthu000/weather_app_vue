<template>
    <div id="app" :class="typeof weather.main != 'undefined' && weather.main.temp > 16 ? 'warm':'' ">
      <main>
        <div class="search-box">
          <div class="search-bar">
            <input 
            class="search-bar"
            placeholder="Search ......"
            v-model="query"
            @keypress="fetchWeather"
            type="text">
          </div>
        </div>

        <div class="weather-wrap" v-if="typeof weather.main != 'undefined' ">

          <div class="location-box">
            <div class="location">{{ weather.name }},{{ weather.sys.country }}</div>
            <div
            style=""
            class="date"> {{dateBuilder() }} </div>
            
          </div>

          <div class="weather-box">
            <div class="temp">{{ Math.round(weather.main.temp) }}°C</div>
            <div class="weather"> {{weather.weather[0].main}} </div>
          </div>


        </div>


    </main>
  </div>
</template>

<script>
  export default {
    name:"App",
    data(){
      return {
        api_key: 'a6b71b088df567ec88d2514bc9c4e563',
        url_base: 'https://api.openweathermap.org/data/2.5/',
        query: '',
        weather:{},
      }
    },

    methods:{
      fetchWeather(e){
        if(e.key == 'Enter'){
            fetch(`${this.url_base}weather?q=${this.query}&units=metric&APPID=${this.api_key}`)
              .then(response => response.json())
              .then(this.setResults);
        }
      },
      setResults(results){
        this.weather = results;
      },
      dateBuilder(){
        let d = new Date();
        let months = [
          'January',
          'February',
          'March',
          'April',
          'May',
          'June',
          'July',
          'August',
          'September',
          'October',
          'November',
          'December',
        ];
        let days=[
          'Sunday',
          'Monday',
          'Tuesday',
          'Wednesday',
          'Thursday',
          'Friday',
          'Saturday'
        ];
        let day = days[d.getDay()];
        let date = d.getDate();
        let month = months[d.getMonth()];
        let year = d.getFullYear();


        return `${day} ${date} ${month} ${year}`;

      }
    }
    
  }
</script>

<style>

*{
  margin: 0;
  padding:0;
  box-sizing: border-box;
}

body{
  /* dsdsd */
}
main{
  min-height: 100vh;
  padding: 25px;
}
#app{
  background-image: url('./assets/weather1.jpg');
  background-size: cover;
  background-position: bottom;
  transition: 0.4s;
}
#app.warm{
  background-image: url('./assets/weather2.jpg');
}
.search-box{
  width: 100%;
  margin-bottom: 30px;

}
.search-box .search-bar{
  display: block;
  width: 100%;
  padding: 15px;

  color: slateblue;
  font-size: 20px;

  appearance: none;
  border: none;
  outline: none;
  background:none;

  background-color: rgba(255, 255, 255, 0.5);
  border-radius: 0px 16px 0px 16px;
  transition:0.5s;
}

.search-box .search-bar:focus{
  
  background-color: rgba(255, 255, 255, 0.75);
  box-shadow: 0px 0px 16px rgba(0, 0, 0, 0.5);
  border-radius: 16px 0 16px 0;

}


.location-box .location{
  color:#ffffff;
  font-size: 32px;
  font-weight: 500;
  text-align: center;
  font-style: italic;

}

.location-box,.weather-box{
  text-align: center;

}
.weather-wrap{
  background: rgba(0,0,0,0.05);
    border-radius: 16px;
    padding-top: 10px;
    padding-bottom: 10px;

}

.weather{
  text-align: center;
}
.weather-box .temp{
  display: inline-block;
  padding: 10px 25px;

  color: #ffffff;
  font-size: 102px;
  font-weight: 900;

  background-color: 3px 6px rgba(255, 255, 255, 0.25);
  box-shadow: rgba(0, 0, 0, 0.25);
  border-radius: 16px;
  margin: 30px 0px;

  box-shadow: rgba(0, 0, 0, 0.25);
  background: rgba(0,0,0,0.25);

}
.weather-box .weather{
  color: #ffffff;
  font-size: 48px;
  font-weight: 700;
  font-style: italic;
  text-shadow: 3px 6px rgba(0, 0, 0, 0.25);
}
.date{
  margin-top:20px;font-weight:700;font-size:30px;color: #ffffff;
}

</style>