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

  <section class="login" v-if="status">
    <div class="title" style="padding-top: 50px">
      <h1 style="color: #e54499">HISTORY TRANSACTION</h1>
      <hr/>
    </div>
    <div v-for="transaksi in data">

      <table class="table table-danger table-striped">
        <thead>
        <tr>
          <th scope="col">ID Transaksi</th>
          <th scope="col">Tanggal Transaksi</th>
          <th scope="col">Total Harga</th>
          <th scope="col">Diskon</th>
          <th scope="col">Total Bayar</th>
          <th scope="col">Pembayaran</th>
          <th scope="col">Kembalian</th>
          <th scope="col">Detail</th>
        </tr>
        </thead>
        <tbody>
        <tr>
          <th scope="row">{{transaksi.id_transaksi}}</th>
          <td>{{transaksi.tanggal_transaksi}}</td>
          <td>{{transaksi.total_harga}}</td>
          <td>{{transaksi.diskon}}</td>
          <td>{{transaksi.total_bayar}}</td>
          <td>{{transaksi.pembayaran}}</td>
          <td>{{transaksi.kembalian}}</td>
          <td>
            <RouterLink :to="{name: 'transaction-detail', params: {id_transaksi: transaksi.id_transaksi, id_user: transaksi.id_user, status: this.status}}">
              <button type="button" class="btn btn-success"> DETAIL</button>
            </RouterLink>
          </td>
        </tr>
        </tbody>
      </table>
    </div>
  </section>

  <section v-else class="unLogin">
    <h1>
      Anda Harus Login Terlebih Dahulu
      <RouterLink to="/">Di Sini</RouterLink>
    </h1>
  </section>

</template>

<script>
export default {
  name: "Transaction",
  data() {
    return {
      data:[],
      status: this.$route.params.status,
      id_user: this.$route.params.id_user
    }
  },
  methods: {
    loadTransaksi() {
      fetch(`http://localhost/fetano/pages/transactions/index4.php?id_user=${this.id_user}`, {
        method: 'GET'
      })
      .then(response => {
        if (response.ok) {
          return response.json()
        }
      })
      .then(json => {
        this.data = json.data
      })
      .catch(() => {
        alert("Terjadi Error")
      })
    }
  },
  mounted() {
    this.loadTransaksi();
  }
};
</script>

<style scoped>
.unLogin {
  margin-top: 100px;
  color: var(--color-heading);
}
</style>
