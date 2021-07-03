<template>
  <div class="container py-5">
    <NavTabs />
    <h1 class="mt-5">
      人氣餐廳
    </h1>

    <hr />
    <div
      class="card mb-3"
      style="max-width: 540px;margin: auto;"
      v-for="restaurant in restaurants"
      :key="restaurant.id"
    >
      <div class="row no-gutters">
        <div class="col-md-4">
          <router-link :to="`/restaurants/${restaurant.id}`">
            <img class="card-img" :src="restaurant.image | emptyImage" />
          </router-link>
        </div>
        <div class="col-md-8">
          <div class="card-body">
            <h5 class="card-title">
              {{ restaurant.name }}
            </h5>
            <span class="badge bg-secondary"
              >收藏數： {{ restaurant.FavoriteCount }}
            </span>
            <p class="card-text">
              {{ restaurant.description }}
            </p>
            <router-link
              :to="`/restaurants/${restaurant.id}`"
              class="btn btn-primary mr-2"
              >Show</router-link
            >

            <button
              v-if="restaurant.isFavorited"
              type="button"
              class="btn btn-danger btn-border favorite mr-2"
              @click.stop.prevent="removeFavorite(restaurant.id)"
            >
              移除最愛
            </button>
            <button
              v-else
              type="button"
              class="btn btn-primary btn-border favorite mr-2"
              @click.stop.prevent="addFavorite(restaurant.id)"
            >
              加到最愛
            </button>
          </div>
        </div>
      </div>
    </div>
  </div>
</template>

<script>
import NavTabs from '../components/Navtabs.vue'
import restaurantsAPI from '../apis/restaurants'
import { Toast } from '../utils/helpers'
import usersAPI from './../apis/users'
import { emptyImageFilter } from '../utils/mixins'

export default {
  name: 'RestaurantsTop',
  components: { NavTabs },
  data() {
    return {
      restaurants: {}
    }
  },
  mixins: [emptyImageFilter],
  methods: {
    favoriteToggle(restaurant) {
      restaurant.isFavorited = !restaurant.isFavorited
    },
    async fetchTopRestaurants() {
      try {
        const { data } = await restaurantsAPI.getTopRestaurants()
        this.restaurants = data.restaurants
        console.log(this.restaurants)
      } catch (error) {
        console.log('error', error)
        Toast.fire({
          icon: 'error',
          title: '無法取得餐廳資料，請稍後再試'
        })
      }
    },
    async addFavorite(restaurantId) {
      try {
        const { data } = await usersAPI.addFavorite({ restaurantId })
        if (data.status !== 'success') {
          throw new Error(data.message)
        }
        this.restaurants = this.restaurants.map(restaurant => {
          if (restaurant.id !== restaurantId) {
            return restaurant
          } else {
            return {
              ...restaurant,
              isFavorited: true,
              FavoriteCount: restaurant.FavoriteCount + 1
            }
          }
        })
      } catch (e) {
        console.log(e)
        Toast.fire({
          icon: 'error',
          title: '加入最愛失敗，請稍候再試'
        })
      }
    },
    async removeFavorite(restaurantId) {
      try {
        const { data } = await usersAPI.deleteFavorite({ restaurantId })
        if (data.status !== 'success') {
          throw new Error(data.message)
        }
        this.restaurants = this.restaurants.map(restaurant => {
          if (restaurant.id !== restaurantId) {
            return restaurant
          } else {
            return {
              ...restaurant,
              isFavorited: false,
              FavoriteCount: restaurant.FavoriteCount - 1
            }
          }
        })
      } catch (e) {
        console.log(e)
        Toast.fire({
          icon: 'error',
          title: '取消最愛失敗，請稍候再試'
        })
      }
    }
  },
  created() {
    this.fetchTopRestaurants()
  }
}
</script>
