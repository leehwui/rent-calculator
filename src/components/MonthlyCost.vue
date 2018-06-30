<template>
  <div class="monthly-cost-page">
      <nav-bar
         @back-btn-clicked="emitBackButtonClicked" >
      </nav-bar>

      <div class="m-c-body">
        <div class="user-input"> {{ userInput }} </div>
      </div>
  </div>
</template>

<script>
import NavBar from './NavBar.vue';
import CalculatorCell from './CalculatorCell.vue';
export default {
  name: 'MonthlyCostPage',

  components: {
    NavBar,
    CalculatorCell,
  },

  props: {
    userInput: String,
  },

  data() {
    return {

    }
  },
  methods: {
    emitBackButtonClicked() {
      this.$emit('back-btn-clicked');
    }
  },
}
</script>

<style>
.m-c-body {
  padding-top: 44px;

}
.m-c-body .user-input {
  margin-top: 15px;
  padding: 20px;
  background: #fbf5ed;
  color: #e9901d;
  box-shadow: 0 1px 4px 0 rgba(0,0,0,.1)
}
.monthly-cost-page {
  position: absolute;
  width:100%;
  height: 100%;
  left: 0;
  top:0;
  z-index: 1;
  overflow: auto;
  background-color: #f7f9fa;
  -webkit-overflow-scrolling: touch;
}

@media screen and (min-width: 999px) {
  .monthly-cost-page {
    position: absolute;
    top: 0;
    height: 100%;
    width: 50%;
    left: 50%;
    background: #ffbe00; 
    z-index:10;
  }

  .m-c-body {
    width: 80%;
    max-width: 500px;
    margin: 0 auto;
  }

  .m-c-body .user-input {
    border-radius: 5px;
    background-color: #fff;
    box-shadow: 0 1px 4px 0 rgba(0,0,0,.1);
    color: #e9901d;
    line-height: 20px;
    margin-left: 150px;
    font-size: 14px;
  }
}
</style>
