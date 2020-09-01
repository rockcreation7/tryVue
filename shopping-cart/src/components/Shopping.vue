<template>
  <div id="shopping-cart" @click="showList()">
    <md-button class="md-accent md-raised" @click="showList()" id="show">{{ cartCount }}</md-button>

 
  </div>
</template>

<script>
export default {
  name: "Shopping",
  computed: {
    StoreCart() {
      return this.$store.getters.StoreCart;
    },
    cartCount() {
      return this.StoreCart.length;
    },
    cart() {
      return this.$store.getters.StoreCart.map(cartitems => {
        return this.$store.getters.products.find(itemForSale => {
          return cartitems === itemForSale.id;
        });
      });
    }
  },
  methods: {
    removeItemComponentLevel(index) {
      this.$store.dispatch("remove__Item", index);
    },
    showList() {
      var modal = document.getElementById("shoppingList");
      var btn = document.getElementById("show");
      btn.onclick = function() {
        console.log("clicked");
        modal.style.display = "block";
      }; 
    }
  }
};
</script>

<style lang="scss" scoped>
#shopping-cart {
  width: 100%;
  max-height: 400px;
  border: 1px solid rgba(#000, 0.12);
  .md-layout {
    margin-top: 2%;
    width: 70%;
    background-color: rgb(255, 255, 255);
    margin: auto;
    z-index: 9999999;
    padding: 20px;
    border-bottom: 1px solid rgb(126, 126, 126);
    .md-layout-item {
      margin-top: 2%;
      img {
        width: 25%;
      }
    }
  }
  .md-span {
    text-align: right;
    width: 100%;
  }
  .shoppingBody {
    display: none;
    position: fixed;
    z-index: 9999999;
    padding-top: 25px;
    left: 0;
    top: 0;
    width: 100%;
    height: 100%;
    overflow: auto;
    background-color: rgb(0, 0, 0);
    background-color: rgba(0, 0, 0, 0.4);
  }
}
</style>