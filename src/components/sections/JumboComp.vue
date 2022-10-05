<template>
  <section>
    <div class="jumbotron container">
      <div class="row my-5 centered">

        <!-- Jumbo Text -->
        <div class="jumbo-text col-7">
          <h1>Quanto costa custodire le tue cripto?</h1>
          <h1 class="text-light mb-5">Scoprilo con Acme Corp.</h1>
          <p class="mb-5">
            Quando il tuo patrimonio cripto inizia a crescere, custodirlo in modo sicuro è fondamentale per evitare di incorrere in truffe e rischi.
            <br/><br/>
            Prova il servizio di custodia affidabile e trasparente di Acme Corp: <span>calcola le tue commissioni mensili e scopri tutti i vantaggi.</span>
          </p>

          <BtnComp
            :buttonText="this.btnTxt"
            :buttonStyle="this.btnStyle"
          />

        </div>
        <!-- /Jumbo Text -->

        <!-- Jumbo Image -->
        <div class="jumbo-image col-5 ">
          <img src="../../assets/Bitcoin 1.png" alt="bitcoin-logo">
        </div>
        <!-- /Jumbo Image -->

      </div>
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
        btnTxt: "calcola la tua fee >",
        btnStyle:" background-color: rgb(191, 13, 13); border: 3px solid rgb(191, 13, 13);",
      }
    }
}
</script>
  
<style scoped lang="scss">
section {
  background-color: rgb(164, 140, 140);
}
.jumbo-text{
  font-family: 'Poppins', sans-serif;
  h1,
  span{
    font-weight: 900;
  }
}
.jumbo-image{
  max-width: 400px;
  img{
    width: 100%;
  }
}
</style>