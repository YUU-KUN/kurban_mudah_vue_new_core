<template>
  <div style="justify-content:center; margin:50px auto; padding: 0 100px; background-color: white">
    <h2><b>Pembayaran</b></h2> 
      <div class="text-center" style="margin: 50px auto; ">
        <div class="align-items-center my-4">
          <div class="card">
            <table v-if="pembayarans.length > 0">
              <div class="text-center" style="margin: 50px auto; padding: auto 20px">
                <div class="row">
                  <div class="col">
                      <h5>Tanggal</h5>
                  </div>
                  <div class="col">
                      <h5>Atas Nama</h5>
                  </div>
                  <div class="col">
                      <h5>Jenis Hewan</h5>
                  </div>
                  <div class="col">
                      <h5>Tipe</h5>
                  </div>
                  <div class="col">
                      <h5>Jumlah</h5>
                  </div>
                  <div class="col">
                      <h5>Total</h5>
                  </div>
                  <div class="col">
                      <h5>Proses Kurban</h5>
                  </div>
                  <div class="col">
                      <h5>Bukti Transfer</h5>
                  </div>
                  <div class="col">
                      <h5>Status</h5>
                  </div>
                </div>
                <br>
                <div class="row d-flex align-items-center mb-4" v-for="(pembayaran,index) in pembayarans" :key="index">
                  <div class="col">
                    <h5>{{pembayaran.created_at | formatDate}}</h5>
                  </div>
                  <div class="col">
                      <h5>{{pembayaran.nama}}</h5>
                  </div>
                  <div class="col">
                      <h5>{{pembayaran.package.nama}} {{pembayaran.package.variant}}</h5>
                  </div>
                  <div class="col">
                      <h5><span v-if="pembayaran.package.tipe == 'kambing_jantan'">Jantan</span></h5>
                      <h5><span v-if="pembayaran.package.tipe == 'sapi'">Sapi</span></h5>
                  </div>
                  <div class="col">
                      <h5>{{pembayaran.jumlah}}</h5>
                  </div>
                  <div class="col">
                    <h5>{{pembayaran.total | rupiah}}</h5>
                  </div>
                  <div class="col">
                    <h5><span v-if="pembayaran.proses == 'inqilabi_farm'">Inqilabi Farm</span></h5>
                    <h5><span v-if="pembayaran.proses == 'dikirjm'">Dikirim</span></h5>
                  </div>
                  <div class="col">
                    <button class="btn btn-primary btn-sm">Lihat</button>
                  </div>
                  <div class="col">
                    <button v-if="pembayaran.status == 'success'" class="btn btn-success text-light font-weight-bold">Success</button>
                    <button v-else-if="pembayaran.status == 'failed'" class="btn btn-danger text-light font-weight-bold">Failed</button>
                    <button v-else class="btn btn-warning text-light font-weight-bold">Pending</button>
                  </div>
                </div>

                <!-- <div class="row d-flex align-items-center mb-4">
                    <div class="col">
                      12/6/2021
                    </div>
                    <div class="col">
                        <h5>Transbara</h5>
                    </div>
                    <div class="col">
                        <h5>Kambing / Domba Super</h5>
                    </div>
                    <div class="col">
                        <h5>Jantan</h5>
                    </div>
                    <div class="col">
                        <h5>1</h5>
                    </div>
                    <div class="col">
                      <h5>Rp 2.500.000</h5>
                    </div>
                    <div class="col">
                      <h5>Inqilabi Farm</h5>
                    </div>
                    <div class="col">
                      <button class="btn btn-primary btn-sm">Lihat</button>
                    </div>
                    <div class="col">
                      <button class="btn btn-success text-light font-weight-bold">Success</button>
                    </div>
                </div>
                <div class="row d-flex align-items-center mb-4">
                    <div class="col">
                      12/6/2021
                    </div>
                    <div class="col">
                        <h5>Transbara</h5>
                    </div>
                    <div class="col">
                        <h5>Sapi</h5>
                    </div>
                    <div class="col">
                        <h5>Patungan 7 Orang</h5>
                    </div>
                    <div class="col">
                        <h5>1</h5>
                    </div>
                    <div class="col">
                      <h5>Rp 2.500.000</h5>
                    </div>
                    <div class="col">
                      <h5>Dikirim</h5>
                    </div>
                    <div class="col">
                      <button class="btn btn-primary btn-sm">Lihat</button>
                    </div>
                    <div class="col">
                      <button class="btn btn-danger text-light font-weight-bold">Failed</button>
                    </div>
                </div>
                <div class="row d-flex align-items-center mb-4">
                    <div class="col">
                      12/6/2021
                    </div>
                    <div class="col">
                        <h5>Transbara</h5>
                    </div>
                    <div class="col">
                        <h5>Sapi</h5>
                    </div>
                    <div class="col">
                        <h5>Patungan 7 Orang</h5>
                    </div>
                    <div class="col">
                        <h5>1</h5>
                    </div>
                    <div class="col">
                      <h5>Rp 2.500.000</h5>
                    </div>
                    <div class="col">
                      <h5>Dikirim</h5>
                    </div>
                    <div class="col">
                      <button class="btn btn-primary btn-sm">Lihat</button>
                    </div>
                    <div class="col">
                      <button class="btn btn-warning text-light font-weight-bold">Pending</button>
                    </div>
                </div> -->
              </div>
            </table>
          </div>
        </div>
      </div>

    <div class="d-flex justify-content-center my-5">
    </div>
  </div>
</template>

<script>
export default {
  data() {
    return {
      pembayarans: [],
    };
  },
  methods: {
    getPembayaranUser() {
      this.axios.get('getPembayaranUser').then(response => {
        this.pembayarans = response.data.data
        // console.log(this.pembayarans);
      }).catch(error => {
        console.log(error.response);
      })
    }
  },
  mounted() {
    this.getPembayaranUser()
  }
};
</script>
