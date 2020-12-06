<template>
  <div id="app">
    <div class="container-fluid">
      <carousel :images="images"></carousel>
      <clima :ciudades="ciudades"></clima>

      <!-- Inicio de la sección de miembros -->
      <div class="row justify-content-center mb-5">
        <div class="col mt-5" v-for="(item, i) of team" :key="i">
          <team-card :member="item"></team-card>
        </div>
      </div>
      <!-- Fin de la sección de miembros -->  
      <footer-equipo :description="description" :team="team"> </footer-equipo>
    </div> 
  </div> 
</template>

<script>
import clima from "./components/ClimaActual.vue";
import TeamCard from "./components/TeamCard.vue";
import FooterEquipo from "./components/Footer.vue";
import Carousel from "./components/Carousel.vue";

export default {
  name: "App",
  components: {
    clima,
    TeamCard,
    FooterEquipo,
    Carousel
  },
  data() {
    return {
      ciudades:[
          'Bogota',
          'Lima',
          'La Paz'
        ],
      images:[
        'http://www.guiasybaquianos.com/wp-content/uploads/2018/12/Medallo-1.jpg',
        'https://wp.es.aleteia.org/wp-content/uploads/sites/7/2020/10/WEB3-LA-PAZ-BOLIVIA-Shutterstock_1791153806-R.M.-Nunes.jpg',
        'https://bogota.gov.co/sites/default/files/styles/1050px/public/2020-08/delitos-en-bogota.jpg',
        'https://www.elespectador.com/resizer/ci87WLmzKKK6AP0z9xO13peAOww=/657x0/cloudfront-us-east-1.images.arcpublishing.com/elespectador/O3YYRMBOSZF2BEZSA4OZSSJHTM.jpg',
        'https://www.lugaresturisticosdeargentina.com/wp-content/uploads/2018/02/chile-argentina-turismo.jpg'
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
      description: "Somos un grupo de jovenes apasinados por la tecnologia y el desarrollo tanto web como de software y apps"
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