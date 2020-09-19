<template>
  <div class="weather-position">
    <h3>直近５日間の３時間毎天気予報</h3>
    <p>GoogleMapから地図の緯度と経度をコピー&ペーストしてください<br>
    凡例：千葉県松戸市緯度35.770874,経度139.896050</p>
    <div class="lat-lon-position">
      <label for="lat" >緯度</label>
          <input id="lat" type="text" v-model="lat">
      <label for="lon" >経度</label>
          <input id="lon" type="text" v-model="lon">
    </div>
    <p v-if="lat && lon">
      <button @click="weatherPoint()" class="weather-get-button">天気情報取得</button>
    </p>
    <p class="weather_city">{{ city }}</p>
    <div v-for="post in posts" :key="post.dt">
      <div class="weather_item">
      {{post.dt|calc}}<br>
      {{post.main.temp}}℃<br>
      {{post.weather[0].main}}<br>
        <p v-if="post.weather[0].main === 'Rain'"><i class="fas fa-umbrella fa-3x"></i></p>
        <p v-else-if="post.weather[0].main === 'Clouds'"><i class="fas fa-cloud fa-3x"></i></p>
        <p v-else-if="post.weather[0].main === 'Clear'"><i class="fas fa-sun fa-3x"></i></p>
        <p v-else>該当しなかった<i class="fas fa-cloud-sun fa-3x"></i></p>
      </div>
    </div>
  </div>
</template>

<script>
import axios from 'axios'
export default {
  data() {
    return {
      city: null, //地域名
      posts:[],//listのデータ一括取得
      baseurl : 'https://api.openweathermap.org/data/2.5/forecast?',
      lat:"",//入力値から取得
      lon:"",//入力値から取得
      units : '&units=metric&',//温度を摂氏で取得
      id : 'appid=キー',
    }
  },
  methods: {
    weatherPoint:function(){
      let url =this.baseurl + 'lat=' + this.lat + '&lon=' + this.lon + this.units + this.id;
      axios.get(url)
          .then(function (response) {
            this.city = response.data.city.name
            this.posts = response.data.list
          }.bind(this))
          .catch(function (error) {
            console.log(error)
          })
      }
    },
  filters: {
    calc(value) {
      let dateTime = new Date((value) *1000);
      return dateTime.toLocaleString("ja");
    }
  }//filters
}//export default
</script>

<style scoped>
.weather_item{
  text-align: left;
  border: 1px solid #2c3e50;
  display: inline-block;
  float:left;
  width:25%;
  height:180px;
  box-sizing: border-box;
}
p{
  margin:0;
}
.weather-position{
  background-image: url("../../src/assets/japan.png");
  border-radius: 8px;
  padding:20px 20px;
  overflow: hidden;
  -moz-border-radius: 8px;
  -webkit-border-radius: 8px;
}
.weather-get-button{
  position: relative;
  display: inline-block;
  padding:0.25em 0.5em;
  text-decoration: none;
  color:#fff;
  background: #fd9535;
  border-radius: 4px;
  -moz-border-radius: 4px;
  -webkit-border-radius: 4px;
  box-shadow: inset 0 2px 0 rgba(255,255,255,0.2),inset 0 -2px 0 rgba(0,0,0,0.05);
  -moz-box-shadow: inset 0 2px 0 rgba(255,255,255,0.2),inset 0 -2px 0 rgba(0,0,0,0.05);
  -webkit-box-shadow: inset 0 2px 0 rgba(255,255,255,0.2),inset 0 -2px 0 rgba(0,0,0,0.05);
  font-weight:bold;
  border: solid 2px #d27d00;
}
.weather-get-button:active{
  box-shadow: 0 0 2px rgba(0,0,0,0.30);
  -moz-box-shadow: 0 0 2px rgba(0,0,0,0.30);
  -webkit-box-shadow: 0 0 2px rgba(0,0,0,0.30);
}
.lat-lon-position{
  margin:30px;
}
</style>
