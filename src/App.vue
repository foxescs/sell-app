<template>
  <div >
    <v-header :seller='seller'></v-header>
    <div class="tab border-1px" >
      <div class="tab-item">
        <router-link :to="'goods'">
          商品
        </router-link>
      </div>
      <div class="tab-item">
        <router-link :to="'ratings'">
          评价
        </router-link>
      </div>
      <div class="tab-item">
        <router-link :to="'seller'">
          商家
        </router-link>
      </div>
    </div>
    <router-view>
      <!-- 刷新链接，他会替换这么链接替换的一部分 -->
    </router-view>
  </div>
</template>

<script>
  import header from './components/header/header.vue';

  const ERR_OK=0;

  export default{
    data(){
      return {
        seller:{}
      }
    },
    created(){
      this.$http.get('/api/seller').then((response)=>{
        if(response.body.errno===ERR_OK){
          this.seller = response.body.data;
        }
      })
    },
    components:{
      'v-header':header
    }
  };
</script>

<style lang='scss' scoped>
  @import './common/css/mixin.scss';

  .tab{
    display:flex;
    height:40px;
    width:100%;
    line-height:40px;
    // border-bottom:1px solid rgba(7,17,27,0.1);
    @include border-1px(rgba(7,17,27,0.1));
    .tab-item{
      flex:1;
      text-align:center;
      a{
        color:rgb(77,85,93);
        text-decoration: none;
        &.active{
          color:rgb(240,20,20)
        }
      }
    }
  }
</style>
