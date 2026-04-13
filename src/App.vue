<script setup>
import { ref, reactive } from "vue";
import Form from "./components/Form.vue";
import Header from "./components/Header.vue";
import Patient from "./components/Patient.vue";

const patients = ref([]);
const editingPatient = ref(false);

const formData = reactive({
  pet: "",
  person: "",
  email: "",
  dischargedAt: "",
  symptoms: "",
});

const savePatient = () => {
  if (editingPatient.value) {
    const patientIndex = patients.value.findIndex(
      (patient) => patient.id === formData.id,
    );
    patients.value[patientIndex] = { ...formData };
    editingPatient.value = false;
  } else {
    patients.value.push({ ...formData, id: Date.now().toString() });
  }
  formData.pet = "";
  formData.person = "";
  formData.email = "";
  formData.dischargedAt = "";
  formData.symptoms = "";
};

const editPatient = (id) => {
  const patient = patients.value.find((patient) => patient.id === id);
  Object.assign(formData, patient);
  editingPatient.value = true;
};

const deletePatient = (id) => {
  patients.value = patients.value.filter((patient) => patient.id !== id);
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
        :editingPatient="editingPatient"
        @save-patient="savePatient"
      />
      <div class="md:w-1/2 md:h-full">
        <h2 class="font-black text-3xl text-center">
          Administra tus Pacientes
        </h2>

        <p class="text-lg mt-5 text-center mb-10">
          Información de
          <span class="text-indigo-600 font-bold">los pacientes</span>
        </p>
        <div
          v-if="patients.length > 0"
          class="max-h-171.75 overflow-hidden overflow-y-scroll"
        >
          <Patient
            v-for="patient in patients"
            :id="patient.id"
            :pet="patient.pet"
            :person="patient.person"
            :email="patient.email"
            :dischargedAt="patient.dischargedAt"
            :symptoms="patient.symptoms"
            @edit-patient="editPatient"
            @delete-patient="deletePatient"
          />
        </div>
        <p v-else class="mt-10 text-2xl text-center">No hay pacientes.</p>
      </div>
    </div>
  </div>
</template>
