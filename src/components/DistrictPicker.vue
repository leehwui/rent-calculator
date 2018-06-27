<template>
  <div class="picker-wrapper">
    <div class="picker-control" @click="showOptions = !showOptions">
      <span>{{ selectedDistrict ? selectedDistrict : 'Please Select' }}</span>
    </div>
    <div class="select-area" v-if="showOptions">
      <ul class="city-list">
        <li v-for="(item, index) in options" v-bind:key="index"> {{ index }} </li>
      </ul>
    </div>
    <div>
    
    </div>
  </div>
</template>

<script>
export default {
  name: 'DistrictPicker',
  data() {
    return {
      selectedDistrict: null,
      showOptions: false,
      options: {
        qingdao: [
          'shinan',
          'shibei',
          'laoshan',
          'sifang',
        ],
      }
    }
  }


}

</script>

<style scoped>
.picker-wrapper {
  height: 50px;
  z-index: 2;
}
.picker-control {
  height: 50px;
  line-height: 50px;
  margin: 0 30px;
  text-align: left;
}
.select-area {
  background: #f7f9fa;
  border-radius: 5px;
}
ul.city-list {
  height: 50px;
  background: #f0f0f0;
  list-style: none;
  display: flex;
  flex-flow: row;
}
.city-list li {
  display: inline-block;
  margin: 0 25px;
  line-height: 50px;
  cursor: pointer;
}
</style>
