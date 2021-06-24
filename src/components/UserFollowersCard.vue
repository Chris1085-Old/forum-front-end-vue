<template>
  <div class="card">
    <div class="card-header">
      <strong>{{ initUser.Followers.length }}</strong> followers (追隨者)
    </div>
    <div class="card-body">
      <router-link
        :to="`/users/${follower.id}`"
        v-for="follower in initUser.Followers"
        :key="follower.id"
      >
        <img :src="follower.image" width="60" height="60" class="avatar" />
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
