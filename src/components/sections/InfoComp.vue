<template>
    <section class="container py-5">
      <h3 class="text-center">Cosa rende sicura e affidabile la custodia di Acme Corp:</h3>
      <div class="row justify-content-around p-3">
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
          title: 'PROTOCOLLO DI CUSTODIA',
          text:'ll nostro protocollo di custodia è basato su due livelli cold storage, tre stadi autorizzativi a firma multipla e 5 aziende indipendenti coinvolte', 
          path: require('@/assets/info-img/scudo.png'),
          rem: 'width: 18rem;',
        },
        { 
          id: 1,
          title: 'Gestore dedicato',
          text:'Hai a tua totale disposizione un gestore dedicato raggungibile via email, chat, telefono e di persona', 
          path: require('@/assets/info-img/gestore.png'),
          rem: 'width: 18rem;',
        },
        { 
          id: 2,
          title: 'Attestazioni OIZ',
          text:'Acme Corp si sottopone ad audit esterno e possiede numerose attestazioni di livello', 
          path: require('@/assets/info-img/doppioscudo.png'),
          rem: 'width: 18rem;',
        },
        { 
          id: 3,
          title: 'Coperture assicurative',
          text:'Qualsiasi cosa accada, la copertura assicurativa garantisce il totale rimborso del patrimonio', 
          path: require('@/assets/info-img/tesoreria.png'),
          rem: 'width: 18rem;',
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