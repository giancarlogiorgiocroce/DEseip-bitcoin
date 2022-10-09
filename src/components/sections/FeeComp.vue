<template>
  <section class="py-5" ref="fees">
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
            <h5 class="mb-4">Inserisci gli asset che vuoi custodire</h5>
            <input class="mb-4" type="number" placeholder="Asset" step="0.01" v-model="asset">
              
            <div @click="doMath">
              <BtnComp
                class="mb-2"
                :buttonText="this.btnTxt"
                :buttonStyle="this.btnStyle"
              />
            </div>
          </div>
          <!-- /Insert asset -->

          <!-- View asset -->
          <div class="down flex-column centered mt-5">

            <div v-if="!fee" class="basic text-center">
              <p>&hyphen;&hyphen;&comma;&hyphen;&hyphen;&euro;</p>
              <span>Dettagli del calcolo</span>
            </div>
            <div v-else class="aftercalc text-center">
              <div class="fee-display mb-5">
                <h3>La tua fee:</h3>
                <p>{{ parseFloat(fee).toFixed(2) }}&euro;</p>
                <span>
                  Dettagli del calcolo
                  <!-- <img src="../../assets/arrow-down-circle.png" alt="->"> -->
                  <i class="fa-regular fa-circle-arrow-down"></i>
                  <!-- <font-awesome-icon icon="fa-regular fa-circle-arrow-down" /> -->
                </span>
              </div>

              <div class="fee-add-info">
                <h3 class="p-1 mb-5">
                  Prova il servizio di custodia <br/>Acme Corp: non potrai più farne a meno.
                </h3>
                <div class="btn-container centered">
                  <a class="m-3" href="#">
                    <BtnComp :buttonText="this.btnTxtSx" :buttonStyle="this.btnStyleSx" />
                  </a>
                  <a class="m-3" href="#">
                    <BtnComp :buttonText="this.btnTxtDx" :buttonStyle="this.btnStyleDx" />
                  </a>
                </div>
              </div>
            </div>

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
      // Generating BtnComp for doMath()
      btnTxt: "calcola",
      btnStyle:" background-color: rgb(191, 13, 13); border: 3px solid rgb(191, 13, 13);",

      // BtnComp for comunication
      btnTxtSx: "Parla con noi",
      btnStyleSx:" background-color: rgb(88, 73, 73); border: 3px solid rgb(255, 255, 255);",

      // BtnComp for account
      btnTxtDx: "Apri un conto",
      btnStyleDx:" background-color: rgb(191, 13, 13); border: 3px solid rgb(191, 13, 13);",

      // Data for DoMath() function
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
          // console.log('inizio il ciclo');
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
  width: 50%;
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
      font-weight: 900;
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
    .fee-add-info{
      a{
        text-decoration: none;
      }
    }
  }
}
  // /FEE

</style>