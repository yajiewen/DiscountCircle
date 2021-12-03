<template>
  <div id = "login">
    <div class="columns">
      <div class="column is-one-quarter is-offset-one-quarter" v-if="islogin == false">
        <form class="box">
          <div class="field">
            <label class="label">用户名</label>
            <div class="control">
              <input class="input" type="text" placeholder="用户名" v-model="username" onkeyup="this.value=this.value.replace(/[^\w_]/g,'');" maxlength="20">
            </div>
          </div>

          <div class="field">
            <label class="label">密码</label>
            <div class="control">
              <input class="input" type="password" placeholder="********" v-model="password" maxlength="20">
            </div>

          </div>

        </form>

          <button class="button is-primary" v-on:click="dologin">登陆</button>


      </div>

      <div class="column">
        <div v-if="islogin" class="content column is-6 is-offset-3">

          <div class="field">
            <label class="label">商店名字(必填)</label>
            <div class="control">
              <input class="input" type="text" placeholder="商店名字" v-model="storename" maxlength="100">
            </div>
          </div>

          <div class="field">
            <label class="label">省份(必填)</label>
            <div class="control">
              <input class="input" type="text" placeholder="省份" v-model="province" maxlength="30">
            </div>
          </div>

          <div class="field">
            <label class="label">市/州</label>
            <div class="control">
              <input class="input" type="text" placeholder="市/州" v-model="city" maxlength="30">
            </div>
          </div>

          <div class="field">
            <label class="label">县</label>
            <div class="control">
              <input class="input" type="text" placeholder="县" v-model="county" maxlength="30">
            </div>
          </div>

          <div class="field">
            <label class="label">街道/乡镇(必填)</label>
            <div class="control">
              <input class="input" type="text" placeholder="街道/乡镇" v-model="street" maxlength="30">
            </div>
          </div>

          <div class="field">
            <label class="label">优惠信息</label>
            <div class="control">
              <textarea class="textarea is-info" placeholder="优惠信息" v-model="disdetail" maxlength="200"></textarea>
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
          <button :class="{'is-loading':isloading}" class="button is-primary" v-on:click="upload">上传</button>
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
      storename:'',
      disdetail:'',

      updata: new FormData(),

      publicKey: 'MIGfMA0GCSqGSIb3DQEBAQUAA4GNADCBiQKBgQC5g5lPtRiiQX6U65RhOv7aipy7kMZQN0cQTim5HlzK7IApdLZIoPXozmhLHcdvcbOkw2nDJnuyYtWtY82rt3bkyOXylTrk6QrcMGZfPoil/T2s51NkFZYDIYUrJ+1Sz2/DyhIWxiIwMCPTUaRK83Bp0WAsdxIgmN0cR7C9gdwqvQIDAQAB',
      imageFileNameList:[],

      placeholderr: {
        img1: '选择文件',
        img2: '选择文件',
        img3: '选择文件',
        img4: '选择文件',
        img5: '选择文件',
        img6: '选择文件'
      },
      imgstyle: ['jpg', 'jpeg', 'png',], //可上传的图片格式
      isloading:false,

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
        this.updata.append("images[]",files[0])
      } else {
        this.placeholderr[imagename] = '请选择文件'
        alert('文件格式不正确')
      }
    },
    upload() {
      this.isloading = true
      if (this.username != '' && this.province != '' &&  this.street != '' && this.storename != '') {
        this.updata.append('username', this.username)
        this.updata.append('storename', this.storename)
        this.updata.append('province', this.province)
        this.updata.append('city', this.city)
        this.updata.append('county', this.county)
        this.updata.append('street', this.street)
        this.updata.append('disdetail', this.disdetail)

        let myAxios = new axios.create({
          headers: {
            'Content-Type': 'multipart/form-data'
          },
          transformRequest: [function (data) {
            return data;
          }]
        })

        myAxios.post("/api/uploadstore", this.updata).then(res => {

          if (res.data != "请重新登陆") {
            alert("上传成功")
            location.reload()
            this.isloading = false
          } else if(res.data == "请重新登陆"){
            alert("请重新登陆")
            location.reload()
            this.isloading = false
            this.islogin = false
          }
        })
      }else{
        alert("信息不完整")
        this.isloading = false
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
      if(res.data == '请重新登陆'){
        this.islogin = false
      }else{
        this.username = res.data
        this.islogin = true
      }
    })
  }
}
</script>

<style scoped>

</style>