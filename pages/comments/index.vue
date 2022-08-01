<template>
  <div class="py-md-4 px-4 px-md-5 mb-5 bord">
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
    <h3 class="pb-2">Comments</h3>
    <comment-box v-if="comments.length" v-for="item in comments" :key="item.id"
                 :data="{
                   title: '',
                   comment: item.acf.commenttxt,
                   thumb: '/images/img1.jpg',
                   time: item.acf.time,
                   productID: item.acf.productid
                 }"/>
    <pagination :pages="5" :select="1"/>
  </div>

</template>

<script>
import CommentBox from "@/components/CommentBox";
import Pagination from "@/components/Pagination";
import axios from "axios";

export default {
  name: "index",
  components: {CommentBox, Pagination},
  layout: "profile",
  data() {
    return {
      data: [
        {
          id: 1,
          thumb: "/images/img1.jpg",
          title: "Sella body butter",
          score: 3,
          time: 'September30,2022 at 10:56 am',
          comment: 'I really had to prep my face to make it super hydrated. I found the coverage better with a brush but'
        },
        {
          id: 2,
          thumb: "/images/img1.jpg",
          title: "Sella body butter",
          score: 3,
          time: 'September30,2022 at 10:56 am',
          comment: 'I really had to prep my face to make it super hydrated. I found the coverage better with a brush but'
        },
        {
          id: 3,
          thumb: "/images/img1.jpg",
          title: "Sella body butter",
          score: 3,
          time: 'September30,2022 at 10:56 am',
          comment: 'I really had to prep my face to make it super hydrated. I found the coverage better with a brush but'
        },
        {
          id: 4,
          thumb: "/images/img1.jpg",
          title: "Sella body butter",
          score: 3,
          time: 'September30,2022 at 10:56 am',
          comment: 'I really had to prep my face to make it super hydrated. I found the coverage better with a brush but'
        },
        {
          id: 5,
          thumb: "/images/img1.jpg",
          title: "Sella body butter",
          score: 3,
          time: 'September30,2022 at 10:56 am',
          comment: 'I really had to prep my face to make it super hydrated. I found the coverage better with a brush but'
        },
        {
          id: 6,
          thumb: "/images/img1.jpg",
          title: "Sella body butter",
          score: 3,
          time: 'September30,2022 at 10:56 am',
          comment: 'I really had to prep my face to make it super hydrated. I found the coverage better with a brush but'
        },
        {
          id: 7,
          thumb: "/images/img1.jpg",
          title: "Sella body butter",
          score: 3,
          time: 'September30,2022 at 10:56 am',
          comment: 'I really had to prep my face to make it super hydrated. I found the coverage better with a brush but'
        },
      ]
    }
  },
  async asyncData() {
    const config = {
      method: 'get',
      url: "https://api.intelligilesolutions.com/wp-json/wp/v2/comments",
      headers: {
        "Accept": "application/json",
        "Authorization": "Bearer eyJ0eXAiOiJKV1QiLCJhbGciOiJIUzI1NiJ9.eyJpc3MiOiJodHRwczpcL1wvYXBpLmludGVsbGlnaWxlc29sdXRpb25zLmNvbSIsImlhdCI6MTY1OTI2NDA5MSwibmJmIjoxNjU5MjY0MDkxLCJleHAiOjE2NTk4Njg4OTEsImRhdGEiOnsidXNlciI6eyJpZCI6IjMwIn19fQ.t9rBxmg6RH6uYkSQY7xQsx9QcQdwmKzBfpzmpznev8I"
      }
    }
    return await axios(config).then(res => {
      return {
        comments: res.data
      }
    }).catch(err => {
      console.log(err)
    })
  }
}
</script>

<style scoped>
.bord {
  border: none;
  border-radius: 16px;
}

@media screen and (min-width: 768px) {
  .bord {
    border: 1px solid #dee2e6;
  }
}
</style>