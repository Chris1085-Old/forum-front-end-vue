<template>
  <div class="container py-5">
    <!-- AdminNav Component -->

    <table class="table">
      <thead class="thead-dark">
        <tr>
          <th scope="col">
            #
          </th>
          <th scope="col">
            Email
          </th>
          <th scope="col">
            Role
          </th>
          <th scope="col" width="140">
            Action
          </th>
        </tr>
      </thead>
      <tbody>
        <tr v-for="(user, index) in users" :key="user.id">
          <th scope="row">
            {{ index + 1 }}
          </th>
          <td>{{ user.email }}</td>
          <td>{{ user.isAdmin ? 'Admin' : 'User' }}</td>
          <td>
            <button
              type="button"
              class="btn btn-link"
              v-if="user.id !== currentUser.id"
              @click.stop.prevent="
                handleUserRole({ userId: user.id, isAdmin: user.isAdmin })
              "
            >
              {{ user.isAdmin ? 'set as user' : 'set as admin' }}
            </button>
          </td>
        </tr>
      </tbody>
    </table>
  </div>
</template>

<script>
import adminAPI from './../apis/admin'
import { Toast } from './../utils/helpers'

export default {
  data() {
    return {
      users: [],
      currentUser: {},
      isLoading: true
    }
  },
  methods: {
    async fetchUser() {
      try {
        const { data } = await adminAPI.users.get()
        this.users = data.users
        this.isLoading = false
      } catch (e) {
        console.log(e)
        Toast.fire({
          icon: 'error',
          title: '資料讀取失敗，請稍候再試'
        })
        this.isLoading = false
      }
    },
    async handleUserRole({ userId, isAdmin }) {
      try {
        const { data } = await adminAPI.users.update({
          userId,
          isAdmin: (!isAdmin).toString()
        })
        if (data.status !== 'success') {
          throw new Error(data.message)
        }
        this.users = this.users.map(user => {
          if (user.id === userId) {
            return {
              ...user,
              isAdmin: !user.isAdmin
            }
          }
          return user
        })
      } catch (e) {
        console.log(e)
        Toast.fire({
          icon: 'error',
          title: '更新失敗，請稍候再試'
        })
      }
    }
  },
  created() {
    this.fetchUser()
  }
}
</script>
