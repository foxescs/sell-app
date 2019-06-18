<template>
    <div class="head-wrapper">
        <div class="content-wrapper ">
            <div class="avatar">
                <img :src="seller.avatar" alt="" width="64px" height="64px" >
            </div>
            <div class="dec">
                <div class="top-dec">
                    <span class='dec-logo'></span>
                    <span class='dec-title'>{{seller.name}}</span>
                </div>
                <div class="mid-dec">
                    <span>{{seller.description}}/{{seller.deliveryTime}}分钟送达</span>
                </div>
                <div class="bottom-dec" v-if='seller.supports'>
                    <span class='support-type' :class="classMap[seller.supports[0].type]"></span>
                    <span class='support'>{{seller.supports[0].description}}</span>
                </div>
            </div>
            <div class="count" v-if="seller.supports" @click="showDetail()">
                <span>{{seller.supports.length}}个</span>
                <i class="icon-keyboard_arrow_right"></i>
            </div>
        </div>
        <div class="bulletin-wrapper">
            <span class="dec-logo"></span>
            <span class="dec-content">{{seller.bulletin}}</span>
            <i class="icon-keyboard_arrow_right"></i>
        </div>
        <div class="background">
            <img :src="seller.avatar" alt="">
        </div>
        <div class="detail" v-show="flag">
            <div class="wrapper">
                <div class="content">
                    <h1 class="name">{{seller.name}}</h1>
                    <stars :size="48" :score="seller.score" class="detail-star"></stars>
                    <div class="special-info" v-show="seller.supports">
                        <div class="seperate" >
                            <span class="left-seperate"></span>
                            <span class="info">优惠信息</span>
                            <span class="right-seperate"></span>
                        </div>
                        <div class="wrapper">
                            <div class="seperate-info" v-for="(item,i) in seller.supports" :key=i >
                                <span :class="classMap[item.type]" class="type-item"></span>
                                <span class="text-info">{{item.description}}</span>
                            </div>
                        </div>
                    </div>
                    <div class="bulletin-info">
                        <div class="seperate">
                            <span class="left-seperate"></span>
                            <span class="info">商家公告</span>
                            <span class="right-seperate"></span>
                        </div>
                        <div class="seperate-info">{{seller.bulletin}}</div>
                    </div>
                </div>
            </div>
            <div class="close">
                <i class="icon-close"></i>
            </div>
        </div>
    </div>
</template>

<script>
import stars from "../stars/stars.vue";

export default {
    data(){
        return {
            flag:false,
            classMap:['decrease','discount','spacial','invoice','guarantee']
        }
    },
    methods:{
        showDetail(){
            this.flag=!this.flag;
        }
    },
    props:{
        seller:{
            type:Object
        }
    },
    components:{
        stars
    }
};
</script>

<style lang='scss' scoped>
@import '../../common/css/mixin.scss';

