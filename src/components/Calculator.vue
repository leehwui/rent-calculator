<template>
  <div class="calc-wrapper">
    <div class="calc" v-bind:class="{ is_calced: isCalced }">

      <intro> </intro>
      <main-page
         :locations="locations"
         :monthlyCost="monthlyCost"
         :oneTimeCost="oneTimeCost"
         :area="area"
         @monthly-clicked="showMonthly"
         @onetime-clicked="showOneTimeCost"
         @location-updated="updateLocation"
         @members-updated="updateMembers"
         @area-updated="updateArea"
         @duration-updated="updateDuration"
         @calculated="showResultPage"
        ></main-page>

      <transition name="slide-from-right" mode="in-out">
        
        <monthly-cost-page
          v-if="isShowingMonthly"
          :user-input="userInput"
          :area="area"
          :location="location"
          @back-btn-clicked="hideMonthlyCostPage"
          @details-clicked="showMonthlyCostDetail"
          >
        
        </monthly-cost-page>


        <one-time-cost 
          v-if="isShowingOneTime"
          :user-input="userInput"
          :area="area"
          :members="members"
          @back-btn-clicked="hideOneTimeCostPage"
          @details-clicked="showOneTimeCostDetail">
        
        </one-time-cost>
      </transition>

      <result-page
        :result="costPerPersion"
          @back-to-main="hideResultPage"
        >
      </result-page>

    </div>
      <modal name="details-monthly" 
             :adaptive="true"
             height="auto"
          >
        <div class="details-modal-title">
          费用参考说明
          <span class="details-modal-close-btn"
            @click="$modal.hide('details-monthly')">
            X
          </span>
        </div>
        <div class="details-modal-body">
          <p>
            • 根据你定义的办公室区域及面积，系统会给出相应费用建议供参考，例:
          </p>
          <p>静安区，8人，100平，则相应费用为 </p>
          <table>
            <tbody>
              <tr>
                <td class="details-table-td">月租金</td>
                <td class="details-table-td">100平*8.8元/平/天*30天＝26,400元</td>
              </tr>
              <tr>
                <td class="details-table-td">物业费</td>
                <td class="details-table-td">100平*25元/平＝2,500元</td>
              </tr>
              <tr>
                <td class="details-table-td">宽带费</td>
                <td class="details-table-td">企业宽带 50M：500元/月</td>
              </tr>
              <tr>
                <td class="details-table-td">水电费</td>
                <td class="details-table-td">100平*10元/平/月＝1,000元</td>
              </tr>
              <tr>
                <td class="details-table-td">保洁费</td>
                <td class="details-table-td">3,000元/月</td>
              </tr>
            </tbody>
          </table>
          <p>
            • 你也可以点击各项栏目，并根据实际情况输入，不涉及的项目输入“0”
          </p>
        </div>
      </modal>

      <modal name="details-one-time-cost" 
             :adaptive="true"
             height="auto"
          >
        <div class="details-modal-title">
          费用参考说明
          <span class="details-modal-close-btn"
            @click="$modal.hide('details-one-time-cost')">
            X
          </span>
        </div>
        <div class="details-modal-body">
          <p>
            • 根据你定义的办公室区域及面积，系统会给出相应费用建议供参考，例:
          </p>
          <p>市南区，5人，40平，则相应费用为 </p>
          <table>
            <tbody>
              <tr>
                <td class="details-table-td">装修费</td>
                <td class="details-table-td">平均600￥/㎡*40㎡＝24000￥</td>
              </tr>
              <tr>
                <td class="details-table-td">办公家具</td>
                <td class="details-table-td">700￥/人*6人＝4200￥</td>
              </tr>
              <tr>
                <td class="details-table-td">传真/打印机</td>
                <td class="details-table-td">平均2300￥／台</td>
              </tr>
              <tr>
                <td class="details-table-td">投影仪</td>
                <td class="details-table-td"> 平均2800￥／台</td>
              </tr>
            </tbody>
          </table>
          <p>
            • 你也可以点击各项栏目，并根据实际情况输入，不涉及的项目输入“0”
          </p>
        </div>
      </modal>

  </div>
</template>

