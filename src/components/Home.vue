<template>
  <div>
    <navbar></navbar><br>
    <div class="container">
      <div class="row">
        <div class="col-md-6">
          <div class="card">
            <h5 class="card-header">Real para Dolar</h5>
            <div class="card-body">
              <div class="row">
                <div class="col-md-12">
                  <div class="input-group mb-3">
                    <div class="input-group-prepend">
                      <span class="input-group-text">$</span>
                    </div>
                    <input type="text" class="form-control text-center" aria-label="Amount (to the nearest dollar)" :value="valorConvertidoParaDolar" disabled>
                  </div>
                </div>
              </div>
              <div class="row">
                <div class="col-md-12">
                  <label for="valor_a_converter_para_dolar">Valor a ser convertido:</label>
                  <div class="input-group mb-3">
                    <div class="input-group-prepend">
                      <span class="input-group-text">R$</span>
                    </div>
                    <input type="text" name="valor_a_converter_para_dolar" id="valor_a_converter_para_dolar" class="dinheiro form-control" placeholder="Valor a ser convertido">
                  </div>
                </div>
              </div>
              <div class="row">
                <div class="col-md-12">
                  <label for="data_a_converter_para_dolar">Data:</label>
                  <input type="date" name="data_a_converter_para_dolar" id="data_a_converter_para_dolar" class="form-control" disabled>
                </div>
              </div>
              <div class="row">
                <div class="col-md-12"><br>
                  <button class="btn btn-success btn-block" @click="converterRealParaDolar">Converter</button>
                </div>
              </div>
            </div>
          </div>
        </div>
        <div class="col-md-6">
          <div class="card">
            <h5 class="card-header">Dolar para Real</h5>
            <div class="card-body">
              <div class="row">
                <div class="col-md-12">
                  <div class="input-group mb-3">
                    <div class="input-group-prepend">
                      <span class="input-group-text">R$</span>
                    </div>
                    <input type="text" class="form-control text-center" aria-label="Amount (to the nearest dollar)" :value="valorConvertidoParaReal" disabled>
                  </div>
                </div>
              </div>
              <div class="row">
                <div class="col-md-12">
                  <label for="valor_a_converter_para_real">Valor a ser convertido:</label>
                  <div class="input-group mb-3">
                    <div class="input-group-prepend">
                      <span class="input-group-text">$</span>
                    </div>
                    <input type="text" name="valor_a_converter_para_real" id="valor_a_converter_para_real" class="dinheiro form-control" placeholder="Valor a ser convertido">
                  </div>
                </div>
              </div>
              <div class="row">
                <div class="col-md-12">
                  <label for="data_a_converter_para_real">Data:</label>
                  <input type="date" name="data_a_converter_para_real" id="data_a_converter_para_real" class="form-control" disabled>
                </div>
              </div>
              <div class="row">
                <div class="col-md-12"><br>
                  <button class="btn btn-success btn-block" @click="converterDolarParaReal">Converter</button>
                </div>
              </div>
            </div>
          </div>
        </div>
      </div>
    </div>

    <footer class="footer navbar-fixed-bottom">
      <div class="card-footer ">
        <div class="row">
          <div class="col-md-12" style="width: 3000px">Desenvolvido por: Dário Santos | Erandir Junior </div>
        </div>
      </div>
    </footer>
  </div>
</template>

<script>
export default {
  name: 'Home',
  data: function () {
    return {
      urlConversaoParaDolar: 'http://economia.awesomeapi.com.br/USD-BRL/1',
      urlConversaoParaReal: 'http://economia.awesomeapi.com.br/USD-BRL/1',
      valorConvertidoParaDolar: '0.00',
      valorConvertidoParaReal: '0.00'
    }
  },
  methods: {
    converterRealParaDolar: function () {
      let self = this
      let valor = document.getElementById('valor_a_converter_para_dolar').value
      this.$http.get(this.urlConversaoParaDolar).then(function (response) {
        console.log(response.data)
        if (response.status === 200) {
          self.valorConvertidoParaDolar = (valor / response.data[0].bid).toFixed(3)
        } else {
          alert('Não foi possivel converter!')
        }
      })
    },
    converterDolarParaReal: function () {
      let self = this
      let valor = document.getElementById('valor_a_converter_para_real').value
      this.$http.get(this.urlConversaoParaReal).then(function (response) {
        if (response.status === 200) {
          self.valorConvertidoParaReal = (valor * response.data[0].bid).toFixed(3)
        } else {
          alert('Não foi possivel converter!')
        }
      })
    }
  }
}
</script>

<style scoped>
  footer {
    position: fixed;
    bottom:0;
    left:0;
  }
</style>
