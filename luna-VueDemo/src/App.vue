<template>
  <div class="container">
    <Search></Search>
    <UsersMain></UsersMain>
  </div>
</template>

<script>
import Main from './components/Main'
import Search from './components/Search'
export default {
  components: {
    Search,
    UsersMain: Main
  }
}
</script>

<style>

</style>
