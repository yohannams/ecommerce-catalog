<template>
  <div class="container">
    <div class="flag">
      <div
        :class="{
          pink:
            currentProduct.category.includes(`women's clothing`) ||
            currentProduct.category.includes(`jewelery`),
          blue:
            currentProduct.category.includes(`men's clothing`) ||
            currentProduct.category.includes(`electronic`),
        }"
        v-if="currentProduct"
      ></div>
      <div class="white"></div>
    </div>
    <div>
      <CardContainer
        :product="currentProduct"
        @next-product="fetchNextProduct"
      />
    </div>
  </div>
</template>

<script>
import CardContainer from "./components/CardContainer.vue";
import axios from "axios";

export default {
  name: "App",
  components: {
    CardContainer,
  },
  data() {
    return {
      products: [],
      currentProductIndex: 1,
      currentProduct: null,
    };
  },
  mounted() {
    this.fetchProducts();
  },
  methods: {
    fetchProducts() {
      axios
        .get("https://fakestoreapi.com/products/" + this.currentProductIndex)
        .then((response) => {
          this.products = response.data;
          this.setCurrentProduct();
        })
        .catch((error) => {
          console.error("Error fetching products:", error);
        });
    },
    setCurrentProduct() {
      this.currentProduct = this.products;
    },
    fetchNextProduct() {
      this.currentProductIndex++;
      if (this.currentProductIndex >= this.products.length) {
        this.currentProductIndex = 0;
      }
      this.fetchProducts();
    },
  },
};
</script>

<style>
:root {
  --bgwomen: #fde2ff;
  --txtwomen: #720060;
  --bgmen: #d6e6ff;
  --txtmen: #002772;
}
#app {
  font-family: Avenir, Helvetica, Arial, sans-serif;
  -webkit-font-smoothing: antialiased;
  -moz-osx-font-smoothing: grayscale;
  color: #2c3e50;
}
body {
  top: 0;
}
.container {
  position: relative;
  width: 100%;
  height: 500px;
}

.flag {
  position: relative;
  width: 100%;
  height: 100%;
}

.pink {
  background-color: var(--bgwomen);
  height: 100%;
}
.blue {
  background-color: var(--bgmen);
  height: 100%;
}
.txtblue {
  color: var(--txtmen);
}
.txtpink {
  color: var(--txtwomen);
}
.bgmen {
  background-color: var(--txtmen);
}
.bgwomen {
  background-color: var(--txtwomen);
}

.white {
  background-color: white;
  height: 30%;
}

.card {
  position: absolute;
  top: 70%;
  left: 50%;
  width: 60%;
  transform: translate(-50%, -50%);
  padding: 20px;
  background-color: #fff;
  border-radius: 10px;
  box-shadow: 0 2px 4px rgba(0, 0, 0, 0.1);
  display: flex;
}
</style>
