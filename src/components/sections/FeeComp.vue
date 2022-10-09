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

        <!-- Fee table -->
        <div v-if="!errPatrimony && !tableActive" class="col-8 fee-calc flex-column centered">
          <!-- Insert asset -->
          <div class="up flex-column centered mb-5">
            <h5 class="mb-4">Inserisci gli asset che vuoi custodire</h5>
            <input class="mb-4" type="number" placeholder="Asset" step="0.01" v-model="asset">
              
            <div @click="doMath">
              <BtnComp
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
              <span @click="toggleTable">Dettagli del calcolo</span>
            </div>
            <div v-else class="aftercalc text-center">
              <div class="fee-display mb-5">
                <h3>La tua fee:</h3>
                <p>{{ parseFloat(fee).toFixed(2) }}&euro;</p>
                <span @click="toggleTable">
                  Dettagli del calcolo
                  <i class="fa-solid fa-circle-arrow-down"></i>
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
        <!-- /Fee table -->
        
        <!-- Error Modal -->
        <div v-if="errPatrimony" class="col-8 error-patrimony flex-column centered">
          <div class="error-box">
            <div class="d-block my-5">
              <img @click="closeModal" src="../../assets/x-circle.png" alt="close">
            </div>
            <h3 class="text-center p-5 m-2">
              Ci dispiace, al momento il nostro servizio è disponibile solo a partire da €15.000
            </h3>
          </div>
        </div>
        <!-- /Error Modal -->

        <!-- Pricing Table -->
        <div v-if="tableActive" class="col-8 price-table flex-column centered">
          <img @click="toggleTable" id="fee-table" src="../../assets/table.png" alt="price-table">
        </div>
        <!-- /Pricing Table -->

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
        //BUTTONS PROPS
      // Generating BtnComp for doMath()
      btnTxt: "calcola",
      btnStyle:" background-color: rgb(191, 13, 13); border: 3px solid rgb(191, 13, 13);",
      // BtnComp for comunication
      btnTxtSx: "Parla con noi",
      btnStyleSx:" background-color: rgb(88, 73, 73); border: 3px solid rgb(255, 255, 255);",
      // BtnComp for account
      btnTxtDx: "Apri un conto",
      btnStyleDx:" background-color: rgb(191, 13, 13); border: 3px solid rgb(191, 13, 13);",

        // BOOLEANS
      // Booleans for modal
      errPatrimony: false,
      tableActive: false,

        // DOMATH()
      // Data for DoMath() function
      asset: null,
      fee: null,
      minPatrimony: 15000,
      // Establishing comparison parameters
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
      if(this.asset < this.minPatrimony){
        this.errPatrimony = true;
      }
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

    },

    closeModal(){
      this.errPatrimony = false;
    },

    toggleTable(){
      this.tableActive = !this.tableActive;
    },
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

  // ERROR PATRIMONY AND PRICING TABLE
.error-patrimony, .price-table{
  position: fixed;
  top: 0;
  left: 0;
  z-index: 100;
  width: 100vw;
  height: 100vh;
  background-color: rgba(189, 171, 171, 0.7);
  .error-box{
    position: relative;
    width: 33%;
    background-color: white;
    border-radius: 25px;
    box-shadow: 0px 10px 0px 10px rgb(131, 112, 112);
    img {
      position: absolute;
      right: 0;
      top: 0;
      max-width: 45px;
    }
  }
  #fee-table{
    max-width: 70%;
    &:hover{
      cursor: pointer;
    }
  }
}
  // ERROR PATRIMONY AND PRICING TABLE

  // FEE
.fee-calc{
  position: relative;

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
    // overflow: auto;

    p{
      font-size: 500%;
      font-weight: 900;
      overflow: hidden;
      text-align: center;
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
    .aftercalc{
      overflow: auto;
    }
  }
}

@media screen and (max-width: 992px) {
  .number{
    font-size: 32px;
    .circle{
      width: 7vw !important;
      height: 7vw !important;
    }
    .shadow{
      width: 7vw !important;
      height: 7vw !important;
    }
  }
  .fee-calc  {
    width: 100%;
  }
}

@media screen and (max-width: 768px) {

  .tutorial{
    flex-direction: row !important;
    li{
      margin: auto 5% !important;
    }
    
  }
  
}

@media screen and (max-width: 450px) {
  .fee-display{
    p{
      font-size: 35px !important;
    }
  }
}
  // /FEE
</style>