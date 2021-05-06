<template>
  <ul class="lista-fotos">
    <li class="fotos" v-for="foto in fotos" :key="foto">
      <img :src="foto">
    </li>
  </ul>
</template>

<script>
export default {
  data: () => ({
    dadosAlbum: '',
    fotos: []
  }),

  created(){
    this.buscaAlbumFotos()
  },

  methods: {
    /* Busca Albuns */
    async buscaAlbumFotos(){
      let resp = await this.$axios.get('https://graph.instagram.com/me/media?fields=id,caption&access_token=IGQVJXYTdVcUg4LVd5c3l6TEdxYnpEcEdyU2pZAYU44QlRJZAHk5LVFmSzFvU0ZAVS3VTSUJCTUtSWFBqcFBINEc3RHF0Y1FSTURhM0oxZAXZA0TGZAoM0RZARmdzc05lTHZABdGNYWnIyeXN5YWVoa2R6OG5tMgZDZD')

      this.dadosAlbuns = resp.data.data.slice(0,4)

      /* Laço que executa o metodo de capturar fotos passando o id da foto por parametro */
      this.dadosAlbuns.forEach(e => {
        this.capturaFotos(e.id)
      })
    },
    /* Busca fotos */
    async capturaFotos(id){
      let resp = await this.$axios.get(`https://graph.instagram.com/${id}?fields=id,media_type,media_url,username,timestamp&access_token=IGQVJXYTdVcUg4LVd5c3l6TEdxYnpEcEdyU2pZAYU44QlRJZAHk5LVFmSzFvU0ZAVS3VTSUJCTUtSWFBqcFBINEc3RHF0Y1FSTURhM0oxZAXZA0TGZAoM0RZARmdzc05lTHZABdGNYWnIyeXN5YWVoa2R6OG5tMgZDZD`)

      this.fotos.push(resp.data.media_url)

      console.log('Resposta das Fotos Individuais', this.fotos)
    }
  }
}
</script>

<!-- Add "scoped" attribute to limit CSS to this component only -->
<style scoped lang="scss">
.lista-fotos{
  width: 100%;
  margin-top: 60px;
  display: flex;
  align-items: center;
  justify-content:center;
  list-style: none;

  .fotos{
    width: 250px;
    height: 250px;
    margin-right: 20px;

    &:last-child{
      margin-right: 0;
    }

    img{
      width: 100%;
      height: 100%;
    }
  }
}
</style>
