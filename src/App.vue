<template>
<div class="container-fluid mt-3" id="app">
    <!-- Filtro por nombre/apellido -->
    <form class="mb-3">
      <input
        type="text"
        class="form-control"
        v-model="criterioNombre"
        placeholder="Buscar por nombre o apellido"
      />
    </form>

    <!-- Filtro por DNI -->
    <form class="mb-3">
      <input
        type="text"
        class="form-control"
        v-model="criterioDni"
        placeholder="Buscar por DNI"
      />
    </form>

    <!-- Alerta de advertencia -->
    <div
      class="alert alert-warning"
      role="alert"
      v-if="mostrarAdvertencia()"
    >
      Por favor, ingrese al menos 3 caracteres en alguno de los filtros para realizar la búsqueda.
    </div>

    <div class="card-deck m-0">
      <div class="row">
        <div class="col" v-for="persona in personasFiltradas" :key="persona.dni">
          <div class="card mb-3">
            <div class="card-body">
              <h5 class="card-title">{{ getNombreCompleto(persona) }}</h5>
              <p class="card-text">dni {{ persona.dni }}</p>
              <a href="#" class="card-link">{{ persona.correo }}</a>
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
      criterioNombre: '',
      criterioDni: '',
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
      // Si ambos filtros están vacíos, no se muestra nada.
      if (!this.criterioNombre && !this.criterioDni)
      {
        return this.personas;
      }

      return this.personas.filter((persona) => {
        const nombreCompleto = `${persona.nombre} ${persona.apellido}`.toLowerCase();
        const dni = persona.dni.toLowerCase();
        const criterioNombre = this.criterioNombre.toLowerCase();
        const criterioDni = this.criterioDni.toLowerCase();

        // Si ambos filtros tienen valor, ambos deben cumplirse (excluyente).
        if (criterioNombre && criterioDni)
        {
          return nombreCompleto.includes(criterioNombre) && dni.includes(criterioDni);
        }

        // Si solo hay filtro de nombre.
        if (criterioNombre)
        {
          return nombreCompleto.includes(criterioNombre);
        }

        // Si solo hay filtro de DNI.
        if (criterioDni)
        {
          return dni.includes(criterioDni);
        }

        // Si no hay ninguno, no muestra nada (ya cubierto arriba).
        return false;
      });
  }
  },
  methods:
  {
    getNombreCompleto(persona)
    {
      return `${persona.nombre} ${persona.apellido}`
    },
    mostrarAdvertencia()
    {
      return (
        (this.criterioNombre.length > 0 && this.criterioNombre.length < 3) ||
        (this.criterioDni.length > 0 && this.criterioDni.length < 3)
      );
    }
  }
}
</script>

<style scoped>
</style>