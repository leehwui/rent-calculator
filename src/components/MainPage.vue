<template>
  <div class="main-page">
    <div class="mp-container">
      <form class="form">
        <div class="c-form-group">
          <label class="c-form-label" for="">办公室所在区域</label>
          <div class="c-form-control-wrapper">
            <treeselect v-model="location" :multiple="false"
              :disable-branch-nodes="true"
              :options="locations" 
              placeholder="请选择"/>
          </div>
        </div>

        <div class="c-form-group">
          <label for="member" class="c-form-label">团队人数 </label>
          <div class="c-form-control-wrapper">
            <input class="c-form-control" v-model="numMember" type="tel" id="member"
            placeholder="请输入">
          </div>
        </div>

        <div v-if="numMember > 0" class="c-form-group">
          <label for="area" class="c-form-label">办公室面积(平方米)</label>
          <div class="c-form-control-wrapper">
            <input class="c-form-control" v-model="area" type="tel" id="area" placeholder="">
            <VueSlideBar v-model="area" />
          </div>
        </div>


        <div class="c-form-group expandable">
          <label for="monthlycost" class="c-form-label">每月支出</label>
          <div class="c-form-control-wrapper" @click="emitMonthly">
            <div class="fake-input">
              <span class="ph">
                租金，物业费等
              </span>
            </div>
          </div>
        </div>

        <div class="c-form-group expandable">
          <label for="onetimecost" class="c-form-label">前期支出</label>
          <div class="c-form-control-wrapper"
            @click="emitOneTime">
            <div class="fake-input">
              <span class="ph">
               装修，家具等 
              </span>
            </div>
          </div>
        </div>

        <div class="c-form-group expandable">
          <label for="member" class="c-form-label">租赁时长 </label>
          <div class="c-form-control-wrapper">
            <select class="c-form-control" id="" name="">
              <option value="0">请选择</option>
              <option value="">6个月</option>
              <option value="">1年</option>
              <option value="">2年</option>
              <option value="">3年</option>
              <option value="">4年</option>
              <option value="">5年</option>
            </select>
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

  .c-form-group {
    padding: 0;
    margin: 0 0 25px;
    border: 0;
  }

  .c-form-label {
    position: absolute;
    left: -60px;
    top: 0;
    width: 195px;
    white-space: nowrap;
    display: block;
    line-height: 50px;
    text-align: right;
    color: rgba(0,0,0,.7);
  }

  .c-form-control-wrapper {
    min-height: 50px;
    border-radius: 5px;
    background-color: rgba(255,255,255,.8);
    box-shadow: 0 1px 4px 0 rgba(0,0,0,.1);
    padding: 0;
    margin-left: 150px;
  }

  .c-form-control {
    height: 50px;
    line-height: normal;
    color: #2b2b2b;
    padding: 10px 30px;
    text-align: left;
    border-radius: 5px;
  }

  .fake-input {
    height: 50px;
    line-height: 50px;
    text-align: left;
    padding: 0 30px;
    color: #000;
  }

  .fake-input .ph {
    color: #999;
  }
}
</style>
