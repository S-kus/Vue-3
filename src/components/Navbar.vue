<template>
  <div class="navbar">
    <nav>
      <img src="@/assets/logo.jpg" alt="logo"/>
      <h1><router-link :to="{ name: 'Home' }">Project Labz</router-link></h1>
      <div class="links">
        <div v-if="user">
          <router-link :to="{ name: 'Home'}">Home</router-link>
          <router-link :to="{ name: 'CreateProjectlist' }">Create Projectlist</router-link>
          <router-link :to="{ name: 'UserProjectlists' }">My Projectlists</router-link>
          <span>Hi there, {{ user.displayName }}</span>
          <button @click="handleClick">Logout</button>
        </div>
        <div v-else>
          <router-link class="btn" :to="{ name: 'Signup' }">Signup</router-link>
          <router-link class="btn" :to="{ name: 'Login' }">Login</router-link>
        </div>
      </div>
    </nav>
  </div> 
</template>

<script>

import getUser from '../composables/getUser'
import useLogout from '../composables/useLogout'
import { useRouter } from 'vue-router'

export default {
  setup() {
    const { user } = getUser()
    const { logout } = useLogout()
    const router = useRouter()

    const handleClick = async () => {
      await logout()
      console.log('logged out')
      router.push({ name: 'Login' })
    }

    return { handleClick, user }
  }
}
</script>

<style scoped>
  .navbar {
    padding: 16px 10px;
    margin-bottom: 60px;
    background: white;
  }
  nav {
    display: flex;
    align-items: center;
    max-width: 1200px;
    margin: 0 auto;
  }
  nav img {
    max-height: 60px;
  }
  nav h1 {
    margin-left: 20px;
  }
  nav .links {
    margin-left: auto;
  }
  nav .links a, button {
    margin-left: 16px;
    font-size: 14px;
  }
  span {
    font-size: 14px;
    display: inline-block;
    margin-left: 16px;
    padding-left: 16px;
    border-left: 1px solid #eee;
  }
</style>