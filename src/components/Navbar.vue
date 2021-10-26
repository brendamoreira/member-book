<template>
  <div class="bar">
    <img class="logo" src="../assets/logo.png" />
    <input
      class="search"
      placeholder="Busque aqui"
      @input="$emit('search', $event.target.value)"
    />
  </div>
</template>
<script>
export default {};
</script>
<style scoped>
.bar {
  grid-area: hd;
  background-color: rgb(237, 237, 237);
  margin: 0;
  height: 50px;
}
.logo {
  height: 60%;
  margin: 10px;
  margin-left: 10%;
  float: left;
}
.search {
  margin: 10px;
  border: 1px solid lightgray;
  border-radius: 20px;
  padding: 5px;
  width: 250px;
}
</style>
