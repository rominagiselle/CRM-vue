<script setup>
import ClientService from '../services/ClientService'
import { FormKit } from '@formkit/vue'
import { useRouter } from 'vue-router';
import RouterLink from '../components/UI/RouterLink.vue'


const router = useRouter()

const handleSubmit = (data) => {
    data.estado = 1
    ClientService.agregarCliente(data)
    .then(response => {
        router.push({ name: 'listado-clientes'})
    } )
    .catch(error => console.log(error))
}
</script>

<template>
    <div>
        <div class="flex justify-end">
            <RouterLink to="listado-clientes"> Volver</RouterLink>
        </div>
        <h1 class="text-4xl font-extrabold text-slate-500">Agregar Cliente</h1>

        <div class="mx-auto mt-10 bg-white shadow">
            <div class="mx-auto md:w-2/3 py-20 px-6">
                <FormKit type="form" submit-label="Agregar Cliente" incomplete-message="No se pudo enviar, revise los campos." @submit="handleSubmit">
                    <FormKit type="text" name="nombre" label="Nombre" placeholder="Nombre de cliente" validation="required"
                        :validation-messages="{ required: 'El nombre del cliente es obligatorio.' }"
                        />
                        <FormKit type="text" name="apellido" label="Apellido" placeholder="Apellido de cliente" validation="required"
                        :validation-messages="{ required: 'El apellido del cliente es obligatorio.' }"
                        />
                        <FormKit type="email" name="email"  label="Email" placeholder="Email de cliente" validation="required|email"
                        :validation-messages="{ required: 'El email del cliente es obligatorio.', email: 'Coloca un email valido.' }"
                        />                        
                        <FormKit type="text" name="telefono" label="Telefono" placeholder="Telefono: XXXXXXXXX" validation="?matches:/^[0-9]{9}$/"
                        :validation-messages="{ matches: 'El formato no es valido.' }"
                        />                        
                        <FormKit type="text" name="empresa" label="Empresa" placeholder="Empresa del cliente"
                        />
                        <FormKit type="text" name="puesto" label="Puesto" placeholder="Puesto del cliente"
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