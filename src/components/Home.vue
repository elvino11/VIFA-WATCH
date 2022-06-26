<template>

  <header v-if="status">
    <RouterLink to="/home">
      <img
        alt="Vue logo"
        class="logo"
        src="@/assets/logo.png"
        width="200"
        height="200"
      />
    </RouterLink>


    <div class="wrapper">
      <nav>
        <RouterLink :to="{name: 'home', params: {status: this.status, id_user: this.id_user}}">Home</RouterLink>
        <RouterLink :to="{name: 'adding', params: {status: this.status, id_user: this.id_user}}">Adding</RouterLink>
        <RouterLink :to="{name: 'cart', params: {status: this.status, id_user: this.id_user}}">Transaction</RouterLink>
        <RouterLink :to="{name: 'transaction', params: {status: this.status, id_user: this.id_user}}">History Transaction</RouterLink>
        <RouterLink :to="{name: 'about', params: {status: this.status, id_user: this.id_user}}">About</RouterLink>
      </nav>

    </div>
  </header>

  <section class="inLogin" v-if="status">
    <div class="higlight">
      <div id="carouselExampleIndicators" class="carousel slide" data-bs-ride="true">
        <div class="carousel-indicators">
          <button type="button" data-bs-target="#carouselExampleIndicators" data-bs-slide-to="0" class="active" aria-current="true" aria-label="Slide 1"></button>
          <button type="button" data-bs-target="#carouselExampleIndicators" data-bs-slide-to="1" aria-label="Slide 2"></button>
          <button type="button" data-bs-target="#carouselExampleIndicators" data-bs-slide-to="2" aria-label="Slide 3"></button>
        </div>
        <div class="carousel-inner">
          <div class="carousel-item active">
            <img src="/src/assets/image5.png" class="d-block w-100" alt="...">
          </div>
          <div class="carousel-item">
            <img src="/src/assets/image6.png" class="d-block w-100" alt="...">
          </div>
          <div class="carousel-item">
            <img src="/src/assets/seiko.png" class="d-block w-100" alt="...">
          </div>
        </div>
        <button class="carousel-control-prev" type="button" data-bs-target="#carouselExampleIndicators" data-bs-slide="prev">
          <span class="carousel-control-prev-icon" aria-hidden="true"></span>
          <span class="visually-hidden">Previous</span>
        </button>
        <button class="carousel-control-next" type="button" data-bs-target="#carouselExampleIndicators" data-bs-slide="next">
          <span class="carousel-control-next-icon" aria-hidden="true"></span>
          <span class="visually-hidden">Next</span>
        </button>
      </div>
    </div>
    <hr/>

<!--
    <RouterLink :to="{name: 'testing', params: {bisa: this.bisa}}">Testing</RouterLink>
-->


    <section class="brand">
      <Brand/>
    </section>
    <section class="product">
      <Product/>
    </section>
  </section>

  <section v-else class="unLogin">
    <h1>
      Anda Harus Login Terlebih Dahulu
      <RouterLink to="/">Di Sini</RouterLink>
    </h1>
  </section>



</template>

<script>
import Product from "./Product.vue";
import Brand from "./Brand.vue";
export default {
  name: "Home",
  components: { Brand, Product },
  data() {
    return {
      status: this.$route.params.status,
      id_user: this.$route.params.id_user
    }
  }
};
</script>

<style scoped>
.product{
  margin-top: 100px;
}
.inLogin{
  margin-top: 100px;
}
.unLogin {
  margin-top: 100px;
  color: var(--color-heading);
}
.collapse{
  color: var(--color-heading);
}
</style>
