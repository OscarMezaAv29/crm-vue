<script setup>
import { onMounted } from "vue";
import ClienteService from "../services/ClienteService";
import { FormKit } from "@formkit/vue";
import { useRouter, useRoute } from 'vue-router';
import RouterLink from "../components/Ui/RouterLink.vue";
import Heading from "../components/UI/Heading.vue";

const router = useRouter()
const route = useRoute()

const { id } = route.params

onMounted(() => {
    ClienteService.obtenerCliente(id)
        .then(({data}) => console.log(data))
        .catch(error => console.log(error))
})


defineProps({
  titulo: {
    type: String,
  },
});

const handleSubmit = (data) => {
  
};
</script>

<template>
  <div>
    <div class="flex justify-end">
      <RouterLink to="listado-clientes"> Volver </RouterLink>
    </div>
    <Heading>{{ titulo }}</Heading>
    <div class="mx-auto mt-10 bg-white shadow">
      <div class="mx-auto md:w-2/3 py-20 px-6">
        <FormKit
          type="form"
          submit-label="Agregar Cliente"
          incomplete-message="Uno o más campos obligatorios están vacíos"
          @submit="handleSubmit"
        >
          <FormKit
            type="text"
            label="Nombre"
            name="nombre"
            placeholder="Nombre de Cliente"
            validation="required"
            :validation-messages="{
              required: 'El nombre del cliente es obligatorio',
            }"
          />

          <FormKit
            type="text"
            label="Apellido"
            name="apellido"
            placeholder="Apellido de Cliente"
            validation="required"
            :validation-messages="{
              required: 'El apellido del cliente es obligatorio',
            }"
          />

          <FormKit
            type="text"
            label="Email"
            name="email"
            placeholder="Email de Cliente"
            validation="required|email"
            :validation-messages="{
              required: 'El email del cliente es obligatorio',
              email: 'Ingrese un email válido',
            }"
          />

          <FormKit
            type="text"
            label="Teléfono"
            name="telefono"
            placeholder="Teléfono: XXX-XXX-XXXX"
            validation="*matches:/^[0-9]{3}-[0-9]{3}-[0-9]{4}$/"
            :validation-messages="{ matches: 'El formato no es válido' }"
          />

          <FormKit
            type="text"
            label="Empresa"
            name="empresa"
            placeholder="Empresa de Cliente"
          />

          <FormKit
            type="text"
            label="Puesto"
            name="puesto"
            placeholder="Puesto de Cliente"
          />
        </FormKit>
      </div>
    </div>
  </div>
</template>

<style>
.formkit-wrapper {
  max-width: 100%;
}
</style>
