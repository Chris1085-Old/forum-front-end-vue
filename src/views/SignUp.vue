<template>
  <div class="container py-5">
    <form class="w-100" @submit.prevent.stop="handleSubmit">
      <div class="text-center mb-4">
        <h1 class="h3 mb-3 font-weight-normal">
          Sign Up
        </h1>
      </div>

      <div class="form-label-group mb-2">
        <label for="name">Name</label>
        <input
          id="name"
          name="name"
          type="text"
          class="form-control"
          placeholder="name"
          autocomplete="username"
          required
          autofocus
          v-model="name"
        />
      </div>

      <div class="form-label-group mb-2">
        <label for="email">Email</label>
        <input
          id="email"
          name="email"
          type="email"
          class="form-control"
          placeholder="email"
          autocomplete="email"
          required
          v-model="email"
        />
      </div>

      <div class="form-label-group mb-3">
        <label for="password">Password</label>
        <input
          id="password"
          name="password"
          type="password"
          class="form-control"
          placeholder="Password"
          autocomplete="new-password"
          required
          v-model="password"
        />
      </div>

      <div class="form-label-group mb-3">
        <label for="password-check">Password Check</label>
        <input
          id="password-check"
          name="passwordCheck"
          type="password"
          class="form-control"
          placeholder="Password"
          autocomplete="new-password"
          required
          v-model="passwordCheck"
        />
      </div>

      <button class="btn btn-lg btn-primary btn-block mb-3 w-100" type="submit">
        Submit
      </button>

      <div class="text-center mb-3">
        <p>
          <router-link to="/signin">
            Sign In
          </router-link>
        </p>

        <p class="text-center mt-3" v-if="!isValidate">
          密碼不正確，請重新輸入
        </p>
      </div>
      <p class="mt-5 mb-3 text-muted text-center">
        &copy; 2017-2018
      </p>
    </form>
  </div>
</template>

<script>
import authorizationAPI from './../apis/authorization'
import { Toast } from './../utils/helpers'
export default {
  name: 'SignUp',
  data() {
    return {
      name: '',
      email: '',
      password: '',
      passwordCheck: '',
      isValidate: true,
      isProcessing: false
    }
  },
  methods: {
    async handleSubmit() {
      try {
        // 判斷註冊資料是否填寫
        if (
          !this.email ||
          !this.name ||
          !this.password ||
          !this.passwordCheck
        ) {
          Toast.fire({
            icon: 'error',
            title: '請確實填入註冊資料'
          })
          return
        }
        // 判斷密碼輸入是否正確
        if (this.password !== this.passwordCheck) {
          Toast.fire({
            icon: 'error',
            title: '密碼與確認密碼不符，請重新輸入'
          })
          return
        }
        // 將註冊資料透過api送給伺服器
        this.isProcessing = true
        const { data } = await authorizationAPI.signUp({
          name: this.name,
          email: this.email,
          password: this.password,
          passwordCheck: this.passwordCheck
        })
        if (data.status !== 'success') {
          this.isProcessing = false
          throw new Error(data.message)
        }
        // 轉址到登入頁
        this.$router.push({ name: 'sign-in' })
      } catch (e) {
        this.isProcessing = false
        console.log(e)
        Toast.fire({
          icon: 'warning',
          title: '無法註冊'
        })
      }
    }
  }
}
</script>
