<template>
  <div class="product-images">
    <div class="product-lg-image-container">
      <img :src="productImages[activeImage]" alt="productImage" class="product-lg-image"/>
    </div>
    <div class="product-sm-image-container">
      <div
          v-for="(smImage, i) in productImages"
          :key="i"
          :class="activeImage === i ? 'active-image product-sm-image' : 'product-sm-image'"
          @click="setActiveImage(i)"
      >
        <img :src="productImages[i]" class="product-sm-image-inner"/>
      </div>
    </div>
  </div>
</template>

<script>
export default {
  name: 'ProductImage',
  props: ['productImages'],
  data() {
    return {
      activeImage: 0
    }
  },
  methods: {
    setActiveImage(i) {
      this.activeImage = i
    }
  }
}
</script>

<style >
.product-images {
  display: flex;
  flex-direction: column;
}

.product-lg-image-container {
  height: 400px;
  margin-bottom: 30px;
}

.product-lg-image {
  max-height: 400px;
}

.product-sm-image-container {
  display: flex;
  flex-direction: row;
  margin-left: 20px;
  max-width: 400px;
  overflow: scroll;
  overflow-y: hidden;
}

.product-sm-image-container::-webkit-scrollbar {
  width: 9px;
  height: 7px;
}

.product-sm-image-container::-webkit-scrollbar-thumb {
  background: #b4b5bf;
  border-radius: 3px;
}

.product-sm-image-container::-webkit-scrollbar-thumb:hover {
  background: #79747a;
}

.product-sm-image {
  border: 1px solid lightgrey;
  margin-right: 10px;
  cursor: pointer;
  justify-content: center;
  align-items: center;
}

.product-sm-image-inner {
  width: 60px;
  height: 60px;
}

.active-image {
  border: 2px solid #616161;
  display: flex;
}

.product-sm-image-inner {
  width: 55px;
  height: 55px;
}
</style>
