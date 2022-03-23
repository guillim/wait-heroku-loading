<script setup lang="ts">
defineProps<{
  msg: string;
  href: string;
}>();
</script>

<template>
  <div class="greetings">
    <a class="greetings" :href=href>{{ msg }}</a>
  </div>
</template>

<style scoped>
a {
  font-size: 1.2rem;
  padding: 10px;
  border: white solid;
}


.greetings a {
  text-align: center;
}

@media (min-width: 1024px) {
  .greetings a {
    text-align: left;
  }
}
</style>
