<template>
  <div id="app">
    <Navbar @search="search = $event" />
    <p>Lista de Membros</p>
    <div class="page">
      <Sidebar :states="states" @check="selectedStates = $event" />
      <div class="container">
        <div class="cards">
          <Card v-for="member in page" :key="member.email" :member="member" />
        </div>
        <Pagination
          :pages="totalPages"
          :pageNumber="pageNumber"
          @changePage="changePage"
        />
      </div>
    </div>
  </div>
</template>

<script>
import Card from "./components/Card.vue";
import Navbar from "./components/Navbar.vue";
import Pagination from "./components/Pagination.vue";
import Sidebar from "./components/Sidebar.vue";

export default {
  name: "App",
  components: {
    Card,
    Navbar,
    Sidebar,
    Pagination,
  },
  data() {
    return {
      search: "",
      selectedStates: [],
      memberList: [],
      pageNumber: 1,
    };
  },
  watch: {
    filteredList: {
      deep: true,
      handler() {
        this.pageNumber = 1;
      }
    }
  },
  created() {
    this.fetchMemberList();
  },
  methods: {
    async fetchMemberList() {
      try {
        const res = await fetch("http://localhost:3000/members");
        const data = await res.json();
        this.memberList = data;
      } catch (error) {
        console.log(error);
      }
    },
    changePage(pagenum) {
      if (pagenum <= this.totalPages && pagenum > 0) {
        this.pageNumber = pagenum;
      }
    },
  },
  computed: {
    filteredList() {
      return this.memberList.filter((member) => {
        let hasName =
          member.name.first.toLowerCase().includes(this.search.toLowerCase()) ||
          member.name.last.toLowerCase().includes(this.search.toLowerCase());
        let hasState = this.selectedStates.includes(member.location.state);
        if (this.selectedStates.length) {
          return hasName && hasState;
        }
        return hasName;
      });
    },
    states() {
      let states = [];
      for (let i = 0; i < this.memberList.length; i++) {
        if (!states.includes(this.memberList[i].location.state)) {
          states.push(this.memberList[i].location.state);
        }
      }
      return states.sort();
    },
    page() {
      let index = (this.pageNumber - 1) * 9;
      return this.filteredList.slice(index, index + 9);
    },
    totalPages() {
      return Math.ceil(this.filteredList.length / 9);
    },
  },
};
</script>

<style>
#app {
  font-family: Avenir, Helvetica, Arial, sans-serif;
  -webkit-font-smoothing: antialiased;
  -moz-osx-font-smoothing: grayscale;
  text-align: center;
  color: #2c3e50;
}
html,
body {
  margin: 0;
  padding: 0;
}
* {
  box-sizing: border-box;
}
.page {
  margin: auto;
  max-width: 80%;
  display: grid;
  grid-template-columns: 20% 80%;
}
.cards {
  display: flex;
  flex-wrap: wrap;
  align-self: center;
  justify-content: center;
}
</style>
