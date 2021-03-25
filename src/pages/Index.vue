<template>
  <q-page>
    <q-btn class="q-ma-md" color="blue" outline label="Print This Page" @click="printPage" />
    <div id="printThis" style="padding: 15px; display: flex; flex-wrap: wrap;
    justify-content: space-between; font-size: 9px;">
      <div style="border: 1px solid grey; padding: 20px 10px; width: 190px; min-height: 267px; margin-top: 10px"
      v-for="laporan in laporanTransaksi" :key="laporan.id">
        <div style="text-align: center;">
          <div>
            <p style="margin: 0; padding: 0; font-size: 11px;">PT. PIONEER</p>
            <p style="margin: 0; padding: 0; font-size: 7px;">Jl Ir H Juanda No. 40-42 Jakarta 10120</p>
          </div>

          <div style="margin-top: 10px;">
            <p style="margin: 0; padding: 0; font-size: 8px;">NPWP:</p>
            <p style="margin: 0; padding: 0; font-size: 8px;">01.313.974.6-073.000</p>
          </div>

          <div style="margin-top: 15px;">
            <p style="margin: 0; padding: 0; font-weight: bold; font-size: 9px;">Villa Duta Sport</p>
            <p style="margin: 0; padding: 0;">Jl Rena Wijaya No. 9 Villa Duta,</p>
            <p style="margin: 0; padding: 0;">Bogor</p>
            <p style="margin: 0; padding: 0;">Telp : 0251.8312852 - 081113224</p>
          </div>

          <div style="display: flex; flex-direction: row; justify-content: space-between;
          margin-top: 10px;">
            <div style="display: flex; flex-direction: row;">
              <p style="margin: 0">Struk:</p>
              <p style="margin: 0">{{ laporan['No Faktur'] }}</p>
            </div>
            <div class="right">
              <p style="margin: 0">{{ laporan['Tanggal'] | dateFormat }} {{ laporan['Jam'] | timeFormat }}</p>
            </div>
          </div>

          <p style="text-align: right; margin: 0;">Tunai</p>

          <div style="margin-bottom: 10px;">
            <fieldset style="border: 1px dashed;box-sizing: border-top;border-left: transparent;
            border-right:transparent; border-bottom: transparent; padding: 0; font-weight: bold;">
              <legend>SALINAN</legend>
            </fieldset>
            <p style="margin: 0; text-align: left;">{{ laporan['Deskripsi Produk'] }}</p>
            <div style="display: flex; flex-direction: row; padding-bottom: 5px;">
              <p style="margin-top: 0; margin-bottom: 0; margin-right: 20px;">x{{ laporan['Jumlah Barang'] }}</p>
              <p style="margin-top: 0; margin-bottom: 0; mergin-left: 20px;">@{{ laporan['Harga Per Barang'] | priceCommas }}</p>
              <p style="margin-top: 0; margin: 0; text-align: right; margin-left: auto; margin-top: auto;">{{ laporan['Subtotal'] | priceCommas }}</p>
            </div>
            <fieldset  style="border: 1px dashed;box-sizing: border-top;border-left: transparent;
            border-right:transparent; border-bottom: transparent; padding: 0; font-weight: bold;">
            </fieldset>
          </div>

          <div class="header-subtotal" style="margin-top: 10px; margin: 0;">
            <div style="display: flex; flex-direction: row; justify-content: space-between;">
              <p style="margin: 0; padding: 0;">Subtotal</p>
              <p style="margin: 0; padding: 0;">{{ laporan['Subtotal'] | priceCommas }}</p>
            </div>
            <div style="display: flex; flex-direction: row; justify-content: space-between;
            font-weight: bold;">
              <p style="margin: 0; padding: 0;">Total</p>
              <p style="margin: 0; padding: 0;">{{ laporan['Subtotal'] | priceCommas }}</p>
            </div>
            <div style="display: flex; flex-direction: row; justify-content: space-between;">
              <p style="margin: 0; padding: 0;">Bayar</p>
              <p style="margin: 0; padding: 0;">{{ laporan['Subtotal'] | priceCommas }}</p>
            </div>
            <div style="display: flex; flex-direction: row; justify-content: space-between;">
              <p style="margin: 0; padding: 0;">Kembali</p>
              <p style="margin: 0; padding: 0;">0</p>
            </div>
          </div>

          <div style="margin-top: 15px;">
            <p>HARGA SUDAH TERMASUK PPN 10%</p>
          </div>
        </div>
      </div>
    </div>
  </q-page>
</template>

<script>
import { mapGetters } from 'vuex'
import { date } from 'quasar'

export default {
  created () {
    if (this.laporanTransaksi) {
      this.laporanTransaksi.forEach((item, i) => {
        item.id = i + 1
      })
    }
  },
  filters: {
    dateFormat (value) {
      if (value) {
        let splitDate = value.split('-').reverse().join('-')
        let getDate = new Date(splitDate)
        let formattedDate = date.formatDate(getDate, 'DD/MM/YY')
        return formattedDate
      }
      return 0
    },
    timeFormat (value) {
      if (value) {
        let splitTime = value.split(':')
        let result = splitTime.slice(0, splitTime.length - 1).join(':')
        return result
      }
      return 0
    },
    priceCommas (val) {
      if (val) {
        return val.toString().replace(/\B(?=(\d{3})+(?!\d))/g, '.')
      }
      return 0
    }
  },
  methods: {
    printPage () {
      const divToPrint = document.getElementById('printThis')
      let newWin = window.open('')
      newWin.document.write(divToPrint.outerHTML)
      newWin.print()
      newWin.close()
    }
  },
  computed: {
    ...mapGetters(['laporanTransaksi'])
  }
}
</script>

<style scoped>
</style>
