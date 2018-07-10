<template>
  <!-- cell for text input -->
  <div class="c-cell" v-if="type=='input'">
    <label class="c-cell-label" for="">{{ label }}</label>
    <div class="c-cell-control">
      <input class="c-cell-input" type="tel" 
                                  placeholder="请输入"
                                  v-model="val"
      @keyup="updateValue">
    </div>
  </div>

  <!-- cell for navigation -->
  <div class="c-cell c-cell-expandable" v-bind:class="{ updated: isUpdated}"
    v-else-if="type=='expandable'">
    <label class="c-cell-label" for="">{{ label }}</label>
    <div class="c-cell-control" @click="emitClickEvent">
      <div class="c-cell-text-wrapper">
        <span class="ph">
          {{ placeholder }}
        </span>
      </div>
    </div>
  </div>

  <!-- cell for slider -->
  <div class="c-cell c-cell-slider" v-else-if="type=='slider'">
    <label class="c-cell-label" for=""> {{ label }}</label>
    <div class="c-cell-control">
      <input class="c-cell-input" type="tel" 
                                  placeholder="请输入"
                                  v-model="val"
      @keyup="updateValue">
      <div class="slider-wrapper">
        <vue-slider ref="slider" 
          v-model="val" 
          tooltip="false"
          :min="1"
          @callback="updateValue"
          width="auto">
        </vue-slider>
      </div>
    </div>
  </div>

  <!-- cell for district selector -->
  <div class="c-cell c-cell-expandable c-cell-dist-picker"
    v-else-if="type=='district-picker'">
    <label class="c-cell-label" for=""> {{ label }} </label>
    <div class="c-cell-control">
      <district-picker 
        :options="locations"
        v-on:district-set="updateValue"> 
      </district-picker>
    </div>
  </div>

  <!-- cell for dropdown -->
  <div class="c-cell c-cell-expandable" v-else-if="type == 'select'">
    <label for="" class="c-cell-label"> {{ label }}</label>
    <div class="c-cell-control">
      <select class="c-cell-select" id="" name="" v-model="val"
        @change="updateValue">
        <option value="" disabled selected>请选择</option>
        <option value="3">3个月</option>
        <option value="6">6个月</option>
        <option value="12">1年</option>
        <option value="24">2年</option>
        <option value="36">3年</option>
        <option value="48">4年</option>
        <option value="60">5年</option>
        <option value="72">6年</option>
        <option value="84">7年</option>
        <option value="96">8年</option>
        <option value="108">9年</option>
        <option value="120">10年</option>
      </select>
    </div>
  </div>

</template>

<script>
import vueSlider from 'vue-slider-component';
import DistrictPicker from './DistrictPicker.vue';

export default {
  name: 'CalculatorCell',

  components: {
    vueSlider,
    DistrictPicker,
  },

  props: {
    label: String, 
    type: String,
    placeholder: String,
    isUpdated: Boolean,
    locations: Array,
    initialVal: {type: Number, default: 0},
  },

  created() {
    if (this.initialVal != 0) {
      this.val = this.initialVal
    }
  },

  data() {
    return {
      val: '',
    }
  },

  methods: {

    refreshSlider() {
      this.$refs.slider.refresh()
    },
    emitClickEvent() {
      this.$emit('control-clicked');
    },

    updateValue($event) {
      if (this.type == 'district-picker' || 
        (this.type == 'slider' && typeof $event.target == 'undefined')) {
        var data = $event;
      } else {
        var data = $event.target.value;
      }
      this.$emit('val-updated', data);
    },
  }
}

</script>


<style scoped>
.c-cell {
  position: relative;
  min-height: 51px;
  border-bottom: 1px solid rgba(0,0,0,.1);
  margin: 0 20px;
}
/*
.c-cell:hover::before {
  position: absolute;
  display: block;
  content: '';
  top: 5px;
  bottom: 5px;
  left: -20px;
  z-index: 2;
  width: 6px;
  background: #ffb600;
}
*/


.c-cell-expandable::after {
  display: block;
  position: absolute;
  content: '';
  width: 10px;
  height: 10px;
  border-top: 2px solid #ddd;
  border-right: 2px solid #ddd;
  right: 3px;
  top: 20px;
  transform: rotate(45deg);
}

