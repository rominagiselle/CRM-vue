<script setup>
import { FormKit } from '@formkit/vue'
import RouterLink from '../components/UI/RouterLink.vue'
</script>

<template>
    <div>
        <div class="flex justify-end">
            <RouterLink to="inicio"> Volver</RouterLink>
        </div>
        <h1 class="text-4xl font-extrabold text-slate-500">Agregar Cliente</h1>

        <div class="mx-auto mt-10 bg-white shadow">
            <div class="mx-auto md:w-2/3 py-20 px-6">
                <FormKit type="form">
                    <FormKit type="text" label="Nombre" placeholder="Nombre de cliente" validation="required"
                        :validation-messages="{ required: 'El nombre del cliente es obligatorio.' }"
                        />

                        <FormKit type="text" label="Apellido" placeholder="Apellido de cliente" validation="required"
                        :validation-messages="{ required: 'El apellido del cliente es obligatorio.' }"
                        />

                        <FormKit type="email" label="Email" placeholder="Email de cliente" validation="required|email"
                        :validation-messages="{ required: 'El email del cliente es obligatorio.', email: 'Coloca un email valido.' }"
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