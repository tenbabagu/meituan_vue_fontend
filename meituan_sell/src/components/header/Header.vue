<template>
    <div class="header">
        <!-- 顶部通栏 -->
        <div class="top-wrapper">
            <div class="back-wrapper">
               <span class="icon-arrow_lift"></span> 
            </div>
            <form class="search-wrapper">
                <span class="search-icon"></span> 
                <input class="search-bar" type="text" placeholder="搜索店内商品"/>
            </form>
            <div class="more-wrapper">
                <a class="spelling-bt" href="#">拼单</a>
                <div class="more-bt">
                    <i class="s-radius"></i>
                    <i class="s-radius"></i>
                    <i class="s-radius"></i>
                </div>
            </div>
        </div>

        <!-- 主题内容 -->
        <div class="content-wrapper">
            <div class="icon" :style="head_bg">
    
            </div>
            <div class="name">
                <h3>{{poiInfo.name}}</h3>
            </div>
            <div class="collect">
                <img src="./star.png" alt="">
                <span>收藏</span>
            </div>
        </div>

        <!-- 公告内容 -->
        <div class="bulletin-wrapper" @click="showBulletin">
            <img class="icon" v-if="poiInfo.discounts2" :src="poiInfo.discounts2[0].icon_url" alt="">
            <span class="text"  v-if="poiInfo.discounts2">{{poiInfo.discounts2[0].info}}</span>
            <div class="details" v-if="poiInfo.discounts2">
                {{poiInfo.discounts2.length}}个活动
                <span class="icon-keyboard_arrow_right"></span>
            </div>
        </div>

        <!-- 背景 -->
        <div class="bg-wrapper" :style="content_bg">
            <!-- <img :src = "poiInfo.head_pic_url" /> -->
        </div>

        <!-- 公告详情 -->
        <transition name="bulletin-detail">
            <div class="bulletin-detail" v-show="isShow">
                <div class="detail-wrapper">
                    <div class="main-wrapper" :style="detail_bg">
                        <div class="icon" :style="head_bg"></div>
                        <h3 class="name">{{poiInfo.name}}</h3>
                        <div class="score">
                            <Star_ratings :score="poiInfo.wm_poi_score"></Star_ratings>
                            <span>{{poiInfo.wm_poi_score}}</span>
                        </div>
                        <p class="tip">
                            {{poiInfo.min_price_tip}} <i>|</i>
                            {{poiInfo.shipping_fee_tip}} <i>|</i>
                            {{poiInfo.delivery_time_tip}} <i>|</i>
                        </p>
                        <p class="time">
                            配送时间{{poiInfo.shipping_time}}
                        </p>
                        <div class="discounts">
                            <p>
                                <img v-if="poiInfo.discounts2" :src="poiInfo.discounts2[0].icon_url">
                                <span v-if="poiInfo.discounts2">{{poiInfo.discounts2[0].info}}</span>
                            </p>
                        </div>
                    </div>
                    <div class="close-wrapper" @click="closeBulletin">
                        <span class="icon-close"></span>
                    </div>
                </div>
            </div>
        </transition>
        
    </div>
</template>

<script>

    import Star_ratings from "components/star_rating/Star_rating.vue"
    export default{
        props:{//组件传值
            poiInfo:{
                type: Object,
                default: {},
            }
        },

        components:{
            Star_ratings,
        },

        computed:{//计算属性
            content_bg(){
                return "background-image: url(" + this.poiInfo.head_pic_url+ ")";
            },
            head_bg(){
                return "background-image: url(" + this.poiInfo.pic_url+ ")";
            },
            detail_bg(){
                return "background-image: url(" + this.poiInfo.poi_back_pic_url+ ")";
            }
        },

        data(){
            return {
                isShow: false,
            }
        },

        methods:{
            showBulletin(){
                this.isShow = true;
            },
            closeBulletin(){
                this.isShow = false;
            }
        }

    
    }
</script>

<style>

@import url("../../common/styles/icon.css");
.header{
    height: 130px;
    padding-top: 20px;
}

/* 顶部通栏 */
.header .top-wrapper{
    position: relative;
}

.header .top-wrapper .back-wrapper{
    width: 50px;
    height: 31px;
    /* background: red; */
    position: absolute;
    left: 0;
    top: 0;
    text-align:center;
    line-height: 31px;
}

.header .top-wrapper .back-wrapper span{
    /* 为了支持text-align和line-height属性 */ 
    display: inline-block;
    color: white;
}

.header .top-wrapper .search-wrapper{
    width: 100%;
    height: 31px;
    /* background: purple; */
    padding: 0 104px 0 50px;
    /* 设置盒子从边框开始计算 */
    box-sizing: border-box;
}

.header .top-wrapper .search-wrapper .search-icon{
    background: url(titans_h5_search@2x.png) no-repeat 11px center;
    width: 56px;
    height: 31px;
    position: absolute;
    background-size: 13px 13px;
}

.header .top-wrapper .search-wrapper .search-bar{
    width: 100%;
    height: 31px;
    border: 0;
    box-sizing: border-box;
    background: #cdcdcc;
    border-radius: 25px;
    padding-left: 28px;
    outline: none;
}

.header .top-wrapper .more-wrapper{
    width: 65px;
    height: 24px;
    position: absolute;
    top: 0;
    right:0;
    /* background: blue; */
    padding: 7px 15px 0 24px;
}

.header .top-wrapper .more-wrapper .spelling-bt{
    width: 30px;
    height: 17px;
    color: white;
    line-height: 17px;
    border: 1px solid white;
    text-align: center;
    float: left;
    text-decoration: none;
    font-size: 10px;
}

