<template>
  <div class="p-3" style=" max-width: 400px; margin: 50px auto; background: #234">
   
    <!-- Calculator Result-->
    <div class="w-full rounded m-2 p-4 text-center lead font-weight-bold text-white bg-vue-dark">
      {{calculatorValue || 0}}
    </div>

    <!-- Calculator Buttons-->
    <div class="row no-gutters">
      <div class="col-3" v-for ="n in calculatorElements" :key="n">
        <div class="lead text-white text-center m-1 py-2 bg-vue-dark rounded hover-class" :class="{'bg-vue-green' : ['C', ',','/', '-', '+', '*', '%' , '='].includes(n)}"
        @click="action (n)"
        >
          {{n}}
        </div>
      </div>

    </div>

  </div>
</template>

<script>
export default {
  name: 'Calculator-app',
  props: {
    msg: String
  },
  data(){
  return {
    calculatorValue: '',
    calculatorElements: [ 'C',"*",'/','-',7,8,9,'+',4,5,6,'%',1,2,3,'=',0,'.'],
    operator: null,
  }
},
methods: {
  action (n){
    if (!isNaN (n) || n === '.'){
      this.calculatorValue += n + '';
    }

    if (n==='C') {
      this.calculatorValue = '';
    }
    if (n==='%') {
      this.calculatorValue = this.calculatorValue / 100 + '';
    }
    if (['/', '*', '-', '+'].includes(n)) {
      this.operator = n;
      this.previusCalculator = this.calculatorValue;
      this.calculatorValue = '';
    }
    if (n==='=') {
      this.calculatorValue= eval (
        this.previusCalculator + this.operator + this.calculatorValue
      );
    }
  }
}
}

</script>

<style scoped>
.bg-vue-dark {
  background: #31475e;
}
.hover-class:hover {
  cursor: pointer;
  background: #3d5875;
}
.bg-vue-green{
  background: #3fb984 ;
}

</style>
