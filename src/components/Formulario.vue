<template>
  <div>
      <b-container>
          <b-row>
              <b-col>
                <b-alert :show="response=='success'" variant="success" dismissible>
                    Se ha realizado la búsqueda con éxito
                </b-alert>
                <b-alert :show="response=='error'" variant="danger" dismissible>
                    Se ha producido un error
                </b-alert>
              </b-col>
          </b-row>
          <b-row>
            <b-col></b-col>
            <b-col>
                <b-overlay :show="procesando" rounded="sm">
                    <b-form-group
                        label="Número a Buscar:"
                        label-for="numero"
                    >
                        <b-form-input
                        id="numero"
                        type="text"
                        v-model="numero"
                        placeholder="Introduzca un número"
                        ></b-form-input>
                    </b-form-group>
                    <b-form-group
                        label="Resultado:"
                        label-for="resultado"
                    >
                        <b-form-input
                        id="resultado"
                        type="text"
                        v-model="result"
                        readonly
                        placeholder="Resultado"
                        ></b-form-input>
                    </b-form-group>
                </b-overlay>
                <b-button @click="calcular">Calcular</b-button>
            </b-col>
            <b-col></b-col>
        </b-row>
      </b-container>
  </div>
</template>

<script>
import http from "../lib/http";

export default {
    name: 'Formulario',
    data: function (){
        return {
            http: http,
            numero: 0,
            result: 0,
            procesando: false,
            response: null
        }
    },
    methods: {
        calcular: function () {
            this.procesando = true;
            let that = this;
            http.get(`${this.numero}`)
            .then(function (res) {
                that.response = 'success';
                that.result = res.data.result;
            })
            .catch(function (error) {
                that.response = 'error';
                that.result = 'Error';
            })
            .then(function () {
                that.procesando = false;
            });;
        }
    }
}
</script>

<style>

</style>