<template>
  <div
    class="filter-item"
    :class="filterData"
    :style="{ backgroundImage: `url(${uploadDataURL})` }"
  >
    {{ filterData }}
  </div>
</template>

<script>
export default {
  name: "FilterBox",
  props: {
    uploadDataURL: String,
    filterData: String,
  },
};
</script>

<style>
.filter-item {
  display: inline-flex;
  justify-content: center;
  align-items: center;
  width: 100px;
  height: 100px;
  margin: 10px 10px 10px auto;
  padding: 8px;
  color: white;
  background-size: cover;
  background-position: center;
}
</style>
