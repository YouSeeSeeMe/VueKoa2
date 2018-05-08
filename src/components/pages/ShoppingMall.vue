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
            <img v-lazy="adBanner.PICTURE_ADDRESS" width="100%">
        </div>
    </div>
</template>

<script>
    import axios from 'axios'
    export default {
        data() {
            return {
                locationIcon: require('../../assets/images/locationa.png'),
                bannerPicArray:[],
                category:[],
                adBanner:''
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
                    this.adBanner = data.advertesPicture;   
                    //轮播图
                    this.bannerPicArray = data.slides
                }
            })
            .catch(error =>{
                console.log(error);
            }) 
        }
    }
</script>

<style scoped>
    .search-bar{
        height: 2.2rem;
        background-color: #e5017d;
        line-height:2.2rem;
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
        max-height: 12rem;
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
</style>