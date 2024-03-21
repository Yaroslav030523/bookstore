<template>
  <div class="main">
    <BasketSaid   :BasketData = BasketData   />
    



    <div class="buttonContainer">


      <div class="buttons">
  <button class="buttonGenre" :class="{ 'active': currentGenre === 'all' }" @click="filtered('all')">all</button>
  <button class="buttonGenre" :class="{ 'active': currentGenre === 'manga' }" @click="filtered('manga')">manga</button>
  <button class="buttonGenre" :class="{ 'active': currentGenre === 'comics' }" @click="filtered('comics')">comics</button>
  <button class="buttonGenre" :class="{ 'active': currentGenre === 'history' }" @click="filtered('history')" >history</button>
  <button class="buttonGenre" :class="{ 'active': currentGenre === 'horror' }" @click="filtered('horror')">horror</button>
  <button class="buttonGenre" :class="{ 'active': currentGenre === 'fantasy' }" @click="filtered('fantasy')">fantasy</button>
</div>



</div>

<div class="searchDiv">
<h2 class="searchH">Search</h2>
    <input class="searchInput" placeholder="example jojo" v-model="titleFilter" @keydown.enter="searched(titleFilter), currentGenre = null"> 
    <button
    class="searchButton"
     @click="searched(titleFilter), currentGenre = null"
     > Go </button>
</div>

<div class="error" v-if="objFiltered.length < 1">
  <h1>Sorri, we don't have that</h1>
  <img src="../../img/error.png"> 
  <h2></h2>
</div>
  <div v-if="noFilter" >
 <div    class="body">

  <div  class="card"
   v-for="(elem, key) in objFiltered" 
   :key = key
   >
    <div 
     class="wrapper">
      <img :src="elem.image1" class="cover-image" />
    </div>
    <div class="title">
    <h2 class="elemTitle">
     <!-- {{ elem.title }}  -->
    </h2>
  </div>
    <img :src="elem.image2" class="character" />
    <div  @click="this.BasketData.push(elem)" class="wrapperFuter">
  <h3 class="red">Price - {{ elem.price}}$</h3>
    <div class="add"><h2>Add</h2></div>
   
  </div>
</div>
  </div>



</div>

</div>
</template>

<script>
import BasketSaid from "../components/BasketSaid.vue";
import { imageData } from "./imageData.js";

export default {
  name: "HelloWorld",
  components: {
    BasketSaid
  },
  props: {
    msg: String,
  },
  created() {
    this.searched('')
  },
  methods: {
    filtered(descriptionFilter) {
      this.currentGenre = descriptionFilter;
      if (descriptionFilter != 'all'  ){
      this.objFiltered = Object.values(this.imageData).filter((obj) => obj.description == descriptionFilter);
      } else {
        this.objFiltered = Object.values(this.imageData).filter((obj) => obj.description );
      }
    },

    searched(titleFilter) {
      if (titleFilter != ''){

        this.objFiltered = Object.values(this.imageData).filter((obj) => obj.title.toUpperCase() == titleFilter.toUpperCase());
      } else {
        this.objFiltered = Object.values(this.imageData).filter((obj) => obj.title );
      }
    },

    deleteItem(index) {
      this.basketData.splice(index, 1);
    }
  },
  data() {
    return {
      currentGenre: null,
      titleFilter: '',
      noFilter: true,
      addVision: false,
      objFiltered: {},
      BasketData: [],
      imageData: imageData // Імпортуйте об'єкт imageData
    }
  }
}

</script>

<!-- Add "scoped" attribute to limi tCSS to this component only -->
<style scoped>
/* .red{
  color: rgb(255, 255, 255);
} */
.filterButton{

  display: flex;
  margin-left: 1%;
  /* justify-content: space-around; */
  /* justify-content: start; */

}
.buttonGenre{
  cursor: pointer;
  font-size: 20px;
  margin-left: 1%;
  color: rgb(0, 0, 0);
  font-weight: bold;
  padding: 2px 8px 2px 8px;
  transition: 0.2s;
}
.buttonGenre:hover{
  color: white;
  background-color: rgb(0, 0, 0);}
  .active {
  background-color: #000000; 
  color: #ffffff; 
}
.searchDiv{
  font-size: 24px;
  /* margin-left: 4%; */
}
.searchInput{
  height: 30px;
}
.searchButton{
  cursor: pointer;
  height: 30px;
  font-weight: bold;
  /* font-size: 20px; */
  width: 50px;
}
.searchButton:hover{
  color: white;
  background-color: black;
}

