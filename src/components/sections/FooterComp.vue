<template>
  <footer>
    <div>

      <!-- Black Row -->
      <div class="row black">
        <img src="../../assets/footer-img.png" alt="acme-info">
      </div>
      <!-- /Black Row -->

      <!-- Red Row -->
      <div class="row red p-1">
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
  width: 100%;
  margin: 0;

  background-color: rgb(33, 30, 30);
  img{
    padding: 0;
    height: 100%;
  }
}

.red {
  margin: 0;
  
  background-color: rgb(215, 15, 15);
  ul{
    margin: 0;
  }
  li{
    margin: 20px;
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