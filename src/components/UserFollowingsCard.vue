<template>
  <div class="card">
    <div class="card-header">
      <strong>{{ initUser.Followings.length }}</strong> followings (追蹤者)
    </div>
    <div class="card-body">
      <router-link
        :to="`/users/${following.id}`"
        v-for="following in initUser.Followings"
        :key="following.id"
      >
        <img :src="following.image" width="60" height="60" class="avatar" />
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