<script>
import Treeselect from '@riophae/vue-treeselect'
import '@riophae/vue-treeselect/dist/vue-treeselect.css'
import VueSlideBar from 'vue-slide-bar'
import Intro from './Intro.vue'
import MainPage from './MainPage.vue'
import MonthlyCostPage from './MonthlyCost.vue'
import OneTimeCost from './OneTimeCost.vue'
import ResultPage from './ResultPage.vue'


export default {
  name: 'Calculator',
  components: { 
    Treeselect, 
    VueSlideBar, 
    Intro,
    MainPage,
    MonthlyCostPage,
    OneTimeCost,
    ResultPage,
  },

  data () {
    return {
      isShowingMonthly: false,
      isShowingOneTime: false,
      showMonthlyPage: false,
      showPreCost: false,
      numMember: 0,
      area: 30,
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
      rentTable: {
        qingdao: {
          shinan: 2.8,
          shibei: 2.2,
          laoshan: 3.2,
          huangdao: 1.5,
          licang: 1.8,
        }
      },
      managementTable: {
        qingdao: {
          shinan: 6.0,
          shibei: 2.0,
          laoshan: 4.5,
          huangdao: 2.8,
          licang: 1.8,
        }
      },
      location: null,
      isCalced: false,
      members: 0,
      monthlyCost: 0,
      oneTimeCost: 0,
      term: 0,
      showAreaSeletion: false,
      cities: ['qingdao', 'shanghai', 'beijing'], 
      duration:0,
      costPerPersion: null,
    }
  },

  computed: {
    userInput: function() {
      var districtStr = '';
      var memberStr = '';
      var areaStr = '';
      var str = '已选择: ';

      if (this.location !== null) {
        for(let city of this.locations) {
          if (this.location.city == city.id) {
            for(let district of city.children) {
              if (this.location.district == district.id)
                districtStr = district.label + '区 ';
            }
          }
        }
      }
      if (this.members > 0 )  {
        var memberStr = this.members + '人团队 ';
      }
      if (this.area > 0) {
        var areaStr = this.area + '平方米 ';
      }

      if (districtStr.length > 0) {
        str += districtStr;
      } 
      if(memberStr.length > 0) {
        str +=  memberStr;
      }
      if(areaStr.length > 0) {
        str += areaStr;
      }

      return str;
    }
  },

  methods: {
    hideResultPage() {
      this.isCalced = false
    },
    showResultPage($e) {
      this.isCalced = true
      this.costPerPersion = parseInt($e)
    },
    updateDuration($e) {
      this.duration = $e
    },
    showMonthlyCostDetail() {
      this.$modal.show('details-monthly');
    },
    showOneTimeCostDetail() {
      this.$modal.show('details-one-time-cost');
    },
    updateArea($e) {
      console.log($e);
      this.area = $e;
    },
    updateLocation($e) {
      console.log($e);
      this.location = $e;
    },
    updateMembers($e) {
      this.members = parseInt($e);
      console.log(this.members);
    },

    hideMonthlyCostPage($e) {
      console.log($e)
      this.monthlyCost = $e
      this.isShowingMonthly = false
    },

    hideOneTimeCostPage($e) {
      console.log($e)
      this.oneTimeCost = $e
      this.isShowingOneTime = false
    },

    showMonthly() {
      if (this.location !== null && this.members !=0) {
        this.isShowingMonthly = true;
      } else {
        console.log('getting here');
        this.$toast("请选择区域、人数", {
          className: ['empty-warning'],
          horizontalPosition: 'center',
          verticalPosition: '',
          duration: 1500,
        });
      }

    },
    showOneTimeCost() {
      if (this.location !== null && this.members !=0) {
        this.isShowingOneTime = true;
      } else {
        console.log('getting here');
        this.$toast("请选择区域、人数", {
          className: ['empty-warning'],
          horizontalPosition: 'center',
          verticalPosition: '',
          duration: 1500,
        });
      }
    },

    calculate: function() {
      this.isCalced = !this.isCalced;
    },
    onAreaClick: function() {
      this.showAreaSeletion = !this.showAreaSeletion;
      console.log('on select Area click...');
    },

    showDetailModal: function() {
      this.$refs.detailModal.open()
    }

  },
}
</script>

