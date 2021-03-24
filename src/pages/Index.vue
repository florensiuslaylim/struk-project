<template>
  <q-page class="q-pa-md row q-gutter-md justify-between">
    <q-card v-for="laporan in laporanTransaksi" :key="laporan.id" style="min-width: 310px">
      <q-card-section class="text-center">
        <div class="header-company">
          <p class="header-companyName">PT. PIONEER</p>
          <p class="header-companyAddress">Jl Ir H Juanda No. 40-42 Jakarta 10120</p>

        </div>
        <p>NPWP:</p>
        <p>01.313.974.6-073.000</p>
        <div class="row justify-between q-mt-md">
          <div class="left row">
            <p>Struk:</p>
            <p>{{ laporan['No Faktur'] }}</p>
          </div>
          <div class="right">
            <p>{{ laporan['Tanggal'] }} {{ laporan['Jam'] }}</p>
          </div>
        </div>
        <p class="text-right" style="margin: 0">Tunai</p>
        <div>
          <fieldset class="border-style"><legend>SALINAN</legend></fieldset>
          <p class="text-left">{{ laporan['Deskripsi Produk'] }}</p>
          <div class="row">
            <p class="text-left" style="margin-right: 30px;">x{{ laporan['Jumlah Barang'] }}</p>
            <p>@{{ laporan['Harga Per Barang'] }}</p>
            <q-space />
            <p>{{ laporan['Subtotal'] }}</p>
          </div>
        </div>
      </q-card-section>
    </q-card>
  </q-page>
</template>

<script>
import Vue from 'vue'
import { mapGetters } from 'vuex'
import Print from 'vue-print-nb'

Vue.use(Print)

export default {
  data() {
    return {
    }
  },
  created () {
    if (this.laporanTransaksi) {
      this.laporanTransaksi.forEach((item, i) => {
        item.id = i + 1
      })
      console.log(this.laporanTransaksi)
    }
  },
  filters: {
    dateFormat () {
    },
    timeFormat () {
    }
  },
  computed: {
    ...mapGetters(['laporanTransaksi'])
  }
}
</script>

<style scoped>
  div .header-company p {
    font-weight: bold;
    margin: 0;
    padding: 0;
  }

  .header-companyName {
    font-size: 20px;
  }

  .header-companyAddress {
    font-size: 9px;
  }

  .border-style {
    border: 1px dashed;
    box-sizing: border-top;
    border-left: transparent;
    border-right:transparent;
    border-bottom: transparent;
    padding: 0;
  }
</style>
