<template>
  <div class="card">
    <div class="card-header">
      <strong>{{ initUser.Comments.length }}</strong> 已評論餐廳
    </div>
    <div class="card-body">
      <router-link
        :to="`/restaurants/${comment.Restaurant.id}`"
        v-for="comment in initUser.Comments"
        :key="comment.id"
      >
        <img
          :src="comment.Restaurant.image"
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
