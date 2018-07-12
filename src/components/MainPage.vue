<template>
  <div class="main-page">
    <div class="mp-container">
      <div class="mp-header">
        <img src="../assets/header.jpg" alt="">
        <div class="mp-header-text-container">
          <div class="mp-header-text">
            <div class="mp-header-title">
              <span>办公室成本计算器</span>
            </div>
            <div class="mp-header-subtitle">
              <span class="mp-header-subtitle">你的办公成本过高吗?</span>
            </div>
          </div>
        </div>
      </div>

      <form class="form">
        <calculator-cell
          label="办公室所在区域"
          placeholder="请选择区域"
          type="district-picker"
          :locations="locations"
          v-on:val-updated="updateLocation"
          >
        </calculator-cell>

        <calculator-cell 
          label="团队人数" 
          type="input" 
          @val-updated="updateMembers">
        </calculator-cell>

        <calculator-cell
          v-if="location !== null && teamMembers !== null"
          label="办公面积"
          type='slider'
          ref='area'
          :initialVal="area"
          @val-updated="emitAreaUpdated">
        </calculator-cell>

        <calculator-cell
          label="每月支出"
          type="expandable"
          :placeholder="monthlyCost == 0 ? '请输入': monthlyCost.toString()"
          :initialVal="monthlyCost"
          @control-clicked="emitMonthlyClickedEvent"
          :isUpdated="isUpdated"
          >
        </calculator-cell>

        <calculator-cell
          label="前期投入"
          type="expandable"
          :placeholder="oneTimeCost == 0 ? '请输入' : oneTimeCost.toString()"
          :initialVal="oneTimeCost"
          @control-clicked="emitOneTimeCostClicked"
          :isUpdated="isUpdated"
          >
        </calculator-cell>

        <calculator-cell
          label="租赁时长"
          type="select"
          @val-updated='updateDuration' >
        </calculator-cell>

        <div class="btn-box">
          <a class="btn-c" href="#" :disabled="!canCalculate" @click="calculate">计算</a>
        </div>
      </form>

    </div>
  </div>
</template>
<script>

import Treeselect from '@riophae/vue-treeselect'
import VueSlideBar from 'vue-slide-bar'
import CalculatorCell from './CalculatorCell.vue'

export default {
  name: 'MainPage',
  components: {
    Treeselect, 
    VueSlideBar, 
    CalculatorCell,
  },
  props: {
    locations: Array,
    monthlyCost: Number,
    oneTimeCost: Number,
    area: Number,
    members: Number,
  },

  computed: {
    canCalculate: function() {
      return this.location !== null && this.teamMembers > 0 
          && this.monthlyCost > 0 && this.oneTimeCost > 0 
          && this.duration > 0
    },
  },

  data() {
    return {
      isUpdated: false,
      teamMembers: null,
      duration: null,
      location: null,
      result: null,
    }
  },

  methods: {
    calculate() {
      if (! this.canCalculate) {
        return false;
      }

      this.result = Math.ceil((this.oneTimeCost/this.duration 
        + this.monthlyCost)/this.members);

      this.$emit('calculated', this.result);
    },

    emitOneTimeCostClicked() {
      this.$emit('onetime-clicked')
    },
    emitAreaUpdated($e) {
      this.$emit('area-updated', $e);
    },

    updateDuration($e) {
      this.duration = $e
      this.$emit('duration-updated', this.duration)
    },

    updateLocation($e) {
      this.location = $e;
      this.$emit('location-updated', $e);
    },

    updateMembers($e) {
      this.teamMembers = $e;
      this.$emit('members-updated', $e);
    },

    emitMonthlyClickedEvent() {
      this.$emit('monthly-clicked');
    },

    updateTeamMembers($e) {
      this.teamMembers = $e;
    },

    updateLoaction($e) {
      console.log($e);
      this.location = $e;
    },
    changeState() {
      this.isUpdated = !this.isUpdated;
    },

    emitMonthly: function() {
      this.$emit('monthly-clicked');
    },
    emitOneTime: function() {
      this.$emit('onetime-clicked');
    },
  },
}

</script>
<style>
.main-page {
  width: 100%;
}

.c-form-group {
  position: relative;
  min-height: 51px;
  border-bottom: 1px solid rgba(0,0,0,.1);
  margin: 0 20px;
}

.c-form-label {
  line-height: 50px;
  display: block;
  position: absolute;
  left: 0;
  top: 0;
  padding: 0;
  text-transform: capitalize;
}

.c-form-control-wrapper {
  padding-right: 20px;
}

.c-form-control {
  display: block;
  width: 100%;
  height: 50px;
  line-height: normal;
  padding: 10px 0;
  text-align: right;
  color: #e9901d;
  -webkit-appearance: none;
  -moz-appearance: none;
  appearance: none;
}

select, input {
  border: 0;
  outline: 0;
  background: 0 0;
}

.expandable::after {
  display: block;
  content: '';
  width: 10px;
  height: 10px;
  border-top: 2px solid #ddd;
  border-right: 2px solid #ddd;
  position: absolute;
  right: 3px;
  top: 20px;
  -webkit-transform: rotate(45deg);
  transform: rotate(45deg);
}

.expandable.not-opened::after {
  border-color: #e9901d;
  -webkit-animation: update-tip 1s cubic-bezier(0.42,.95,.44,.75) infinite;
  animation: update-tip 1s cubic-bezier(0.42,.95,.44,.75) infinite;
}

.fake-input {
  height: 50px;
  line-height: 50px;
  text-align: right;
  color: #e9901d;
}

.fake-input.ph {
  color: #999;
}

.mp-header {
  position: relative;
  box-shadow: 0 1px 4px 0 rgba(0, 0, 0,.1);
  padding-top: 31.88%;
}

.mp-header img {
  position: absolute;
  display: block;
  height: 100%;
  width: 100%;
  top: 0;
  left: 0;
}

.mp-header-text-container {
  position: absolute;
  left: 0;
  top: 0;
  right: 0;
  bottom: 0;
  display: flex;
  align-items: center;
  line-height: 22px;
}

.mp-header-text {
  color: #e9901d;
  padding-left: 20px;
  line-height: 1.5;
}

.mp-header-title {
  font-size: 20px;
}

.mp-header-subtitle {
  font-size: 12px;
  text-align: left;
}

.btn-box {
  padding: 30px 20px;
}

.btn-c {
  display: block;
  text-align: center;
  color:#fff; 
  height: 50px;
  line-height: 50px;
  border-radius: 5px;
  background-color: #e9901d;
  font-size: 20px;
}

@media screen and (min-width: 999px) {
  .main-page {
    position: absolute;
    top: 0;
    height: 100%;
    width: 50%;
    left: 50%;
    background: #45af5e; 
    z-index:10;
  }

  .main-page::before {
    display: block;
    content: '';
    width: 15px;
    height: 15px;
    background: #45af5e;
    position: absolute;
    right: -8px;
    top: 50%;
    margin-top: -8px;
    transform: rotate(45deg);
    z-index: 2;
  }

  .mp-container {
    display: -webkit-flex;
    display: flex;
    flex-direction: column;
    justify-content: center;
    align-items: center;
    height: 100%;
  }

  .mp-container form {
    width: 80%;
  }
  
  .mp-header {
    display: none;
  }

  .btn-box {
    padding: 0 0 0 150px;
  }

  .btn-box a[disabled] {
    opacity: 1;
    cursor: not-allowed;
  }

  .btn-c {
    background: #000;
  }
  
}
</style>
