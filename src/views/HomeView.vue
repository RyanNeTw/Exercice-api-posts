<template>
  <div>
    <p>List posts</p>
  </div>
  <Posts />
</template>

<script>
import Posts from "@/components/Posts.vue";
export default {
  name: "HomeView",
  components: {
    Posts,
  },
};
</script>

<style scoped>
div {
  display: flex;
  justify-content: center;
  align-items: center;
}

p {
  font-size: 2rem;
  font-family: "Roboto", sans-serif;
  margin:20px 0px 20px 0px;
}
</style>
