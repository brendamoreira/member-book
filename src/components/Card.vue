<template>
  <div class="card">
    <img class="avatar" src="../assets/logo.png">
    <p class="name captalize"><b>{{ member.name.first }} {{member.name.last}}</b></p>
    <p class="adress captalize">{{ location }}</p>
    <p class="info captalize">{{ member.location.city }}</p>
    <p class="info captalize">{{ member.location.state }} - CEP: {{member.location.postcode }}</p>

  </div>
</template>

<script>
export default {
  name: "Card",
  props: ['member'],
  data() {
    return {
      
    }
  },
  computed: {
    location(){
      const memberLocation = this.member.location.street;
      let index = memberLocation.indexOf(" ");
      let number = memberLocation.slice(0, index);
      let street = memberLocation.replace(number, "");
      return street.trim().concat(", ", number)
    }
  }
};
</script>

<style scoped>
.card{
  height: 300px;
  width: 250px;
  border: 1px solid lightgray;
  margin:5px;
}
.avatar{
  height: 20%;
  margin: 15px;
  padding: 10px;
}
.name{
 margin: 0 0 10 0;
 font-size: 18px;
}
.info{
  font-size: 12px;
  margin:0;
}
.captalize{
  text-transform: capitalize;
}
</style>