<!-- Add "scoped" attribute to limit CSS to this component only -->
<style>
.calc-wrapper {
  height: 100%;
  overflow: hidden;
  position: relative;
}
.calc {
  height: 100%;
  position: absolute;
  left: 0;
  top: 0;
  width: 100%;
  color: #2b2b2b;
  overflow: visible;
  font-size: 16px;
}


.left {
  display: none;
}

.result {
  left: 100% !important;
}

.calc-page {
  position: absolute;
  width: 100%;
  height: 100%;
  left: 0;
  top: 0;
  z-index: 1;
  overflow: auto;
  background-color: #f7f9fa;
  -webkit-overflow-scrolling: touch;
}

.is_calced {
  left: -100%;
  transition: all .5s ease
}

.cal__form {
  position: relative;
  margin-top: 15px;
  background-color: #fff;
  box-shadow: 0 1px 4px 0 rgba(0,0,0,.1)
}

.cal__fp {
  position: relative;
  min-height: 51px;
  border-bottom: 1px solid rgba(0,0,0,.1);
  margin: 0 20px;
}

.cal__label {
  line-height: 50px;
  display: block;
  position: absolute;
  left: 0;
  top: 0;
  padding: 0;
  text-transform: capitalize;
}

.calc__fp.is-sel .calc__mid {
  padding-right: 20px;
}

.clearfix {
  clear: both;
}

.calc__mid {
  padding: 0;
}

.calc__label {
  line-height: 50px;
  display: block;
  position: absolute;
  left: 0;
  top: 0;
  padding: 0;
  text-transform: capitalize;
}

