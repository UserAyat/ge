<template>
  <div className="wrapper">
    <h1 class="h1">Weather App</h1>
    <p className="city__name-p">find out the weather in your {{ city == "" ? "city" :  cityName }}</p>
    <input type="text" placeholder="City" className="input" v-model="city">
    <button className="btn" v-if="city != ''" @click="getInfo()">Get Info</button>
    <button className="btn btn__dis" v-else disabled>Enter your city name </button>
    <p className="error">{{ error }}</p>
    <div class="info__block" v-if="info != null">
      <p className="weather__info-text"><img src="../src/assets/img/weather.svg" alt="" className="weather__icon"> {{ showTemp }}</p>
      <p className="weather__info-text"><img src="../src/assets/img/feels__like.png" alt="" className="weather__icon"> {{ showFeelsLike }}</p>
      <p className="weather__info-text"><img src="../src/assets/img/sun_5127060.png" alt="" className="weather__icon"> {{ showMaxTemp}}</p>
      <p className="weather__info-text"><img src="../src/assets/img/cold.png" alt="" className="weather__icon"> {{ showMinTemp }}</p>
    </div>
   
  </div>
</template>

<script>
import axios from 'axios';
export default {
  data () {
    return {
      city:'',
      error:'',
      info:null
    }
  },
  computed:{
    cityName(){
      return "<<" + this.city + ">>"
    },
    showTemp(){
      return "Temp " + this.info.main.temp + " ℃"
    },
    showFeelsLike(){
      return "Feels Like: " + this.info.main.feels_like + " ℃"
    },
    showMinTemp(){
      return "Min Temp: " + this.info.main.temp_min + " ℃"
    },
    showMaxTemp(){
      return "Max Temp: " + this.info.main.temp_max + " ℃"
    }
  },
  methods:{
    getInfo(){
      if(this.city.trim().length < 2){
        this.error = 'The city name needs more than one character!'
        return false
      }
      this.error = ''
     axios.get(`https://api.openweathermap.org/data/2.5/weather?q=${this.city}&units=metric&appid=e99a10076add3d1ac406de139e11d578`).then(res => this.info = res.data)
    }
  }
}
</script>

<style lang="scss" scoped>
.wrapper{
  width: 900px;
  min-height: 500px;
  height: 100%;
  border-radius: 50px;
  background-color: #123;
  color: white;
  padding: 20px;
  text-align: center;
  overflow: hidden;
}
.wrapper h1{
 margin-top: 25px;
}
.wrapper  p{
 margin-top: 20px;
}
.input{
  margin-top: 30px;
  background: transparent;
  border: 0px;
  border-bottom: 2px solid #110813;
  color: #fcfcfc;
  font-size: 14px;
  padding: 5px 8px;
  outline: none;
}
.input:focus{
  border-bottom-color: #6e2d;
}
.btn{
  background: #e3bc4b;
  color: white;
  padding: 10px 15px;
  margin-left: 20px;
  cursor: pointer;
  transition: transform 500ms ease;
  border: 2px solid #b99935;
  border-radius: 10px;
}
.btn:hover{
  transform: scale(1.1) translateY(-5px);
  color: #110813;
}
.btn__dis{
  cursor: not-allowed;
  background-color: #746027;
}
.error{
  color: red;
  font-size: 16px;
  text-align: center;
}
.weather__icon{
  width: 50px;
  height: 50px;
}
.info__block{
  width: 250px;
  align-self: center;
  margin: 0 auto;
}
.weather__info-text{
  display: flex;
  align-items: center;
  gap: 25px;
}
.city__name-p{
  word-break: break-all;
}

@media (max-width: 970px) {
  .wrapper{
    width: 700px;
  }
}
@media (max-width: 730px) {
  .wrapper{
    width: 500px;
  }
}
@media (max-width: 550px) {
  .wrapper{
    width: 320px;
  }
  .btn{
    margin-top: 20px;
  }
  .h1{
    font-size: 15px;
  }
  .city__name-p{
    font-size: 10px;
  }
}
@media (max-width: 320px) {
  .wrapper{
    width: 300px;
  }
}
</style>