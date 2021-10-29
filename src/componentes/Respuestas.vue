<template>

  <section class="src-componentes-respuestas">
    <div class="jumbotron">
      <h2>Respuestas</h2>
      <br>

      <div class="table-responsive">
        <table class="table table-dark">
          <tr>
            <th>Numero de Pregunta</th>
            <th>Respuesta</th>
          </tr>
          <tr>
            <td>1</td>
            <td>['d']</td>
          </tr>
          <tr>
            <td>2</td>
            <td>['a', 'b', 'c']</td>
          </tr>
          <tr>
            <td>3</td>
            <td>['e']</td>
          </tr>
        </table>
      </div>      

    </div>
  </section>

</template>

<script>

  export default  {
    name: 'src-componentes-respuestas',
    props: [],
    mounted () {

    },
    data () {
      return {
        preguntas : [
          { numero: 1, respuestas: ['d'] },
          { numero: 2, respuestas: ['a', 'b', 'c'] },
          { numero: 3, respuestas: ['e'] }
        ]
      }
    },
    methods: {

    },
    computed: {

    }
}


</script>

<style scoped lang="css">
  .src-componentes-respuestas {

  }

  .jumbotron {
    background-color: rgb(248, 224, 250);
    color: rgb(68, 9, 63);
  }
</style>