.calc__ins {
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

.calc__bar {
  position: absolute;
  left: 0;
  top: 0;
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

.calc__bar .back {
  width: 10px;
  height: 10px;
  display: inline-block;
  border-top: 2px solid #fff;
  border-left: 2px solid #fff;
  -webkit-transform: rotate(-45deg);
  transform: rotate(-45deg);
  vertical-align: middle;
}

.calc__bar .right {
  position: absolute;
  right: 0;
  top: 0;
  z-index: 2;
  color: #fff;
  padding: 0 20px;
  opacity: .7;
  font-size: 14px;
}

a, a:link, a:hover, a:active, a:visited {
  text-decoration: none;
  cursor: pointer;
}

.monthly-cost .t1, .pre-cost .t1 {
  margin-top: 15px;
  padding: 20px;
  background: #fbf5ed;
  color: #e9901d;
  box-shadow: 0 1px 4px 0 rgba(0,0,0,.1);
}

.monthly-cost .t2 a, .pre-cost .t2 a {
  width: 16px;
  height: 16px;
  line-height: 16px;
  border-radius: 50%;
  text-align: center;
  color: #ffb600;
  border: 1px solid #ffb600;
  vertical-align: middle;
  display: inline-block;
  margin-left: 10px;
  font-size: 12px;
}
.result {
  left: 100%
}

.slide-from-right-enter-active {
  transition:  all 1.2s ease;
}

.slide-from-right-leave-active {
  transition: all 1.2s ease;
}

.slide-from-right-enter,.slide-from-right-leave-to {
  transform: translateX(100%);
  left: 100%;
}

@media screen and (min-width: 999px) {
  .calc-wrapper: {
    height: 100%;
  }

  .calc {
    position: absolute;
    left: 0;
    top: 0;
    bottom: 0;
    height: auto;
    width: 100%;
    overflow: visible;
  }

  .wrapper {
    height: 100%;
    overflow: auto;
    display: -webkit-box;
    display: -ms-flexbox;
    display: flex;
    -webkit-box-align: center;
    -ms-flex-align: center;
    align-items: center;
    padding: 20px 0;
  }

  .intro {
    display: block;
    position: relative;
    z-index: 11;
    background: #fff;
    padding: 0;
    overflow: visible;
  }

  .calc-page {
    width: 50%;
    right: auto;
    left: 0;
  }

  .calc__fp.is-unit {
    padding-right: 0;
  }

  .main {
    overflow: visible;
    z-index: 10;
    background: #ffbe00;
    left: 50%;
  }

  .pre-cost, .monthly-cost {
    z-index: 11;
    background: #ffbe00;
    left: 50%;
  }

  .main .content  {
    width: 80%;
    max-width: 500px;
    margin: 0 auto;
  }

  .result {
    background-color: #fff;
    left: 100%;
  }

  .is_calced {
    left: -50%;
    transition: left .5s linear
  }

  .form-item {
    margin: 0 0 25px;
    min-height: 51px;
  }

  .form-item label {
    height: 50px;
  }

  .form-item .form-input {
    min-height: 50px;
  }

  .calc__form {
    background: 0 0;
    box-shadow: 0 0 0;
    font-size: 16px;
  }

  .calc__fp.is-sel {
    padding: 0;
  }

  .calc__fp: {
    padding: 0;
    margin: 0 0 25px;
    border: 0;
  }

  .calc__label: {
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

  .calc__mid {
    min-height: 50px;
    border-radius: 5px;
    background-color: rgba(255,255,255,.8);
    box-shadow: 0 1px 4px 0 rgba(0,0,0,.1);
    padding: 0;
    margin-left: 150px;
  }

  .calc__ins {
    height: 50px;
    line-height: normal;
    color: #2b2b2b;
    padding: 10px 30px;
    text-align: left;
    border-radius: 5px;
  }


  .calc__bar {
    position: absolute;
    left: 0;
    top: 0;
    right: 0;
    height: 0;
  }

  .calc__bar .left {
    position: absolute;
    left: 50px;
    top: 30px;
    width: 30px;
    height: 30px;
    line-height: 30px;
    border: 1px solid #000;
    border-radius: 50%;
    display: block;
    padding: 0;
  }

  .calc__bar .left .back {
    border-color: #000;
    margin-left: 3px;
    margin-top: -3px;
  }

  .calc__bar span {
    display: none;
  }

  .calc__bar .right {
    display: none;
  }

  .monthly-cost .mid, .pre-cost .mid {
    width: 80%;
    max-width: 500px;
    margin: 0 auto;
  }

  .monthly-cost .t1, .pre-cost .t1 {
    border-radius: 5px;
    background-color: #fff;
    box-shadow: 0 1px 4px 0 rgba(0,0,0,.1);
    color: #e9901d;
    line-height: 20px;
    margin-left: 150px;
    font-size: 14px;
  }

  .monthly-cost .t2, .pre-cost .t2 {
    text-align: center;
    color: #000;
    font-size: 17px;
    padding: 20px 0 0;
    margin-left: 150px;
  }

  .monthly-cost .t2 a, .pre-cost .t2 a {
    border-color: #000;
    color: #000;
    width: 17px;
    height: 17px;
    font-size: 12px;
    margin-left: 10px;
    cursor: pointer;
  }
  
  .monthly-cost .wrapper, .pre-cost .wrapper {
    display: -webkit-box;
    display: -ms-flexbox;
    display: flex;
    -webkit-box-align: center;
    -ms-flex-align: center;
    align-items: center;
    padding: 20px 0;
  }

  .expendable {
    cursor: pointer;
  }
}

@media screen and (max-height: 550px) and (min-width: 999px) {
  .main .wrapper {
    display: block;
  }
}

@media screen and (max-height: 660px) and (min-height: 999px) {
  .pre-cost .wrapper {
    display: block;
  }
}


.area {
  width: 100%;
}

.input-container {
  position: relative;
}

.input-container i {
  position: absolute;
  top: 10px;
  right: 20px;
}

.details-modal-title {
  position: relative;
  line-height: 54px;
  background: #4a90e2;
  padding: 0 20px;
}

.details-modal-title span {
  width: 54px;
  display: inline-block;
  float: right;
  color: #fff;
  text-align: center;
  margin-right: -20px;
}

.details-modal-body {
  padding: 10px 20px 20px;
  font-size: 12px;
}


.details-modal-body p {
  color: #2b2b2b;
  line-height: 16px;
  padding: 5px 0;
}

.details-modal-body table {
  border-collapse: collapse;
}

.details-modal-body table td{
  padding: 10px;
  border: solid 1px #2b2b2b;
}

.empty-warning {
  top: 50%;
}
</style>
