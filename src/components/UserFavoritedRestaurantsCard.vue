<template>
  <div class="card">
    <div class="card-header">
      <strong>{{ initUser.FavoritedRestaurants.length }}</strong> 收藏的餐廳
    </div>
    <div class="card-body">
      <router-link
        :to="`/restaurants/${favoritedRestaurant.id}`"
        v-for="favoritedRestaurant in initUser.FavoritedRestaurants"
        :key="favoritedRestaurant.id"
      >
        <img
          :src="favoritedRestaurant.image"
          width="60"
          height="60"
          class="avatar"
        />
      </router-link>
    </div>
  </div>
</template>

<script>
export default {
  props: {
    initUser: {
      type: Object,
      required: true
    }
  }
}
</script>
