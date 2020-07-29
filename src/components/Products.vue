<template>
  <div class="row product-container">
    <app-product v-for="product in productList ">
      <img class="card-img-top" :src="product.selectedImage" :alt="product.title">
      <div class="card-body">
        <h5 class="card-title"> {{ product.title }} </h5>
        <small><strong>Adet :</strong>{{ product.count }}</small>
        <br>
        <small><strong>Fiyat : </strong>{{ product.price }}</small>
        <br>
        <small><strong>Tutar : </strong>{{ product.totalPrice }}</small>
      </div>
    </app-product>
  </div>
</template>

<script>
  import Product from "./Product"
  import {eventBus} from "../main";

  export default{
    data(){
      return{
        productList: [],
      }
    },
    components: {
      appProduct:Product
    },
    created(){
      eventBus.$on("productAdded",(product) => {                     /* product object event listiner */
        if(this.productList.length < 2){
          this.productList.push(product);
          eventBus.$emit("progressBarUpdate",this.productList.length);       /* progress bar update event */
        }else{
          alert("Daha fazla urun ekleyemezsin");
        }
      });
    }
  }
</script>