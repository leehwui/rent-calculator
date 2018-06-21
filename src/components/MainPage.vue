<template>
  <div class="main-page">
    <div class="mp-container">
      <form class="form">
        <div class="form-group form-group-lg row">
          <label class="col-sm-4 col-form-label" for="monthlyrent">monthly rent</label>
          <div class="col-sm-6">
            <input class="form-control" type="tel" id="monthlyrent">
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
export default {
  name: 'MainPage'
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
