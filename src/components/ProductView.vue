<template>
  <div class="product-container">
    <div class="product-image-container">
      <product-image :product-images="selectImage"/>
    </div>

    <div class="product-detail-container">
      <product-title :title="data.productTitle"/>

      <div v-for="(attribute, i) in data.selectableAttributes" :key="i" class="product-attribute-container">
        <div class="product-attribute-label">
          {{ attribute.name }}
        </div>
        <div class="product-attribute-value-container">
          <div
              v-for="(value, j) in attribute.values"
              :key="j"
              @click="deneme(attribute.name, value)"
              class="product-attribute-value"
              :class="selectedFirstValue ==='' ? '' : selectedFirstValue === value || selectedSecondValue == value ? 'selected-value'
              : availableVariants.indexOf(value) === -1 && i > 0 ? 'disabled' : '' "
          >
            <!--            availableVariants.indexOf(value) === -1 attributes[attribute.name] === value ? 'selected-value' : availableVariants.indexOf(value) === -1 && i > 0 ? 'disabled' : '' -->
            {{ value }}
          </div>
        </div>
      </div>

      <product-price :data="data.baremList" @event_child="handleBarem"/>

      <div class="add-to-cart-container">
        <button class="add-to-cart-btn" :disabled="selectedSecondValue.indexOf(0)!=='' && barem.quantity=== 0" @click="addToBasket">Sepete Ekle</button>
      </div>
    </div>
  </div>
</template>

<script>
import ProductImage from "./ProductImage";
import ProductTitle from "./partial/ProductTitle";
import ProductPrice from "./partial/ProductPrice";
export default {
  name: "ProductView",
  components: {
    'product-image': ProductImage,
    'product-title': ProductTitle,
    'product-price': ProductPrice,
  },
  data() {
    return {
      attributes: {},
      productAttribute: {},
      barem: {quantity: 0},
      selectedFirstValue: "",
      selectedSecondValue: ""
    }
  },
  props: {
    data: Object
  },
  computed: {
    selectImage() {
      let productImages = []
      if (this.selectedSecondValue) {
        this.data.productVariants.forEach((variant) => {
          if (variant.attributes[0].value === this.selectedSecondValue && variant.attributes[1].value === this.selectedFirstValue) {
            productImages = variant.images
          }
        })
        return productImages
      } else {
        return this.allImages
      }

    },
    availableVariants() {
      let firstAttribute = this.selectedFirstValue,
          availableVariants = []

      this.data.productVariants.forEach((variants) => {
        if (variants.attributes[1].value === firstAttribute) {
          availableVariants = this.attributes[firstAttribute]
        }
      })
      return availableVariants
    },
    allImages() {
      let allImages = []
      this.data.productVariants.forEach(variant => {
        variant.images.forEach(img => {
          allImages.push(img)
        })
      })
      return allImages
    },
  },
  created() {
    this.data.selectableAttributes[0].values.forEach((value) => {
      this.attributes[value] = []
    })
    this.prepareAttributes()
  },
  methods: {
    deneme(prop, value) {
      console.log(prop)
      console.log(value)
      if (prop === "Renk") {
        this.selectedFirstValue = value
        this.productAttribute[prop] = value
        this.selectedSecondValue = ""
        this.productAttribute["Beden"] = ""
      } else {
        this.selectedSecondValue = value
        this.productAttribute["Beden"] = value
      }

    },
    prepareAttributes() {
      this.data.selectableAttributes[0].values.forEach((value) => {
        this.data.productVariants.forEach((variants) => {
          if (variants.attributes[1].value === value) {
            this.attributes[value].push(variants.attributes[0].value)
          }
        })
      })
      console.log(this.attributes)
    },
    handleBarem(value) {
      this.barem = value
    },
    addToBasket(){
      this.barem["Renk"]= this.selectedFirstValue
      this.barem["Beden"]= this.selectedSecondValue
      console.log(this.barem)
    }
  }
}
</script>

<style scoped>
.product-container {
  display: flex;
  flex-direction: row;
  justify-content: center;
  gap: 50px;
}

.product-image-container {
  flex-direction: column;
  width: 375px;
  height: 550px;
}

.product-detail-container {
  flex-direction: row;
}

.product-attribute-container {
  padding-bottom: 7px;
  display: flex;
  flex-direction: row;
}

.product-attribute-label {
  height: 36px;
  width: 50px;
  display: flex;
  align-items: center;
  justify-content: start;
  font-size: 14px;
}

.product-attribute-value-container {
  display: flex;
  flex-direction: row;
  max-width: 450px;
  flex-wrap: wrap;
}

.product-attribute-value {
  width: 120px;
  height: 36px;
  cursor: pointer;
  border: 2px solid #e0e0e0;
  border-radius: 2px;
  display: flex;
  justify-content: center;
  align-items: center;
  margin-left: 15px;
  font-size: 13px;
  margin-bottom: 12px;
}

.selected-value {
  border-width: 2px;
  line-height: 31px;
  border-color: darkred;
  background-color: #edf4fb;
  font-weight: bold;
}

.disabled {
  cursor: not-allowed;
  pointer-events: none;
  color: #e0e0e0;
}

.add-to-cart-container {
  display: flex;
  justify-content: flex-start;
  margin-top: 50px;
}

.add-to-cart-btn {
  border: 1px solid #febe2c;
  background-color: #febe2c;
  color: #ffffff;
  padding: 10px 15px;
}

.add-to-cart-btn:hover {
  border: 1px solid #b48c2e;
  background-color: #b48c2e;
  color: #ffffff;
  cursor: pointer;
}

.add-to-cart-btn:disabled {
  border: 1px solid #999999;
  background-color: #cccccc;
  color: #666666;
  cursor: not-allowed;
}


</style>