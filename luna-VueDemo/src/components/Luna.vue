<template>
  <div>
    <p class="msg">{{msg}}</p>
  </div>
</template>

<script>
export default {// 配置对象与Vue一致
  name: 'Luna',
  data () {
    return {
      msg: "Hello Luna I'm Vue"
    }
  }
}
</script>

<style scoped>
  .msg {
    color: #42b983;
    font-size: 30px;
  }
</style>
