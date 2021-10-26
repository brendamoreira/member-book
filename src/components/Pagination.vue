<template>
  <div class="pagination">
    <button
      class="buttonleft"
      @click="$emit('changePage', pageNumber - 1)"
    ></button>
    <ul>
      <li
        v-for="page in pages"
        :class="pageNumber === page ? 'active' : 'none'"
        :key="page"
        @click="$emit('changePage', page)"
      >
        {{ page }}
      </li>
    </ul>
    <button
      class="buttonright"
      @click="$emit('changePage', pageNumber + 1)"
    ></button>
  </div>
</template>
<script>
export default {
  name: "Pagination",
  props: ["pages", "pageNumber"],
};
</script>
<style scoped>
ul {
  display: inline-block;
  padding: 0;
}
.active {
  font-weight: bold;
  font-size: larger;
  text-decoration-line: underline;
}
li {
  list-style: none;
  display: inline-block;
  margin: 5px;
}
.buttonleft {
  border-width: 0 1px 1px 0;
  display: inline-block;
  padding: 3px;
  transform: rotate(135deg);
  -webkit-transform: rotate(135deg);
  background-color: white;
}
.buttonleft:hover {
  border-width: 0 4px 4px 0;
  cursor: pointer;
}

.buttonleft:focus {
  outline: none;
}
.buttonright {
  border-width: 0 1px 1px 0;
  display: inline-block;
  padding: 3px;
  transform: rotate(-45deg);
  -webkit-transform: rotate(-45deg);
  background-color: white;
}
.buttonright:hover {
  border-width: 0 4px 4px 0;
  cursor: pointer;
}
.buttonright:focus {
  outline: none;
}
</style>
