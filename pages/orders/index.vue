<template>
  <div class="px-4 px-sm-0">
    <Portal to="under-header">
      <div class="container-full d-lg-none py-2 subNavPage px-4">
        <div class="row w-100 justify-content-between g-0">
          <nuxt-link class="col d-flex align-items-center gap-3 text-dark text-decoration-none" to="/profile">
            <img src="~/assets/svg/angle-small-right.svg" alt="">
            <span>Back</span>
          </nuxt-link>
          <!--  Actions are here  -->
          <a href="#" class="col-auto g-0 d-flex align-items-center gap-3 text-dark text-decoration-none">
            <img src="~/assets/svg/sort.svg" alt="">
            <span>Sort</span>
          </a>
        </div>
      </div>
    </Portal>

    <!--  Title selectors  -->
    <div class="d-flex gap-4 mb-2">
      <h3 class="order" :class="{'selected':state==='delivered'}" @click="state='delivered'">Delivered</h3>
      <h3 class="order" :class="{'selected':state==='pending'}" @click="state='pending'">Pending</h3>
    </div>

    <div class="container g-0 mb-10">
      <!--  Delivered Items -->
      <div class="row row-cols-1 gap-3" v-if="state==='delivered'">
        <OrderBox v-if="ordersDelivered.length"
                  v-for="item in ordersDelivered" :key="item.id" :price="item.acf.product_price"
                  :date="item.acf.date" :time="item.acf.time"
                  state="delivered"
                  :orders="[{
                        date: item.acf.date,
                         price: item.acf.product_price,
                          time: item.acf.time,
                           title: item.acf.product_title,
                            thumb: item.acf.productimage
                      }]"/>
      </div>
      <div class="row row-cols-1 gap-3" v-if="state==='pending'">
        <!--  Pending orders  -->
        <OrderBox v-if="ordersPending.length"
                  v-for="item in ordersPending" :key="item.id" :price="+item.acf.product_price"
                  :date="new Date(item.acf.date).toDateString()" :time="item.acf.time"
                  :orders="[{
                        price: item.acf.product_price,
                       title: item.acf.product_title,
                        thumb: item.acf.productimage
                      }]"/>
      </div>
    </div>
  </div>
</template>
<script>
import OrderBox from "@/components/OrderBox";
import axios from "axios";

export default {
  name: "index",
  components: {OrderBox},
  layout: "profile",
  data() {
    return {
      state: 'delivered',
      data: [
        {id: 1, thumb: "/images/img1.jpg", title: "Sella body butter", price: 250},
        {id: 2, thumb: "/images/img1.jpg", title: "Sella body butter", price: 450},
        {id: 3, thumb: "/images/img1.jpg", title: "Sella body butter", price: 350},
      ],
      ordersDelivered: [],
      ordersPending: []
    }
  },
  async asyncData() {
    const config = {
      method: 'get',
      url: "https://api.intelligilesolutions.com/wp-json/wp/v2/orders",
      headers: {
        "Accept": "application/json",
        "Authorization": "Bearer eyJ0eXAiOiJKV1QiLCJhbGciOiJIUzI1NiJ9.eyJpc3MiOiJodHRwczpcL1wvYXBpLmludGVsbGlnaWxlc29sdXRpb25zLmNvbSIsImlhdCI6MTY1OTI2NDA5MSwibmJmIjoxNjU5MjY0MDkxLCJleHAiOjE2NTk4Njg4OTEsImRhdGEiOnsidXNlciI6eyJpZCI6IjMwIn19fQ.t9rBxmg6RH6uYkSQY7xQsx9QcQdwmKzBfpzmpznev8I"
      }
    }
    return await axios(config).then(res => {
      return {
        ordersDelivered: res.data.filter(item => {
          return item.acf.orderstatus === 'delivered'
        }),
        ordersPending: res.data.filter(item => {
          return item.acf.orderstatus === 'pending'
        })
      }
    }).catch(err => {
      console.log(err)
    })
  }
}
</script>

<style scoped>
.order {
  cursor: pointer;
  padding-bottom: 8px;
}

.selected {
  color: #e99d7b;
  border-bottom: 3px solid #e99d7b;
}
</style>