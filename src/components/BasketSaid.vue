<template>
  <div class="BasketSaidMain">
    <div class="heder">
      <h1 class="Bookstore">Bookstore</h1>
      <img class="basketImgOn" @click="toggleBasketVisibility()" src="../../img/cart.png" alt="">
    </div>
    <div class="basket" v-if="basketVision">
      <div @click="toggleBasketVisibility()" class="blure"></div>
      <div class="said scroll-container">
        <div class="topBasket">
          <img class="basketImgOf" @click="toggleBasketVisibility()" src="../../img/cart.png" alt="">
       
          <div class="textBasket"> 
            <p> {{ localBasketData.length }} books</p>
            <p>Total price: {{ sum.toFixed(1) }} $</p>
          </div>
        </div>
        <div class="empty" v-if="localBasketData.length < 1"> <h2>Your cart is currently empty</h2></div>
        <div class="BasketCard" v-for="(item, key) in sortedUniqueBooks" :key="key"> 
          <img class="imgBasket" :src="item.image1" width="100px" alt="img">
          <div class="text">
            <div class="flex">
            <h3 class="itemTitle">{{ item.title }}</h3>
            <p v-if="computedItemQuantity[item.title] > 1"> ( {{ computedItemQuantity[item.title] }} )</p>
          </div>
          <h3>Price: {{ item.price }}</h3>
            <img class="delete" @click="deleteItem(item)" src="../../img/x.png" width="40px" alt="">
          </div>
        </div>
        <button v-if="localBasketData.length" class="pay">Pay</button>
      </div>
    </div>
  </div>
</template>

<script>
export default {
  name: "BasketSaid",
  props: { BasketData: Array },
  data() {
    return {
      sum: 0,
      basketVision: false,
      localData: [],
      localBasketData: [],
    };
  },
  methods: {
    toggleBasketVisibility() {
      this.basketVision = !this.basketVision;
      this.addLocale();
      this.booksPrice();
    },
    booksPrice() {
      this.sum = this.localBasketData.reduce((total, item) => total + +item.price, 0);
    },
    addLocale() {
      this.localBasketData = [...this.BasketData];

      for (const item of this.localData) {
        const index = this.localBasketData.findIndex(element => element.title === item.title);
        if (index !== -1) {
          this.localBasketData.splice(index, 1);
        }
      }
    },
    deleteItem(itemToRemove) {
      this.localData.push(itemToRemove);

      const index = this.localBasketData.indexOf(itemToRemove);

      if (index !== -1) {
        const deletedItemPrice = +this.localBasketData[index].price;

        this.sum -= deletedItemPrice;
        this.localBasketData.splice(index, 1);
      }
    }
  },
  computed: {
    sortedUniqueBooks() {
      const uniqueBooks = Array.from(new Set(this.localBasketData.map(item => item.title)));
      return uniqueBooks
        .map(title => this.localBasketData.find(item => item.title === title))
        .sort((a, b) => a.title.localeCompare(b.title));
    },
    computedItemQuantity() {
      return this.localBasketData.reduce((count, item) => {
        count[item.title] = (count[item.title] || 0) + 1;
        return count;
      }, {});
    }
  }
};
</script>



  
<style scoped>
.Bookstore{
  cursor: default;
  font-size: 54px;
}
.heder{
  padding: 1% 1% 1% 5%;
  display: flex;
}
.textBasket{
    padding: 6px;
    font-size: 20px;
}

.topBasket{
    display: flex;
}

.empty{
  cursor: default;
  margin-top: 5%;
  font-size: 36px;
}
.scroll-container {
    height: 100vh; /* Фіксована висота контейнера */
    overflow-y: auto; /* Додавання вертикальної прокрутки, якщо контент перевищує висоту */
}



.basketImgOn{

  /* width: 200px; */
    margin-left: 78%;
    cursor: pointer;
}
.basketImgOn:hover{
    transform: rotate(15deg);

}
.basketImgOf{
    /* margin-right: 85%; */
    cursor: pointer;
}
.basketImgOf:hover{
    transform: rotate(-15deg);

}

.delete{
    cursor: pointer;
    width: 40px;
}
.delete:hover{
    width: 44px;
}
.delete:active{
  width: 36px;
}
.pay{
  color: white;
  font-size: 20px;
  border-radius: 10px 0px 10px 0px ;
  background-color: rgb(0, 0, 0);
  height: 30px;
  width: 30%;
  margin-top: 2%;
  margin-bottom: 2%;
}
.pay:hover{
  opacity: 0;
}
.flex{
  display: flex;
}
.text{
  color: rgba(0, 0, 0, 0.859);
    /* background-color: rgba(137, 43, 226, 0.241); */
}
.itemTitle{
    /* width: 50px; */
    justify-content: start;
    margin-left: 0px;
    /* transform: rotate(90deg); */
}
.BasketCard{
  background-image: linear-gradient(to right, #7dc1d587, #0000ff00);
    display: flex;
    /* width: 10%; */
margin: 1%;


}
.basket{
    position: fixed;
    top: 0;
    left: 0;
    width: 100vw;
    min-height: 250vh;
    height: 100%;
    display: flex;
    z-index: 999;
    padding-bottom: 2000px;
}
.blure{
    width: 70%;
    background-color: rgba(58, 58, 58, 0.858);
}
.said{
width: 30%;
background-color: rgb(210, 227, 242);

}
@media (max-width: 1250px){
  .basketImgOn{
    margin-left: 60%;
  }
}
@media (max-width: 799px){
  .blure{
    width: 50%;
}
.said{
width: 50%;
}
  .topBasket{
    display: block;
}
  /* .basketImgOn{
    margin-left: 30%;
  } */
}
  @media (max-width: 666px){
  .basketImgOn{
    margin-left: 0;
  }
  .blure{
    width: 0;
}
.said{
width: 100%;
}
  .imgBasket{
    width: 30%;
  }
  }
</style>