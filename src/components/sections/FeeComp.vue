<template>
  <section>
    <div class="container">
      <div class="row title text-center">
        <h2>Calcola la tua fee</h2>
      </div>
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
      <div class="row calculator">

      </div>
    </div>
  </section>
</template>
  
<script>
export default {

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

</style>