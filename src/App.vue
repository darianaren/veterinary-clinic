<script setup>
import { ref, reactive } from "vue";
import Form from "./components/Form.vue";
import Header from "./components/Header.vue";

const patients = ref([]);

const formData = reactive({
  pet: "",
  person: "",
  email: "",
  dischargedAt: "",
  symptoms: "",
});

const savePatient = () => {
  patients.value.push({ ...formData });
  formData.pet = "";
  formData.person = "";
  formData.email = "";
  formData.dischargedAt = "";
  formData.symptoms = "";
};
</script>

<template>
  <div class="container mx-auto my-20">
    <Header />
    <div class="mt-12 md:flex">
      <Form
        v-model:pet="formData.pet"
        v-model:person="formData.person"
        v-model:email="formData.email"
        v-model:dischargedAt="formData.dischargedAt"
        v-model:symptoms="formData.symptoms"
        @save-patient="savePatient"
      />
      <div class="md:w-1/2 md:h-screen overflow-y-scroll">
        <h3 class="font-black text-3xl text-center">
          Administra tus Pacientes
        </h3>

        <div v-if="patients.length > 0"></div>
        <p v-else class="mt-10 text-2xl text-center">No hay pacientes.</p>
      </div>
    </div>
  </div>
</template>
