<script setup>
import { reactive } from "vue";
import Alert from "./Alert.vue";

const alert = reactive({
  type: "",
  message: "",
});

const emit = defineEmits([
  "update:pet",
  "update:person",
  "update:email",
  "update:dischargedAt",
  "update:symptoms",
  "save-patient",
]);

const props = defineProps({
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

const sendForm = () => {
  if (Object.values(props).includes("")) {
    alert.message = "Todos los campos son obligatorios";
    alert.type = "error";
    return;
  }

  emit("save-patient");
  alert.message = "Paciente agregado correctamente";
  alert.type = "success";

  setTimeout(() => {
    alert.message = "";
    alert.type = "";
  }, 3000);
};
</script>

<template>
  <div class="md:w-1/2">
    <h2 class="font-black text-3xl text-center">Seguimiento Pacientes</h2>

    <p class="text-lg mt-5 text-center mb-10">
      Añade Pacientes y
      <span class="text-indigo-600 font-bold">Adminístralos</span>
    </p>

    <Alert v-if="alert.message" :message="alert.message" :type="alert.type" />

    <form
      class="bg-white shadow-md rounded-lg py-10 px-5"
      @submit.prevent="sendForm"
    >
      <div class="mb-5">
        <label for="pet" class="block text-gray-700 uppercase font-bold"
          >Nombre mascota</label
        >
        <input
          id="pet"
          type="text"
          placeholder="Nombre de la mascota"
          class="border-2 border-gray-300 w-full p-2 mt-2 placeholder-gray-400 rounded-md"
          :value="pet"
          @input="$emit('update:pet', $event.target.value)"
        />
      </div>

      <div class="mb-5">
        <label for="person" class="block text-gray-700 uppercase font-bold"
          >Nombre dueño</label
        >
        <input
          id="person"
          type="text"
          placeholder="Nombre del dueño"
          class="border-2 border-gray-300 w-full p-2 mt-2 placeholder-gray-400 rounded-md"
          :value="person"
          @input="$emit('update:person', $event.target.value)"
        />
      </div>

      <div class="mb-5">
        <label for="email" class="block text-gray-700 uppercase font-bold"
          >Correo electrónico</label
        >
        <input
          id="email"
          type="text"
          placeholder="Correo electrónico"
          class="border-2 border-gray-300 w-full p-2 mt-2 placeholder-gray-400 rounded-md"
          :value="email"
          @input="$emit('update:email', $event.target.value)"
        />
      </div>

      <div class="mb-5">
        <label
          for="dischargedAt"
          class="block text-gray-700 uppercase font-bold"
          >Fecha de alta</label
        >
        <input
          id="dischargedAt"
          type="date"
          class="border-2 border-gray-300 w-full p-2 mt-2 placeholder-gray-400 rounded-md"
          :value="dischargedAt"
          @input="$emit('update:dischargedAt', $event.target.value)"
        />
      </div>

      <div class="mb-5">
        <label for="symptoms" class="block text-gray-700 uppercase font-bold"
          >Síntomas</label
        >
        <textarea
          id="symptoms"
          placeholder="Describe los síntomas del paciente"
          class="h-30 border-2 border-gray-300 w-full p-2 mt-2 placeholder-gray-400 rounded-md"
          :value="symptoms"
          @input="$emit('update:symptoms', $event.target.value)"
        ></textarea>
      </div>

      <input
        type="submit"
        class="bg-indigo-600 w-full p-3 text-white uppercase font-bold hover:bg-indigo-700 cursor-pointer transition-colors"
        value="Registrar Paciente"
      />
    </form>
  </div>
</template>
