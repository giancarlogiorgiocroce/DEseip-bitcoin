<template>
    <div class="card centered" :style="cardSize">
        <img class="card-img-top" 
            :src="cardImg" 
            :alt="cardTitle">
        <div class="card-body centered flex-column">
            <h5 v-if="cardTitle"
                class="card-title text-center">
                {{ cardTitle }}
            </h5>
            <p class="card-text text-center">
                {{ cardText }}
            </p>
        </div>
    </div>
</template>
  
<script>
export default {
    props: {
        cardImg: String,
        cardTitle: String,
        cardText: String,
        cardSize: String,
    }
}
</script>
  
<style scoped lang="scss">
.card{
    margin: 2% 0;
    border: none !important;
}
img{
    max-width: 90px;
}
.card-title{
    text-transform: uppercase;
    font-weight: 900;
}
</style>