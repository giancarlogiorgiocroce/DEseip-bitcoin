<template>
  <div id="app">
    <HeaderComp/>

    <JumboComp/>
    <InfoComp/>
    <FeeComp id="fees"/>
    <ServicesComp/>

    <FooterComp/>
  </div>
</template>

<script>
import HeaderComp from './components/sections/HeaderComp.vue';
import FooterComp from './components/sections/FooterComp.vue';
import JumboComp from './components/sections/JumboComp.vue';
import InfoComp from './components/sections/InfoComp.vue';
import FeeComp from './components/sections/FeeComp.vue';
import ServicesComp from './components/sections/ServicesComp.vue';

export default {
  name: 'App',
  components: {
    HeaderComp,
    FooterComp,
    JumboComp,
    InfoComp,
    FeeComp,
    ServicesComp
  },
}
</script>

<style lang="scss">
*{
  font-family: 'Poppins', sans-serif;
}
ul{
    list-style: none;
}
.centered{
  display: flex;
  justify-content: center;
  align-items: center;
}
</style>
