<template>
  <div class="sidebar">
    <p><b>Por Estado</b></p>
    <ul>
      <li v-for="state in states" :key="state">
        <input
          type="checkbox"
          :value="state"
          v-model="selectedStates"
          @change="$emit('check', selectedStates)"
        />
        <label>{{ state }}</label>
      </li>
    </ul>
  </div>
</template>
<script>
export default {
  name: "Sidebar",
  props: ["states"],
  data() {
    return {
      selectedStates: [],
    };
  },
};
</script>
<style scoped>
.sidebar {

  height: fit-content;

  border: 1px solid lightgray;


}
ul {
  padding: 0;
}
li {
  list-style: none;
  text-align: left;
  margin-left: 15px;
}
label {
  padding-left: 5px;
}
</style>
