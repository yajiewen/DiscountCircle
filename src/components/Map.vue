<template>
  <div id="Map">

  </div>
  <div>
    zhongxin
    {{center}}
    {{city}}
    {{province}}
  </div>
</template>
<script>
import AMapLoader from '@amap/amap-jsapi-loader';
export default {
name: "Map",
  data(){
    return{
      center:'',
      city:'',
      province:'',
    }
  },
  methods:{

  },
  created(){
    AMapLoader.load({
      "key": "40163607020c4873795606a4f98b1074",                                          // 申请好的Web端开发者Key，首次调用 load 时必填
      "version": "1.4.15",                                // 指定要加载的 JSAPI 的版本，缺省时默认为 1.4.15
      "plugins": ['AMap.CitySearch','AMap.ToolBar'],                                      // 需要使用的的插件列表，如比例尺'AMap.Scale'等
      "AMapUI": {                                         // 是否加载 AMapUI，缺省不加载
        "version": '1.1',                               // AMapUI 缺省 1.1
        "plugins":[],                                   // 需要加载的 AMapUI ui插件
      },
      "Loca":{                                            // 是否加载 Loca， 缺省不加载
        "version": '1.3.2'                              // Loca 版本，缺省 1.3.2
      },
    }).then((AMap)=>{
      let map = new AMap.Map('Map', {
        resizeEnable: true,
        zoom: 13
      });

      this.center = map.getCenter()

      var citySearch = new AMap.CitySearch()
        citySearch.getLocalCity( (status, result) =>{
          if (status === 'complete' && result.info === 'OK') {
            console.log(result);
            this.city = result.city
            this.province = result.province
          }
        })

    }).catch(e => {
      console.log(e);
    })


  },
}
</script>

<style scoped>
#Map {width:300px; height: 180px; }
</style>