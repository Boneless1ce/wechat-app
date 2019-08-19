<template>
    <view>
        <swiper class="swiper" 
            indicator-dots="true" 
            indicator-color="rgba(43,153,57,.8)"
            indicator-active-color="#fff"
            autoplay="true"
            interval="2000">
            <swiper-item class="swiper-item">
                <image src="../static/7de912646addeaec74c47e6e3a7090872484dabe.png@880w_440h.jpg" mode="widthFix"></image>
            </swiper-item>
            <swiper-item class="swiper-item">
                <image src="../static/173ff321d6f95fc4ea2c95b599f76a63.jpg@880w_440h.jpg" mode="widthFix"></image>
            </swiper-item>
            <swiper-item class="swiper-item">
                <image src="../static/9805f8d01561fd359a1972e923ef022f44f80a97.jpg@880w_440h.jpg" mode="widthFix"></image>
            </swiper-item>
            <swiper-item class="swiper-item">
                <image src="../static/e192cbc5ba2931b3761640fe1b62ccd00cf78f63.jpg@880w_440h.jpg" mode="widthFix"></image>
            </swiper-item>
        </swiper>
    </view>
</template>

<script>
export default {
    
}
</script>

<style>
    .swiper-item{
        width: 100%;
    }
    .swiper-item image{
        width: 100%;
    }
</style>
