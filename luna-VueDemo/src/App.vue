<template>
  <div>
    <header class="site-header jumbotron">
    <div class="container">
      <div class="row">
        <div class="col-xs-12">
          <h1>请发表对Vue的评论</h1>
        </div>
      </div>
    </div>
    </header>
    <div class="container">
      <Add></Add>
      <List></List>
    </div>
  </div>
</template>

<script>
import Add from './comporents/Add.vue'
import List from './comporents/List.vue'

export default {
  name: 'App',
  components: {
    Add,
    List
  }
}
</script>

<style scoped>

</style>
