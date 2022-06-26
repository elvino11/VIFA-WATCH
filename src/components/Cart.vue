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
      <h1 style="color: #e54499">TRANSACTION</h1>
      <hr/>
    </div>

    <div class="dataTransaksi">
      <div v-for="keranjang in data">
        <table class="table table-danger table-striped">
          <thead>
          <tr>
            <th scope="col">#</th>
            <th scope="col">ID Keranjang</th>
            <th scope="col">Gambar Barang</th>
            <th scope="col">Nama Barang</th>
            <th scope="col">Harga Barang</th>
            <th scope="col">Kuantitas</th>
            <th scope="col">Total Harga</th>
            <th scope="col">ID Transaksi</th>
          </tr>
          </thead>
          <tbody>
          <tr>
            <th scope="row"><input type="checkbox" :value="keranjang.total_harga" v-model="this.harga"></th>
            <td>{{keranjang.id_keranjang}}</td>
            <td><img :src="keranjang.barang.gambar" width="100" height="100" alt="gambar"></td>
            <td>{{keranjang.barang.nama_barang}}</td>
            <td>{{keranjang.barang.harga}}</td>
            <td>{{keranjang.kuantitas}}</td>
            <td>{{keranjang.total_harga}}</td>
            <td>{{keranjang.id_transaksi}}</td>
          </tr>
          </tbody>
        </table>
      </div>
    </div>




    <div v-if="isCheckOut" class="transaksi">
      <div class="container-mt-5">
        <div class="row d-flex justify-content-center">
          <div class="col-md-6">
            <h2 style="color: #e54499; font-weight: bold">Transaction</h2>
            <div class="card px-5 py-5" style="border-radius: 30px; border-color:#e54499; border-width: 3px">
              <div class="register">
                <div class="mb-3">
                  <label for="id_transaksi" class="form-label">ID Transaksi</label>
                  <input type="text" class="form-control" id="id_transaksi" :placeholder="this.id_transaksi" v-model="this.addTransaksi.id_transaksi">
                </div>
                <div class="mb-3">
                  <label for="total_harga" class="form-label">Total Harga</label>
                  <input type="number" class="form-control" id="total_harga" placeholder="Total Harga" v-model="this.addTransaksi.total_harga">
                </div>
                <div class="mb-3">
                  <label for="diskon" class="form-label">Diskon</label>
                  <input type="number" class="form-control" id="diskon" placeholder="Diskon" v-model="this.addTransaksi.diskon">
                </div>
                <div class="mb-3">
                  <label for="pembayaran" class="form-label">Pembayaran</label>
                  <input type="number" class="form-control" id="pembayaran" placeholder="Pembayaran" v-model="this.addTransaksi.pembayaran">
                </div>
                <RouterLink :to="{name: 'transaction', params: {status: this.status, id_user: this.id_user}}">
                  <button class="btn btn-success" type="button" @click="payTransaction">PAY</button>
                </RouterLink>
              </div>
            </div>
          </div>
        </div>
      </div>
    </div>

    <div class="notTransactionYet" v-if="isForm" >
      <h1>
        Harap Lakukan Transaksi Terlebih Dahulu
        <RouterLink to="/product">
          Di Sini
        </RouterLink>
      </h1>
      <h3>Atau cari ID Transaksi yang telah dimasukkan</h3>
      <div class="mb-3">
        <label for="transaksiID" class="form-label">ID Transaksi</label>
        <input type="text" class="form-control" id="transaksiID" placeholder="ID Transaksi" v-model="this.id_transaksi">
      </div>
      <button class="btn btn-success" @click="search">SEARCH</button>
    </div>

    <div v-if="isCheck" class="checkOut">
      <button @click="checkOut" class="btn btn-success">Check Out</button>
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
  name: "Cart",
  data() {
    return {
      data : [],
      id_user : this.$route.params.id_user,
      status : this.$route.params.status,
      isLoading : false,
      isForm: true,
      isCheck: true,
      harga: [],
      kuantitas: [],
      isCheckOut: false,
      id_transaksi : this.$route.params.id_transaksi,
      addTransaksi: {
        total_harga: 0,
        id_transaksi: '',
        diskon: 0,
        pembayaran: 0,
        id_user: this.$route.params.id_user
      }
    }
  },
  methods: {
    loadKeranjang() {
      this.isLoading = true;
      fetch(`https://vifawatch.000webhostapp.com/pages/keranjang/index.php?id_user=${this.id_user}&id_transaksi=${this.id_transaksi}`, {
        method: 'GET'
      })
      .then(response => {
        if (response.ok) {
          return response.json()
        }
      })
      .then(json => {
        this.data = json.data;
        console.log(this.data);
      })
      .catch(() => {
        alert('Terjadi Error')
      })
      .finally(() => {
        this.isLoading = false;
      })
    },
    checkOut() {
      this.isCheckOut = true;
      for (let i = 0; i < this.harga.length; i++) {
        this.addTransaksi.total_harga += this.harga[i]
      }
      this.isForm = false;
      this.isCheck = false;
    },
    payTransaction() {
      if (confirm("are you sure wan to pay ?")) {
        const formTransaksi = new URLSearchParams({
          id_transaksi: this.addTransaksi.id_transaksi,
          total_harga: this.addTransaksi.total_harga,
          diskon: this.addTransaksi.diskon,
          pembayaran: this.addTransaksi.pembayaran,
          id_user: this.addTransaksi.id_user
        })
        fetch(`https://vifawatch.000webhostapp.com/pages/transactions/create.php`, {
          method: 'POST',
          headers: {
            'Content-Type': 'application/x-www-form-urlencoded',
            'API-Key': 'secret'
          },
          body: formTransaksi.toString(),
        })
          .then(response => {
            return response.json();
          })
          .then(json => {
            if (!json.status) {
              alert(json.error);
            } else {
              this.data.push(json.data);
              console.log(this.data);
            }
          })
          .catch((e) => {
            alert('Terjadi Error'+e.toString())
          })
          .finally(() => {
            this.isCheckOut = false;
          })
      }
    },
    search() {
      this.loadKeranjang();
      this.isForm = false;
    }
  },
  mounted() {
    this.loadKeranjang();
  }
};
</script>

<style scoped>
.transaksi{
  color: black;
}
.checkOut{
  padding-top: 30px;
}
.dataTransaksi{
  padding-top: 50px;
}
.notTransactionYet{
  color: var(--color-heading);
}
.unLogin {
  margin-top: 100px;
  color: var(--color-heading);
}
</style>
