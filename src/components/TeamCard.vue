<template>
  <div class="card bg-black">
    <div class="d-flex justify-content-center p-2">
      <img
        :src="member.image"
        alt="Foto de integrante del equipo"
        width="200px"
        height="200px"
      />
    </div>
    <h3 class="card-title">
      <span>{{ member.nombre }}</span>
    </h3>
    <div class="card-body">
      <p class="card-text">{{ member.descripcion }}</p>
      <p class="card-text">
        <span>{{ member.rol }}</span>
      </p>
    </div>
    <div class="card-footer">
      <small class="text-muted">{{ member.codigo }}</small>
    </div>
  </div>
</template>

<script>
export default {
  name: "TeamCard",
  props: ["member"],
};
</script>

<style scoped>
.card {
  height: 100%;
}

img {
  text-align: center;
  margin-right: 5px;
  margin-left: 5px;
  border-radius: 500px;
  padding: 25px;
}

span {
  font-weight: bold;
}
</style>