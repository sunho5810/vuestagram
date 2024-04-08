<template>
  <div class="header">
    <ul class="header-button-left">
      <li>Cancel</li>
    </ul>
    <ul class="header-button-right">
      <li v-if="tabShowContent === 1" @click="tabShowContent++">Next</li>
      <li v-if="tabShowContent === 2" @click="publish">발행</li>
    </ul>
    <img src="./assets/logo.png" class="logo" />
  </div>
  <button v-for="(tabs, i) in tabsList" :key="i" @click="tabFunc(i)">
    {{ tabs }}
  </button>

  <Container
    :dataList="dataList"
    :tabShowContent="tabShowContent"
    :uploadDataURL="uploadDataURL"
    @sendText="getText($event)"
  />

  <button @click="moreView">더보기</button>

  <div class="footer">
    <ul class="footer-button-plus">
      <!-- input multiple : multiple 속성을 넣으면 여러개를 input으로 받아올 수 있음 -->
      <input @change="upload" type="file" id="file" class="inputfile" />
      <label for="file" class="input-plus">+</label>
    </ul>
  </div>
</template>

<script>
import Container from "./components/Container.vue";
import dataList from "./assets/data";

/* ajax width axios 1 : 개념
  server - 데이터 요청하면 주는 곳
  get - url을 이용해 서버에서 데이터를 가져오는 요청
  post - url을 이용해 서버로 데이터를 보내는 요청
  ajax - get과 post를 하면 브라우저가 무조건 새로고침 되는데 ajax를 이용하면
        새로고침 없이 get과 post를 사용할 수 있음
*/
/* ajax width axios 2 : 
  ajax요청을 하려면?
  1. axios 라이브러리 사용 
  2. 기본 fetch api함수 사용
  두 방법이 흡사 하지만 fetch는 브라우저에서 지원해주는 기능이라
  대부분 axios라이브러리를 사용
*/
/* axios 1 : import axios from 'axios'로 선언 */
import axios from "axios";

export default {
  name: "App",
  data() {
    return {
      dataList: dataList,
      tabsList: ["POST", "FILTERS", "WRITE"],
      tabShowContent: 0,
      getCount: 0,
      uploadDataURL: "",
      recText: "",
    };
  },
  methods: {
    moreView() {
      /* axios 2 : 
      get - 선언한 axios를 이용하여 axios.get(url)로 가져온다.
      post - 선언한 axios를 이용하여 axios.post(url)로 보내준다.
      성공 시 실행할 코드는 .then(콜백함수)를 이용한다.
      실패 시 실행할 코드는 .catch(콜백함수)를 이용한다.
     */
      axios
        .get(`https://codingapple1.github.io/vue/more${this.getCount % 2}.json`)
        /* function(){}과 ()=>{} (익명함수)의 차이
        function의 this는 함수 안에서 재정의 해주지만
        ()=>{}의 this는 기존에 쓰던 this를 사용한다.
        따라서 뷰에서는 익명함수를 쓰는것을 더 권장한다.
      */
        .then((result) => {
          // console.log("성공!!", result.data);
          /* push - 배열에 데이터 삽입 */
          this.dataList.push(result.data);
          this.getCount++;
        });
    },
    tabFunc(idx) {
      this.tabShowContent = idx;
    },
    upload(e) {
      let files = e.target.files;
      // console.log("files?", files[0]);
      /* file upload 1 : 이미지 업로드 한걸 보여주려면?
        1. FileReader()
        2. URL.createObjectURL()
      */
      /* URL.createObjectURL() : 대상의 url을 blob 데이터로 가져옴 */
      let url = URL.createObjectURL(files[0]);
      // console.log("url?", url);
      this.uploadDataURL = url;
      this.tabShowContent = 1;
    },
    getText(str){
      this.recText = str;
    },
    publish() {
      var myPost = {
        name: "Ju Sunho",
        userImage: "https://picsum.photos/100?random=3",
        postImage: this.uploadDataURL,
        likes: 777,
        date: "April 9",
        liked: false,
        content: this.recText,
        filter: "perpetua",
      };
      this.dataList.unshift(myPost);
      this.tabShowContent = 0;
    },
  },
  components: {
    Container,
  },
};
</script>

<style lang="scss">
body {
  margin: 0;
}
ul {
  padding: 5px;
  list-style-type: none;
}
.logo {
  width: 22px;
  margin: auto;
  display: block;
  position: absolute;
  left: 0;
  right: 0;
  top: 13px;
}
.header {
  width: 100%;
  height: 40px;
  background-color: white;
  padding-bottom: 8px;
  position: sticky;
  top: 0;
}
.header-button-left {
  color: skyblue;
  float: left;
  width: 50px;
  padding-left: 20px;
  cursor: pointer;
  margin-top: 10px;
}
.header-button-right {
  color: skyblue;
  float: right;
  width: 50px;
  cursor: pointer;
  margin-top: 10px;
}
.footer {
  width: 100%;
  position: sticky;
  bottom: 0;
  padding-bottom: 10px;
  background-color: white;
}
.footer-button-plus {
  width: 80px;
  margin: auto;
  text-align: center;
  cursor: pointer;
  font-size: 24px;
  padding-top: 12px;
}
.sample-box {
  width: 100%;
  height: 600px;
  background-color: bisque;
}
.inputfile {
  display: none;
}
.input-plus {
  cursor: pointer;
}
#app {
  box-sizing: border-box;
  font-family: "consolas";
  margin-top: 60px;
  width: 100%;
  max-width: 460px;
  margin: auto;
  position: relative;
  border-right: 1px solid #eee;
  border-left: 1px solid #eee;
}
</style>
