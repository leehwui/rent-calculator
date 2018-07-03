<template>
  <div class="page-result">
    <div class="nav-bar-result">
      <a class="btn-back" href="#" @click="$emit('back-to-main')">
        <i class="back"></i>
        <span class="btn-back-lg">修改</span>
      </a>
      <span>计算费用结果</span>
    </div>
    <a class="btn-appointment" href="http://www.linkfounder.cn/#17">
      预约参观
    </a>
    <div class="page-result-container">
      <div class="result-header">
        <div class="result-header-title">
          计算费用结果
        </div>
        <div class="result-header-subtitle">
          每月人均费用： <span> {{ result }}  RMB</span>
        </div>
      </div>
      <div class="result-header-2">
        人均 ¥1,800 如何租到颜值高且地段好的办公室？
      </div>
      <div class="result-carousal">
        <swiper
          ref="photoSwiper" :options="swiperOptions">
          <swiper-slide>
            <div class="carousal-img-container">
              <img src="../assets/slide1.png" alt="">
            </div>
            <p>认真工作也是热爱生活的一部分，高颜值多功能办公室，让你的工作更有效率。</p>
          </swiper-slide>
          <swiper-slide>
            <div class="carousal-img-container">
              <img src="../assets/slide2.png" alt="">
            </div>
            <p>
              每月精彩纷呈社区活动，社交、人脉、资源拓展一个都不能少。
            </p>
          </swiper-slide>
          <swiper-slide>
            <div class="carousal-img-container">
              <img src="../assets/slide3.png" alt="">
            </div>
            <p>
            全青岛覆盖多区域联动的办公空间
            </p>
          </swiper-slide>
          <swiper-slide>
            <div class="carousal-img-container">
              <img src="../assets/slide4.png" alt="">
            </div>
            <p>
            拒绝传统高成本租房模式，一键全包，轻投入获得最高性价比。
            </p>
          </swiper-slide>
        </swiper>
      </div>
      <div class="rst-btm-mobile">
        <div class="p1">现在预约参观，即可享受优惠</div>
        <div class="p3">咨询热线 400-1871-087</div>
        <div class="p4"> <a href="#"> > 了解邻客产品及价格 </a></div>
      </div>
      <div class="rst-btm-pc">
        <div class="rst-btm-pc-container">
          <div class="rst-btm-left">
            <div class="p1">现在预约参观即可享受优惠</div>
            <div class="p3">咨询热线 400-1871-087</div>
          </div>
          <div class="rst-btm-right">
            <div class="p2"><a class="btn" href="http://www.linkfounder.cn/#17">预约参观</a></div>
            <div class="p4"><a href="#">> 了解邻客产品及价格</a></div>
          </div>
        </div>
      </div>
    </div>
  </div>
</template>

<script>
import 'swiper/dist/css/swiper.css'
import { swiper, swiperSlide } from 'vue-awesome-swiper'
export default {
  name: 'ResultPage',

  components: {
    swiper,
    swiperSlide,
  },

  props: {
    result: {
      type: Number,
      default: 0,
    },
  },

  data() {
    return {
      swiperOptions: {
        autoplay: {
          delay: 2500,
          disableOnInteraction: false,
        }
      }
    }
  }

}
</script>

<style scoped>
.page-result {
  left: 100%;
  position: absolute;
  width:100%;
  height:100%;
  top: 0;
  z-index:1;
  overflow: auto;
  background-color: #f7f9fa;

}

.nav-bar-result {
  position: absolute;
  left: 0;
  top: 0;
  right: 0;
  z-index: 10;
  height: 44px;
  line-height: 44px;
  background-color: #2b2b2b;
  box-shadow: 0 0.5px 0 0 rgba(0,0,0,.2);
  color: #fff;
  font-size: 17px;
  text-align: center;
}

.btn-back {
  position: absolute;
  left: 0;
  top: 0;
  z-index: 2;
  color: #fff;
  padding: 0 20px;
  opacity: .7;
}

