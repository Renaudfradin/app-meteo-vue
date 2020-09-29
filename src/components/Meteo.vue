<template>
    <div class="container">
        <h1 class="my-4">APP Meteo</h1>
        <div class="form-group mb-5">
            <label for="position">Entree une ville</label>
            <input id="position" type="text" class="form-control" v-model="requette" @keypress.enter="goMeteo">
            <!--<button @keypress.enter="goMeteo">aaa</button>-->
        </div>
        <div class="w-75 m-auto" v-if="temps">
            <h3 class="text-center mb-3">Position : {{ temps.name }}</h3>
            <div class="card text-center p-5">
                <p class="texte-affichage">Temperature : {{ temps.main.temp.toFixed()}} °C</p>
                <p class="texte-affichage">Humidité : {{ temps.main.humidity }} %</p>
                <p class="texte-affichage">Pression : {{ temps.main.pressure }}</p>
                <p class="texte-affichage">Temperature max  : {{ temps.main.temp_max }} °C</p>
                <p class="texte-affichage">Temperature min : {{ temps.main.temp_min }} °C</p>
                <p class="texte-affichage">Latitute : {{ temps.coord.lat }}</p>
                <p class="texte-affichage">Longitude : {{ temps.coord.lon }}</p>
                <p class="texte-affichage">Temps : {{temps.weather[0].description}}</p>
            </div>
        </div>
    </div>
</template>
<script>
import Axios from 'axios'
export default {
    name:'Meteo',
    data(){
        return{
            requette:'',
            temps : undefined,
            key_api:'4905eac944022ae6bb02d2b49f21a9c7',
            url_recherche:'https://api.openweathermap.org/data/2.5/weather?',

        }
    },
    methods:{
        goMeteo(){
            Axios.get(`${this.url_recherche}q=${this.requette}&units=metric&lang=fr&appid=${this.key_api}`)
            .then(reponse =>{
                console.log(reponse);
                this.temps = reponse.data;
                console.log(this.temps);
            })
            this.requette = ''
        }
    }
}
</script>
<style scoped>
.texte-affichage{
    font-size: 30px;
    font-weight: 300;
    line-height: 1.2;
}
</style>