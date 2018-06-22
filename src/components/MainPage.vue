<template>
  <div class="main-page">
    <div class="mp-container">
      <form class="form">
        <div class="form-group form-group-lg row">
          <label class="col-sm-4 col-form-label" for="">办公室所在区域</label>
          <div class="col-sm-6 form-input">
            <treeselect v-model="location" :multiple="false"
              :disable-branch-nodes="true"
              :options="locations" 
              placeholder="请选择"/>
          </div>
        </div>

        <div class="form-group form-group-lg row">
          <label for="member" class="col-sm-4 col-form-label">团队人数 </label>
          <div class="col-sm-6">
            <input class="form-control" v-model="numMember" type="tel" id="member"
            placeholder="请输入">
          </div>
        </div>

        <div v-if="numMember > 0" class="form-group form-group-lg row">
          <label for="area" class="col-sm-4 col-form-label">办公室面积(平方米)</label>
          <div class="col-sm-6">
            <input class="form-control" v-model="area" type="tel" id="area" placeholder="">
            <VueSlideBar v-model="area" />
          </div>
        </div>


        <div class="form-group form-group-lg row">
          <label for="monthlycost" class="col-sm-4 col-form-label">每月支出</label>
          <div class="col-sm-6 input-container" @click="emitMonthly">
            <input class="form-control expendable" type="text" id="monthlycost"
            placeholder="租金物业费等" readonly="readonly">
            <i class="fa fa-chevron-right"></i>
          </div>
        </div>

        <div class="form-group form-group-lg row">
          <label for="onetimecost" class="col-sm-4 col-form-label">前期支出</label>
          <div class="col-sm-6 input-container" @click="emitOneTime">
            <input class="form-control expendable" type="text" id="ontimecost" 
            placeholder="装修家具等" readonly="readonly">
            <i class="fa fa-chevron-right"></i>
          </div>
        </div>

        <div class="form-group form-group-lg row">
          <label class="col-sm-4 col-form-label" for="monthlyrent">monthly rent</label>
          <div class="col-sm-6">
            <input class="form-control" type="tel" id="monthlyrent">
          </div>
        </div>
        
      </form>
    </div>
  </div>
</template>
<script>

import Treeselect from '@riophae/vue-treeselect'
import VueSlideBar from 'vue-slide-bar'

export default {
  name: 'MainPage',
  components: {
    Treeselect, 
    VueSlideBar, 
  },
  data() {
    return {
      numMember: 0,
      area: 0,
      locations: [
        {
          id: 'qingdao',
          label: '青岛',
          children: [
            {
              'id' : 'shinan',
              'label': '市南'
            },
            {
              'id' : 'shibei',
              'label': '市北',
            },
            {
              'id': 'laoshan',
              'label': '崂山',
            },
            {
              'id': 'huangdao',
              'label': '黄岛',
            },
            {
              'id': 'licang',
              'label': '李沧',
            }
          ]
        }
      ], 
      location: null,

    }
  },

  methods: {
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