.back {
  width: 10px;
  height: 10px;
  display: inline-block;
  border-top: 2px solid #fff;
  border-left: 2px solid #fff;
  transform: rotate(-45deg);
  vertical-align: middle;
}

.btn-back span {
  font-size: 14px;
}

.page-result-container {
  height: 100%;
  overflow: auto;
  padding-bottom: 0;
}

.result-header {
  padding: 84px 0 50px;
  background: #2b2b2b;
  color: #fbf5ed;
  font-size: 12px;
  box-shadow: 0 1px 4px 0 rgba(0,0,0,.4);
}

.result-header-title {
  display: none;
}

.result-header-subtitle span {
  color: #e9901d;
  font-size: 30px;
}

.result-header-2 {
  background: #fff;
  font-size: 18px;
  font-weight: 500;
  color: #2b2b2b;
  text-align: center;
  padding: 25px 20px 5px;
}

.result-carousal {
  position: relative;
  width: 90%;
  max-width: 520px;
  margin: 35px auto 0;
}

.carousal-img-container {
  width: 100%
}

.carousal-img-container img{
  width: 100%;
}

.rst-btm-pc {
  background: #f5f5f5;
  position: absolute;
  left: 0;
  bottom: 0;
  right: 0;
  z-index: 10;
  height: 115px;
  display: none;
}

.rst-btm-mobile {
  background: #f5f5f5;
  margin-top: 15px;
  padding: 30px 0 50px;
}

.rst-btm-mobile .p1 {
  font-size: 16px;
  font-weight: 500;
  text-align: center;
  color: #4a4a4a;
}

.rst-btm-mobile .p3 {
  font-size: 16px;
  text-align: center;
  color: #4a4a4a;
  margin-top: 45px;
}

.rst-btm-mobile .p4 {
  text-align: center;
  margin-top: 15px;
}

.rst-btm-mobile .p4 a {
  font-size: 12px;
  color: #e9901d;
}

.rst-btm-pc-container {
  position: relative;
  width: 90%;
  max-width: 520px;
  margin: 0 auto;
}

.rst-btm-left {
  position: absolute;
  width: 60%;
  left: 0;
  top: 0;
  padding: 25px 0;
}

.rst-btm-right {
  position: absolute;
  width: 160px;
  right: 0;
  top: 0;
  padding: 25px 0
}

.rst-btm-right .p2 a {
  display: inline-block;
  width: 160px;
  height: 46px;
  line-height: 46px;
  background-color: #e9901d;
  font-size: 14px;
  color: #fff;
  text-align: center;
}

.rst-btm-right .p4 {
  text-align: center;
  margin-top: 5px;
}

.rst-btm-right .p4 a {
  font-size: 12px;
  color: #e9901d;
}

.btn-appointment {
  position: absolute;
  width: 100%;
  height: 46px;
  line-height: 46px;
  background-color: #e9901d;
  font-size: 16px;
  color: #fff;
  left: 0;
  bottom: 0;
  z-index: 999;
  display:block;
  text-align: center;
}

@media screen and (min-width: 999px) {
  .page-result {
    background-color: #fff;
    left: 100%;
    width: 50%;
  }

  .nav-bar-result {
    display: none;
    position: absolute;
    left: 0;
    top:0;
    right: 0;
    height: 0;
  }

  .page-result-container {
    padding: 0;
    display: flex;
    flex-flow: column;
    height: 100%;
    align-items: center;
  }

  .result-header {
    position: relative;
    padding: 30px 0;
    color: #fff;
    width: 100%;
  }

  .result-header-title {
    font-size: 26px;
    text-align: center;
    display: block;
  }

  .result-header-subtitle {
    width: 400px;
    margin: 30px auto 0;
    font-size: 16px;
    color: #fbf5ed;
  }

  .rst-btm-mobile {
    display: none;
  }

  .rst-btm-pc {
    display: block;
  }

  .btn-appointment {
    display: none
  }
}
</style>
