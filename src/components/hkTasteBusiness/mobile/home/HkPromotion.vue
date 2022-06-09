<template>
  <div class="PromotionMain">
          <!-- AD1 -->
          <div class="InnerSide">
           <div class="RecommendText">{{Title}}</div>
            <div class="RecommendBg">
                <ul>
                  <li v-for="(slide, index) in banner" :key="index"><router-link :to="slide.Url"><img :src="slide.Image" /></router-link></li>
                </ul>
            </div>
          </div>
    <!-- 限时大平卖 -->
    <div class="SalesMain">
          <HkHotProduct />
    </div>
  </div>
</template>
<script lang="ts">
import { Vue, Prop, Component } from 'vue-property-decorator';
import { swiper, swiperSlide } from 'vue-awesome-swiper/src';
@Component({
  components: {
    HkHotProduct: () => import('@/components/hkTasteBusiness/mobile/home/HkHotProduct.vue'),
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
<style lang="less" scoped>
.RecommendText{
  color:#333;
  display: block;
  height: 70px;
  display: flex;
  align-items: center;
  justify-content: center;
  font-size:2rem;
}
.PromotionMain{
    background: #fff;
    background-size: 100% 100%;
    display: inline-block;
    width: 100%;
    padding-top: 3rem;
    padding-bottom: 2rem;
    margin-top: -.5rem;
    position: relative;
  .SalesMain{
    width: 90%;
    margin: 0 auto;
  }
  .InnerSide{
    width: 90%;
    margin: 0 auto;
    .RecommendBg{
      width: 100%;
      display:flex;
      flex-wrap: wrap;
      ul{
        width:100%;
        display:flex;
        flex-wrap: wrap;
        li{
          width:100%;
          display:flex;
          flex-wrap: wrap;
          margin-bottom: 1rem;
          img{
            width:100%;
          }
        }
      }
    }

  }
}
</style>
