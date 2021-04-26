<template>
<section>
  <div id="nav">
    <the-header></the-header>
    <router-view />
  </div>

</section>
</template>

<script>
import TheHeader from "./components/layout/TheHeader.vue"
export default {
  data(){
    return {}
  },
  components:{
    TheHeader
  }
}
</script>


<style>
@import url("https://fonts.googleapis.com/css2?family=Roboto:wght@400;700&display=swap");

* {
  box-sizing: border-box;
}

html {
  font-family: "Roboto", sans-serif;
}

body {
  margin: 0;
}
</style>
