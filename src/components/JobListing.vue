<script setup>
// Importamos los módulos necesarios desde Vue y Vue Router
import { RouterLink } from 'vue-router'
import { defineProps, ref, computed } from 'vue'

// Definimos las propiedades (props) que este componente espera recibir
const props = defineProps({
  job: Object, // El prop `job` debe ser un objeto que contiene los datos del trabajo
})

// Variable reactiva que controla si se muestra la descripción completa o truncada
const showFullDescription = ref(false)

// Método para alternar entre mostrar y ocultar la descripción completa
const toggleFullDescription = () => {
  showFullDescription.value = !showFullDescription.value
}

// Propiedad computada que devuelve la descripción truncada o completa según el estado de `showFullDescription`
const truncatedDescription = computed(() => {
  let description = props.job.description // Obtenemos la descripción desde el prop `job`
  if (!showFullDescription.value) {
    // Si `showFullDescription` es false, truncamos la descripción a 90 caracteres
    description = description.substring(0, 90) + '...'
  }
  return description // Devolvemos la descripción procesada
})
</script>

<template>
  <!-- Contenedor principal con estilos -->
  <div class="bg-white rounded-xl shadow-md relative">
    <!-- Sección de encabezado -->
    <div class="p-4">
      <!-- Tipo y título del trabajo -->
      <div class="mb-6">
        <div class="text-gray-600 my-2">{{ job.type }}</div>
        <!-- Tipo de trabajo -->
        <h3 class="text-xl font-bold">{{ job.title }}</h3>
        <!-- Título del trabajo -->
      </div>

      <!-- Sección de descripción -->
      <div class="mb-5">
        <div>
          {{ truncatedDescription }}
          <!-- Descripción truncada o completa -->
        </div>
        <!-- Botón para alternar entre "Más" y "Menos" -->
        <button @click="toggleFullDescription" class="text-green-500 hover:text-green-600 mb-5">
          {{ showFullDescription ? 'Less' : 'More' }}
          <!-- Texto dinámico del botón -->
        </button>
      </div>

      <!-- Salario -->
      <h3 class="text-green-500 mb-2">{{ job.salary }} / Year</h3>
      <!-- Salario anual -->

      <!-- Línea divisoria -->
      <div class="border border-gray-100 mb-5"></div>

      <!-- Ubicación y enlace -->
      <div class="flex flex-col lg:flex-row justify-between mb-4">
        <!-- Ubicación -->
        <div class="text-orange-700 mb-3">
          <i class="pi pi-map-marker text-orange-700"></i>
          <!-- Icono de ubicación -->
          {{ job.location }}
          <!-- Ubicación del trabajo -->
        </div>
        <!-- Enlace a la página de detalles del trabajo -->
        <RouterLink
          :to="'/jobs/' + job.id"
          class="h-[36px] bg-green-500 hover:bg-green-600 text-white px-4 py-2 rounded-lg text-center text-sm"
        >
          Read More
          <!-- Texto del enlace -->
        </RouterLink>
      </div>
    </div>
  </div>
</template>
