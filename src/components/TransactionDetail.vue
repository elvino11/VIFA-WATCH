<template>

  <section class="login" v-if="status">
    <div class="back">
      <h5>
        <RouterLink :to="{name: 'transaction', params: {status: this.status, id_user: this.id_user}}">
          <IconBack/> Go back to transaction
        </RouterLink>

      </h5>

    </div>
    <div class="title" style="padding-top: 50px">
      <h1 style="color: #e54499">DETAIL TRANSACTION</h1>
      <hr/>
    </div>

    <div v-for="detail in data">
      <table class="table table-danger table-striped">
        <thead>
        <tr>
          <th scope="col">ID Keranjang</th>
          <th scope="col">Gambar</th>
          <th scope="col">Kode Barang</th>
          <th scope="col">Nama Barang</th>
          <th scope="col">Harga</th>
          <th scope="col">Kuantitas</th>
          <th scope="col">Total Harga</th>
        </tr>
        </thead>
        <tbody>
        <tr>
          <th scope="row">{{detail.id_keranjang}}</th>
          <td><img :src="detail.barang.gambar" width="100" height="100" alt="gambar"></td>
          <td>{{detail.barang.kode_barang}}</td>
          <td> {{detail.barang.nama_barang}}</td>
          <td>{{detail.barang.harga}}</td>
          <td>{{detail.kuantitas}}</td>
          <td>{{detail.total_harga}}</td>
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
import IconBack from "./icons/IconBack.vue";
export default {
  name: "TransactionDetail",
  components: { IconBack },
  data() {
    return {
      data: [],
      id_transaksi: this.$route.params.id_transaksi,
      id_user: this.$route.params.id_user,
      status: this.$route.params.status,
      isLoading: false,
    }
  },
  methods: {
    loadDetailTransaksi() {
      this.isLoading = true;
      fetch(`https://vifawatch.000webhostapp.com/pages/transactions/get.php?id_transaksi=${this.id_transaksi}&id_user=${this.id_user}`, {
        method: 'GET',
      })
      .then(response => {
        if (response.ok) {
          return response.json();
        }
      })
      .then(json => {
        this.data = json.data;
      })
      .catch(() => {
        alert("Terjadi Error")
      })
    }
  },
  mounted() {
    this.loadDetailTransaksi();
  }
};
</script>

<style scoped>
.back{
  padding-top: 50px;
}
.unLogin {
  margin-top: 100px;
  color: var(--color-heading);
}
</style>
