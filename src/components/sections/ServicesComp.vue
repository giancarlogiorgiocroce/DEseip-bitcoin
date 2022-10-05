<template>
  <section class="container py-5">
    <h3 class="text-center">Cosa rende sicura e affidabile la custodia di Acme Corp:</h3>
    <div class="row justify-content-center py-3 px-5 mx-5">
      <CardComp
        v-for="card in cardsArray"
        :key="card.id"
        :cardImg="card.path"
        :cardTitle="card.title"
        :cardText="card.text"
        :cardSize="card.rem"
      />
    </div>
  </section>
</template>

<script>
import CardComp from '../cyclables/CardComp.vue';
export default {
  components: { CardComp },
  data: () => ({
  cardsArray: [
      { 
        id: 0,
        title: '',
        text:'Gestore dedicato', 
        path: require('@/assets/services-img/domanda.png'),
        rem: 'width: 20rem;',
      },
      { 
        id: 1,
        title: '',
        text:'Nomina di un esecutore', 
        path: require('@/assets/services-img/esecutore.png'),
        rem: 'width: 20rem;',
      },
      { 
        id: 2,
        title: '',
        text:'Apertura di rapporti intestati a società e fiduciarie', 
        path: require('@/assets/services-img/fiduciarie.png'),
        rem: 'width: 20rem;', 
      },
      { 
        id: 3,
        title: '',
        text:'Apertura di rapporti cointestati', 
        path: require('@/assets/services-img/mani.png'),
        rem: 'width: 20rem;', 
      },
      { 
        id: 4,
        title: '',
        text:'Passaggio generazionale', 
        path: require('@/assets/services-img/schema.png'),
        rem: 'width: 20rem;', 
      },
    ],
})
}
</script>

<style scoped lang="scss">
h3{
  font-weight: 900;
}
</style>