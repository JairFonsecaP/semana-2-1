<template>
  <div id="app">
    <div class="container-fluid">
      <clima :ciudades="ciudades"></clima>

      <!-- Inicio de la sección de miembros -->
      <div class="row justify-content-center mb-5">
        <div class="col mt-5" v-for="(item, i) of team" :key="i">
          <team-card :member="item"></team-card>
        </div>
      </div>
      <!-- Fin de la sección de miembros -->
    </div>
  </div>
</template>

<script>
import clima from "./components/ClimaActual.vue";
import TeamCard from "./components/TeamCard.vue";

export default {
  name: "App",
  components: {
    clima,
    TeamCard
  },
  data() {
    return {
      ciudades:[
          'Bogota',
          'Lima',
          'La Paz'
        ],
      team: [
        {
          codigo: 1,
          nombre: "Juan Pablo Correa",
          descripcion:
            "Apasionado por la tecnología y por cómo esta puede mejorarlo todo, desde las actividades de la vida cotidiana hasta los proyectos más complejos. Me gustan las mascotas, los idiomas y aprender nuevas cosas todos los días.",
          rol: "Arquitecto de Software",
          imagen:
            "https://raw.githubusercontent.com/jpcorreap/semana-1-1/develop/src/img/JuanPablo.png",
        },
        {
          codigo: 2,
          nombre: "Wilson Bojacá",
          descripcion:
            "Soy matemático de la universidad Distrital Francisco José de Caldas, apasionado por la tecnología y la música. En mis tiempos libres me gusta leer sobre matemáticas y tocar la guitarra.",
          rol: "Backend",
          imagen:
            "https://raw.githubusercontent.com/jpcorreap/semana-1-1/develop/src/img/WilsonBajaca.png",
        },
        {
          codigo: 3,
          nombre: "Heiler Melendez",
          descripcion:
            "Heiler Alfonso Meléndez Mena, estudiante de ingeniería de software, me apasiana la programación y el desarrollo. Mi aspiración es llegar a un excelente arquitecto de Software.",
          rol: "Analista de Software",
          imagen:
            "https://raw.githubusercontent.com/jpcorreap/semana-1-1/develop/src/img/HeilerMelendez.png",
        },
        {
          codigo: 4,
          nombre: "Mishell Arboleda",
          descripcion:
            "Apasionada por la naturaleza, la música, las comunicaciones y la tecnología. Familiar, calida y alegre.",
          rol: "Frontend",
          imagen:
            "https://raw.githubusercontent.com/jpcorreap/semana-1-1/develop/src/img/MishellArboleda.jpeg",
        },
        {
          codigo: 5,
          nombre: "Jair Fonseca P.",
          descripcion:
            "Vivo en Tierra del fuego, Chile. Tengo Dos huskies siberianos que son mi vida, me encanta la nieve, el frío y viajar, me gusta montar bicicleta, nadar y programar.",
          rol: "Tester",
          imagen:
            "https://raw.githubusercontent.com/jpcorreap/semana-1-1/develop/src/img/JairFonseca.jpg",
        },
      ],
    };
  },
};
</script>

<style>
#app {
  font-family: SF;
  -webkit-font-smoothing: antialiased;
  -moz-osx-font-smoothing: grayscale;
  text-align: center;
  color: #2c3e50;
  margin-top: 60px;
  font-family: "Noto Sans TC", sans-serif;
}
</style>