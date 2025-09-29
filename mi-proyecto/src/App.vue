<template>
  <div class="container-fluid mt-3">
    <h3 class="mb-3">Listado de Personas</h3>

    <input
      type="text"
      class="form-control mb-2"
      v-model="criterioNombre"
      placeholder="Buscar por nombre o apellido..."
      :disabled="criterioDni.length > 0 && !criterioNombre"
    />

    <input
      type="text"
      class="form-control mb-2"
      v-model="criterioDni"
      placeholder="Buscar por DNI..."
      :disabled="criterioNombre.length > 0 && !criterioDni"
    />

    <div
      class="alert alert-warning"
      v-if="(criterioNombre && criterioNombre.length < 3) || (criterioDni && criterioDni.length < 3)"
    >
      Por favor, ingrese al menos 3 caracteres en los filtros.
    </div>

    <Personas :personas="personasFiltradas" />
  </div>
</template>

<script>
import Personas from "./components/Personas.vue";

export default {
  name: "App",
  components: { Personas },
  data() {
    return {
      criterioNombre: "",
      criterioDni: "",
      personas: [
        {
          nombre: "Daniel",
          apellido: "Sanchez",
          correo: "danielsanchez68@hotmail.com",
          dni: "20442873",
        },
        {
          nombre: "Lucas",
          apellido: "Villani",
          correo: "lv@gmail.com",
          dni: "41005463",
        },
        {
          nombre: "Mathias",
          apellido: "Prez",
          correo: "mp@gmail.com",
          dni: "928371923",
        },
        {
          nombre: "Lucas",
          apellido: "Montes",
          correo: "lucas@gmail.com",
          dni: "11223344",
        },
      ],
    };
  },
  computed: {
    personasFiltradas() {
      return this.personas.filter((persona) => {
        let coincideNombre = true;
        let coincideDni = true;

        if (this.criterioNombre) {
          let nombreCompleto = `${persona.nombre} ${persona.apellido}`.toLowerCase();
          coincideNombre = nombreCompleto.includes(this.criterioNombre.toLowerCase());
        }

        if (this.criterioDni) {
          coincideDni = persona.dni.includes(this.criterioDni);
        }

        return coincideNombre && coincideDni;
      });
    },
  },
};
</script>
