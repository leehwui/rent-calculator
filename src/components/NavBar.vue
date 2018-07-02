<template>
  <div class="nav-bar">
    <a class="nav-bar-btn nav-bar-btn-back" href="#"
      @click="emitBackButtonClicked">
      <i class="back"></i>
    </a>
    <span>title</span>
    <a class="nav-bar-btn nav-bar-btn-ok" @click="emitOkClicked"
      href="#">确认</a>
  </div>
</template>

<script>
export default {
  name: 'NavBar',
  methods: {
    emitBackButtonClicked() {
      this.$emit('back-btn-clicked');
    },
    emitOkClicked() {
      this.$emit('ok-btn-clicked');
    },
  },
}
</script>

<style scoped>
.nav-bar {
  position: absolute;
  left:0;
  top:0;
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

.nav-bar-btn {
  position: absolute;
  top: 0;
  z-index: 2;
  color: #fff;
  padding: 0 20px;
  opacity: .7;

}

.nav-bar-btn-back {
  left: 0;
}

.nav-bar-btn-ok {
  right: 0;
}

.nav-bar .back {
  width: 10px;
  height: 10px;
  display: inline-block;
  border-top: 2px solid #fff;
  border-left: 2px solid #fff;
  transform: rotate(-45deg);
  vertical-align: middle;
}

@media screen and (min-width: 999px) {
  .nav-bar {
    position: absolute;
    left: 0;
    top: 0;
    right: 0;
    height:0;
  }

  .nav-bar-btn-back {
    position: absolute;
    left: 50px;
    top: 35px;
    width: 30px;
    height: 30px;
    line-height: 30px;
    border: 1px solid #000;
    border-radius: 50%;
    display: block;
    padding: 0;
  }

  .nav-bar .nav-bar-btn-back .back {
    border-color: #000;
    margin-left: 3px;
    margin-top: -3px;
  }

  .nav-bar span {
    display: none;
  }

  .nav-bar .nav-bar-btn-ok {
    display: none;
  }
}
</style>
