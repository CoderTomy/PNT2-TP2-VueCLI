<template>
  <div class="container-fluid mt-3" id="app">
        <input type="text" class="form-control" v-model="criterioDeBusqueda"
            placeholder="Ingresar un criterio de búsqueda">
        <br>
        <div class="card-deck m-0">
            <div class="row">
                <div class="col" v-for="persona in personasFiltradas">
                    <div class="card mb-3">
                        <div class="card-body">
                            <h5 class="card-title">{{getNombreCompleto(persona)}}</h5>
                            <p class="card-text">dni {{persona.dni}}</p>
                            <a href="#" class="card-link">{{persona.correo}}</a>
                        </div>
                    </div>
                </div>
            </div>
        </div>
    </div>
</template>

<script>
export default
{
  name: 'app',
  props:[],
  data()
  {
    return {
      criterioDeBusqueda: '',
      //Aquí, en este array es donde tienen que agregar su información
      personas:
      [
        {
          nombre: "Daniel",
          apellido: "Sanchez",
          correo: "danielsanchez68@hotmail.com",
          dni: "20442873"
        },
        {
          nombre: "Juan",
          apellido: "Perez",
          correo: "j@p.gmail.com",
          dni: "12345678"
        },
        {
          nombre: "Ana",
          apellido: "Suarez",
          correo: "a@s.gmail.com",
          dni: "87654321"
        },
        {
          nombre: "Pedro",
          apellido: "Marquez",
          correo: "pedro.marquez@outlook.com",
          dni: "16135477"
        },
      ]
    }
  },
  computed:
  {
    personasFiltradas()
    {
      return this.personas.filter((persona) => {
        let registroCompleto = `${persona.nombre} ${persona.apellido} ${persona.dni} ${persona.correo}`
        return registroCompleto.toLowerCase().includes(this.criterioDeBusqueda.toLowerCase())
      });
    }
  },
  methods:
  {
    getNombreCompleto(persona)
    {
      return `${persona.nombre} ${persona.apellido}`
    }
  }
}
</script>

<style scoped>
</style>