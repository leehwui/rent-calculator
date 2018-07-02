<template>
    <div class="calc-page intro">
      <div class="logo">
        <img src="../assets/link.jpg" alt="">
      </div>
      <div class="desc">
        <div class="calc-img">
          <img src="../assets/calculator.png" alt="">
        </div>
        <h1>办公室费用计算器</h1>
        <h5>请根据实际情况填写你的花费，帮你核算你每月办公室的具体费用是否合算？</h5>
      </div>
    </div>
</template>

<script>
export default {
  name: 'Intro',
}
</script>

<style>
.intro {
  display: none;
}

@media screen and (min-width: 999px) {
  .intro {
    display: block;
    position: relative;
    z-index: 2;
    background: #fff;
    padding: 0;
    overflow: visible;
  }

  .intro::before {
    content: '';
    display: block;
    width: 15px;
    height: 15px;
    background: #fff;
    position: absolute;
    right: -8px;
    top: 50%;
    margin-top: -8px;
    transform: rotate(45deg);
    z-index: 2;
  }

  .logo {
    position: absolute;
    top: 20px;
    left: 20px;
    height: 96px;
    width: 96px;
    border-radius: 50%;
    overflow: hidden;
  }

  .logo img {
    width: 100%;
    height: 100%;
  }

  .desc {
    position: absolute;
    top: 50%;
    left: 50%;
    transform: translate(-50%,-50%)
  }

  .calc-img  {
    margin-bottom: 25px;
  }

  .desc h1, h5 {
    margin-bottom: 25px;
  }
}


</style>
