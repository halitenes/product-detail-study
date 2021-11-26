<template>
  <div>
    <div class="product-prices">
      <div class="product-quantity-price">
        <div class="product-price-label">
          <span class="quantity-range product-price-header">Toptan Fiyat</span>
          <span class="price-per-item product-price-subheader">(Adet)</span>
        </div>
        <div
            v-for="(barem, i) in data"
            :key="i"
            @click="handleBarem(barem)"
            :class="quantity >= barem.minimumQuantity && barem.maximumQuantity >= quantity ? 'selected-barem barem-container' : 'barem-container'"
        >
          <span class="barem-price product-price-subheader">{{ barem.price }}TL</span>
          <span
              class="barem-quantitiy product-price-header">{{barem.minimumQuantity }} {{ barem.maximumQuantity > 10000 ? '+' : ' - ' + barem.maximumQuantity }}</span>
        </div>
      </div>
      <div class="product-quantity">
        <span class="quantity-header product-price-subheader">Miktar</span>
        <div class="product-quantity-input-container">
          <input type="number" v-model="quantity" :min="0" class="product-quantity-input">
        </div>
      </div>
      <div class="total-price-container">
        <span class="total-price-label product-price-subheader">Toplam</span>
        <span class="total-price">{{(quantity * currentRangePrice).toFixed(2) }} TL</span>
      </div>
    </div>
  </div>
</template>

<script>
export default {
  name: "ProductPrice",
  props: {
    data: Array
  },
  data() {
    return {
      barem: {},
      totalPrice: 0,
      quantity: 0,
      currentRangePrice: 0
    }
  },
  computed: {

  },
  watch:{
    quantity(){
      this.data.forEach((barem)=>{
        if(barem.minimumQuantity <= this.quantity || barem.maximumQuantity < this.quantity){
          this.currentRangePrice = barem.price
          this.barem["quantity"]= this.quantity
          this.barem["totalPrice"] = (this.quantity*barem.price).toFixed(2)
          this.barem["price"] = barem.price
          this.$emit('event_child', this.barem)
        }
      })
    },
  },
  methods: {
    handleBarem(barem) {
      this.quantity = barem.minimumQuantity
      this.currentRangePrice = barem.price
      this.barem["quantity"] = barem.minimumQuantity
      this.barem["price"] = barem.price
      this.barem["totalPrice"] = this.totalPrice.toFixed(2)
      this.$emit('event_child', this.barem)
    },
  }
}
</script>

<style scoped>
.product-prices {
  width: 100%;
  height: 170px;
  padding: 15px;
  background-color: #f5f5f5;
  display: flex;
  flex-direction: column;
  justify-content: flex-start;
}

.product-quantity-price {
  display: flex;
  flex-direction: row;
}

.product-price-label {
  padding-top: 12px;
  padding-left: 13px;
  display: flex;
  flex-direction: column;
  align-items: flex-end;
}

.barem-container {
  display: flex;
  flex-direction: column;
  max-height: 48px;
  margin-top: 12px;
  margin-left: 15px;
  border-left: 1px solid #e0e0e0;
  align-items: flex-start;
  padding-left: 5px;
  width: 90px;
  cursor: pointer;
}

.selected-barem {
  background-color: #ffedb9;
}

.product-quantity {
  display: flex;
  flex-direction: row;
  justify-content: flex-start;
  padding-top: 20px;
  padding-left: 10px;
}

.quantity-header {
  display: flex;
  align-items: center;
  padding-left: 5px;
}

.product-quantity-input-container {
  margin-left: 20px;
}

.quantity-button {
  height: 36px;
  width: 36px;
}

.product-quantity-input {
  width: 50px;
  text-align: center;
  -moz-appearance: textfield;
  height: 25px;
}

.total-price {
  margin-top: 0px;
  padding-left: 15px;
  font-size: 16px;
  font-weight: 500;
}

.total-price-label {
  padding-left: 0px;
}

.total-price-container {
  display: flex;
  flex-direction: row;
  justify-content: flex-start;
  align-items: center;
  margin-top: 0px;
  padding-left: 15px;
  padding-top: 25px;
}
</style>