<template>
  <div class="box">
    <div class="box-body">
      <img id="thumb" :src="product.acf.productimage" alt="">
      <div>
        <h4>{{ product.acf.productname }}</h4>
        <div class="d-flex gap-3 justify-content-between flex-wrap">
          <!--          <ProductScore :score="product.score"/>-->
          <span>{{ data.time }}</span>
        </div>
        <p class="d-none d-md-block">{{ data.comment }}</p>
      </div>
    </div>
    <p class="d-block d-md-none">{{ data.comment }}</p>
  </div>
</template>

<script>
import ProductScore from "@/components/ProductScore";
import axios from "axios";

export default {
  name: "CommentBox",
  components: {ProductScore},
  props: ['data'],
  data() {
    return {
      product: {
        acf: {}
      }
    }
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
      this.product = res.data
    }).catch(err => {
      console.log(err)
    })
  }
}
</script>

<style scoped>
.box {
  padding-bottom: 20px;
  margin-bottom: 28px;
  justify-content: space-between;
  border-bottom: solid 1px #e0e0e2;
}

.box-body {
  flex: 1;
  display: flex;
  gap: 24px;
  align-items: flex-start;
}

.box-body #thumb {
  min-width: 100px;
  height: 100px;
  overflow: hidden;
  object-fit: cover;
  border-radius: 8px;
}

.box-body h4 {
  font-size: 20px;
  color: #055452;
}

.box-body p, .box p {
  font-size: 18px;
  font-weight: 400;
  margin-bottom: 5px;
  padding-top: 14px;
  color: #707070 !important;
}

.box-body span {
  color: #b2b2b2;
  font-size: 14px;
}

</style>