<template>
  <div class="header">
    <!-- {{poiInfo.name}} -->
    <!-- 顶部通栏开始 -->
    <div class="top-wrapper">
        <div class="back-wrapper">
            <span class="icon-arrow_lift"></span>
        </div>

        <form action="" class="search-wrapper">
            <span class="search-icon"></span>
            <input type="text" placeholder="搜索店内商品" class="search-bar">
        </form>

        <div class="more-wrapper">
            <a href="#" class="spelling-bt">拼单</a>
            <div class="more-bt">
                <i class="s-radius"></i>
                <i class="s-radius"></i>
                <i class="s-radius"></i>
            </div>
        </div>
           
    </div>
    <!-- 顶部通栏结束 -->

    <!-- 背景内容开始 -->
    <div class="bg-wrapper" :style='head_pic_url'>
        <!-- <img :src="poiInfo.head_pic_url" alt=""/> -->
    </div>
    <!-- 背景内容结束 -->
    <!-- 主题内容 开始 -->
    <div class="content-wrapper">
        <div class="icon" :style="head_bg">
            
        </div>
        <div class="name">
            <h3>{{poiInfo.name}}</h3>
        </div>
        <div class="collect">
            <img src="./img/star.png" alt="">
            <span>收藏</span>
        </div>
    </div>
    <!-- 主题内容 结束 -->
    <!-- 公告内容 开始 -->
    <div class="bulletin-wrapper">
        <img v-if="poiInfo.discounts2" :src="poiInfo.discounts2[0].icon_url" alt="" class="icon"/>
        <span v-if="poiInfo.discounts2" class="text">{{poiInfo.discounts2[0].info}}</span>
        <div class="detail" v-if="poiInfo.discounts2" @click="showBulletin">          
            {{poiInfo.discounts2.length}}个活动
            <span class="icon-keyboard_arrow_right"></span>
        </div>
    </div>
    <!-- 公告内容 结束 -->
    <!-- 公告详情 开始 -->
    <transition name="bulletin-detail">
        <div class="bulletin-detail" v-show="isShow">
            <div class="detail-wrapper">
            <!-- 相关内容容器 -->
            <div class="main-wrapper" :style="detail_bg">
                <div class="icon" :style="head_bg"></div>
                <h3 class="name">{{poiInfo.name}}</h3>
                <!-- 星级评价 -->
                <div class="score">
                <app-star :score="poiInfo.wm_poi_score"></app-star>
                <span>{{poiInfo.wm_poi_score}}</span>
              </div>
                <p class="tip">
                    {{poiInfo.min_price_tip}} <i>|</i>{{poiInfo.shipping_fee_tip}}<i>|</i>
                    {{poiInfo.delivery_time_tip}}
                </p>
                <p class="time">
                    配送时间: {{poiInfo.shipping_time}}
                </p>
                <div class="discounts" v-if="poiInfo.discounts2">
                    <p>
                        <img :src="poiInfo.discounts2[0].icon_url
                        " alt="">
                        <span>{{poiInfo.discounts2[0].info}}</span>
                    </p>
                </div>
            </div>
            <!-- 关闭 内容容器 -->
            <div class="close-wrapper">
                <span class="icon-close" @click="closeBulletin"></span>
            </div>
            </div>
        </div>
    </transition>
   
    <!-- 公告详情 结束 -->
  </div>  
</template>

<script>
import Star from '../star/Star'
export default {
    data(){
        return {
            isShow:false
        }
    },
    components:{
        "app-star":Star,
    },
    props:{
        poiInfo:{
            type:Object,
            default:{}
        }
    },
    computed:{
        head_pic_url(){
            return "background-image:url("+this.poiInfo.head_pic_url+")"
        },
        head_bg(){
            return "background-image:url("+this.poiInfo.pic_url+")"
        },
        detail_bg(){
            return "background-image:url("+this.poiInfo.poi_back_pic_url+")"
        }
    },
    methods:{
        showBulletin(){
            this.isShow = true
        },
        closeBulletin(){
            this.isShow = false
        }
    }
 
}
</script>

