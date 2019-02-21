<template>
  <v-content>
    <v-form class="ma-2" v-if="formAdicionarVisivel">
      <v-container fluid class="elevation-1 mb-4">
        <v-layout row wrap>
          <v-flex>
            <v-text-field
              label="Dia Vencimento"
            ></v-text-field>
          </v-flex>
          <v-flex>
            <v-text-field
              label="Descrição"
            ></v-text-field>
          </v-flex>
          <v-flex>
            <v-text-field
              label="Valor"
            ></v-text-field>
          </v-flex>
        </v-layout>
        <v-card-text style="height: 30px; position: relative">
          <v-btn
            absolute
            right
            bottom
            @click.prevent.stop="cancelaAdicionar"
          >
            Adicionar
          </v-btn>
          <v-btn
            absolute
            left
            bottom
            @click.prevent.stop="adicionar"
          >
            Cancelar
          </v-btn>
        </v-card-text>
      </v-container>
    </v-form>
    <v-data-table
      :headers="cabecalho"
      :items="contas"
      :expand="expandir"
      class="elevation-1 ma-2"
      hide-actions
      item-key="desc"
    >
      <template slot="items" slot-scope="props" >
        <tr @click="props.expanded = !props.expanded">
          <td>
            {{ props.item.dia }}
          </td>
          <td>
            {{ props.item.desc }}
          </td>
          <td
            class="text-xs-right">
            <v-icon
              v-if="props.item.receb === 'OK'"
              >mdi-email-open-outline
            </v-icon>
          </td>
          <td
            class="text-xs-right">
            {{ props.item.valor }}
          </td>
          <td
            class="text-xs-right">
            <v-icon
              v-if="props.item.pago === 'OK'"
              >mdi-currency-usd
            </v-icon>
          </td>
        </tr>
      </template>
      <template slot="expand">
        <v-card flat color="#cccccc">
          <v-btn
            relative
            fab
            small
            @click.prevent.stop="abreFormAdicionar"
          >
            <v-icon>mdi-pencil-outline</v-icon>
          </v-btn>
          <v-btn
            relative
            fab
            small
            @click.prevent.stop="perguntaExcluir"
          >
            <v-icon>mdi-delete-outline</v-icon>
          </v-btn>
          <v-btn
            relative
            fab
            small
          >
            <v-icon>mdi-email-open-outline</v-icon>
          </v-btn>
          <v-btn
            relative
            fab
            small
          >
            <v-icon>mdi-currency-usd</v-icon>
          </v-btn>
        </v-card>
      </template>
    </v-data-table>
    <v-card-text style="height: 50px; position: relative">
      <v-btn
        absolute
        fab
        bottom
        right
        @click.prevent.stop="abreFormAdicionar"
        v-if="botaoAdicionarVisivel"
      >
        <v-icon>mdi-plus</v-icon>
      </v-btn>
    </v-card-text>
    <v-dialog
      v-model="dialogExcluir">
      <v-card>
        <v-card-title
          class="headline grey lighten-2"
          primary-title="">
          Confirma?
        </v-card-title>
        <v-card-text>
          Deseja realmente excluir essa conta?
        </v-card-text>
        <v-divider></v-divider>
        <v-card-actions>
          <v-btn
            relative
            @click="dialogExcluir=false"
          >
            <v-icon>mdi-cancel</v-icon> Cancelar
          </v-btn>
          <v-spacer></v-spacer>
          <v-btn
            relative
            @click="dialogExcluir=false"
          >
            <v-icon>mdi-check</v-icon> Confirmar
          </v-btn>
        </v-card-actions>
      </v-card>
    </v-dialog>
  </v-content>
</template>

<script>
export default {
  data() {
    return {
      dialogExcluir: false,
      expandir: false,
      formAdicionarVisivel: false,
      botaoAdicionarVisivel: true,
      cabecalho: [
        { text: 'Dia', value: 'dia', width: '10%' },
        { text: 'Descrição', value: 'desc', width: '60%' },
        {
          text: 'Recebido',
          value: 'receb',
          width: '10%',
          align: 'right',
        },
        {
          text: 'Valor',
          value: 'valor',
          width: '10%',
          align: 'right',
        },
        {
          text: 'Pago',
          value: 'pago',
          width: '10%',
          align: 'right',
        },
      ],
      contas: [
        {
          dia: 2,
          desc: 'Aluguel Marília',
          receb: 'OK',
          valor: 1120.55,
          pago: 'OK',
        },
        {
          dia: 7,
          desc: 'Parcela AP Tupã',
          receb: 'OK',
          valor: 690.00,
          pago: null,
        },
        {
          dia: 10,
          desc: 'Concomínio AP Fco Morato',
          receb: null,
          valor: 399.34,
          pago: null,
        },
      ],
    };
  },
  methods: {
    abreFormAdicionar() {
      this.formAdicionarVisivel = true;
      this.botaoAdicionarVisivel = false;
    },
    cancelaAdicionar() {
      this.formAdicionarVisivel = false;
      this.botaoAdicionarVisivel = true;
    },
    adicionar() {
      this.formAdicionarVisivel = false;
      this.botaoAdicionarVisivel = true;
    },
    alterarRecebido() {
      console.log('Click recebido');
    },
    alterarPago() {
      console.log('Click pago');
    },
    perguntaExcluir() {
      this.dialogExcluir = true;
    },
  },
};
</script>

<style>
table.v-table tbody td:first-child,
table.v-table tbody td:not(:first-child),
table.v-table tbody th:first-child,
table.v-table tbody th:not(:first-child),
table.v-table thead td:first-child,
table.v-table thead td:not(:first-child),
table.v-table thead th:first-child,
table.v-table thead th:not(:first-child) {
  padding: 0 10px
}
</style>
