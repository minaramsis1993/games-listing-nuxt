<template>
  <div>
    <AppHeader />
    <Nuxt />
  </div>
</template>

<script>
import AppHeader from "../components/AppHeader";
export default {
  name: "Default",
  components: {
    AppHeader
  }
};
</script>

<style>
:root {
  --primary-color: #572589;
  --border-color: #e0e0e0;
}
body {
  font-family: "Tajawal", sans-serif;
  letter-spacing: 0.02rem;
  background: #f5f5f5;
}
</style>
