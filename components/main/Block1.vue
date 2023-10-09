<template>
  <div class="main-top-wrapper">
    <div class="content">
      <div class="grid grid-cols-2 block1">
        
        <div class="block1-left">
          <h1>Smart OrderFlow Aggregator</h1>
          <p class="block-text">Programmable Liquidity Protocol for Modular Networks</p>
          <div class="course">
            <img src="/img/btc.svg" class="inline-block" style="filter:hue-rotate(288deg)"/>
            <span>BTC Price: {{ course.toFixed(2) }} USDT</span>
          </div>
          <a class="btn" href="https://docsend.com/view/26nvcmwmnpiybdap" target="_blank">White Paper</a>
        </div>
        <div class="block1-right">
          <lottie :options="lottieOptions"/>
        </div>

      </div>
      
        
      <div class="background-lottie">
          <lottie :options="backgroundLottieOptions"/>
      </div>
    </div>
  </div>
</template>
<script>
import ShogunLogoLottie from '../../static/assets/shogun_logo_lottie.json'
//import BackgroundLottie from "../../static/assets/lottie-blocks-zoom.json"
import BackgroundLottie from "../../static/assets/wave.json"
import lottie from 'vue-lottie/src/lottie.vue'

export default {
  props: ['course'],
  components: {
    lottie
  },
  data() {
    return {
      lottieOptions: { animationData: ShogunLogoLottie, loop: true },
      backgroundLottieOptions: { animationData: BackgroundLottie, loop: true },
    }
  },
}
</script>
<style>
.main-top-wrapper {
  /*background: #292256;*/
  background: #180010;
  position: relative;
  padding: 100px 0 0px;
}
body h1 {
  color: #fff;
  padding-bottom: 29px;
  font-size: 80px;
  font-weight: 700;
  line-height: 90px;
}
.background-lottie {
  position: absolute;
  top: 0px;
  left: 100px;
  height: 100%;
  opacity: 0.3;
}
.block-text {
  font-size: 24px;
  color: #FFF;
  padding-bottom: 29px;
  padding-top: 40px;
}
.block1-right {
  overflow: hidden;
  z-index: 100;
}
.block1-left {
  padding-top: 250px;
  z-index: 100;
}
.course {
  padding-bottom: 40px;
}
.course span {
  font-size: 18px;
  color: #fff;
  position: relative;
  left: 2px;
  top: 1px;
}
.btn {
  margin-bottom: 50px;
}
@media(max-width: 900px) {
  .background-lottie {
    position: absolute;
    top: 50%;
    height: 50%;
    opacity: 0.3;
  }
  .block1 {
    display: flex !important;
    flex-direction: column;
    align-items: center;
  }
  .block1-left {
    order: 1;
    padding-top: 30px;
  }
  .block1-right {
    overflow: hidden
  }
  .main-top-wrapper {
    padding: 62px 0 45px;
  }
  .block1-left h1 {
    padding-bottom: 12px;
    line-height: 1.4;
  }
  .block-text {
    font-size: 18px;
    padding-top: 20px;
  }
  .course span {
    font-size: 16px;
  }
  .course {
    padding-bottom: 25px;
  }
  .btn {
    height: 44px;
    font-size: 13px;
    padding: 15px 30px;
    margin-bottom: 0px;
  }
}
</style>
