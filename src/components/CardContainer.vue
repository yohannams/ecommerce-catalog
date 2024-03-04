<template>
  <div class="card" v-if="product">
    <img :src="product.image" width="300px" height="383px" />
    <div style="padding: 10px; display: flex; flex-direction: column">
      <div>
        <h2
          style="text-align: center"
          :class="{
            txtpink:
              product.category.includes(`women's clothing`) ||
              product.category.includes(`jewelery`),
            txtblue:
              product.category.includes(`men's clothing`) ||
              product.category.includes(`electronic`),
          }"
        >
          {{ product.title }}
        </h2>
        <div style="display: flex; width: 100%">
          <label style="text-align: left; width: 50%">{{
            product.category
          }}</label>
          <div style="text-align: right; width: 50%">
            <label style="margin-right: 5px">{{ product.rating.rate }}/5</label>
            <svg
              width="18"
              height="18"
              viewBox="0 0 18 18"
              fill="none"
              xmlns="http://www.w3.org/2000/svg"
            >
              <circle cx="9" cy="9" r="9" fill="#002772" />
            </svg>
            <svg
              width="18"
              height="18"
              viewBox="0 0 18 18"
              fill="none"
              xmlns="http://www.w3.org/2000/svg"
            >
              <circle cx="9" cy="9" r="8.5" fill="white" stroke="#002772" />
            </svg>
          </div>
        </div>
        <hr />
        <p>{{ product.description }}</p>
      </div>
      <div>
        <hr />
        <h2>${{ product.price }}</h2>
        <div style="display: flex">
          <button
            style="
              margin-right: 5px;
              width: 50%;
              padding: 5px;
              font-weight: 700;
            "
            :class="{
              btnBuyBgWomen:
                product.category.includes(`women's clothing`) ||
                product.category.includes(`jewelery`),
              btnBuyBgMen:
                product.category.includes(`men's clothing`) ||
                product.category.includes(`electronic`),
            }"
          >
            Buy Now
          </button>
          <button
            style="
              margin-left: 5px;
              width: 50%;
              padding: 5px;
              background-color: white;
              font-weight: 700;
            "
            @click="$emit('next-product')"
            :class="{
              btnBgWomen:
                product.category.includes(`women's clothing`) ||
                product.category.includes(`jewelery`),
              btnBgMen:
                product.category.includes(`men's clothing`) ||
                product.category.includes(`electronic`),
            }"
          >
            Next Product
          </button>
        </div>
      </div>
    </div>
  </div>
  <div class="container-loader" v-else>
    <div class="loader"></div>
  </div>
</template>

<script>
export default {
  name: "CardContainer",
  props: {
    product: Object,
  },
};
</script>

<!-- Add "scoped" attribute to limit CSS to this component only -->
<style scoped>
:root {
  --bgwomen: #fde2ff;
  --txtwomen: #720060;
  --bgmen: #d6e6ff;
  --txtmen: #002772;
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
.btnBgMen {
  color: var(--txtmen);
  border: solid 2px var(--txtmen);
}
.btnBgWomen {
  color: var(--txtwomen);
  border: solid 2px var(--txtwomen);
}
.btnBuyBgMen {
  color: var(--bgmen);
  background-color: var(--txtmen);
}
.btnBuyBgWomen {
  color: var(--bgwomen);
  background-color: var(--txtwomen);
}

.white {
  background-color: white;
  height: 30%;
}

.loader {
  border: 16px solid #f3f3f3; /* Light grey */
  border-top: 16px solid #3498db; /* Blue */
  border-radius: 50%;
  width: 120px;
  height: 120px;
  animation: spin 2s linear infinite;
}
.container-loader {
  position: absolute;
  top: 70%;
  left: 50%;
  transform: translate(-50%, -50%);
  padding: 20px;
  background-color: transparent;
}

@keyframes spin {
  0% {
    transform: rotate(0deg);
  }
  100% {
    transform: rotate(360deg);
  }
}
</style>
