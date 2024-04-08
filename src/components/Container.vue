<template>
  <div>
    <Post v-for="(data, i) in dataList" :key="i" :data="data"/>
    <!-- <Post />
    <Post /> -->
  </div>
</template>

<script>
import Post from './Post.vue'

export default {
    name: "layout-container",
    components: {
        Post,
    },
    props:{
      dataList: Array,
    }
};
</script>

<style></style>
