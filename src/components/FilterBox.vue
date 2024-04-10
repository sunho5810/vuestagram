<template>
  <div
    class="filter-item"
    :class="filterData"
    :style="{ backgroundImage: `url(${uploadDataURL})` }"
  >
    <!-- slot 1 : 
        props보다 더 직관적이고 번거로운 작업 없이 사용할 수 있다.
    -->
    <!-- slot 3 : 여러개
      name=""을 사용하여 구분해준다.
    -->
      <!-- slot 5 : slot props
        slot을 사용할 때 부모가 자식의 데이터를 필요로 할 때 사용
        slot에 :작명="데이터" 으로 바인딩 해서 부모에게 전달
      -->
    <!-- <slot name="a"></slot>
    <slot name="b"></slot> -->
    <slot></slot>
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
