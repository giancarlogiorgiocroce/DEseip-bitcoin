<template>
  <section class="py-5">
    <div class="container">

      <!-- Title -->
      <div class="row title text-center">
        <h2>Calcola la tua fee</h2>
      </div>
      <!-- /Title -->

      <!-- Tutorial -->
      <div class="row tutorial">
        <ul class="centered">

          <!-- Pair -->
          <li class="number">
            <div class="shadow"></div>
            <div class="circle centered">1</div>
          </li>
          <li class="text">
            Inserisci l&apos;ammontare del tuo patrimonio in criptovalute
          </li>
          <!-- /Pair -->

          <!-- Pair -->
          <li class="number centered">
            <div class="shadow"></div>
            <div class="circle centered">2</div>
          </li>
          <li class="text">
            Scopri la tua fee mensile
          </li>
          <!-- /Pair -->

          <!-- Pair -->
          <li class="number centered">
            <div class="shadow"></div>
            <div class="circle centered">1</div>
          </li>
          <li class="text">
            Apri il conto e godi di tutti i vantaggi
          </li>
          <!-- /Pair -->

        </ul>
      </div>
      <!-- /Tutorial -->

      <!-- Fee calculator -->
      <div class="row calculator centered">
        <div class="col-8 fee-calc flex-column centered">

          <!-- Insert asset -->
          <div class="up flex-column centered mb-5">
            <h5 class="mb-2">Inserisci gli asset che vuoi custodire</h5>
            <input class="mb-2" type="number" placeholder="Asset" step="0.01" v-model="asset">
            <BtnComp
              class="mb-2"
              @click="doMath"
              :buttonText="this.btnTxt"
              :buttonStyle="this.btnStyle"
            />
          </div>
          <!-- /Insert asset -->

          <!-- View asset -->
          <div class="down flex-column centered mt-5">
            <!-- <p>&hyphen;&hyphen;&comma;&hyphen;&hyphen;&euro;</p> -->

            <p v-if="!fee">&hyphen;&hyphen;&comma;&hyphen;&hyphen;&euro;</p>
            <p v-else>{{ parseFloat(fee).toFixed(2) }}&euro;</p>

            <span>Dettagli del calcolo</span>
          </div>
          <!-- /View asset -->

        </div>
      </div>
      <!-- /Fee calculator -->

    </div>
  </section>
</template>
  
<script>
import BtnComp from '../cyclables/BtnComp.vue';
export default {
  components: { BtnComp },
  data(){
    return{
      // Generating BtnComp
      btnTxt: "calcola",
      btnStyle:" background-color: rgb(191, 13, 13); border: 3px solid rgb(191, 13, 13);",

      asset: null,
      fee: null,
      minPatrimony: 15000,

      // establishing comparison parameters
      params: [
        { price: 0.7, range:[0, 500000]},
        { price: 0.6, range:[500000, 1000000]},
        { price: 0.5, range:[1000000, 5000000]},
        { price: 0.4, range:[5000000, 10000000]},
        { price: 0.3, range:[10000000, 1000000000]},
      ]
    }
  },
  methods:{
    doMath(){
      // reset fee
      this.fee = 0;
      // asset is transformed in currency format.
      this.asset = parseFloat(this.asset).toFixed(2);

      // doing math
      if(this.asset < this.minPatrimony) this.fee = 0;
      else{
        this.params.forEach(el => {
          if(this.asset > el.range[0] && this.asset >= el.range [1]){
            let feeable = el.range[1] - el.range[0];
            this.fee += feeable * el.price / 100 / 12;
            // console.log('superiore ad entrambi');
          }
          else if(this.asset < el.range[0] && this.asset < el.range [1]){
            this.fee += 0;
            // console.log('inferiore ad entrambi');
          }
          else if(this.asset > el.range[0] && this.asset < el.range [1]){
            let fakeAsset = this.asset - el.range[0];
            this.fee += fakeAsset * el.price / 100 / 12;
            // console.log('a metà');
          }
        });
      }
      // /doing math

    }
  }
}
</script>
  
<style scoped lang="scss">
section{
  background-color: rgb(228, 218, 218);
  .row{
    margin-bottom: 50px;
  }
}
  // TUTORIAL
.tutorial{
  ul{
    margin: 0;
    li{
      margin: auto 1%;
      max-width: 14%;
    }
    .number{
      position: relative;
      z-index: 1;

      font-size: 54px;
      font-weight: 700;
      color: white;
      .circle{
        width: 4.5vw;
        height: 4.5vw;
        background-color: rgb(164, 140, 140);
        border: 3px solid rgb(33, 30, 30);
        border-radius: 50%;
      }
    }
    .shadow{
      box-sizing: border-box;

      position: absolute;
      z-index: -1;
      width: 4.5vw;
      height: 4.5vw;
      left: 4px;
      top: 4px;

      background: #584949;
      border: 3px solid #211E1E;
      border-radius: 50%;
    }
    .text{
      text-align: center;
    }
  }
}
  // /TUTORIAL

  // FEE
.fee-calc{
  // height: 585px;
  padding: 3%;
  background-color: rgb(88, 73, 73);
  border: 3px solid rgb(0, 0, 0);
  border-radius: 50px;

  color: white;

  .up{
    padding: 0.5%;
    h5{
      text-transform: uppercase;
    }
    input{
      width: 110%;
      padding: 1.5% 3%;
      text-align: center;
      border-radius: 10px;
    }
  }

  .down{
    width: 100%;
    p{
      font-size: 500%;
      max-width: 100%;
      overflow: auto;
    }
    span{
      text-decoration: underline;
      &:hover{
        color: burlywood;
        cursor: pointer;
      }
    }
  }
}
  // /FEE

</style>