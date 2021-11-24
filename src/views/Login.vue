<template>
  <div id = "login">
    <div class="columns">
      <div class="column is-one-quarter is-offset-one-quarter" v-if="islogin == false">
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

      <div class="column">
        <div v-if="islogin" class="content column is-6 is-offset-3">

          <div class="field">
            <label class="label">省份</label>
            <div class="control">
              <input class="input" type="text" placeholder="省份" v-model="province">
            </div>
          </div>

          <div class="field">
            <label class="label">市/州</label>
            <div class="control">
              <input class="input" type="text" placeholder="市/州" v-model="city">
            </div>
          </div>

          <div class="field">
            <label class="label">县</label>
            <div class="control">
              <input class="input" type="text" placeholder="县" v-model="county">
            </div>
          </div>

          <div class="field">
            <label class="label">街道/乡镇</label>
            <div class="control">
              <input class="input" type="text" placeholder="街道/乡镇" v-model="street">
            </div>
          </div>


          <div class="columns ">
            <div class="column">
              <div class="file has-name is-boxed">
                <label class="file-label">
                  <input class="file-input" type="file" name="resume" v-on:change="getFile($event,'img1')">
                  <span class="file-cta">
                <span class="file-icon">
                  <i class="fas fa-upload"></i>
                </span>
                <span class="file-label">
                  选择一张照片
                </span>
            </span>
                  <span class="file-name">
                    {{placeholderr.img1}}
                  </span>
                </label>
              </div>
            </div>

            <div class="column">
              <div class="file has-name is-boxed">
                <label class="file-label">
                  <input class="file-input" type="file" name="resume" v-on:change="getFile($event,'img2')">
                  <span class="file-cta">
                <span class="file-icon">
                  <i class="fas fa-upload"></i>
                </span>
                <span class="file-label">
                  选择一张照片
                </span>
            </span>
                  <span class="file-name">
                    {{placeholderr.img2}}
                  </span>
                </label>
              </div>
            </div>

            <div class="column">
              <div class="file has-name is-boxed">
                <label class="file-label">
                  <input class="file-input" type="file" name="resume" v-on:change="getFile($event,'img3')">
                  <span class="file-cta">
                <span class="file-icon">
                  <i class="fas fa-upload"></i>
                </span>
                <span class="file-label">
                  选择一张照片
                </span>
            </span>
                  <span class="file-name">
                    {{placeholderr.img3}}
                  </span>
                </label>
              </div>
            </div>

            <div class="column">
              <div class="file has-name is-boxed">
                <label class="file-label">
                  <input class="file-input" type="file" name="resume" v-on:change="getFile($event,'img4')">
                  <span class="file-cta">
                <span class="file-icon">
                  <i class="fas fa-upload"></i>
                </span>
                <span class="file-label">
                  选择一张照片
                </span>
            </span>
                  <span class="file-name">
                    {{placeholderr.img4}}
                  </span>
                </label>
              </div>
            </div>

            <div class="column">
              <div class="file has-name is-boxed">
                <label class="file-label">
                  <input class="file-input" type="file" name="resume" v-on:change="getFile($event,'img5')">
                  <span class="file-cta">
                <span class="file-icon">
                  <i class="fas fa-upload"></i>
                </span>
                <span class="file-label">
                  选择一张照片
                </span>
            </span>
                  <span class="file-name">
                    {{placeholderr.img5}}
                  </span>
                </label>
              </div>
            </div>

            <div class="column">
              <div class="file has-name is-boxed">
                <label class="file-label">
                  <input class="file-input" type="file" name="resume" v-on:change="getFile($event,'img6')">
                  <span class="file-cta">
                <span class="file-icon">
                  <i class="fas fa-upload"></i>
                </span>
                <span class="file-label">
                  选择一张照片
                </span>
            </span>
                  <span class="file-name">
                    {{placeholderr.img6}}
                  </span>
                </label>
              </div>
            </div>

          </div>
          <button class="button is-primary" v-on:click="upload">上传</button>
        </div>
      </div>

    </div>
  </div>
</template>

<script>
import axios from 'axios'
import JSEncrypt from 'jsencrypt'
import * as imageConversion from "image-conversion";
export default {
  name: "login",
  data(){
    return{
      username: '',
      password: '',
      islogin: false,

      province:'',
      city:'',
      county:'',
      street:'',

      updata: new FormData(),

      publicKey: 'MIGfMA0GCSqGSIb3DQEBAQUAA4GNADCBiQKBgQC5g5lPtRiiQX6U65RhOv7aipy7kMZQN0cQTim5HlzK7IApdLZIoPXozmhLHcdvcbOkw2nDJnuyYtWtY82rt3bkyOXylTrk6QrcMGZfPoil/T2s51NkFZYDIYUrJ+1Sz2/DyhIWxiIwMCPTUaRK83Bp0WAsdxIgmN0cR7C9gdwqvQIDAQAB',
      placeholderr: {
        img1: '选择文件',
        img2: '选择文件',
        img3: '选择文件',
        img4: '选择文件',
        img5: '选择文件',
        img6: '选择文件'
      },
      imgstyle: ['jpg', 'jpeg', 'png',], //可上传的图片格式
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
    },

    getFile(event,imagename){
      let files = event.target.files
      this.placeholderr[imagename] = files[0].name //获取文件名字

      if (this.imgstyle.includes(this.placeholderr[imagename].split('.').pop())) {
        // 开始压缩图片
        imageConversion.compress(files[0], 0.6).then(res => {
          this.updata.append(imagename,res)
        })
      } else {
        this.placeholderr[imagename] = '请选择文件'
        alert('文件格式不正确')
      }
    },
    upload(){
      if(this.username !='' && this.province!='' && this.city!='' && this.county!='' && this.street!=''){

      }else{
        alert("请重新填写")
      }
    }

  },
  created(){
    let myAxios = new axios.create({
      headers: {
        'Content-Type': 'application/json'
      },
      transformRequest: [ function (data){
        data = JSON.stringify(data)
        return data;
      }]
    })

    myAxios.get('/api/islogin').then(res => {
      if(res.data != true){
        alert(res.data)
        this.islogin = false
      }else{
        this.islogin = true
      }
    })
  }
}
</script>

<style scoped>

</style>