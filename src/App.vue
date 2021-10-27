<template>
  <div id="app">
    <div>제작 493 SIR 우진</div>
    <br>
    <div>백투백 랠리 계산용 1번째 랠리기준</div>
    <div>1번째랠리 행군시간</div>
    <input type="number" v-model="M1" style="width:80px">
    <label style="width:40px">분</label>
    <input type="number" v-model="S1" style="width:80px">
    <label style="width:40px">초</label>
    <input type="text" placeholder="랠리장 이름 메모" style="width:200px">
    <div>2번째랠리 행군시간</div>
    <input type="number" v-model="M2" style="width:80px">
    <label style="width:40px">분</label>
    <input type="number" v-model="S2" style="width:80px">
    <label style="width:40px">초</label>
    <input type="text" placeholder="랠리장 이름 메모" style="width:200px">
    <br>
    <label>2번째랠리 출발시간 : </label>
    <input type="text" v-model="T2" disabled>
    <div>3번째랠리 행군시간</div>
    <input type="number" v-model="M3" style="width:80px">
    <label style="width:40px">분</label>
    <input type="number" v-model="S3" style="width:80px">
    <label style="width:40px">초</label>
    <input type="text" placeholder="랠리장 이름 메모" style="width:200px">
    <br>
    <label>3번째랠리 출발시간 : </label>
    <input type="text" v-model="T3" disabled>
    <br>
  </div>
</template>

<script>
export default {
  name: 'App2',
  data () {
    return {
        Inf : 0,
        Rid : 0,
        Hun : 0,
        all : 0,
        M1 : 0,
        M2 : 0,
        M3 : 0,
        M4 : 0,
        S1 : 0,
        S2 : 0,
        S3 : 0,
        S4 : 0,
        T1 : 0,
        T2 : 0,
        T3 : 0,
        T4 : 0,
        BS1 : 0,
        BS2 : 0,
        BM1 : 0,
        BM2 : 0,
        BT1 : 0,
        BT2 : 0,
    }
  },
  watch:{
    'M1': {
        handler: function(val, oldVal) {
            if(val != oldVal){
                this.setTime();
            }
        }
    },
    'M2': {
     handler: function(val, oldVal) {
         if(val != oldVal){
             this.setTime();
         }
     }
    },
    'M3': {
    handler: function(val, oldVal) {
       if(val != oldVal){
           this.setTime();
       }
    }
    },
    'M4': {
     handler: function(val, oldVal) {
         if(val != oldVal){
             this.setTime();
         }
     }
    },
     'S1': {
         handler: function(val, oldVal) {
             if(val != oldVal){
                 this.setTime();
             }
         }
     },
     'S2': {
      handler: function(val, oldVal) {
          if(val != oldVal){
              this.setTime();
          }
      }
     },
     'S3': {
     handler: function(val, oldVal) {
        if(val != oldVal){
            this.setTime();
        }
     }
     },
     'S4': {
      handler: function(val, oldVal) {
          if(val != oldVal){
              this.setTime();
          }
      }
      },
     'BS1': {
      handler: function(val, oldVal) {
          if(val != oldVal){
              this.setBackToBack();
          }
        }
      },
     'BS2': {
      handler: function(val, oldVal) {
          if(val != oldVal){
              this.setBackToBack();
          }
        }
      },
     'BM1': {
      handler: function(val, oldVal) {
          if(val != oldVal){
              this.setBackToBack();
          }
        }
      },
     'BM2': {
      handler: function(val, oldVal) {
          if(val != oldVal){
              this.setBackToBack();
          }
      }
     }
  },
  methods:{
    setUnit: function(){
    },
    setTime: function(){
        this.T1 = parseInt(this.M1*60)+parseInt(this.S1);
        var t2,t3;
        
        if(this.M2 != '')
            t2 = (300-(parseInt(this.T1) - (parseInt(this.M2*60) + parseInt(this.S2))));
        else
            t2 = (300-(parseInt(this.T1) - (parseInt(this.S2))));
        if(parseInt(t2)%60>10)
            this.T2 = Math.floor(parseInt(t2)/60) + ':' + parseInt(t2)%60;
        else
            this.T2 = Math.floor(parseInt(t2)/60) + ':0' + parseInt(t2)%60;
        if(this.M3 != '')
            t3 = (300-(parseInt(this.T1) - (parseInt(this.M3*60) + parseInt(this.S3))));
        else
            t3 = (300-(parseInt(this.T1) - (parseInt(this.S3))));
        
        if(parseInt(t3%60)>10)
            this.T3 = Math.floor(t3/60) + ':' + t3%60;
        else
            this.T3 = Math.floor(t3/60) + ':0' + t3%60;
    }
  },
}
</script>

<style>
label {
    width:100px;
    font-size: 20px;
    font-weigh: border;
}
input{
    width:200px;
    font-size: 20px;
}
div {
    font-size: 20px;
    font-weight:bold;
}

</style>
