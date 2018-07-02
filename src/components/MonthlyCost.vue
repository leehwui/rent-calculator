<template>
  <div class="monthly-cost-page">
      <nav-bar
         @back-btn-clicked="emitBackButtonClicked" >
      </nav-bar>

      <div class="m-c-body">
        <div class="user-input"> {{ userInput }} </div>
        <div class="detail">每月办公室支出明细 <a href="#"
            @click=emitDetailsClicked>!</a> </div>

        <div class="m-c-form">
          <calculator-cell
              label="月租金"
              type="input"
              :initialVal="rent"
              @val-updated="updateRent"
            ></calculator-cell>
        
            <calculator-cell
                label="物业费"
                type="input"
                :initialVal="managementFee"
                @val-updated="updateManagementFee"
              ></calculator-cell>

            <calculator-cell
                label="宽带费"
                type="input"
                :initialVal="internetFee"
                @val-updated="updateInternetFee"
              ></calculator-cell>

            <calculator-cell
                label="水电费"
                type="input"
                :initialVal="electricity"
                @val-updated="updateElectricity"
              ></calculator-cell>
            <calculator-cell
                label="保洁费"
                type="input"
                :initialVal="cleaningFee"
                @val-updated="updateCleaningFee"
              ></calculator-cell>
        </div>

        <div class="m-c-result">
          每月总和: <b>{{ result }} RMB</b>
        </div>

        <div class="button-box">
          <a class="confirm-btn" href="#" @click="emitBackButtonClicked">确认</a>
        </div>
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
    location: Object,
    area: Number,
  },

  computed: {
    //rent: function() {
    //  var rent = 0
    //  if (typeof this.location.city != 'undefined'
    //    && typeof this.location.district != 'undefined') {
    //      rent = this.rentTable[this.location.city][this.location.district]
    //      * this.area
    //    }

    //  return  parseFloat(rent.toFixed(2))
    //},

    //managementFee: function() {
    //  var managementFee = 0
    //  if (typeof this.location.city != 'undefined'
    //    && typeof this.location.district != 'undefined') {
    //      managementFee =
    //        this.managementTable[this.location.city][this.location.district] *
    //      this.area
    //    }

    //  return parseFloat(managementFee.toFixed(2))
    //},
    //    
    //internetFee: {
    //  get: function() {
    //    return Math.ceil(this.area/100) * 100;
    //  },
    //  set: function(newVal) {
    //    
    //  }
    //},

    //electricity: function() {
    //  return this.area * 8.5;
    //},

    result: function() {
      var cleaningFee = 0
      if (typeof this.cleaningFee == 'number') {
        cleaningFee = this.cleaningFee
      }

      return this.rent + this.managementFee 
        + this.internetFee + this.electricity
        + cleaningFee
    },
  },
  created() {
    var rent =0
    if (typeof this.location.city != 'undefined'
      && typeof this.location.district != 'undefined') {
        rent = this.rentTable[this.location.city][this.location.district]
        * this.area
      }

    this.rent = Math.ceil(rent.toFixed(2))

    var managementFee = 0
    if (typeof this.location.city != 'undefined'
      && typeof this.location.district != 'undefined') {
        managementFee =
          this.managementTable[this.location.city][this.location.district] *
        this.area
      }

    this.managementFee =  Math.ceil(managementFee.toFixed(2))
    this.internetFee = Math.ceil(this.area/100) * 100;
    this.electricity = Math.ceil(this.area * 8.5)
  },

  data() {
    return {
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
      rent: 0,
      managementFee: 0,
      internetFee: 0,
      electricity: 0,
      cleaningFee: 0,
    }
  },
  methods: {
    updateCleaningFee($e) {
      if (isNaN(parseInt($e))) {
        this.cleaningFee = 0
      } else {
        this.cleaningFee = parseInt($e)
      }
      console.log(this.cleaningFee)
    },
    updateElectricity($e) {
      this.electricity = parseInt($e)
    },
    updateInternetFee($e) {
      this.internetFee = parseInt($e)
    },
    updateManagementFee($e) {
      this.managementFee = parseInt($e)
    },
    updateRent($e) {
      this.rent = parseInt($e)
    },
    emitBackButtonClicked() {
      this.$emit('back-btn-clicked', this.result)
    },
    emitDetailsClicked() {
      this.$emit('details-clicked')
    },
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

.m-c-body .detail {
  padding: 15px 15px 0;
  color: #9b9b9b;
  line-height: 20px;
}

.m-c-body .detail a {
  width: 16px;
  height: 16px;
  line-height: 16px;
  border-radius: 50%;
  text-align: center;
  color: #ffb600;
  border: 1px solid #ffb600;
  vertical-align: center;
  display: inline-block;
  margin-left: 10px;
  font-size: 12px;
}

.details-modal {
  z-index: 12;
}

.m-c-form {
  position: relative;
  margin-top: 15px;
  background-color: #fff;
  box-shadow: 0 1px 4px 0 rgba(0,0,0,.1)
}

.m-c-result {
  padding: 20px;
  text-align: right;
}

.m-c-result b {
  font-size: 20px;
  color: #e9901d;
}

.button-box {
  display: none;
}

.confirm-btn {
  display: block;
  text-align: center;
  color: #fff;
  height: 50px;
  line-height: 50px;
  border-radius: 6px;
  background-color: #e9901d;
  font-size: 20px;
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

  .m-c-body .detail {
    text-align: center;
    color: #000;
    font-size: 17px;
    padding: 20px 20px 0;
    margin-left: 150px;
  }

  .m-c-body .detail a{
    border-color: #000;
    color: #000;
    width: 17px;
    height: 17px;
    font-size: 12px;
    margin-left: 10px;
    cursor: pointer;
  }

  .m-c-form {
    background: 0 0;
    box-shadow: 0 0 0;
    font-size: 16px;
  }

  .m-c-result {
    padding: 0;
  }

  .m-c-result b {
    color: #000;
  }

  .button-box {
    display: block;
    padding: 20px 0 20px 150px;
  }

  .confirm-btn {
    background: #000;
  }

}
</style>
