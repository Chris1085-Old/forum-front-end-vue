<template>
  <div class="row text-center">
    <div class="col-3">
      <a href="#">
        <img
          class="card-img-top"
          :src="user.image"
          alt="User image not found"
          width="140px"
          height="140px"
        />
      </a>
      <h2>{{ user.name }}</h2>
      <span class="badge bg-secondary">追蹤人數：{{ user.FollowerCount }}</span>
      <p class="mt-3">
        <button
          v-if="user.isFollowed"
          type="button"
          class="btn btn-danger btn-border favorite mr-2"
          @click.stop.prevent="deleteFollower"
        >
          取消追蹤
        </button>
        <button
          v-else
          type="button"
          class="btn btn-primary btn-border favorite mr-2"
          @click.stop.prevent="addFollower"
        >
          追蹤
        </button>
      </p>
    </div>
  </div>
</template>

<script>
export default {
  props: {
    initialUser: {
      type: Object,
      required: true
    }
  },
  data() {
    return {
      user: this.initialUser
    }
  },
  methods: {
    addFollower() {
      this.user = {
        ...this.user,
        isFollowed: true
      }
    },
    deleteFollower() {
      this.user = {
        ...this.user,
        isFollowed: false
      }
    }
  }
}
</script>
