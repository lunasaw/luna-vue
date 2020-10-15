<template>
  <div>
    <div v-if="!repoUrl">loading</div>
    <div v-else>most star repo is <a :href='repoUrl'>{{repoName}}</a></div>
  </div>
</template>

<script>
import axios from 'axios'
export default {
  data () {
    return {
      repoUrl: '',
      repoName: ''
    }
  },

  mounted () {
    // 发ajax请求
    const url = `https://api.github.com/search/repositories?q=v&sort=stars`
    this.$http.get(url).then(
      response => {
        const result = response.data
        // 得到第一个最受欢迎的repo
        const mostRepo = result.items[0]
        this.repoUrl = mostRepo.html_url
        this.repoName = mostRepo.full_name
      },
      response => {
        alert(`请求失败`)
      }
    )

    // // 使用axios 发送ajax 请求
    // axios.get(url).then(
    //   response => {
    //     const result = response.data
    //     // 得到第一个最受欢迎的repo
    //     const mostRepo = result.items[0]
    //     this.repoUrl = mostRepo.html_url
    //     this.repoName = mostRepo.full_name
    //   }).catch(error => {
    //   alert(`请求失败`)
    // })
  }
}
</script>

<style>

</style>
