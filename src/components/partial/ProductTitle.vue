<template>
  <div class="product-title-container">
        <span class="product-title">
            {{ title }}
        </span>
  </div>
</template>

<script>
export default {
  name: "ProductTitle",
  props: {
    title: String
  }
}
</script>

<style scoped>
.product-title-container {
  text-align: left;
  padding: 0 0 20px 0;
}
.product-title {
  font-size: 18px;
  font-weight: normal;
  font-family: Arial,Helvetica,sans-serif;
  color: #202020;
}
</style>