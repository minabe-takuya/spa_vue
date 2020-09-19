<template>
  <div id="app">
    <Firebase></Firebase>
    <Weather></Weather>
  </div>
</template>
<script>
  import Weather from "@/components/Weather";
  import Firebase from "@/components/Firebase";
  export default {
    components:{
      Firebase,
      Weather
    },
  }
</script>
<style>
#app {
  font-family: Avenir, Helvetica, Arial, sans-serif;
  -webkit-font-smoothing: antialiased;
  -moz-osx-font-smoothing: grayscale;
  text-align: center;
  color: #2c3e50;
  margin-top: 60px;
}
</style>
