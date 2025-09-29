<template>
  <div>
    <div class="row">
      <div class="col" v-for="persona in personas" :key="persona.dni">
        <div class="card mb-3">
          <div class="card-body">
            <h5 class="card-title">{{ getNombreCompleto(persona) }}</h5>
            <p class="card-text">DNI {{ persona.dni }}</p>
            <a href="#" class="card-link">{{ persona.correo }}</a>
          </div>
        </div>
      </div>
    </div>
  </div>
</template>

<script>
export default {
  name: "Personas",
  props: {
    personas: {
      type: Array,
      required: true,
    },
  },
  methods: {
    getNombreCompleto(persona) {
      return `${persona.nombre} ${persona.apellido}`;
    },
  },
};
</script>
