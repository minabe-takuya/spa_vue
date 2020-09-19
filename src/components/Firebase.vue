<template>
  <div>
    <h3>ファイヤーベースに送信</h3>
    <label for="name">ニックネーム</label>
    <input type="text" id="name" v-model="name">
    <br><br>
    <label for="comment">コメント</label>
    <textarea id="comment" v-model="comment"></textarea>
    <br><br>
    <button @click="createComment">コメントをサーバに送る</button>
    <h2>ファイヤーベースから受信</h2>
    <div v-for="post in posts" :key="post.name">
      <div>{{post.fields.comment.stringValue}}</div>
      <div>{{post.fields.name.stringValue}}</div>
    </div>
  </div>
</template>

<script>
import axios from 'axios'
export default {
  data(){
    return{
      name:"",
      comment:"",
      posts:[]
    }
  },
  //最初のロード時に読み込まれる
  created() {
    axios.get('https://firestore.googleapis.com/v1/projects/vuejs-http-af604/databases/(default)/documents/comments'
    )
        .then(response =>{
          this.posts = response.data.documents;
          console.log(response.data.documents);
        });
  },
  methods:{
    createComment(){
      axios.post('https://firestore.googleapis.com/v1/projects/vuejs-http-af604/databases/(default)/documents/comments',
          {
            fields:{
              name:{
                stringValue:this.name
              },
              comment:{
                stringValue: this.comment
              }
            }
          })
          .then(response =>{
            console.log(response);
          })
          .catch(error =>{
            console.log(error)
          });
      this.name="";
      this.comment = "";
    }
  }
}
</script>

<style scoped>

</style>