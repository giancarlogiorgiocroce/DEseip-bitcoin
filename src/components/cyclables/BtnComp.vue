<template>
  <div class="button" :style="buttonStyle">
    {{ buttonText }}
  </div>
</template>

<script>
export default {
    props: {
        buttonText: String,
        buttonStyle: String,
    } 
}
</script>

<style scoped lang="scss">
.button {
    padding: 3% 0;
    width: 16vw;

    color: white;
    text-transform: uppercase;
    text-align: center;
    
    &:hover {
        background-color: rgb(150, 13, 13) !important;
        border: 3px solid rgb(100, 13, 13) !important;
        color: burlywood;
        cursor: pointer;
    }
}
</style>