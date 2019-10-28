<template>
  <div id="app">
   <div v-for="(user ,index) in users" :key="index">
    <div style="float: left; width: 220px;height: 220px;">
      <img :src="user.avatar_url" alt="" style="float: left; width: 200px;height: 200px;">
      <p>{{user.login}}</p>
    </div>
   </div>
  </div>
</template>

<script>
import axios from 'axios'
export default {
  data: function () {
    return {
      users:null
    }
  },
  mounted: function () {
    const url = 'https://api.github.com/search/users?q=v'
    axios.get(url).then(
      response => {
        const result = response.data
        const users = result.items.map(item =>({
                 url:item.html_url,
                 avatar_url:item.avatar_url,
          login:item.login
        }))
        this.users = users
      }
    ).catch(Error => {
      alert('hehe')
    })
  }

}
</script>

<style>

</style>
