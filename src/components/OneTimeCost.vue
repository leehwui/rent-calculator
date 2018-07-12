<template>
  <div class="page-one-time-cost">
    <nav-bar
       title="前期投入"
       @back-btn-clicked="emitBackButtonClicked" 
       @ok-btn-clicked="emitBackButtonClicked">
    </nav-bar>
    <div class="body-o-t-c">
        <div class="user-input"> {{ userInput }} </div>
        <div class="detail">前期投入明细 <a href="#"
            @click=emitDetailsClicked>!</a> </div>
    
        <div class="form-o-t-c">
          <calculator-cell
              label="装修费"
              type="input"
              :initialVal="renovationCost"
              @val-updated="updateRenovationCost"
            ></calculator-cell>
          <calculator-cell
              label="办公家具"
              type="input"
              :initialVal="furnitureCost"
              @val-updated="updateFurnitureCost"
            ></calculator-cell>
          <calculator-cell
              label="打印机"
              type="input"
              :initialVal="printerCost"
              @val-updated="updatePrinterCost"
            ></calculator-cell>
          <calculator-cell
              label="投影仪"
              type="input"
              :initialVal="projectorCost"
              @val-updated="updateProjectorCost"
            ></calculator-cell>
        </div>

        <div class="result-o-t-c">
          固定成本总和: <b>{{ result }} RMB</b>
        </div>

        <div class="button-box">
          <a class="confirm-btn" href="#" @click="emitBackButtonClicked">确认</a>
        </div>
    </div>
  </div>
</template>

<script>
import NavBar from './NavBar.vue'
import CalculatorCell from './CalculatorCell.vue'

export default {
  name: 'OneTimeCost',

  components: {
    NavBar,
    CalculatorCell,
  },

  props: {
    userInput: String,
    area: Number,
    members: Number,
  },

  data() {
    return {
      renovationCost: 0,
      furnitureCost: 0,
      printerCost: 2300,
      projectorCost: 2800,
    }
  },

  computed: {
    result: function() {
      return this.renovationCost + this.furnitureCost + this.printerCost 
      + this.projectorCost
    }
  },

  created() {
    this.renovationCost = this.area * 600
    this.furnitureCost = this.members * 700
  },

  methods: {
    updateRenovationCost($e) {
      if (isNaN(parseInt($e))) {
        this.renovationCost = 0
      } else {
        this.renovationCost = parseInt($e)
      }
    },

    updateFurnitureCost($e) {
      if (isNaN(parseInt($e))) {
        this.furnitureCost = 0
      } else {
        this.furnitureCost = parseInt($e)
      }
    },

    updatePrinterCost($e) {
      if (isNaN(parseInt($e))) {
        this.printerCost = 0
      } else {
        this.printerCost = parseInt($e)
      }
    },

    updateProjectorCost($e) {
      if (isNaN(parseInt($e))) {
        this.projectorCost = 0
      } else {
        this.projectorCost = parseInt($e)
      }
    },

    emitBackButtonClicked() {
      this.$emit('back-btn-clicked', this.result)
    },
    emitDetailsClicked() {
      this.$emit('details-clicked');
    }
  }
}
</script>

<style scoped>
.page-one-time-cost {
  position: absolute;
  width:100%;
  height: 100%;
  left: 0;
  top:0;
  z-index: 5;
  overflow: auto;
  background-color: #f7f9fa;
  -webkit-overflow-scrolling: touch;
}

.body-o-t-c {
  padding-top: 44px;

}

.body-o-t-c .user-input {
  margin-top: 15px;
  padding: 20px;
  background: #fbf5ed;
  color: #e9901d;
  box-shadow: 0 1px 4px 0 rgba(0,0,0,.1)
}

.body-o-t-c .detail {
  padding: 15px 15px 0;
  color: #9b9b9b;
  line-height: 20px;
}

.body-o-t-c .detail a {
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


.form-o-t-c {
  position: relative;
  margin-top: 15px;
  background-color: #fff;
  box-shadow: 0 1px 4px 0 rgba(0,0,0,.1)
}

.result-o-t-c {
  padding: 20px;
  text-align: right;
}
.result-o-t-c  b {
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
  .page-one-time-cost {
    position: absolute;
    top: 0;
    height: 100%;
    width: 50%;
    left: 50%;
    background: #45af5e; 
    z-index:10;
  }

  .body-o-t-c {
    width: 80%;
    max-width: 500px;
    margin: 0 auto;
  }

  .body-o-t-c .user-input {
    border-radius: 5px;
    background-color: #fff;
    box-shadow: 0 1px 4px 0 rgba(0,0,0,.1);
    color: #e9901d;
    line-height: 20px;
    margin-left: 150px;
    font-size: 14px;
  }

  .body-o-t-c .detail {
    text-align: center;
    color: #000;
    font-size: 17px;
    padding: 20px 20px 0;
    margin-left: 150px;
  }

  .body-o-t-c .detail a{
    border-color: #000;
    color: #000;
    width: 17px;
    height: 17px;
    font-size: 12px;
    margin-left: 10px;
    cursor: pointer;
  }

  .form-o-t-c {
    background: 0 0;
    box-shadow: 0 0 0;
    font-size: 16px;
  }

  .result-o-t-c {
    padding: 0;
  }

  .result-o-t-c b {
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
