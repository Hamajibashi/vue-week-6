<template>
  <h2>產品列表</h2>
  <div class="container">
    <div class="row row-cols-1 row-cols-lg-4 g-3">
      <div class="col" v-for="item in products" :key="item.id">
        <div class="card h-100">
          <img :src="item.imageUrl" class="card-img-top img-fluid" alt="" />
          <div class="card-body">
            <h5 class="card-title">{{item.title}}</h5>
            <p class="card-text">
              {{item.description}}
            </p>
            <router-link :to="`/product/${item.id}`" class="btn btn-primary">產品詳細</router-link>
          </div>
        </div>
      </div>
    </div>
  </div>
</template>

<script>
export default {
  data() {
    return {
      products: [],
    };
  },
  methods: {
    getProducts() {
      const apiUrl = process.env.VUE_APP_API;
      const apiPath = process.env.VUE_APP_PATH;
      this.$http.get(`${apiUrl}/v2/api/${apiPath}/products/all`)
        .then((res) => {
          this.products = res.data.products;
        })
        .catch((err) => {
          console.log(err.data);
        });
    },
  },
  mounted() {
    this.getProducts();
  },
};
</script>
