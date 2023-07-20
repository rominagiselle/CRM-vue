<script setup>
import { onMounted, reactive } from 'vue'
import ClientService from '../services/ClientService'
import { FormKit } from '@formkit/vue'
import { useRouter, useRoute } from 'vue-router';
import RouterLink from '../components/UI/RouterLink.vue'


const router = useRouter()
const route = useRoute()

const { id } = route.params

 const formData = reactive({})

onMounted(() => {
    ClientService.obtenerCliente(id)
    .then(({data}) => {
        Object.assign(formData, data)
    })
    .catch(error => console.log(err))
})

const handleSubmit = (data) => {
    ClientService.actualizarCliente(id, data)
    .then(() => router.push({name: 'listado-clientes'}))
    .catch(error => console.log(error))
}
</script>

<template>
    <div>
        <div class="flex justify-end">
            <RouterLink to="listado-clientes"> Volver</RouterLink>
        </div>
        <h1 class="text-4xl font-extrabold text-slate-500">Editar Cliente</h1>

        <div class="mx-auto mt-10 bg-white shadow">
            <div class="mx-auto md:w-2/3 py-20 px-6">
                <FormKit type="form" submit-label="Editar Cliente" incomplete-message="No se pudo enviar, revise los campos." @submit="handleSubmit" :value="formData">
                    <FormKit type="text" name="nombre" label="Nombre" placeholder="Nombre de cliente" validation="required"
                        :validation-messages="{ required: 'El nombre del cliente es obligatorio.' }"  v-model="formData.nombre"
                        />
                        <FormKit type="text" name="apellido" label="Apellido" placeholder="Apellido de cliente" validation="required"
                        :validation-messages="{ required: 'El apellido del cliente es obligatorio.' }"  v-model="formData.apellido"
                        />
                        <FormKit type="email" name="email"  label="Email" placeholder="Email de cliente" validation="required|email"
                        :validation-messages="{ required: 'El email del cliente es obligatorio.', email: 'Coloca un email valido.' }" v-model="formData.email"
                        />                        
                        <FormKit type="text" name="telefono" label="Telefono" placeholder="Telefono: XXXXXXXXX" validation="?matches:/^[0-9]{9}$/"
                        :validation-messages="{ matches: 'El formato no es valido.' }" v-model="formData.telefono"
                        />                        
                        <FormKit type="text" name="empresa" label="Empresa" placeholder="Empresa del cliente" v-model="formData.empresa"
                        />
                        <FormKit type="text" name="puesto" label="Puesto" placeholder="Puesto del cliente"  v-model="formData.puesto"
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