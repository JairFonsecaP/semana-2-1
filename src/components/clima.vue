<template>
    
        <div id='clima'>
            <div id='clima_temperatura'> 
                <button @click="darClima()"><b>Muestrame el clima en mi ciudad</b></button>
            </div>
            <div id='clima_sol'></div>
            <div id='clima_nuvosidad'></div>
            <div id='clima_presion'></div>

        </div>
   
</template>

<script>
export default {
  name: 'clima',
  props: {
    msg: String
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
        function printOnScreen(info){
            const clima_temperatura = document.getElementById('clima_temperatura');
            const clima_sol = document.getElementById('clima_sol');
            //const nuvosidad = document.getElementById('clima_nuvosidad');
            //const presion = document.getElementById('clima_presion');           

            function cambiarHora(unix)
            {
              let fecha = new Date(unix*1000);
              let horas = fecha.getUTCHours().toString().padStart(2,0);
              let minutos = fecha.getUTCMinutes().toString().padStart(2,0);
              let segundos = fecha.getUTCSeconds().toString().padStart(2,0);              
              return horas +':'+minutos+':' + segundos;
              
            }

            //const atardecerHora = cambiarHora(sys.sunset);

            const {name,main,weather,wind,sys, timezone} = info;
            console.log(weather);
          
            const city = document.createElement('h4');
            city.textContent = 'Usted está en  '+name +', '+sys.country+'.';
            
            const temp = document.createElement('p');
            temp.textContent = 'La temperatura es: '+ main.temp + ' °C';  
            
            const maximaT = document.createElement('p');
            maximaT.textContent = 'Maxima '+ main.temp_max + ' °C';
          
            const minimaT = document.createElement('p');
            minimaT.textContent = 'Mínima: '+ main.temp_min + ' °C';
          
            const realFeel = document.createElement('p');
            realFeel.textContent = 'Se siente como:  '+ main.feels_like + ' °C';
            
            const amanecer =  document.createElement('p');
            amanecer.textContent = 'Hoy amaneció a las ' + cambiarHora(sys.sunrise + timezone ) + '.';

            const atardecer =  document.createElement('p');
            atardecer.textContent = 'Hoy atardecerá a las ' + cambiarHora(sys.sunset + timezone) + '.';
            
            const velocidad = document.createElement('p');
            velocidad.textContent = 'La velocidad del viento es '+ wind.speed + ' km/h';


            clima_temperatura.appendChild(city);
            clima_temperatura.appendChild(temp); 
            clima_temperatura.appendChild(realFeel);
            clima_temperatura.appendChild(maximaT);
            clima_temperatura.appendChild(minimaT);            
            clima_sol.appendChild(amanecer);
            clima_sol.appendChild(atardecer);
            clima_temperatura.appendChild(velocidad);   
            
            
        }
        navigator.geolocation.getCurrentPosition(localizacion, error);
    },
    
  },
}
</script>

<!-- Add "scoped" attribute to limit CSS to this component only -->
<style>
</style>