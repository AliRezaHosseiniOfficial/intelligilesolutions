<template>
  <div class="box">
    <img :src="product.acf.productimage" alt="" />
    <div class="box-inner">
      <div class="px-3">
        <h4>{{ product.acf.productname }}</h4>
        <span>{{ product.acf.productdesc }}</span>
      </div>
      <div class="unit-price">
        <span class="price" :class="{ 'has-discount': data.discount }">${{ product.acf.productprice }}</span>
        <span class="price" v-if="data.discount">${{ product.acf.productprice * (1 - product.discount) }}</span>
      </div>
      <div class="counter-wrapper">
        <div class="counter">
          <span @click="decrease">-</span>
          <span class="num">{{ product.count }}</span>
          <span class="next" @click="increase">+</span>
        </div>
        <div class="d-flex flex-column justift-content-center align-items-center">
          <span class="title">subtotal</span>
          <span class="price">${{ product.totalprice }}</span>
        </div>
      </div>
      <div class="close">
        <span> &#215; </span>
      </div>
    </div>
  </div>
</template>

<script>
import axios from "axios";

export default {
  name: "ProductItemBox",
  props: ["data"],
  data: () => ({
    product: {
      acf: {
        productprice: 0,
      },
      count: 1,
      totalprice: 0,
      discount: 0
    }
  }),
  methods: {
    increase() {
      this.product.count++;
      this.product.totalprice = this.product.count * this.product.acf.productprice * (1 - this.product.discount);
    },
    decrease() {
      if (this.product.count > 1) this.product.count--;
      this.product.totalprice = this.product.count * this.product.acf.productprice * (1 - this.product.discount);
    },
  },
  async created() {
    const config = {
      method: 'get',
      url: `https://api.intelligilesolutions.com/wp-json/wp/v2/products/${this.data.productID}`,
      headers: {
        "Accept": "application/json",
        "Authorization": "Bearer eyJ0eXAiOiJKV1QiLCJhbGciOiJIUzI1NiJ9.eyJpc3MiOiJodHRwczpcL1wvYXBpLmludGVsbGlnaWxlc29sdXRpb25zLmNvbSIsImlhdCI6MTY1OTI2NDA5MSwibmJmIjoxNjU5MjY0MDkxLCJleHAiOjE2NTk4Njg4OTEsImRhdGEiOnsidXNlciI6eyJpZCI6IjMwIn19fQ.t9rBxmg6RH6uYkSQY7xQsx9QcQdwmKzBfpzmpznev8I"
      }
    }
    await axios(config).then(res => {
      this.product.acf = res.data.acf
    }).catch(err => {
      console.log(err)
    })
  }
};
</script>

<style scoped>
.box {
  display: flex;
  align-items: center;
  padding: 14px;
  margin-bottom: 10px;
  border-radius: 16px;
  box-shadow: 0 1px 6px 2px rgb(214, 214, 214);
  background: white;
  position: relative;
}

.box-inner {
  width: 100%;
  display: flex;
  flex-direction: column;
  justify-content: space-between;
}

.box img {
  height: 120px;
  width: 120px;
  min-width: 120px;
  border-radius: 16px;
  overflow: hidden;
}

.box h4 {
  font-size: 20px;
  color: #055452;
}

.unit-price {
  display: none;
}

.price {
  font-weight: 600;
  font-size: 20px;
  color: #055452;
}

.has-discount {
  color: #c6c6c6;
  text-decoration: line-through;
}

.counter-wrapper {
  display: flex;
  padding-left: 1rem;
  flex-direction: row-reverse;
  justify-content: space-between;
  align-items: center;
}

.counter {
  display: flex;
  align-items: center;
  justify-content: space-around;
  width: 150px;
  height: 50px;
  border: 1px solid #c6c6c6;
  border-radius: 28px;
  box-shadow: inset 5px 2px 9px 4px #e0e0e0;
}

.counter span {
  font-size: 22px;
  font-weight: 600px;
  cursor: pointer;
  text-align: center;
  width: 50px;
}

.counter .next {
  color: #055452;
}

.counter .num {
  color: #055452;
  cursor: default;
  width: 80px;
}

.num::after {
  content: "|";
  color: #dad9d9;
  margin-left: 20px;
}

.num::before {
  content: "|";
  color: #dad9d9;
  margin-right: 20px;
}

.title {
  color: #c6c6c6;
  text-transform: uppercase;
  font-size: 12px;
  display: none;
}

.close {
  position: absolute;
  right: 10px;
  top: 0;
}

.close span {
  cursor: pointer;
  color: #d90f0f;
  font-size: 40px;
  padding: 10px;
}

@media screen and (min-width: 1200px) {
  .box-inner {
    flex-direction: row;
    align-items: center;
  }

  .unit-price {
    display: flex;
    flex-direction: column;
  }

  .counter-wrapper {
    display: flex;
    flex-direction: row;
    justify-content: space-between;
  }

  .counter {
    margin-right: 16%;
  }

  .close {
    position: relative;
  }

  .title {
    display: block;
  }
}
</style>
