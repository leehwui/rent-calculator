<template>
  <div class="main-page">
    <div class="mp-container">
      <form class="form">
        <calculator-cell
          label="办公室所在区域"
          placeholder="请选择区域"
          type="district-picker"
          :locations="locations"
          v-on:val-updated="emitLocationUpdated"
          >
        </calculator-cell>

        <calculator-cell 
          label="团队人数" 
          type="input" 
          @val-updated="emitMemebersUpdated">
        </calculator-cell>

        <calculator-cell
          v-if="location !== null && teamMembers !== null"
          label="办公面积"
          type='slider'
          @val-updated="emitAreaUpdated">
        </calculator-cell>

        <calculator-cell
          label="每月支出"
          type="expandable"
          placeholder="请输入"
          @control-clicked="emitMonthlyClickedEvent"
          :isUpdated="isUpdated"
          >
        </calculator-cell>



        <button @click="changeState">change state</button>
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
  data() {
    return {
      isUpdated: false,
      teamMembers: null,
      area: 0,
      locations: [
        {
          id: 'qingdao',
          label: '青岛',
          children: [
            {
              id: 'shinan',
              label: '市南',
            },
            {
              id: 'shibei',
              label: '市北',
            },
            {
              id: 'sifang',
              label: '四方',
            },
            {
              id: 'licang',
              label: '李沧',
            }
          ],
        },
        {
          id:'jinan',
          label: '济南',
          children: [
            {
              id: 'damahou',
              label: '大马猴',
            },
            {
              id: 'choulaomian',
              label: '臭老黾',
            },
            {
              id: 'xinlaide',
              label: '新来的',
            },
          ] 
        }
      ],
      location: null,

    }
  },

  methods: {
    emitAreaUpdated($e) {
      this.$emit('area-updated', $e);
    },

    emitLocationUpdated($e) {
      this.location = $e;
      this.$emit('location-updated', $e);
    },

    emitMemebersUpdated($e) {
      this.teamMembers = $e;
      console.log($e);
      this.$emit('members-updated', $e);
    },

    emitMonthlyClickedEvent() {
      this.$emit('monthly-clicked');
    },
    navigateToMonthlyCost() {
      console.log("naviagting to monthly cost page....");
    },
    bar() {
    
    },
    updateTeamMembers($e) {
      this.teamMembers = $e;
      console.log(this.teamMembers);
    },

    updateLoaction($e) {
      console.log($e);
      this.location = $e;
    },
    changeState() {
      this.isUpdated = !this.isUpdated;
    },

    foo(val) {
      console.log('val changed to: ', val);
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
  width: 100%
}

@media screen and (min-width: 999px) {
  .main-page {
    position: absolute;
    top: 0;
    height: 100%;
    width: 50%;
    left: 50%;
    background: #ffbe00; 
    z-index:10;
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
}
</style>