.head-wrapper{
    position:relative;
    overflow: hidden;
    .content-wrapper{
        background-color:rgba(0,0,0,0.2);
        padding:24px 12px 18px 24px;
        font-size:0;
        position:relative;
        .avatar{
            margin-left:16px;
            display:inline-block;
            border-radius: 2px;
        }
        .dec{
            display:inline-block;
            padding-left:16px;
            font-size:14px;
            .top-dec{
                padding:2px 0 8px 0;
                .dec-logo{
                    display:inline-block;
                    width:30px;
                    height:18px;
                    @include bg-image('brand');
                    background-size:30px 18px;
                }
                .dec-title{
                    padding-left:6px;
                    color:rgb(255,255,255);
                    font-weight:bold;
                    line-height:18px;
                    font-size:16px;
                }
            }
            .mid-dec{
                margin-bottom:10px;
                font-size:12px;
                color:rgb(255,255,255);
                line-height:12px;
            }
            .bottom-dec{
                margin-bottom:2px;
                .support-type{
                    display:inline-block;
                    width:12px;
                    height:12px;
                    background-size:12px 12px;
                    background-repeat:no-repeat;
                    &.decrease{
                        @include bg-image('decrease_1')
                    }
                    &.guarantee{
                        @include bg-image('guarantee_1')
                    }
                    &.invoice{
                        @include bg-image('invoice_1')
                    }
                    &.spacial{
                        @include bg-image('special_1')
                    }
                    &.discount{
                        @include bg-image('discount_1')
                    }
                }
                
                .support{
                    display:inline-block;
                    margin-left:4px;
                    font-size:10px;
                    line-height:12px;
                    font-weight:100;
                    color:white;
                    vertical-align: top;
                }
            }
        }
        .count{
            padding:7px 8px 7px 8px;
            position:absolute;
            right:12px;
            bottom:18px;
            height:10px;
            font-size:10px;
            color:white;
            font-weight:100;
            line-height:10px;
            background-color:rgba(0,0,0,0.2);
            border-radius: 14px;
            vertical-align: center;
            span{
                display:inline-block;
                margin-right:2px;
            }
            i{
                display:inline-block;
            }
        }
    }
    .bulletin-wrapper{
        padding:0 12px;
        overflow: hidden;
        text-overflow: ellipsis;
        white-space: nowrap;
        background-color:rgba(7,17,27,0.5);
        padding-right:21px;
        color:white;
        position: relative;
        .dec-logo{
            @include bg-image('bulletin');
            width:22px;
            height:12px;
            background-size:22px 12px;
            background-repeat: no-repeat;
            display:inline-block;
            margin-top:8px;
        }
        .dec-content{
            font-size:10px;
            color:white;
            line-height:28px;
            margin-left:4px;
            font-weight:100;
            vertical-align: top; 
        }
        .icon-keyboard_arrow_right{
            position:absolute;
            right:12px;
            bottom:5px;
        }
    }
    .background{
        width:100%;
        height:100%;
        position:absolute;
        left:0;
        top:0;
        z-index:-1;
        img{
            filter:blur(10px);
            background-size:100% 100%;
            width:100%;
            height:100%;
        }
    }
    .detail{
        position:fixed;
        background-color:rgba(7,17,27,0.8);
        overflow:auto;
        left:0;
        top:0;
        width:100%;
        height:100%;
        .wrapper{
            min-height:100%;
            .content{
                margin-top:64px;
                padding-bottom:64px;
                color:white;
                .name{
                    font-size:16px;
                    height:16px;
                    font-weight:700;
                    color:white;
                    text-align:center;
                }
                .detail-star{
                    text-align: center;
                    margin-top:16px;
                }
                .special-info{
                    padding:28px 36px 24px 36px;
                    .seperate{
                        font-size:0;
                        .left-seperate{
                            display:inline-block;
                            height:0;
                            border-bottom:1px solid rgba(225,225,225,0.2);
                            width:112px;
                            margin-right:12px;
                            margin-bottom:9px;
                        }
                        .info{
                            display:inline-block;
                            font-weight:500;
                            font-size:18px; 
                            vertical-align: center;                       
                        }
                        .right-seperate{
                            display:inline-block;
                            height:0;
                            border-bottom:1px solid rgba(225,225,225,0.2);
                            width:112px;
                            margin-left:12px;
                            margin-bottom:9px;
                        }
                    }
                    .wrapper{
                        margin-top:24px;
                        .seperate-info{
                            margin-right:24px;
                            .type-item{
                                display:inline-block;
                                width:16px;
                                height:16px;
                                background-size:16px 16px;
                                background-repeat:no-repeat;
                                margin-bottom:12px;
                                &:last-child{
                                    margin-bottom:0;
                                }
                                &.decrease{
                                    @include bg-image('decrease_1')
                                }
                                &.guarantee{
                                    @include bg-image('guarantee_1')
                                }
                                &.invoice{
                                    @include bg-image('invoice_1')
                                }
                                &.spacial{
                                    @include bg-image('special_1')
                                }
                                &.discount{
                                    @include bg-image('discount_1')
                                }
                            }
                            .text-info{
                                margin-left:6px;
                                font-size:12px;
                                color:white;
                                line-height:12px;
                                font-weight:200;
                                vertical-align: top;
                                margin-top:2px;
                                display:inline-block;
                            }
                        
                        }
                    }
                    
                }
                .bulletin-info{
                    padding:28px 36px 24px 36px;
                    .seperate{
                        font-size:0;
                        .left-seperate{
                            display:inline-block;
                            height:0;
                            border-bottom:1px solid rgba(225,225,225,0.2);
                            width:112px;
                            margin-right:12px;
                            margin-bottom:9px;
                        }
                        .info{
                            display:inline-block;
                            font-weight:500;
                            font-size:18px; 
                            vertical-align: center;                       
                        }
                        .right-seperate{
                            display:inline-block;
                            height:0;
                            border-bottom:1px solid rgba(225,225,225,0.2);
                            width:112px;
                            margin-left:12px;
                            margin-bottom:9px;
                        }
                    }
                    .seperate-info{
                        padding:24px 12px 0 12px;
                        line-height:24px;
                        font-size:12px;
                        font-weight:200;
                        vertical-align: center;
                    }
                }
            }
        }
        .close{
            width:32px;
            height:32px;
            position:relative;
            margin:-64px auto 0 auto;
            color:white;
            clear:both;
            font-size: 32px;
        }
    }
}
</style>