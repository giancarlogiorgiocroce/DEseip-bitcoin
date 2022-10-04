<template>
  <section>
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
            <button class="mb-2" @click="doMath">CALCOLA</button>
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
export default {
  data(){
    return{
      asset: null,
      fee: null,

      // establishing comparison parameters
      patrimonyA: 15,
      patrimonyB: 500,
      patrimonyC: 1000,
      patrimonyD: 5000,
      patrimonyE: 10000,
      patrimonyF: 1000000,

      priceA: 0.7,
      priceB: 0.6,
      priceC: 0.5,
      priceD: 0.4,
      priceE: 0.3,

      params: [
        // { range:[15000, 500000, 1000000], price: [0.7, 0.6,] },
        // { range:[500000, 1000000, 5000000], price: [0.6, 0.5 ]},
        // { range:[1000000, 5000000, 10000000], price: [0.5, 0.4] },
        // { range:[5000000, 10000000, 1000000000], price: [0.4, 0.3] },
        // { range:[10000000, 1000000000, 5000000000], price: [0.3,] },

        { range:[15001, 500000, 1000000], price: 0.7, },
        { range:[500001, 1000000, 5000000], price: 0.6, },
        { range:[1000001, 5000000, 10000000], price: 0.5, },
        { range:[5000001, 10000000, 1000000000], price: 0.4, },
        { range:[10000001, 1000000000, 5000000000], price: 0.3, },
      ]
      // params: [
      //   { patrimony: 500, price: 0.7, },
      //   { patrimony: 1000, price: 0.6, },
      //   { patrimony: 5000, price: 0.5, },
      //   { patrimony: 10000, price: 0.4, },
      //   { patrimony: 1000000, price: 0.3, },
      // ]
    }
  },
  methods:{
    doMath(){
      // reset fee
      this.fee = 0;
      // asset is transformed in currency format.
      this.asset = parseFloat(this.asset).toFixed(2);

      // return true if in range, otherwise false
      // function inRange(x, min, max) {
      //     return ((x-min)*(x-max) <= 0);
      // }



      if(this.asset < this.patrimonyA){
        this.fee = 0;
        // console.log('troppo poco');
      }
      else if(this.asset == this.patrimonyA){
        this.fee = this.asset * 0.7 / 12;
        // console.log('il giusto');
      }
      else{
        this.params.forEach(el => {



          if (this.asset < el.range[0] && this.asset < el.range[1]){
            this.fee += 0;
          }
          // else if(this.asset >= el.range[1] && this.asset < el.range[2]){
          //   this.fee += el.range[1] * el.price / 100 / 12;
          //   console.log('superiore', el.price, (el.range[1] * el.price / 100 / 12));
          // } 
          // else if (this.asset == el.range[2]){
          //   let fakeAsset = this.asset;
          //   this.fee += (fakeAsset - el.range[1]) * el.price / 100 / 12;
          // } 
          // else if (this.asset > el.range[0] && this.asset < el.range[1]){
          //   let fakeAsset = this.asset;
          //   this.fee += (fakeAsset - el.range[0]) * el.price / 100 / 12;
          // } 
        });
        console.log('si vola');
      }

      // if(this.asset < this.patrimonyA){
      //     this.fee = 0;
      //     console.log('sei povero');
      // }
      // else if(this.asset >= this.patrimonyA && this.asset <= this.patrimonyB){
      //   this.fee = this.asset * this.priceA / 12;
      // }
      // else if(this.asset > this.patrimonyB && this.asset <= this.patrimonyC){
      //   this.fee += this.patrimonyB * this.priceA / 12;
      //   this.fee += (this.asset - this.patrimonyB) * this.priceB / 12;
      // }
      // else if(this.asset > this.patrimonyC && this.asset <= this.patrimonyD){
      //   this.fee += this.patrimonyB * this.priceA / 12;
      //   this.fee += this.patrimonyC * this.priceB / 12;
      //   this.fee += (this.asset - this.patrimonyC) * this.priceC / 12;
      // }
      // else if(this.asset > this.patrimonyD && this.asset <= this.patrimonyE){
      //   this.fee += this.patrimonyB * this.priceA / 12;
      //   this.fee += this.patrimonyC * this.priceB / 12;
      //   this.fee += this.patrimonyD * this.priceC / 12;
      //   this.fee += (this.asset - this.patrimonyD) * this.priceD / 12;
      // }
      // else if(this.asset > this.patrimonyE && this.asset <= this.patrimonyF){
      //   this.fee += this.patrimonyB * this.priceA / 12;
      //   this.fee += this.patrimonyC * this.priceB / 12;
      //   this.fee += this.patrimonyD * this.priceC / 12;
      //   this.fee += this.patrimonyE * this.priceD / 12;
      //   this.fee += (this.asset - this.patrimonyE) * this.priceE / 12;
      // }

      // if(this.asset < this.patrimonyA){
      //     this.fee = 0;
      //     console.log(this.fee, 'sei povero');
      // }
      // else {
      //   this.params.forEach(el => {
      //     if(this.asset >= el.patrimony){
      //       console.log('è maggiore o uguale a', el.patrimony);
      //       this.fee += (el.patrimony*el.price/12);
      //       console.log(this.fee);
      //     }
      //   })
      // }

      // if (this.asset == this.patrimonyA) {
      //   this.fee = this.patrimonyA * this.priceA / 12;
      //   console.log('sono 15!');
      // } else if (this.asset > this.patrimonyA){
      //   this.params.forEach((el, i) => {
          // console.log(i);
          // let segnaposto = i + 1;
          // console.log(segnaposto);

          // console.log(el);

          // if(this.asset > el[i].patrimony && this.asset < el.patrimony[segnaposto]){
          //   this.fee +=  this.asset * el.price / 12;
          //   console.log('sono in mezzo tra', el.patrimony[i], 'e', el.patrimony[segnaposto]);
          // } 
          // else if (this.asset > el.patrimony[i] && this.asset > el.patrimony[segnaposto]){
          //   this.fee += el.patrimony * el.price / 12;
          // } 
          // else if (this.asset < el.patrimony[i] && this.asset < el.patrimony[segnaposto]){
          //   return;
          // }
      //   })
      // } else {
      //   console.log('fermati!');
      // } 
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

      font-family: 'Poppins', sans-serif;
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
    button{
      background-color: rgb(191, 13, 13);
      border: 3px solid rgb(191, 13, 13);

      color: white;
      padding: 3% 0;
      width: 40%;
      
      &:hover{
        background-color: rgb(150, 13, 13);
        border: 3px solid rgb(100, 13, 13);
        color: burlywood;
      }
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

</style>