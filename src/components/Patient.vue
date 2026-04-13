<script setup>
const props = defineProps({
  id: {
    type: String,
    required: true,
  },
  pet: {
    type: String,
    required: true,
  },
  person: {
    type: String,
    required: true,
  },
  email: {
    type: String,
    required: true,
  },
  dischargedAt: {
    type: String,
    required: true,
  },
  symptoms: {
    type: String,
    required: true,
  },
});
</script>

<template>
  <div class="mx-5 mb-10 bg-white shadow-md px-5 py-10 rounded-xl">
    <p class="font-bold mb-3 text-gray-700 uppercase">
      ID:
      <span class="font-normal normal-case"> {{ id }} </span>
    </p>

    <p class="font-bold mb-3 text-gray-700 uppercase">
      Nombre:
      <span class="font-normal normal-case"> {{ pet }} </span>
    </p>

    <p class="font-bold mb-3 text-gray-700 uppercase">
      Propietario:
      <span class="font-normal normal-case"> {{ person }} </span>
    </p>

    <p class="font-bold mb-3 text-gray-700 uppercase">
      Email:
      <span class="font-normal normal-case"> {{ email }} </span>
    </p>

    <p class="font-bold mb-3 text-gray-700 uppercase">
      Fecha Alta:
      <span class="font-normal normal-case"> {{ dischargedAt }} </span>
    </p>

    <p class="font-bold mb-3 text-gray-700 uppercase">
      Síntomas:
      <span class="font-normal normal-case"> {{ symptoms }} </span>
    </p>

    <div class="grid md:grid-cols-2 gap-5 mt-10">
      <button
        type="button"
        class="block w-full py-2 px-10 bg-indigo-600 hover:bg-indigo-700 text-white font-bold uppercase rounded-lg"
      >
        Editar
      </button>

      <button
        type="button"
        class="block w-full py-2 px-10 bg-red-600 hover:bg-red-700 text-white font-bold uppercase rounded-lg"
      >
        Eliminar
      </button>
    </div>
  </div>
</template>
