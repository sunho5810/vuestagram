<template>
  <div>
    <div v-if="tabShowContent === 0">
      <Post v-for="(data, i) in dataList" :key="i" :data="data" />
    </div>

    <!-- 필터선택페이지 -->
    <div v-if="tabShowContent === 1">
      <div class="upload-image" :style="{backgroundImage: `url(${uploadDataURL})`}"></div>
      <div class="filters">
        <!-- slot 2 : 
          부모 컴포넌트 사이에 데이터를 넣으면 자식 컴포넌트에 만들어둔 slot안으로 삽입된다.
          태그 안에 데이터 바인딩 할 때만 사용 가능. 속성으로는X
          태그도 바인딩 가능!
        -->
        <FilterBox v-for="(item, i) in filterData" :key="i" :filterData="item" :uploadDataURL="uploadDataURL">
          <!-- slot 4 : 데이터 여러개를 slot으로 보낼 때
            template태그에 v-slot:지어준name 으로 보내준다.
          -->
          <!-- slot 5 : slot props 
            v-slot:default="작명"해서
            {{ 작명.데이터 }}로 받아서 사용한다.
          -->
          <!-- <template v-slot:a>데이터1</template>
            <template v-slot:b>데이터2</template> -->
            <span>{{ item }}</span>
        </FilterBox>
      </div>
    </div>

    <!-- 글작성페이지 -->
    <div v-if="tabShowContent === 2">
      <div class="upload-image" :style="{backgroundImage: `url(${uploadDataURL})`}"></div>
      <div class="write">
        <textarea class="write-box" @input="send">write!</textarea>
      </div>
    </div>
  </div>
</template>

<script>
import Post from "./Post.vue";
import FilterBox from "./FilterBox.vue";
import filterData from '../assets/filterData';

export default {
  name: "layout-container",
  data(){
    return {
      filterData: filterData,
    }
  },
  components: {
    Post,
    FilterBox,
  },
  props: {
    dataList: Array,
    tabShowContent: Number,
    uploadDataURL: String,
  },
  methods: {
    send(e){
      this.$emit('sendText', e.target.value);
    }
  }
};
</script>

<style lang="scss">
.upload-image{
width: 100%;
height: 450px;
background: cornflowerblue;
background-size : cover;
}
.filters{
overflow-x:scroll;
white-space: nowrap;
}
.filter-1 {
width: 100px;
height: 100px;
background-color: cornflowerblue;
margin: 10px 10px 10px auto;
padding: 8px;
display: inline-block;
color : white;
background-size: cover;
}
.filters::-webkit-scrollbar {
height: 5px;
}
.filters::-webkit-scrollbar-track {
background: #f1f1f1; 
}
.filters::-webkit-scrollbar-thumb {
background: #888; 
border-radius: 5px;
}
.filters::-webkit-scrollbar-thumb:hover {
background: #555; 
}
.write-box {
border: none;
width: 90%;
height: 100px;
padding: 15px;
margin: auto;
display: block;
outline: none;
}
</style>