.c-cell-label {
  line-height: 50px;
  display: block;
  position: absolute;
  left: 0;
  top: 0;
  padding: 0;
  text-transform: capitalize;
}

.c-cell-control {
  padding: 0;
}
.c-cell.c-cell-expandable .c-cell-control {
  padding-right: 20px;
}

.c-cell.c-cell-expandable.c-cell-dist-picker  .c-cell-control {
  padding-right: 0px;
}

.c-cell-control:hover {
  background: #fff;
}

.c-cell-input {
  display: block;
  width: 100%;
  height: 50px;
  line-height: normal;
  padding: 10px 0;
  text-align: right;
  color: #e9901d;
}

.c-cell-select {
  color: #e9901d;
  height: 50px;
  line-height: 50px;
  display: block;
  width: auto;
  direction: rtl;
  appearance: none;
  float: right;
}

.c-cell-text-wrapper {
  height: 50px;
  line-height: 50px;
  text-align: right;
  color: #e9901d;
}

.c-cell-expandable.updated::after {
  border-color: #e9901d;
  animation: update-tip 1s cubic-bezier(0.42,.95,.44,.75) infinite;
}

.ph {
  color: #999;
}

.slider-wrapper {
  height: 30px;
}

.area-text-wrapper-sm {
  display: block;
}

.area-text-wrapper-lg {
  display: none;
}

.dist-picker-lg {
  display: none;
}

.dist-picker-sm {
  display: block;
}

.dis-picker-bar {

}


.btn-concel {

}

select,input {
  font-family: inherit;
  font-size: inherit;
  padding: 0;
  border: 0;
  outline: 0;
  background: 0 0;
}

@media screen and (min-width: 999px) {
  .c-cell {
    padding: 0;
    margin: 0 0 25px;
    border: 0;
  }

  .c-cell-expandable::after {
    right: 30px;
    bottom: 20px;
    top: auto;
    border-color: #000;
  }
  .c-cell-label {
    position: absolute;
    left: -60px;
    top: 0;
    width: 195px;
    white-space: nowrap;
    display: block;
    line-height: 50px;
    text-align: right;
    color: rgba(0,0,0,.7)
  }

  .c-cell-control {
    min-height: 50px;
    border-radius: 5px;
    background-color: rgba(255,255,255,.8);
    box-shadow: 0 1px 4px 0 rgba(0,0,0,.1);
    padding: 0;
    margin-left: 150px;
  }

  .c-cell-input {
    height: 50px;
    line-height: normal;
    color: #2b2b2b;
    padding: 10px 30px;
    text-align: left;
    border-radius: 5px;
  }

  .c-cell-select {
    height: 50px;
    line-height: 50px;
    color: #2b2b2b;
    direction: ltr;
    padding: 0 30px;
    width: 100%;
  }

  .c-cell-text-wrapper {
    height: 50px;
    line-height: 50px;
    text-align: left;
    padding: 0 30px;
    color: #000;
  }

  .slider-wrapper {
    margin: 0 30px;
  }

  .area-text-wrapper-sm {
    display: none;
  }

  .area-text-wrapper-lg {
    display: block;
  }

  .dist-picker-lg {
    display: block;
  }
  .dist-picker-sm {
    display: none;
  }
}

@-webkit-keyframes update-tip{
  0%{-webkit-transform:translateX(0) rotate(45deg);transform:translateX(0) rotate(45deg)}
  50%{-webkit-transform:translateX(5px) rotate(45deg);transform:translateX(5px) rotate(45deg)}
  100%{-webkit-transform:translateX(0px) rotate(45deg);transform:translateX(0px) rotate(45deg)}
}
@keyframes update-tip{
  0%{-webkit-transform:translateX(0) rotate(45deg);transform:translateX(0) rotate(45deg)}
  50%{-webkit-transform:translateX(5px) rotate(45deg);transform:translateX(5px) rotate(45deg)}
  100%{-webkit-transform:translateX(0px) rotate(45deg);transform:translateX(0px) rotate(45deg)}}
</style>
