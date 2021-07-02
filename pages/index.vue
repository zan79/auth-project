<template>
  <div>
    <NavBar />
    <div class="container mt-5">
      <h1 class="text-warning text-center pt-5">Welcome to the page</h1>

      <h3 class="text-light text-center mt-5" v-if="$auth.loggedIn">
      {{$auth.user.name}}
      </h3>

      <h2 class="text-secondary text-center mt-5">
        Have a nice day =)
      </h2>
    </div>
    
  </div>
</template>

<script>
export default {
  auth: false
}
</script>

<style>
body{
  background-color: #212121;
}
</style>