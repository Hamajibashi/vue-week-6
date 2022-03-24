<template>
  <h2>單一產品</h2>
  <div class="container">
    <h3>{{product.title}}</h3>
    <img :src="product.imageUrl" alt="">
  </div>
</template>

<script>
export default {
  data() {
    return {
      product: [],
    };
  },
  methods: {
    getProduct() {
      const apiUrl = process.env.VUE_APP_API;
      const apiPath = process.env.VUE_APP_PATH;
      const { id } = this.$route.params;
      this.$http.get(`${apiUrl}/v2/api/${apiPath}/product/${id}`)
        .then((res) => {
          this.product = res.data.product;
        })
        .catch((err) => {
          console.log(err.data);
        });
    },
  },
  mounted() {
    this.getProduct();
  },
};
</script>
