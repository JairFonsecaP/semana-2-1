<template>
    <div id="clima">
        <div id="weatherContainer">
            <div id='weatherContainer__temperatura'> 
                <button @click="darClima()">Muestrame el clima en mi ciudad</button>
            </div>
            <div></div>
            <div></div>
            <div></div>

        </div>
    </div>
</template>

<script>
export default {
  name: 'clima',
  props: {
    msg: String
  },
  data(){
      return{
        resultJson : []
      }
  },
  methods : {
    
    darClima(){
        var output = document.getElementById("clima");
        if (!navigator.geolocation) {
        output.innerHTML = "<p>Tu navegador no puede obtener geolocalizacion</p>";
        } 
        function localizacion(posicion) {
        const latitud = posicion.coords.latitude;
        const longitud = posicion.coords.longitude;
        
        apiWeather(latitud,longitud);
        }
        function error() {
        output.innerHTML = "<p>No se pudo obtener tu ubicacion, intenta de nuevo.</p>";
        }
        async function  apiWeather(latitud,longitud){
        const result =  await fetch ( `http://api.openweathermap.org/data/2.5/weather?lat=${latitud}&lon=${longitud}&appid=281fb38f9bd1f45f7be4dbb64129b3a2&units=metric`,{
        method :'GET',
        })
        let resultJson = await result.json()
        if (result.ok){
        printOnScreen(resultJson);
        }
        }
        function printOnScreen(dataText){
            const weatherContainer = document.getElementById('weatherContainer__temperatura')
            const {name,main,weather,wind,sys} = dataText
            console.log(weather)

            let ciudad ='Usted está en  '+name +', '+sys.country+'.';
            const city = document.createElement('h2');
            city.textContent = ciudad;

            let temperatura ='La temperatura es: '+ main.temp + ' °C';
            const temp = document.createElement('h3')
            temp.textContent = temperatura;
            
            let viento ='La velocidad del viento es '+ wind.speed + ' km/h';
            const velocidad = document.createElement('h3')
            velocidad.textContent = viento;

            

            weatherContainer.appendChild(city);
            weatherContainer.appendChild(temp); 
            weatherContainer.appendChild(velocidad);    
        }
        navigator.geolocation.getCurrentPosition(localizacion, error);
    },
    
  },
}
</script>

<!-- Add "scoped" attribute to limit CSS to this component only -->
<style>
</style>