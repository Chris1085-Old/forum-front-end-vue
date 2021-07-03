<template>
  <div class="container py-5">
    <NavTabs />
    <h1 class="mt-5">
      美食達人
    </h1>
    <hr />

    <UsersTopCards v-for="user in users" :key="user.id" :initialUser="user" />
  </div>
</template>

<script>
import NavTabs from '../components/Navtabs.vue'
import UsersTopCards from '../components/UsersTopCards.vue'
import usersAPI from './../apis/users'
import { Toast } from './../utils/helpers'

export default {
  name: 'userTop',
  components: { NavTabs, UsersTopCards },
  data() {
    return {
      users: {}
    }
  },
  methods: {
    async fetchTopUsers() {
      try {
        const { data } = await usersAPI.getTopUsers()

        this.users = data.users.map(user => ({
          id: user.id,
          name: user.name,
          image: user.image,
          followerCount: user.FollowerCount,
          isFollowed: user.isFollowed
        }))
      } catch (error) {
        console.log(error)
        Toast.fire({
          icon: 'error',
          title: '無法取得美食達人，請稍後再試'
        })
      }
    }
  },
  created() {
    this.fetchTopUsers()
  }
}
</script>
