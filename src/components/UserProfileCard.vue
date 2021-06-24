<template>
  <div class="card mb-3">
    <div class="row no-gutters">
      <div class="col-md-4">
        <img :src="userProfile.profile.image" width="300px" height="300px" />
      </div>
      <div class="col-md-8">
        <div class="card-body">
          <h5 class="card-title">{{ userProfile.profile.name }}</h5>
          <p class="card-text">
            {{ userProfile.profile.email }}
          </p>
          <ul class="list-unstyled list-inline">
            <li>
              <strong>{{ userProfile.profile.Comments.length }}</strong>
              已評論餐廳
            </li>
            <li>
              <strong>{{
                userProfile.profile.FavoritedRestaurants.length
              }}</strong>
              收藏的餐廳
            </li>
            <li>
              <strong>{{ userProfile.profile.Followings.length }}</strong>
              followings (追蹤者)
            </li>
            <li>
              <strong>{{ userProfile.profile.Followers.length }}</strong>
              followers (追隨者)
            </li>
          </ul>
          <p>
            <router-link
              v-if="currentUser.id === userProfile.profile.id"
              :to="`/users/${currentUser.id}/edit`"
            >
              <button type="submit" class="btn btn-primary">
                edit
              </button>
            </router-link>

            <button
              v-if="
                userProfile.isFollowed &&
                  currentUser.id !== userProfile.profile.id
              "
              type="button"
              class="btn btn-danger follow"
              @click.stop.prevent="followToggle"
            >
              取消追蹤
            </button>
            <button
              v-else-if="
                !userProfile.isFollowed &&
                  currentUser.id !== userProfile.profile.id
              "
              type="button"
              class="btn btn-primary follow"
              @click.stop.prevent="followToggle"
            >
              追蹤
            </button>
          </p>
        </div>
      </div>
    </div>
  </div>
</template>

<script>
const dummyUser = {
  currentUser: {
    id: 1,
    name: '管理者',
    email: 'root@example.com',
    image: 'https://i.pravatar.cc/300',
    isAdmin: true
  },
  isAuthenticated: true
}

export default {
  props: {
    initUserProfile: {
      type: Object,
      required: true
    }
  },
  data() {
    return {
      currentUser: dummyUser.currentUser,
      userProfile: this.initUserProfile
    }
  },
  methods: {
    followToggle() {
      this.userProfile.isFollowed = !this.userProfile.isFollowed
    }
  }
}
</script>
