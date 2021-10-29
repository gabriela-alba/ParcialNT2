<template>

  <section class="src-componentes-ingreso">
    <div class="jumbotron">
      <h2>Ingreso de Gastos</h2>
      <hr>

      <vue-form :state="formstate" @submit.prevent="enviar()">
        
        <!-- Campo nombre -->
        <validate tag="div">
          <label for="nombre">Nombre</label>
          <input type="text" id="nombre" name="nombre" class="form-control" autocomplete="off" v-model="formData.nombre" 
                 required 
                 :minNombre="nombreMin"
                 :maxNombre="nombreMax"
                 no-espacios/>
    
          <field-messages name="nombre" show="$dirty">
            <div slot="required" class="alert alert-danger mt-1">Este campo es obligatorio.</div>
            <div slot="no-espacios" class="alert alert-danger mt-1">No se permiten espacios intermedios en este campo.</div>
            <div slot="minNombre" class="alert alert-danger mt-1">Este campo requiere como mínimo {{nombreMin}} caracteres.</div>
            <div v-if="formData.nombre.length == nombreMax" class="alert alert-danger mt-1">Este campo requiere como máximo {{nombreMax}} caracteres.</div>
          </field-messages>
        </validate>
        <br>

        <!-- Campo descripción -->
        <validate tag="div">
          <label for="descripcion">Descripción</label>
          <input type="text" id="descripcion" v-model="formData.descripcion" required name="descripcion" autocomplete="off" class="form-control" />
    
          <field-messages name="descripcion" show="$dirty">
            <div slot="required" class="alert alert-danger mt-1">Este campo es obligatorio</div>
          </field-messages>
        </validate>
        <br>
        
        <!-- Campo importe -->
        <validate tag="div">
          <label for="importe">Importe</label>
          <input type="number" id="importe" v-model.number="formData.importe" required name="presupuesto" autocomplete="off" class="form-control" />
    
          <field-messages name="importe" show="$dirty">
            <div slot="required" class="alert alert-danger mt-1">Este campo es obligatorio</div>
          </field-messages>
        </validate>
        <br>

        <button class="btn btn-success my-3" :disabled="formstate.$invalid" type="submit">Enviar</button>
      </vue-form>
      <br>
      <hr>

      <!-- Tabla para representar los datos ingresados -->
      <h2>Detalle de Gastos</h2>
      <br>

      <!-- Campo presupuesto -->
        <validate tag="div">
          <label for="presupuesto">Presupuesto</label>
          <input type="number" id="presupuesto" v-model.number="formData.presupuesto" name="presupuesto" autocomplete="off" class="form-control" />
        </validate>
        <br>

      <div v-if="gastos.length" class="table-responsive">
        <table class="table">
          <tr>
            <th>Nombre</th>
            <th>Descripción</th>
            <th>Importe</th>
            <th>Fecha</th>
          </tr>
          <tr v-for="(gasto,index) in gastos" :key="index" :style="{color: calcularTotal().color }">
            <td>{{ gasto.nombre }}</td>
            <td>{{ gasto.descripcion }}</td>
            <td>{{ gasto.importe }}</td>
            <td>{{ gasto.fecha }}</td>
            <td>{{ calcularTotal().valor }}</td>
          </tr>

          <tr :style="{color: calcularTotal().color }">TOTAL: {{calcularTotal().valor}}</tr>

        </table>
      </div>
      <h3 v-else class="alert alert-info">No hay gastos ingresados</h3>
    </div>  
  </section>

</template>

<script>

  export default  {
    name: 'src-componentes-ingreso',
    props: [],
    mounted () {

    },
    data () {
      return {
        formstate : {},
        formData : this.getInitialData(),
        nombreMin : 3,
        nombreMax : 15,
        gastos : []
      }
    },
    methods: {
      getInitialData() {
        return {
          nombre : null,
          descripcion: null,
          importe: null,
        }
      },
      enviar() {
        let gasto = {...this.formData}
        gasto.fecha = new Date().toLocaleString()

        console.log(gasto)
        this.gastos.push(gasto)

        this.formData = this.getInitialData()
        this.formstate._reset()
      },
      calcularTotal() {
        let impMin = 1000
        let impMax = 5000
        let suma = 0
        this.datos.forEach(i => {
          suma += i.importe
        })
        let color = '#080'
        if(suma > impMin) color = '#39FF33'
        if(suma < impMax) color = '#ff00ff'
        else color = '#F39D28'
        return {
          valor : suma,
          color
        }
      }
    },
    computed: {
    }
}


</script>

<style scoped lang="css">
  .src-componentes-ingreso {

  }

  .jumbotron {
    background-color: rgb(164, 213, 240);
    color: rgb(54, 42, 165);
  }

  hr {
    background-color: rgb(196, 191, 191);
  }

  pre {
    color: rgb(191, 186, 186);
  }
</style>
