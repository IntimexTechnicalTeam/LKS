<template>
  <!-- 商品推荐开始 -->
    <div class="indexMiddle">
    <div class="indexRecommend">
        <div class="RecommendText">{{Title}}</div>
        <div class="RecommendBg">
            <ul>
              <li v-for="(slide, index) in banner" :key="index"><router-link :to="slide.Url"><img :src="slide.Image" /></router-link></li>
            </ul>
        </div>
    <!-- 商品推荐结束 -->
    <div class="clear"></div>
    <!-- 限时平卖开始 -->
    <HkHotProduct />
    <!-- 限时平卖结束 -->
  </div>
</div>
</template>
<script lang="ts">
import { Vue, Prop, Component } from 'vue-property-decorator';
import { swiper, swiperSlide } from 'vue-awesome-swiper/src';
@Component({
  components: {
    HkHotProduct: () => import(/* webpackChunkName: "home" */ '@/components/hkTasteBusiness/pc/home/HkHotProduct.vue'),
    swiper,
    swiperSlide
  }
})
export default class HkPromotion extends Vue {
  banner: any[] = [];
  content:string='';
  Title:string='';
  current:boolean=false;
  getHeaderBannerLst () {
    var _this = this;
    this.$Api.promotion.getPromotion('Home', 1).then(result => {
      _this.banner = result.Promotion._BannerList;
      _this.Title = result.Promotion.Name;
      _this.content = result.Promotion._BannerList[0].Content;
    });
  }
  created () {
    this.getHeaderBannerLst();
  }
  get lang () {
    return this.$Storage.get('locale');
  }
}
</script>
<style>
.indexMiddle  .swiperInner{
  padding: 10px;
}
</style>
<style lang="less" scoped>
.RecommendText{
  color:#333;
  display: block;
  height: 70px;
  display: flex;
  align-items: center;
  justify-content: center;
  font-size: 30px;
}
.indexMiddle{
    width: 100%;
    background: #ffffff;
    background-size: 100% 100%;
    display: inline-block;
    padding-top: 80px;
    padding-bottom: 80px;
    position: relative;
}
.indexRecommend{
    width: 1200px;
    margin: 0 auto;
}
.indexRecommendInner{
    width: 30%;
    float: left;
    margin-right: 5%;
}
.indexRecommendInner:nth-child(3){
    margin-right: 0%!important;
}
.RecommendBg{
    width: 100%;
    background-size: 100% 100%;
    overflow: hidden;
    position: relative;
    box-sizing: border-box;
    margin-top: 10px;
    margin-left: auto;
    margin-right: auto;
    ul{
      width: 100%;
      display:flex;
      flex-wrap: wrap;
      li{
        width:48%;
        float: left;
        margin-right: 4%;
        img{
          width:100%;
        }
        &:last-child{
          margin-right: 0px!important;
        }
      }
    }
}
.RecommendBg img{
  width: 100%;
}

.indexRecommendInner p{
    text-align: center;
    color: #806339;
    font-size: 36px;
    padding-top: 20px;
    padding-bottom: 20px;
    display: block;
}
</style>
