<template>
    <div>
        <div class="search-bar">
            <van-row>
                <van-col span="3">
                    <img :src="locationIcon" class="location-icon" width="80%">
                </van-col>
                <van-col span="16">
                    <input type="text" class="search-input">
                </van-col>
                <van-col span="5">
                    <van-button size="mini">查找</van-button>
                </van-col>
            </van-row>
        </div>
        <!-- swipe area -->
        <div class="swiper-area">
            <van-swipe :autoplay="3000">
                <van-swipe-item v-for="( banner, index ) in bannerPicArray" :key="index">
                    <img width="100%" v-lazy="banner.image" alt="">
                </van-swipe-item>
            </van-swipe>
        </div>
        <!-- type bar -->
        <div class="type-bar">
            <div v-for="( cate, index ) in category" :key="index">
                <img v-lazy="cate.image" alt="" width="90%">
                <span>{{cate.mallCategoryName}}</span>
            </div>
        </div>
        <!--AD banner area-->
        <div class="ad-banner">
            <img v-lazy="adBanner" width="100%">
        </div>
        <!--Recommend goods area-->
        <div class="recommend-area">
            <div class="recommend-title">
                商品推荐
            </div>
            <div class="recommend-body">
                <swiper :options="swiperOptions" >
                    <swiper-slide v-for="( item , index ) in recommendGoods" :key="index">
                        <div class="recommend-item">
                            <img :src="item.image" width="100%">
                            <div>{{ item.goodsName }}</div>
                            <div>￥{{item.price}} (￥{{item.mallPrice}})</div>
                        </div>
                    </swiper-slide>
                </swiper>
            </div>
        </div>
    </div>
</template>

<script>
    import axios from 'axios'
    import 'swiper/dist/css/swiper.css'
    import { swiper, swiperSlide } from 'vue-awesome-swiper'

    export default {
        components: {
            swiper, swiperSlide
        },
        data() {
            return {
                locationIcon: require('../../assets/images/locationa.png'),
                bannerPicArray:[],
                category:[],
                adBanner:'',
                recommendGoods:[],
                swiperOptions:{
                    slidesPerView: 3
                },
            }
        },
        created() {
            axios({
                url:'https://www.easy-mock.com/mock/5af1968fca5c747a72cdb001/index/index',
                method:'get'
            })
            .then(response => {
                console.log(response);
                if( response.status == '200' ) {
                    let data = response.data.data;
                    //获取分类
                    this.category = data.category; 
                    //获取广告图片
                    this.adBanner = data.advertesPicture.PICTURE_ADDRESS;   
                    //轮播图
                    this.bannerPicArray = data.slides;
                    //推荐商品
                    this.recommendGoods = data.recommend;
                }
            })
            .catch(error =>{
                console.log(error);
            }) 
        },
        methods: {
        }
    }
</script>

<style scoped>
    .search-bar{
        height: 2.2rem;
        background-color: #e5017d;
        line-height:2.2rem;
        overflow: hidden;
    }
    .search-input{
        width: 100%;
        height: 1.3rem;
        border-top: 0;
        border-left: 0;
        border-right: 0;
        border-bottom: 1px solid #fff !important;
        background-color: #e5017d;
        color: #fff;
    }
    .location-icon{
        padding-top: .2rem;
        padding-left: .3rem;
    }
    .swiper-area{
        clear: both;
        height: 8rem;
        overflow: hidden;
    }
    .type-bar{
        background-color: #fff;
        margin:0 .3rem .3rem .3rem;
        border-radius: .3rem;
        font-size:14px;
        display: flex;
        flex-direction:row;
        flex-wrap:nowrap;
    }
    .type-bar div{
        padding: .3rem;
        font-size: 12px;
        text-align: center;
    }
    .recommend-area{
       background-color: #fff;
       margin-top: .3rem;
    }
    .recommend-title{
        border-bottom:1px solid #eee;
        font-size:14px;
        padding:.2rem;
        color:#e5017d;
    }
    .recommend-item{
      width:99%;
      border-right: 1px solid #eee;
      font-size: 12px;
      text-align: center;
    }
</style>