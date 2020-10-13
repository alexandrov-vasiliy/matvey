<template>
    <div class="form-wether">

        <input @keypress="getWeather" type="text" v-model="cityName" class="control-form w-100">

        <h1 class="text-center">{{this.cityName}}</h1>
        <div class="btn btn-primary" v-on:click="getWeather">ПОГОДА</div>
        <p>{{this.main.temp}}</p>
        <p>{{this.getCel(this.main.temp)}}</p>
    </div>
</template>

<script>

export default {
    name: "wether-component",

    data(){
        return{
            cityName: 'london',
            apiKey: 'a26a983a15e39d7203163ab71ce56c57',
            dataJson: {

            },
            main:{

            }
        }
    },
    methods: {

        getWeather(event){
            if(event.keyCode === 13){
                $.ajax({
                    url:`http://api.openweathermap.org/data/2.5/weather?q=${this.cityName}&appid=${this.apiKey}&lang=ru`,
                    method:"GET",

                    success: res => {
                        this.dataJson = res;
                        this.main = this.dataJson.main
                        console.log(this.main);
                    },
                    error: err => console.log(err),
                });
            }
            $.ajax({
                url:`http://api.openweathermap.org/data/2.5/weather?q=${this.cityName}&appid=${this.apiKey}&lang=ru`,
                method:"GET",

                success: res => {
                    this.dataJson = res;
                    this.main = this.dataJson.main
                    console.log(this.main);
                },
                error: err => console.log(err),
            });
        },

        getCel(f){
            if (f){
            let cel = f - 273.15;

            return cel.toFixed(1);
            }
            return null;

        },

    }
}
</script>

<style scoped>

</style>
