<template>
  <footer>
    <div class="container">

      <!-- Black Row -->
      <div class="row black">
        <ul class="centered flex-column">
          <li class="mb-5">
            <img src="" alt="acme-logo">
          </li>
          <li class="my-2">
            <h5>Acme Corp Inc.</h5>
          </li>
          <li>Via Emilio Marchi 4, Milano (MI) - ITALY</li>
          <li>info@acmecorp.com</li>
          <li class="mt-1">
            <span>Design by Deseip</span>
          </li>
        </ul>
      </div>
      <!-- /Black Row -->

      <!-- Red Row -->
      <div class="row red">
        <ul class="centered">
          <li>2022 Acme Corp Inc. - P.IVA 01234567890</li>
          <li>
            <a href="#">privacy policy</a>
          </li>
          <li>
            <a href="#">cookie policy</a>
          </li>
          <li>
            <a href="#">cookies preferences</a>
          </li>
        </ul>
      </div>
      <!-- /Red Row -->

    </div>

  </footer>
</template>

<script>
export default {

}
</script>

<style scoped lang="scss">
footer {
  color: white;
}

.black {
  height: 369px;
  background-color: rgb(33, 30, 30);
  span{
    color: grey;
    font-size: small;
  }
}

.red {
  height: 70px;
  background-color: rgb(215, 15, 15);
  ul{
    margin: 0;
  }
  li{
    margin: 0 20px;
  }
  a{
    text-decoration: none;
    color: white;
    text-transform: uppercase;
    &:hover{
      text-decoration: underline;
      color: burlywood;
    }
  }
}
</style>