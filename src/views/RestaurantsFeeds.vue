<template>
  <div class="container py-5">
    <Navtabs />

    <h1 class="mt-5">
      最新動態
    </h1>
    <hr />
    <div class="row">
      <div class="col-md-6">
        <h3>最新餐廳</h3>
        <!-- 最新餐廳 NewestRestaurants -->
        <NewestRestaurants :restaurants="restaurants" />
      </div>
      <div class="col-md-6">
        <!-- 最新評論 NewestComments-->
        <h3>最新評論</h3>
        <NewsetComments :comments="comments" />
      </div>
    </div>
  </div>
</template>

<script>
import Navtabs from '../components/Navtabs.vue'
import NewestRestaurants from '../components/NewestRestaurants'
import NewsetComments from '../components/NewestComments.vue'
import restaurantsAPI from '../apis/restaurants'
import { Toast } from '../utils/helpers'

export default {
  components: { Navtabs, NewestRestaurants, NewsetComments },
  data() {
    return {
      restaurants: [],
      comments: []
    }
  },
  created() {
    this.fetchFeeds()
  },
  methods: {
    async fetchFeeds() {
      try {
        const response = await restaurantsAPI.getFeeds()
        this.restaurants = response.data.restaurants
        this.comments = response.data.comments.filter(
          comment => comment.Restaurant && comment.text
        )
      } catch (error) {
        console.log(error)
        Toast.fire({
          icon: 'error',
          title: '無法取得最新評論，請稍後再試'
        })
      }
    }
  }
}
</script>
