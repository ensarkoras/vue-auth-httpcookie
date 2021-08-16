<template>
  <nav class="navbar navbar-expand-md navbar-dark bg-dark mb-4">
    <div class="container-fluid">
      <router-link class="navbar-brand" tag="a" to="/">Home</router-link>

      <div>
        <ul class="navbar-nav me-auto mb-2 mb-md-0" v-if="!auth">
          <li class="nav-item">
            <router-link class="nav-link" aria-current="page" tag="a" to="/login">Login</router-link>
          </li>
          <li class="nav-item">
            <router-link class="nav-link" aria-current="page" tag="a" to="/register">Register</router-link>
          </li>
        </ul>

        <ul class="navbar-nav me-auto mb-2 mb-md-0" v-if="auth">
          <li class="nav-item">
            <router-link class="nav-link" aria-current="page" tag="a" to="/login" @click="logout">Logout</router-link>
          </li>
        </ul>

      </div>
    </div>
  </nav>
</template>

<script>
import {computed} from 'vue'
import {useStore} from "vuex";

export default {
name: "Nav",
  setup(){
    const store = useStore();
    const auth = computed(()=> store.state.authenticated)

    const logout = async ()=> {
      await fetch('http://localhost:5000/api/logout', {
        method: 'POST',
        headers: {'Content-Type': 'application/json'},
        credentials: 'include',
      })

      await store.dispatch('setAuth', false);

    }

    return {
      auth,
      logout
    }
  }
}
</script>

<style scoped>

</style>