.buttonContainer{
  width: 40vw;
   display: flex;
   flex-direction: column;
   margin-left: -5vw;
  /* justify-content: start;  */
}
/* h3 {
  margin: 40px 0 0;
}
ul {
  list-style-type: none;
  padding: 0;
}
li {
  display: inline-block;s
  margin: 0 10px;
}
a {
  color: #42b983;
} */
.elemTitle{
  color:rgb(255, 255, 255);
text-shadow: 4px 4px 4px rgb(0, 0, 0); 
  margin-bottom: 20px;
  font-size: 40px;
  width: 30vh;
}
.wrapperFuter{
cursor: pointer;
/* color: black; */
  color: rgb(0, 0, 0);
  /* text-shadow: 1px 1px 2px rgb(0, 0, 0);  */
  width: 100px;
  border-color: rgb(0, 0, 0);
  border-width: 1px;
  border-style: solid;
border-style: solid;
    
    transform: rotate(-10deg); /* Повертаємо трикутник на 45 градусів */
  background-color: rgba(255, 255, 255, 0.855);
  /* margin-top: 50%; */
  display: block;
}
.wrapperFuter:hover{
  border-color: rgb(255, 255, 255);
color: rgb(255, 255, 255);
/* color: rgba(226, 226, 226, 0.895); */
  background-color:rgba(0, 0, 0, 0.882)
}
.wrapperFuter:active{
  border-color: rgb(0, 0, 0);
  color: rgb(0, 0, 0);
  background-color:rgba(55, 255, 0, 0.882)
}

.add{

  width: 100px;
  border-radius: 10px;
  /* background-color: rgba(255, 255, 255, 0.808); */
}
.main{
  width: 100vw;
  /* padding-top: 25%; */
  /* height: 100%; */
  /* background-color: aqua; */
}

:root {
  /* --card-height: 300px; */
  --card-width: calc(var(--card-height) / 1.5);
}
* {
  box-sizing: border-box;
}
.body {
  padding-top: 20%;
  width: 98.9vw;

  height: 100%;
  margin: 0;
  display: flex;
  flex-wrap: wrap;
  justify-content: center;
  align-items: center;
  /* background: #000000; */
}
.searchH{
cursor: default;
}
.card {


  width: 15%;
  /* width: var(--card-width);
  height: var(--card-height); */
  position: relative;
  display: flex;
  justify-content: center;
  align-items: flex-end;
  padding: 0 3%;
  perspective: 100vw;
  margin: 0 50px;

  margin-top: 5%;
  margin-bottom: 20%;
}

.cover-image {
  width: 100%;
  height: 100%;
  object-fit: cover;
}

.wrapper {
  display: block;
  transition: all 0.5s;
  position: absolute;
  width: 100%;
  z-index: -1;
  height: 350px;
}

.card:hover .wrapper {
  transform: perspective(900px) translateY(-5%) rotateX(25deg) translateZ(0);
  box-shadow: 2px 35px 32px -8px rgba(0, 0, 0, 0.75);
  -webkit-box-shadow: 2px 35px 32px -8px rgba(0, 0, 0, 0.75);
  -moz-box-shadow: 2px 35px 32px -8px rgba(0, 0, 0, 0.75);
}

.wrapper::before,
.wrapper::after {
  content: "";
  opacity: 0;
  width: 100%;
  height: 80px;
  transition: all 0.5s;
  position: absolute;
  left: 0;
}
.wrapper::before {
  top: 0;
  height: 100%;
  background-image: linear-gradient(
    to top,
    transparent 46%,
    rgba(12, 13, 19, 0.5) 68%,
    rgba(12, 13, 19) 97%
  );
}
.wrapper::after {
  bottom: 0;
  opacity: 1;
  background-image: linear-gradient(
    to bottom,
    transparent 46%,
    rgba(12, 13, 19, 0.5) 68%,
    rgba(12, 13, 19) 97%
  );
}

.card:hover .wrapper::before,
.wrapper::after {
  opacity: 1;
}

.card:hover .wrapper::after {
  height: 120px;
}
.title {
  width: 100%;
  transition: transform 0.5s;
}
.card:hover .title {
  transform: translate3d(0%, -50px, 100px);
}

.character {
  width: 260px;
  opacity: 0;
  transition: all 0.5s;
  position: absolute;
  z-index: -1;
}

.card:hover .character {
  opacity: 1;
  transform: translate3d(0%, -30%, 100px);
}


.containerCard{
  background-color: red;
}
.error{
  margin-top: 1%;
  color: #ffffff;
  font-size: 36px;
}
@media (max-width: 1250px){
  
  .buttonContainer{

   margin-left: 0px;
  /* justify-content: start;  */
}
  .wrapper {
    height: 30vh;
  }
  .card:hover .wrapper::after {
  height: 60px;
}
.character{
  width: 150px;
}
.body{
  width: 100vw;
}}
@media (max-width: 799px){
  .buttons{
    display: block;
  }
.elemTitle{
width: 100%;
  font-size: 24px;
}
.elemTitle{

  width: 10%;
}
.card{
  margin-top: 10%;
  margin-bottom: 20%;
}
}
@media (max-width: 666px){
.body{

  /* display: block; */
}
.card{
  margin-top: 25%;
  margin-bottom: 20%;
  width: 50vw;
  height: 30vh;
}
.character{
  width: 40vw;
  height: 35vh;
}
.cover-image{
  height: 50vh
}
.title{
  padding-top: 1px;
}
.wrapper {
  height: 50vh;
}
}
@media (max-width: 400px){
  .card{
    margin-top: 30%;
    margin-bottom: 20%;
  }
.buttons{
  width: 95vw;
  display: flex;
  align-items:center;
  flex-direction: column;
}
.buttonGenre{
  margin-top: 1%;
  width: 50%;
}
}
</style>
