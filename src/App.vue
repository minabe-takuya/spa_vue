<template>
  <div id="app">
    <Firebase></Firebase>
    <Weather></Weather>
    <Gurunabi></Gurunabi>
  </div>
</template>
<script>
  import Weather from "@/components/Weather";
  import Firebase from "@/components/Firebase";
  import Gurunabi from "@/components/Gurunabi";
  export default {
    components:{
      Firebase,
      Weather,
      Gurunabi,
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
