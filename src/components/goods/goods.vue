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
        <div class="goods-content">
            <ul class="li-goods-list">
                <li v-for="(item,i) in goods" :key=i>
                    <h1 class="item-name">{{item.name}}</h1>
                    <ul >
                        <li v-for="(details,j) in item.foods" :key=j>
                            <div class="box">
                                <img :src="details.icon" alt="" class="icon">
                            </div>
                            <div class="pic-content">
                                <div class="name">{{details.name}}</div>
                                <div class="simple-name" v-show="details.description">{{details.description}}</div>
                                <div class="sale-count">
                                    <span class="count">月售{{details.sellCount}}份</span>
                                    <span class="rating">好评率{{details.rating}}</span>
                                </div>
                                <div class="price">
                                    <span class="now">￥{{details.price}}</span>
                                    <span class="old" v-show="details.oldPrice">￥{{details.oldPrice}}</span>
                                </div>
                            </div>
                        </li>
                    </ul>
                </li>
            </ul>
        </div>
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
            background: #f3f5f7;
            .goods-title-list{
                overflow: hidden;
                font-size:0;
                .goods-item{
                    height:54px;
                    line-height:14px;
                    display:table;
                    @include border-1px( rgba(7,17,27,0.1));
                    box-sizing: border-box;
                    padding:12px;
                    vertical-align: middle;
                    text-align: center;
                    width:100%;
                    .goods-type{
                        display:inline-block;
                        margin-top:1px;
                        width:12px;
                        height:12px;
                        background-size:12px 12px;
                        background-repeat: no-repeat;
                        @include icon-abstarct('decrease_3','guarantee_3','invoice_3','special_3','discount_3');
                    }
                    .goods-name{   
                        display:table-cell;
                        text-align: center;
                        vertical-align: middle;
                        font-size:12px;
                        font-weight:100;
                        color:black;
                        
                    }
                }
            }

        }
        .goods-content{
            .item-name{
                font-size:14px;
                line-height:14px;
                color:rgba(7,17,27,0.3);
                background:rgba(7,17,27,0.2);
                font-weight:600;
                padding-top:10px;
                padding-bottom:10px;
                padding-left:12px;
                
            }
            .box{
                display:inline-block;
                .icon{
                    width:72px;
                    height:72px;
                    padding-top:18px;
                    padding-left:18px;
                }
            }
            .pic-content{
                padding:18px 12px 18px 10px;
                display:inline-block;
                width:150px;
                .name{
                    font-size:14px;
                    margin-top:2px;
                    color:rgb(7,17,27);
                    line-height:14px;
                }
                .simple-name{
                    margin-top:8px;
                    font-size:10px;
                    color:rgb(147,153,159);
                    line-height: 10px;
                    padding:2px;
                    width:100%;
                    white-space: nowrap;
                    text-overflow: ellipsis;
                    overflow: hidden;
                }
                .sale-count{
                    font-size:0;
                    margin-top:8px;
                    .count{
                        font-size:10px;
                        color:rgb(147,153,159);
                        line-height: 10px;
                    }
                    .rating{
                        margin-left:12px;
                        font-size:10px;
                        color:rgb(147,153,159);
                        line-height: 10px;
                    }
                }
                .price{
                    margin-top:8px;
                    .now{
                        font-size:14px;
                        color:red;
                        font-weight:700;
                        line-height: 24px;

                    }
                    .old{
                        font-size:10px;
                        color:rgba(7,17,27,0.2);
                        font-weight:700px;
                        text-decoration: line-through;
                        margin-left:8px;
                    }
                }
            }

        }
    }
</style>