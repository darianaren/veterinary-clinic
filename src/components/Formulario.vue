<script setup>
import { reactive } from "vue";
import Alert from "./Alert.vue";

const alert = reactive({
  type: "",
  message: "",
});

const formData = reactive({
  pet: "",
  person: "",
  email: "",
  dischargedAt: "",
  symptoms: "",
});

const sendForm = () => {
  if (Object.values(formData).includes("")) {
    alert.message = "Todos los campos son obligatorios";
    alert.type = "error";
    return;
  }
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
      class="bg-white shadow-md rounded-lg py-10 px-5 mb-10"
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
          v-model="formData.pet"
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
          v-model="formData.person"
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
          v-model="formData.email"
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
          v-model="formData.dischargedAt"
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
          v-model="formData.symptoms"
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
