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
                    <img width="100%" v-lazy="banner.imageUrl" alt="">
                </van-swipe-item>
            </van-swipe>
        </div>
    </div>
</template>

<script>
    export default {
        data() {
            return {
                locationIcon: require('../../assets/images/locationa.png'),
                bannerPicArray:[
                    {imageUrl:'http://7xjyw1.com1.z0.glb.clouddn.com/simleVueDemoPic001.jpg'},
                    {imageUrl:'http://7xjyw1.com1.z0.glb.clouddn.com/simleVueDemoPic002.jpg'},
                    {imageUrl:'http://7xjyw1.com1.z0.glb.clouddn.com/simleVueDemoPic003.jpg'},
                ]
            }
        },
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
        max-height: 15rem;
        overflow: hidden;
    }
</style>