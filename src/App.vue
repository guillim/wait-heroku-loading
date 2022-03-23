<script setup lang="ts">
import HelloWorld from "./components/HelloWorld.vue";
import Lien from "./components/Lien.vue";
</script>

<script lang="ts">
export default {
  data() {
    return {
      ready: false,
      count: 0,
      herokuUrl: import.meta.env.VITE_HEROKUURL,
      subtitle: import.meta.env.VITE_SUBTITLE,
      title: import.meta.env.VITE_TITLE,
      title: import.meta.env.VITE_BTN,
    };
  },
  methods: {
    async checkReady() {
      if (this.count > 30) return false;
      setTimeout(async () => {
        this.count++
        const response = await fetch(this.herokuUrl);
        console.log(response);
        if(response.status === 200){
          this.ready = true;
        }else if(response.status === 404){
          this.checkReady()
        }else{
          console.log('other problem');
          this.checkReady()
        }
      }, 5000);
    }
  },
  created(){
    this.checkReady()
  }
}
</script>

<template>
  <header>
    <img
      v-if="!ready"
      alt="Vue logo"
      class="logo"
      src="./assets/loader.gif"
      width="125"
      height="125"
    />
  </header>

  <main>
    <HelloWorld v-if="!ready" :msg=title :subtitle=subtitle />
    <Lien v-if="ready" :msg=btn :href=herokuUrl />
  </main>
</template>

<style>
@import "./assets/base.css";

#app {
  max-width: 1280px;
  margin: 0 auto;
  padding: 2rem;

  font-weight: normal;
}

header {
  line-height: 1.5;
}

.logo {
  display: block;
  margin: 0 auto 2rem;
}

a,
.green {
  text-decoration: none;
  color: hsla(160, 100%, 37%, 1);
  transition: 0.4s;
}

@media (hover: hover) {
  a:hover {
    background-color: hsla(160, 100%, 37%, 0.2);
  }
}

@media (min-width: 1024px) {
  body {
    display: flex;
    place-items: center;
  }

  #app {
    display: grid;
    grid-template-columns: 1fr 1fr;
    padding: 0 2rem;
  }

  header {
    display: flex;
    place-items: center;
    padding-right: calc(var(--section-gap) / 2);
  }

  header .wrapper {
    display: flex;
    place-items: flex-start;
    flex-wrap: wrap;
  }

  .logo {
    margin: 0 2rem 0 0;
  }
}
</style>
