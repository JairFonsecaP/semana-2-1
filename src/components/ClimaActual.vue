<template>
    <div id='clima'>
      <div id='clima_temperatura'> 
        
      </div>
      <div class="col-md-12">
        <div id='clima_sol' class="row">
          <div class="p-3 mb-2 bg-light col-md-6" id="ubicacion">
            <h4>Usted está en {{ubi.nombre}}</h4>
            <img :src="ubi.icn">
            <ul class="list-group">
              <li class="list-group-item d-flex justify-content-between align-items-center">
                Temperatura
                <span class="text-success"><strong>{{ubi.temperatura}} °C</strong></span>
              </li>
              <li class="list-group-item d-flex justify-content-between align-items-center">
                Temperatura Máxima
                <span class="text-success"><strong>{{ubi.max}} °C</strong></span>
              </li>
              <li class="list-group-item d-flex justify-content-between align-items-center">
                Temperatura Mínima
                <span class="text-success"><strong>{{ubi.min}} °C</strong></span>
              </li>
              <li class="list-group-item d-flex justify-content-between align-items-center">
                Sensación Térmica
                <span class="text-success"><strong>{{ubi.sensacion}} °C</strong></span>
              </li>
              <li class="list-group-item d-flex justify-content-between align-items-center">
                Hoy Amanece
                <span class="text-success"><strong>{{ubi.amanece}}</strong></span>
              </li>
              <li class="list-group-item d-flex justify-content-between align-items-center">
                Hoy Atardece
                <span class="text-success"><strong>{{ubi.atardece}},</strong></span>
              </li>
              <li class="list-group-item d-flex justify-content-between align-items-center">
                Velocidad del Viento
                <span class="text-success"><strong>{{ubi.viento}}</strong></span>
              </li>
            </ul>
          </div>
          <hr>
          <div v-for="itm in ciudades" :key="itm" class="p-3 mb-2 bg-light col-md-6" :id="generaId(itm)">
            <h4>{{city[itm].nombre}}</h4>
            <img :src="city[itm].icn">
            <ul class="list-group">
              <li class="list-group-item d-flex justify-content-between align-items-center">
                Temperatura
                <span class="text-success"><strong>{{city[itm].temperatura}} °C</strong></span>
              </li>
              <li class="list-group-item d-flex justify-content-between align-items-center">
                Temperatura Máxima
                <span class="text-success"><strong>{{city[itm].max}} °C</strong></span>
              </li>
              <li class="list-group-item d-flex justify-content-between align-items-center">
                Temperatura Mínima
                <span class="text-success"><strong>{{city[itm].min}} °C</strong></span>
              </li>
              <li class="list-group-item d-flex justify-content-between align-items-center">
                Sensación Térmica
                <span class="text-success"><strong>{{city[itm].sensacion}} °C</strong></span>
              </li>
              <li class="list-group-item d-flex justify-content-between align-items-center">
                Hoy Amanece
                <span class="text-success"><strong>{{city[itm].amanece}}</strong></span>
              </li>
              <li class="list-group-item d-flex justify-content-between align-items-center">
                Hoy Atardece
                <span class="text-success"><strong>{{city[itm].atardece}},</strong></span>
              </li>
              <li class="list-group-item d-flex justify-content-between align-items-center">
                Velocidad del Viento
                <span class="text-success"><strong>{{city[itm].viento}}</strong></span>
              </li>
            </ul>
          </div>
        </div>
      </div>

    </div>
   
</template>

<script>
export default {
  name: 'clima',
  props:['ciudades'],
  data(){
    return {
      city:{},
      ubi:{}
    }
  },
  beforeMount:function(){
    let me = this;
    for(let inf of me.ciudades){
        me.city[inf] = {
          nombre:'',
          temperatura:'',
          sensacion:'',
          max:'',
          min:'',
          viento:'',
          amanece:'',
          atardece:'',
          icn:''
        };
    }
    me.ubi = {
      nombre:'',
      temperatura:'',
      sensacion:'',
      max:'',
      min:'',
      viento:'',
      amanece:'',
      atardece:'',
      icn:''
    };
    for(let inf of me.ciudades){
      me.climaCiudad(inf);
    }
    me.darClima();
  },
  methods : {
    generaId:function(i){
      return `${i}`;
    },
    darClima(){
      let me = this;
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
            function cambiarHora(unix)
            {
              let fecha = new Date(unix*1000);
              let horas = fecha.getUTCHours().toString().padStart(2,0);
              let minutos = fecha.getUTCMinutes().toString().padStart(2,0);
              let segundos = fecha.getUTCSeconds().toString().padStart(2,0);              
              return horas +':'+minutos+':' + segundos;
              
            }
            const {name,main,weather,wind,sys, timezone} = info;me.ubi = {
                  nombre:`${name} ${sys.country}`,
                  temperatura:`${main.temp}`,
                  sensacion:`${main.feels_like}`,
                  max:`${main.temp_max}`,
                  min:`${main.temp_min}`,
                  viento:`${wind.speed}`,
                  amanece:`${cambiarHora(sys.sunrise + timezone )}`,
                  atardece:`${cambiarHora(sys.sunset + timezone )}`,
                  icn:`http://openweathermap.org/img/wn/${weather[0].icon}@2x.png`
            } 
            
        }
        navigator.geolocation.getCurrentPosition(localizacion, error);
    },
    climaCiudad(ciudad){
      let me = this;
        async function  apiWeather(ciudad){
          const result =  await fetch ( `http://api.openweathermap.org/data/2.5/weather?q=${ciudad}&appid=281fb38f9bd1f45f7be4dbb64129b3a2&units=metric`,{
            method :'GET',
          })
          let resultJson = await result.json()
          if (result.ok){
            printOnScreen(resultJson);
          }
        }
        function printOnScreen(info){
            function cambiarHora(unix)
            {
              let fecha = new Date(unix*1000);
              let horas = fecha.getUTCHours().toString().padStart(2,0);
              let minutos = fecha.getUTCMinutes().toString().padStart(2,0);
              let segundos = fecha.getUTCSeconds().toString().padStart(2,0);              
              return horas +':'+minutos+':' + segundos;
              
            }
            const {name,main,weather,wind,sys, timezone} = info;         
            me.city[ciudad] = {
                  nombre:`${name} ${sys.country}`,
                  temperatura:`${main.temp}`,
                  sensacion:`${main.feels_like}`,
                  max:`${main.temp_max}`,
                  min:`${main.temp_min}`,
                  viento:`${wind.speed}`,
                  amanece:`${cambiarHora(sys.sunrise + timezone )}`,
                  atardece:`${cambiarHora(sys.sunset + timezone )}`,
                  icn:`http://openweathermap.org/img/wn/${weather[0].icon}@2x.png`
            }          
        }
        apiWeather(ciudad);
    }
  },
}
</script>