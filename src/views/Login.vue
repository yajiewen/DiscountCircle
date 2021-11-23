<template>
  <div id = "login" class="column is-one-quarter is-offset-one-quarter" v-if="islogin == false">
    <form class="box">
      <div class="field">
        <label class="label">用户名</label>
        <div class="control">
          <input class="input" type="text" placeholder="用户名" v-model="username">
        </div>
      </div>

      <div class="field">
        <label class="label">密码</label>
        <div class="control">
          <input class="input" type="password" placeholder="********" v-model="password">
        </div>
      </div>

    </form>
    <button class="button is-primary" v-on:click="dologin">登陆</button>
  </div>

  <div id="login" v-if="islogin">
    <h2>这里是上传页面</h2>
  </div>
</template>

<script>
import axios from 'axios'
import JSEncrypt from 'jsencrypt'
export default {
  name: "login",
  data(){
    return{
      username: '',
      password: '',
      islogin: false,

      publicKey: 'MIGfMA0GCSqGSIb3DQEBAQUAA4GNADCBiQKBgQC5g5lPtRiiQX6U65RhOv7aipy7kMZQN0cQTim5HlzK7IApdLZIoPXozmhLHcdvcbOkw2nDJnuyYtWtY82rt3bkyOXylTrk6QrcMGZfPoil/T2s51NkFZYDIYUrJ+1Sz2/DyhIWxiIwMCPTUaRK83Bp0WAsdxIgmN0cR7C9gdwqvQIDAQAB'
    }
  },
  methods:{
    dologin(){
      let encryptor = new JSEncrypt()
      encryptor.setPublicKey(this.publicKey)

      let enUsername = encryptor.encrypt(this.username)
      let enPassword = encryptor.encrypt(this.password)

      let myAxios = new axios.create({
        headers: {
          'Content-Type': 'application/json'
        },
        transformRequest: [ function (data){
          data = JSON.stringify(data)
          return data;
        }]
      })

      let data = {
        'username': enUsername,
        'password': enPassword
      }
      myAxios.post('/api/login',data).then(res => {
        if(res.data == ''){
          alert("请重新登陆")
        }else{
          this.islogin = true
        }
      })

    }

  },
  created(){

  }
}
</script>

<style scoped>

</style>