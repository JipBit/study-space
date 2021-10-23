<template>
  <div>
    <Navigation/>

    <NuxtChild/>
    <Pomodoro v-show="$route.path == '/app/pomodoro'"/>
  </div>
</template>

<script>
export default {};
</script>

<style>
  body{
    font-family: DM Sans, sans-serif;
    @apply bg-[#141518] md:mx-24 mx-6;
  }
</style>