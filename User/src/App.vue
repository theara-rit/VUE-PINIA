<template>
<div class="container">
    <user-view></user-view>
</div>
</template>

<script>
import UserView from "@/components/UserView.vue"

export default({ 
  components:{
    "user-view" : UserView,
  }
})
</script>
<style>
#app {
  font-family: Avenir, Helvetica, Arial, sans-serif;
  -webkit-font-smoothing: antialiased;
  -moz-osx-font-smoothing: grayscale;
  color: #2c3e50;
}

body{
  margin: 0;
  padding: 0;
}
.container{
  width: 40%;
  margin: auto;
}
</style>
