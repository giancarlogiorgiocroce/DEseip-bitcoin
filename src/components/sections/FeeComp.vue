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
          <li class="number">
            1
          </li>
          <li class="text">
            Inserisci l&apos;ammontare del tuo patrimonio in criptovalute
          </li>
          <li class="number">
            2
          </li>
          <li class="text">
            Scopri la tua fee mensile
          </li>
          <li class="number">
            3
          </li>
          <li class="text">
            Apri il conto e godi di tutti i vantaggi
          </li>
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
            <button class="mb-2">CALCOLA</button>
          </div>
          <!-- /Insert asset -->

          <!-- View asset -->
          <div class="down flex-column centered mt-5">
            <p v-if="asset == null">&hyphen;&hyphen;&comma;&hyphen;&hyphen;&euro;</p>
            <p v-else>{{ parseFloat(asset).toFixed(2) }}&euro;</p>

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
    }
  },
  methods:{
    setRound(){
      Math.round((this.asset) * 100) / 100
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
      margin: auto 2%;
      max-width: 14%;
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
    p{
      font-size: 500%;
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