<!-- Add "scoped" attribute to limit CSS to this component only -->
<style scoped>
@import url(../../common/css/icon.css);
.header{
    height: 130px;
    padding-top:20px;
}
/* 顶部通栏样式 */
.header .top-wrapper{
    position: relative;
}
.header .top-wrapper .back-wrapper{
    position: absolute;
    left: 0;
    top: 0;
    width: 50px;
    height: 31px;
    text-align: center;
    line-height: 31px;
}
.header .top-wrapper .back-wrapper span{
    display: inline-block;
    color: #fff;
}
.header .top-wrapper .search-wrapper{
    width: 100%;
    height: 31px;
    /* background:pink; */
    padding: 0 104px 0 50px; 
    box-sizing: border-box;
}
.header .top-wrapper .search-wrapper .search-icon{
    position: absolute;
    width: 14px;
    height: 14px;
    background: url(./img/search.png) no-repeat;
    background-size:100%;
    margin:7px 5px 7px 12px;
} 
.header .top-wrapper .search-wrapper .search-bar{
    width: 100%;
    height: 31px;
    border: 0;
    box-sizing: border-box;
    background: #cdcdcd;
    border-radius: 25px;
    padding-left: 28px;
    outline: none;
}
.header .top-wrapper .more-wrapper{
    position: absolute;
    right: 0;
    top: 0;  
    width:65px;
    height:24px;
    /* background:orange; */
    padding:7px 15px 0 24px;  
}
.header .top-wrapper .more-wrapper .spelling-bt{  
    width:30px;
    height:17px;
    border: 1px solid #fff;
    color: #fff;
    text-decoration: none;
    text-align: center;
    line-height:17px;  
    font-size: 13px;
    padding: 0 3px;
}
.header .top-wrapper .more-wrapper .more-bt{
    display: block;
    float:right;
    font-size:12px;
}
.header .top-wrapper .more-wrapper .more-bt .s-radius{
    width:2px;
    height:2px;
    border-radius:50%;
    border:1px solid #fff;
    margin-right:1px;
    display: inline-block;   
}   
 /*图片背景样式 */
 .header .bg-wrapper{
     width: 100%;
     height: 150px;
     position: absolute;
     left: 0;
     top: 0;
     z-index: -1;
     background-size:100% 135%;
     background-position: center -12px;
 }
 /* 主题内容样式 */
 .header .content-wrapper{
     padding:17px 10px 11px;
     height:50px;
 }
 .header .content-wrapper .icon{
     width:50px;
     height: 50px;
     background-size: 135% 100%;
     background-position: center;
     border-radius: 5px;
     float: left;
 }
 .header .content-wrapper .name{
     float: left;
     padding: 18px 0 0 12px;
 }
 .header .content-wrapper .name h3{
     font-size: 16px;
     font-weight: bold;
     color: #fff;
 }
 .header .content-wrapper .collect{
     width: 25px;
     height: 37px;
     float: right;
     text-align: center;
     padding-top: 6px;
 }
 .header .content-wrapper .collect img{
     width: 20px;
     height: 20px;
 }
 .header .content-wrapper .collect span{
     margin-top: 7px;
     color: #fff;
     font-size: 11px;
 }
 /* 公告内容 样式*/
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
     font-size: 11px;
     color: #fff;
     float: left;
     line-height: 16px;
 }
 .header .bulletin-wrapper .detail{
     color: #fff;
     float: right;
     font-size: 11px;
     line-height: 16px;
 }
 .header .back-wrapper .detail span{
     font-size: 16px;
     line-height: 16px;
     float: right;
 }
 /* 公告详情 样式 */
.header .bulletin-detail {
		width: 100%;
		height: 100%;
		position: absolute;
		left: 0;
		top: 0;
		background: rgba(98, 98, 98, 0.8);
        z-index: 999;
}
	
.header .bulletin-detail .detail-wrapper {
		width: 100%;
		height: 100%;
		padding: 43px 20px 125px;
		box-sizing: border-box;
}
	
.header .bulletin-detail .detail-wrapper .main-wrapper {
		width: 100%;
		height: 100%;
		background-size: 100% 100%;
		border-radius: 10px;
		text-align: center;
}
	
.header .bulletin-detail .detail-wrapper .main-wrapper .icon {
		width: 60px;
		height: 60px;
		background-size: 135% 100%;
		background-position: center;
		border-radius: 5px;
		display: inline-block;
		margin-top: 40px;
}
	
.header .bulletin-detail .detail-wrapper .main-wrapper .name {
		font-size: 15px;
		color: white;
		margin-top: 13px;
}
	
.header .bulletin-detail .detail-wrapper .main-wrapper .score {
		height: 10px;
		margin-top: 6px;
		text-align: center;
		font-size: 0;
}
.header .bulletin-detail .detail-wrapper .main-wrapper .score .star{
    display: inline-block;
    margin-right: 7px;
}
.header .bulletin-detail .detail-wrapper .main-wrapper .score span{
    display: inline-block;
    font-size: 10px;
    color: #fff;
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
    vertical-align: middle;
}
.header .bulletin-detail .detail-wrapper .main-wrapper .discounts span{
     font-size: 11px;
     line-height: 16px;
     color: #fff;
 }
.header .bulletin-detail .detail-wrapper .close-wrapper span{
     width: 40px;
     height: 40px;
     line-height: 40px;
     border-radius: 50%;
     font-size: 14px;
     text-align: center;
     color: #fff;
     display: block;
     background: rgba(118,118,118,.7);
     border: 1px solid rgba(140,140,140,.9);
     margin: 0 auto;
 }

 /* 过度动画 */
.bulletin-detail-enter-active,
.bulletin-detail-leave-active{
    transition: 2s all;
}
.bulletin-detail-enter,
.bulletin-detail-leave-to{
    opacity:0;
}
.bulletin-detail-enter-to,
.bulletin-detail-leave{ 
    opacity:1;
}
</style>
