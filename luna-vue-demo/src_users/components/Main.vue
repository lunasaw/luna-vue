<template>
  <div>
    <h2 v-if="firstView">输入用户名搜索</h2>
    <h2 v-if="loading">Loading...</h2>
    <h2 v-if="errorMsg">{{errorMsg}}</h2>
    <div class="row">
      <div class="card" v-for="(user, index) in users" :key="index">
        <a :href="user.url" target="_blank">
          <img :src="user.avatar_url" style='width: 100px'/>
        </a>
        <p class="card-text">{{user.name}}</p>
      </div>
    </div>
  </div>
</template>

<script>
import axios from 'axios'
import PubSub from 'pubsub-js'

export default {
  data () {
    return {
      firstView: true,
      loading: false,
      users: null,
      errorMsg: ''
    }
  },
  name: 'Main',
  methods: {
    // 不在此发ajax请求 而是在点击search后
  },
  mounted () {
    // 订阅消息
    PubSub.subscribe('search', (msg, searchName) => {
      // 发送ajax请求
      const url = `https://api.github.com/search/users?q=${searchName}`
      // 更新状态(请求中)
      this.firstView = false
      this.loading = true
      this.users = null
      this.errorMsg = ''
      // 使用axios 发送ajax 请求
      axios.get(url).then(
        response => {
          const result = response.data
          // 得到用户组
          const users = result.items.map(item => ({
            url: item.html_url,
            avatar_url: item.avatar_url,
            name: item.login
          }))
          // 更新成功状态
          this.loading = false
          this.users = users
        }).catch(error => {
        // 更新为失败
        this.errorMsg = `更新失败:${error}`
        alert(`请求失败`)
      })
    })
  }
}
</script>

<style scoped>
  .card {
    float: left;
    width: 33.333%;
    padding: .75rem;
    margin-bottom: 2rem;
    border: 1px solid #efefef;
    text-align: center;
  }

  .card > img {
    margin-bottom: .75rem;
    border-radius: 100px;
  }

  .card-text {
    font-size: 85%;
  }
</style>
