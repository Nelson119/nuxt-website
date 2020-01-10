<template>
  <div class="container" role="content">
    <div>
      <!-- <logo /> -->
      <h1 class="title">
        <!-- nuxt-website -->
      </h1>
      <h2 class="subtitle">
        <!-- My beautiful Nuxt.js project --> 
      </h2>
      <p>
            <locales></locales>
        外送：<i class="active el-icon-shopping-bag-2"></i> 
        先繳訂金：<i class="active el-icon-money"></i>
        停車 ：<i class="active el-icon-guide"></i>
      </p>
      <el-row class="stores">
        <el-collapse v-model="activeNames">
          <el-col :xs="24" :sm="12" :md="6" v-for="(item,index) in stores" :key="index">
            <!-- <span></span> -->
              <el-collapse-item :title="item.name" :name="index">
                <div>
                  <el-row>
                    <el-col :xs="12" :sm="12" >日
                    </el-col>
                    <el-col :xs="12" :sm="12" >{{item.日}}
                    </el-col>
                    <el-col :xs="12" :sm="12" >一
                    </el-col>
                    <el-col :xs="12" :sm="12" >{{item.一}}
                    </el-col>
                    <el-col :xs="12" :sm="12" >二
                    </el-col>
                    <el-col :xs="12" :sm="12" >{{item.二}}
                    </el-col>
                    <el-col :xs="12" :sm="12" >三
                    </el-col>
                    <el-col :xs="12" :sm="12" >{{item.三}}
                    </el-col>
                    <el-col :xs="12" :sm="12" >四
                    </el-col>
                    <el-col :xs="12" :sm="12" >{{item.四}}
                    </el-col>
                    <el-col :xs="12" :sm="12" >五
                    </el-col>
                    <el-col :xs="12" :sm="12" >{{item.五}}
                    </el-col>
                    <el-col :xs="12" :sm="12" >六
                    </el-col>
                    <el-col :xs="12" :sm="12" >{{item.六}}
                    </el-col>
                    <el-col :xs="12" :sm="12" >類型：
                    </el-col>
                    <el-col :xs="12" :sm="12" >
                      {{item.類型}}
                    </el-col>
                    <el-col :xs="12" :sm="12" >米其林星：
                    </el-col>
                    <el-col :xs="12" :sm="12" >
                      <el-rate v-model="item.米其林星" disabled></el-rate>
                    </el-col>
                    <el-col :xs="24" :sm="24" >
                    </el-col>
                    <el-col :xs="12" :sm="12" >評價：
                    </el-col>
                    <el-col :xs="12" :sm="12" >
                      <el-rate v-model="item.評價" disabled></el-rate>
                    </el-col>
                    <el-col :xs="24" :sm="24">
                      <a target="blank" :href="'https://www.google.com/maps/@'+item.地理位子+',12z'"><i class="active el-icon-location"></i> </a>
                      <i v-if="item.外送 == '有'" class="active el-icon-shopping-bag-2"></i> 
                      <i v-if="item.先繳訂金 == '是'" class="active el-icon-money"></i> 
                      <i v-if="item.停車 == '有'" class="active el-icon-guide"></i> 
                    </el-col>
                  </el-row>
                </div>
                <!-- <div>Visual feedback: reflect current state by updating or rearranging elements of the page.</div> -->
              </el-collapse-item>
          </el-col>
        </el-collapse>
      </el-row>
    </div>
  </div>
</template>

<script>
// import Logo from '~/components/Logo.vue'
import Store from '~/components/Store.vue'
import locales from '../components/Locale';
const axios = require('axios');

export default {
  components: {
    locales,
    Store
  },
  data: () => {
    return {
      stores : [],
      activeNames: 0
    }
  },
  mounted: function(){
    var $this = this;
    axios.get('data.json').then((res) =>{
        // console.log(res.data)
        $this.stores = res.data;
      }).catch(function (error) {
        // handle error
        console.log(error);
      })
      .finally(function () {
        for(var i in $this.stores){
          $this.stores[i].serial = i*1+1;
        }
      });
  }
}
</script>

<style lang="scss">
 @import '../assets/scss/main.scss';
</style>