<template>
    <div>
        <h1 class="centralizado">{{titulo}}</h1>
        <input type="search" class="filtro" v-on:input="filtro = $event.target.value" placeholder="Insira o título da imagem">
        <ul class="lista-fotos">
            <li class="lista-fotos-item" v-for="foto of fotosComFiltro">
                <meu-painel :titulo="foto.titulo">
                  <img class="imagem-responsiva" :src="foto.url" :alt="foto.titulo">
                  <meu-botao tipo="button" rotulo="REMOVER" @click.native="remove(foto)"/>
                </meu-painel>
             </li>
        </ul>
    </div>
</template>

<script>
import Painel from "../shared/painel/Painel.vue";
import Botao from "../shared/botao/Botao.vue";

export default {
  components: {
    "meu-painel": Painel,
    "meu-botao": Botao
  },

  data() {
    return {
      titulo: "Imagens aleatórias",
      fotos: [],
      filtro: ""
    };
  },

  methods: {
    remove(foto) {
      if (confirm("Confirma?")) {
        alert("Me remove! " + foto.titulo);
      }
    }
  },

  computed: {
    fotosComFiltro() {
      if (this.filtro) {
        let exp = new RegExp(this.filtro.trim(), "i");
        return this.fotos.filter(foto => exp.test(foto.titulo));
      } else {
        return this.fotos;
      }
    }
  },

  created() {
    this.$http
      .get("http://localhost:3000/v1/fotos")
      .then(res => res.json())
      .then(fotos => (this.fotos = fotos), err => console.log(err));
  }
};
</script>

<style scope>
.centralizado {
  text-align: center;
}

.lista-fotos {
  list-style: none;
}

.lista-fotos .lista-fotos-item {
  display: inline-block;
}

.imagem-responsiva {
  width: 100%;
}

.filtro {
  display: block;
  width: 70%;
}
</style>
