<template>
  <header id="header">
    <nav class="navbar navbar-expand-lg navbar-dark bg-dark">
      <a class="navbar-brand" href="/"> Sprint 2 Equipo 1</a>
      <button
        class="navbar-toggler"
        type="button"
        data-toggle="collapse"
        data-target="#navbarNavDropdown"
        aria-controls="navbarNavDropdown"
        aria-expanded="false"
        aria-label="Toggle navigation"
      >
        <span class="navbar-toggler-icon"></span>
      </button>
      <div class="collapse navbar-collapse" id="navbarNavDropdown">
        <ul class="navbar-nav">
          <li class="nav-item active">
            <a class="nav-link" href="#carousel">Carrusel</a>
          </li>
          <li class="nav-item active">
            <a class="nav-link" href="#clima">Clima</a>
          </li>
          <li class="nav-item active">
            <a class="nav-link" href="#team">Equipo</a>
          </li>
          <li class="nav-item active">
            <a class="nav-link" href="#footer">Footer</a>
          </li>
        </ul>
      </div>
    </nav>
  </header>
</template>


<script>
export default {
  name: "HeaderEquipo",
};
</script>

<style scoped>
#header {
  font-family: SF;
  font-family: "Noto Sans TC", sans-serif;
}
</style>
