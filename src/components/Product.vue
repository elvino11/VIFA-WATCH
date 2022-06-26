<template>

  <section class="login" v-if="status">
    <div class="title" style="margin-bottom: 30px; margin-top: 30px">
      <h1 style="color: #e54499">AVAILABLE PRODUCT</h1>
      <hr/>
    </div>


    <section class="product">
      <div class="row row-cols-1 row-cols-md-3 g-4">
        <div v-for="(product, index) in data">
          <div class="col" >
            <div class="card mb-3" style="max-width: 540px; height: 250px; border-radius: 30px; border-color:#e54499; border-width: 3px" >
              <div class="row g-0">
                <div class="col-md-4">
                  <RouterLink :to="{name: 'product-detail', params: { kode_barang: product.kode_barang, index, id_user: this.id_user, status: this.status}}">
                    <img :src="product.gambar" class="img-fluid rounded-start" alt="gambar">
                  </RouterLink>
                </div>
                <div class="col-md-8">
                  <div class="card-body">
                    <h4 class="card-title" align="center">{{ product.brand.nama_brand }}</h4>
                    <h5 class="card-title">{{ product.nama_barang }}</h5>
                    <p class="card-text">Rp {{product.harga}}</p>
                    <p class="card-text">Stok : {{product.stok_barang}}</p>
                    <p class="card-text"><small class="text-muted">{{ product.created_at }}</small></p>
                    <div class="text-end">
                      <RouterLink :to="{name: 'product-detail', params: { kode_barang: product.kode_barang, index, id_user: this.id_user, status: this.status}}">
                        <IconChart/>
                      </RouterLink>
                    </div>
                  </div>
                </div>
              </div>
            </div>
          </div>
        </div>
      </div>
    </section>

    <div class="title" style="margin-bottom: 30px; margin-top: 30px">
      <h1 style="color: #e54499">NOT AVAILABLE</h1>
      <hr/>
    </div>

    <section class="noProduct">
      <div class="row row-cols-1 row-cols-md-3 g-4">
        <div v-for="(product, index) in data2">
          <div class="col" >
            <div class="card mb-3" style="max-width: 540px; height: 250px; border-radius: 30px; border-color:#e54499; border-width: 3px" >
              <div class="row g-0">
                <div class="col-md-4">
                  <RouterLink :to="{name: 'product-detail', params: { kode_barang: product.kode_barang, index, id_user: this.id_user, status: this.status}}">
                    <img :src="product.gambar" class="img-fluid rounded-start" alt="gambar">
                  </RouterLink>
                </div>
                <div class="col-md-8">
                  <div class="card-body">
                    <h4 class="card-title" align="center">{{ product.brand.nama_brand }}</h4>
                    <h5 class="card-title">{{ product.nama_barang }}</h5>
                    <p class="card-text">Rp {{product.harga}}</p>
                    <p class="card-text">Stok : {{product.stok_barang}}</p>
                    <p class="card-text"><small class="text-muted">{{ product.created_at }}</small></p>
                    <div class="text-end">
                      <RouterLink :to="{name: 'product-detail', params: { kode_barang: product.kode_barang, index, status: this.status, id_user: this.id_user}}">
                        <IconChart/>
                      </RouterLink>
                    </div>
                  </div>
                </div>
              </div>
            </div>
          </div>
        </div>
      </div>
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
import IconPlus from "./icons/IconPlus.vue";
import IconMin from "./icons/IconMin.vue";
import IconChart from "./icons/IconChart.vue";
export default {
  name: "Product",
  components: { IconChart, IconMin, IconPlus },
  data() {
    return {
      kuantitas : 0,
      data : [],
      data2:[],
      isLoading : false,
      status: this.$route.params.status,
      id_user: this.$route.params.id_user
    }
  },
  methods: {
    ProductView() {
      this.isLoading = true;
      fetch(`https://vifawatch.000webhostapp.com/pages/products/index.php`, {
        method: 'GET'
      })
      .then(response => {
        if (response.ok) {
          return response.json();
        }
      })
      .then(json =>{
        this.data = json.data;
        console.log(this.data);
      })
      .catch(() => {
        alert('Terjadi Error');
      })
      .finally(() => {
        this.isLoading = false;
      })
    },
    add() {
      this.kuantitas++;
    },
    min() {
      if (this.kuantitas > 0) {
        this.kuantitas--;
      } else {
        this.kuantitas = 0;
      }
    },
    NoProductView() {
      this.isLoading = true;
      fetch(`https://vifawatch.000webhostapp.com/pages/products/index2.php`, {
        method: 'GET'
      })
        .then(response => {
          if (response.ok) {
            return response.json();
          }
        })
        .then(json =>{
          this.data2 = json.data;
          console.log(this.data2);
        })
        .catch(() => {
          alert('Terjadi Error');
        })
        .finally(() => {
          this.isLoading = false;
        })
    },
  },
  mounted() {
    this.ProductView();
    this.NoProductView();
  }
};
</script>

<style scoped>
.product{
  margin-top: 50px;
}
.col{
  color: black;
}
img{
  margin-top: 20px;
}
.unLogin {
  margin-top: 100px;
  color: var(--color-heading);
}
</style>
