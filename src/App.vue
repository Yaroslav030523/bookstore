<template>
  <div class="main">
    <div class="header">
    <!-- <h1>bookstore</h1> -->
  </div>
    <div class="content" >
  <HelloWorld />

</div>
</div>
</template>

<script>

import HelloWorld from "./components/HelloWorld.vue";


export default {
  name: "App",
  components: {
    HelloWorld,
  },
data(){
  return {
    lol: "lol"
  }
}
}

</script>

<style>
@font-face {
  font-family: 'tangak';
  src: url('../fonts/tangak.otf') format('woff2'),
}
*{
  font-family: 'tangak', sans-serif;
  padding: 0px;
  margin: 0px;
  
}
#app {
  margin: 0px;
  padding: 0px;
  text-align: center;
  color: #2c3e50;

  background-size: cover;
  width: 100%;
  height: 100%;


}
.main{
  /* background-color: rgba(165, 90, 165, 0.615); */
  background-image: linear-gradient(to bottom, #ffffff, #000000,#000000, #000000);
}
.content{
  display: flex;
  background-image: url ("../img/fon.png");
}



</style>
