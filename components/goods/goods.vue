<template>
    <div class="goods-info">
        <div class="goods-title">
            <ul class="goods-title-list" >
                <li class="goods-item" v-for="(item,i) in goods" :key="i">
                    <span class="goods-type" v-show="item.type>0" :class="classMap[item.type]"></span>
                    <span class="goods-name">{{item.name}}</span>
                </li>
            </ul>
        </div>
        <div class="goods-content"></div>
    </div>
</template>

<script>
const ERR_OK=0;
export default {
    data(){
        return{
            goods:{},
            classMap:['decrease','discount','special','invoice','guarantee']
        }
    },
    props:{
        seller:{
            type:Object
        }
    },
    created(){
        this.$http.get('/api/goods').then((res)=>{
            if(res.body.errno===ERR_OK){
                this.goods=res.body.data;
            }
        })
    }
};
</script>

<style lang='scss' scoped>
@import '../../common/css/mixin.scss';
    .goods-info{
        position:absolute;
        top:179px;
        bottom:58px;
        display:flex;
        .goods-title{
            flex:0 0 80px;
            background: rgba(7,17,27,0.1);
            .goods-title-list{
                font-size:0;
                .goods-item{
                    padding:12px;
                    .goods-type{
                        display:inline-block;
                        width:12px;
                        height:12px;
                        background-size:12px 12px;
                        background-repeat: no-repeat;
                        @include icon-abstarct('decrease_3','guarantee_3','invoice_3','special_3','discount_3');
                    }
                    .goods-name{
                        font-size:12px;
                        font-weight:200;
                        
                    }
                }
            }

        }
        .goods-content{

        }
    }
</style>