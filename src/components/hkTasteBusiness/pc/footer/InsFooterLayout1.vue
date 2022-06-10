<template>
<div id="footer">
  <div class="footbg">
    <div class="footerMain">
        <div class="footerBotttom">
          <div class="footerLeft">
              <ul v-for="(n,index) in footerMenus" :key="index">
                <li>
                  <router-link
                    :to="n.Type === 0 ? n.Url : n.Type === 1 ? '/cms/catDetail/' + n.Value.Id : n.Type === 2 ? '/CMS/content/' + n.Value.Id : n.Type === 3 ? '/RegNPay/Form/' + n.Value.Id : n.Type === 4 ? '/product/CatProduct?catId=' + n.Value.Id : n.Type === 5 ? '/product/list?key=&attr=' + n.Value.Id : '/product/list?key=&attr=' + n.ParentId + '&attrId=' + n.Value.Id"
                  >{{n.Name}}</router-link>
                  <ul>
                    <li v-for="(c,index2) in n.Childs" :key="index2">
                       <router-link :to="To(c)">{{c.Name}}</router-link>
                    </li>
                  </ul>
                </li>
             </ul>
          </div>
          <div class="footerRight">
            <p><img src="/images/pc/pcindex_09.png" /></p>
          </div>
          <div class="clear"></div>
           <p class="footercopy"><span>Copyright {{currentYear}} © LKS Display Box Acrylic HK  power by eventizer<img src="/images/pc/startup-logo.png"></span><span><img src="/images/pc/vm.png" /></span></p>
        </div>
    </div>
  </div>
</div>

</template>

<script lang="ts">
import { Component, Prop, Vue } from 'vue-property-decorator';

@Component
export default class InsFooterLayout1 extends Vue {
  currentYear: number = 0;
  footerMenus: any[] = [];
  goToTop () {
    let sTop = document.documentElement.scrollTop;
    let times = setInterval(() => {
      sTop -= 50;
      if (sTop <= 0) {
        document.documentElement.scrollTop = 0;
        clearInterval(times);
      } else {
        document.documentElement.scrollTop = sTop;
      }
    }, 1);
  }
  To (n) {
    return n.Type === 1 ? '/cms/catDetail/' + n.Value.Id : n.Type === 2 ? '/CMS/content/' + n.Value.Id : n.Type === 3 ? '/RegNPay/Form/' + n.Value.Id : n.Type === 4 && !this.$store.state.catMenuType ? '/product/cat/' + n.Value.Id : n.Type === 4 && this.$store.state.catMenuType ? '/product/search/-?catalogs=' + JSON.stringify([parseInt(n.Value.Id)]) + '&type=0' : n.Type === 5 ? '/product/search/-?attrs=' + JSON.stringify([{ Id: parseInt(n.Value.Id), Vals: [] }]) + '&type=0' : '/product/search/-?attrs=' + JSON.stringify([{ Id: parseInt(n.ParentId), Vals: [parseInt(n.Value.Id)] }]) + '&type=0';
  }
  getMenu () {
    this.$Api.promotion.getMenu().then((result) => {
      this.footerMenus = result.ReturnValue.FooterMenus;
    });
  }
  created () {
    var date = new Date();
    this.currentYear = date.getFullYear();
    this.getMenu();
  }
}
</script>

<style scoped lang="less">
/* 底部文件 */
.footbg{
    background: #fff;
    background-size: cover;
    width: 100%;
    display: inline-block;
    padding-bottom: 10px;
    min-height: 278px;
    border-top: 1px solid #eee;
}
.footerMain{
    width: 1200px;
    margin: 0 auto;
}
.footerTop{
    text-align: center;
    padding-top: 25px;
    padding-bottom: 25px;
    width: 100%;
}
.footerTop p{
    text-align: center;
    display: inline-block;
    margin-right: 50px;
}
.footerTop p span{
    font-size: 14px;
    color: #FFF;
    line-height: 35px;
    margin-right: 15px;
}
.footerTop p b{
    font-weight: 100;
    font-size: 35px;
    color: #FFF;
    line-height: 35px;
}
.footerBotttom{
    width: 100%;
    margin-top: 50px;
}
.footerLeft{
    float: left;
    width: 50%;
}
.footerLeft > ul{
    float: left;
    margin-right: 10%;
}
.footerLeft > ul >li{
    width: 100%;
    line-height: 30px;
}
.footerLeft > ul >li >a{
    font-size:20px;
    color:#333;
}
.footerLeft > ul >li >ul{
  width: 100%;
}
.footerLeft > ul >li >ul a{
    font-size: 16px;
    color:#333;
    display: inline-block;
    text-transform: uppercase;
}
.footerLeft > ul >li >ul a:hover{
   transform: translateY(-3px);
}
.footerLeft p{
    width: 100%;
    display: block;
    font-size: 14px;
    color: #fff;
    padding-top: 20px;
}
.footerLeft p img{
    display: inline-block;
    vertical-align: middle;
    padding-left: 10px;
}
.footerRight{
    float: right;
    width: 40%;
    text-align: center;
    p{
      text-align: center;
      display: inline-block;
      img{
          width: 100%;
          display: block;
      }
    }
}
.footercopy{
  width: 100%;
  display: inline-block;
  margin-top: 20px;
}
.footercopy span:nth-child(1){
  float: left;
  color:#333;
  font-size: 14px;
}
.footercopy span:nth-child(1) img{
  display: inline-block;
  vertical-align:middle;
  padding-left: 10px;
  height: 50px;
}
.footercopy span:nth-child(2){
  float: right;
  width: 40%;
  text-align: center;
  color:#333;
  font-size: 14px;
}
.footercopy span:nth-child(2) img{
  display: inline-block;
  vertical-align:middle;
  padding-left: 10px;
  height: 50px;
}
</style>
