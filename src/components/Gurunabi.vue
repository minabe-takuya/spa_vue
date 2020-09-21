<template>
  <div>
    <div>
      <h3>近くの飲食店を検索できます</h3>
      <input type="text" id="name" v-model="name" placeholder="店名"><br>
      <p v-if="name">
        <button @click="searchShop" class="shop-get-button">検索</button>
      </p>
      <input type="text" id="freeWord" v-model="freeWord" placeholder="フリーワード"><br>
      <p v-if="freeWord">
        <button @click="searchFree" class="shop-get-button">検索</button>
      </p>
      <hr>
    </div>
    <h3>検索結果を表示</h3>
    <div v-for="info in shopInfo" :key="info.id">
      <div class="main-block">
        <div class="top-block">
          <div class="side-pic">
            <a :href="info.url" target="_blank">
              <img :src=info.image_url.shop_image1 alt="">
            </a>
          </div>
          <div class="comment-area">
            <h3>{{info.name}}</h3>
            <p><b>{{info.address}}</b></p>
            <p><b>{{info.tel}}</b></p>
            <p><b>{{info.opentime}}</b></p>
          </div>
        </div>
        <div class="pr-comment">
          <p>{{info.pr.pr_long}}</p>
          <button :href=info.url target="_blank" class="shop-get-button">お店の予約</button>
        </div>
      </div>
    </div>
  </div>
</template>

<script>
import axios from 'axios'
export default {
  data(){
    return{
      name:'',//入力値から取得
      freeWord:'',//入力値から取得
      baseurl:'https://api.gnavi.co.jp/RestSearchAPI/v3/?',
      id:'keyid=19ae9e3136cd8d5d7f0424a567690e36',
      shopInfo:[],
    }
  },
  methods:{
    searchShop:function(){
        let url= this.baseurl + this.id + '&name=' + this.name;
        axios.get(url)
      .then(function (response) {
          this.shopInfo = response.data.rest
        }.bind(this))
          .catch(function (error) {
            console.log(error);
            alert('検索結果は見つかりませんでした');
          })
    },
    searchFree:function(){
      let url1= this.baseurl + this.id + '&freeword=' + this.freeWord;
      axios.get(url1)
          .then(function (response) {
            this.shopInfo = response.data.rest
          }.bind(this))
          .catch(function (error) {
            console.log(error);
            alert('検索結果は見つかりませんでした');
          })
    },
  },
}
</script>

<style scoped>
.shop-get-button{
  position: relative;
  display: inline-block;
  padding:0.25em 0.5em;
  text-decoration: none;
  color:#fff;
  background: #fd9535;
  border-radius: 4px;
  -moz-border-radius: 4px;
  -webkit-border-radius: 4px;
  box-shadow: inset 0 2px 0 rgba(255,255,255,0.2),inset 0 -2px 0 rgba(0,0,0,0.05);
  -moz-box-shadow: inset 0 2px 0 rgba(255,255,255,0.2),inset 0 -2px 0 rgba(0,0,0,0.05);
  -webkit-box-shadow: inset 0 2px 0 rgba(255,255,255,0.2),inset 0 -2px 0 rgba(0,0,0,0.05);
  font-weight:bold;
  border: solid 2px #d27d00;
}
.shop-get-button:active{
  box-shadow: 0 0 2px rgba(0,0,0,0.30);
  -moz-box-shadow: 0 0 2px rgba(0,0,0,0.30);
  -webkit-box-shadow: 0 0 2px rgba(0,0,0,0.30);
}
.main-block{
  background: #fff;
  width:960px;
  margin:100px auto;
  border: 0.5px solid #2c3e50;
}
.top-block{
  overflow: hidden;
}
.side-pic{
  width:30%;
  float: left;
}
.side-pic:hover{
  cursor: pointer;
}
.comment-area{
  width:70%;
  box-sizing: border-box;
  padding:29px;
  float:left;
  text-align: left;
}
.pr-comment{
  width:100%;
  box-sizing: border-box;
  padding:20px;
  background: #f6f5f4;
}
input[type="text"]{
  width:30%;
  padding:10px;
  border: .5px solid #2c3e50;
}
</style>