.header .top-wrapper .more-wrapper .more-bt{
    float: left;
    width: 20px;
    height: 24px;
    margin-left: 13px;
    margin-top: 6px;
}
.header .top-wrapper .more-wrapper .more-bt .s-radius{
    width: 3px;
    height: 3px;
    border-radius: 50%;
    display: block;
    float: left;
    border: 1px solid white;
    margin-right: 1px;

}

.header .bg-wrapper{
    width: 100%;
    height: 150px; 
    position: absolute;
    left: 0;
    top: 0;
    z-index: -1;
    background-size: 100% 135%;
    background-position: center -12px;
}

.header .content-wrapper{
    padding: 17px 10px 11px;
    height: 50px;
}

.header .content-wrapper .icon{
    height: 50px;
    width: 50px;
    border-radius: 5px;
    background-size: 135% 100%;
    background-position: center;
    float: left;
}

.header .content-wrapper .name{
    float: left;
    padding: 18px 0 0 12px;
}

.header .content-wrapper .name h3{
    font-size: 16px;
    font-weight: bold;
    color: white;
}

.header .content-wrapper .collect{
    float: right;
    width: 25px;
    height: 37px;
    text-align: center;
    padding-top: 6px;
}

.header .content-wrapper .collect img{
    width: 20px;
    height: 20px;
}

.header .content-wrapper .collect span{
    margin-top: 7px;
    color:white;
    font-size: 11px;
}

/* 公告内容 */
.header .bulletin-wrapper{
    height: 16px;
    padding: 0 10px;
}

.header .bulletin-wrapper .icon{
    width: 16px;
    height: 16px;
    float: left;
    margin-right: 6px;
}

.header .bulletin-wrapper .text{
    font-size:11px;
    color: white;
    float: left;
    line-height: 16px;
}

.header .bulletin-wrapper .details{
    color: white;
    float: right;
    font-size: 11px;
    line-height: 16px;
}

.header .bulletin-wrapper .details span{
    font-size: 16px;
    line-height: 16px;
    float: right;
}

.header .bulletin-detail{
    width: 100%;
    height: 100%;
    position: absolute;
    left: 0;
    top: 0;
    background: rgba(98,98,98,0.8);
    z-index: 999;
}

.header .bulletin-detail .detail-wrapper{
    width: 100%;
    height: 100%;
    padding: 43px 20px 125px;
    box-sizing: border-box;
}

.header .bulletin-detail .detail-wrapper .main-wrapper{
    width: 100%;
    height: 100%;
    background-size: 100% 100%;
    border-radius: 10px;
    text-align: center;
}

.header .bulletin-detail .detail-wrapper .main-wrapper .icon{
    height: 60px;
    width: 60px;
    border-radius: 5px;
    background-size: 135% 100%;
    background-position: center;
    display: inline-block;
    margin-top: 40px;
}

.header .bulletin-detail .detail-wrapper .main-wrapper .name{
    font-size: 15px;
    color:white;
    margin-top: 13px;
}

.header .bulletin-detail .detail-wrapper .main-wrapper .tip{
    font-size: 11px;
    color: #bababc;
    margin-top: 8px;
}

.header .bulletin-detail .detail-wrapper .main-wrapper .tip i{
    margin: 0 7px;
}

.header .bulletin-detail .detail-wrapper .main-wrapper .time{
    font-size: 11px;
    color: #bababc;
    margin-top: 13px;
}

.header .bulletin-detail .detail-wrapper .main-wrapper .discounts{
    margin-top: 20px;
    padding: 0 20px;
}

.header .bulletin-detail .detail-wrapper .main-wrapper .discounts p{
    padding-top: 20px;
    border-top: 1px solid #bababc;
}

.header .bulletin-detail .detail-wrapper .main-wrapper .discounts img{
    width: 16px;
    height: 16px;
    /* margin-right: 10px; */
    vertical-align: middle;
}

.header .bulletin-detail .detail-wrapper .main-wrapper .discounts span{
    font-size: 11px;
    line-height: 16px;
    color: white;
}

.header .bulletin-detail .detail-wrapper .main-wrapper .score{
    height: 10px;
    margin-top: 6px;
    text-align: center;
    font-size: 0;
}
.header .bulletin-detail .detail-wrapper .main-wrapper .score .star{
    
    margin-right: 7px;
    display: inline-block;
}

.header .bulletin-detail .detail-wrapper .main-wrapper .score span{
    display: inline-block;
    font-size: 10px;
    color: white;
}

.header .bulletin-detail .detail-wrapper .close-wrapper{
    padding-top: 40px;
    height: 40px;
    text-align: center;
}


.header .bulletin-detail .detail-wrapper .close-wrapper span{
    width: 40px;
    height: 40px;
    line-height: 40px;
    border-radius: 50%;
    font-size: 14px;
    color: white;
    display: inline-block; 
    background: rgba(118, 118, 118, 0.7);
    border: 1px solid rgba(140, 140, 140, 0.9);
}

/* vue过度效果 */
/* .detail-enter 
.detail-enter-to
.detail-enter-active

.detail-leave
.detail-leave-to
.detail-leave-active */

.bulletin-detail-enter-active, .detail-leave-active{
    transition: 0.5s all;
}
.bulletin-detail-enter, .detail-leave-to{
   opacity: 0;
}

.bulletin-detail-enter-to, .detail-leave{
    opacity: 1;
}

</style>

