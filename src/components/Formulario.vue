<template>
  <div>
      <b-container>
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
            procesando: false
        }
    },
    methods: {
        calcular: function () {
            this.show = true;
            let that = this;
            http.get(`${this.numero}`).then(function (res) {
                console.log('res', res);
                that.result = res.data.result;
                this.show = false;
            })
            .catch(function (res) {
                console.error('res', res);
                that.result = res.data.result;
                this.show = false;
            });
        }
    }
}
</script>

<style>

</style>