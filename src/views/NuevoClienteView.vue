<script setup>
    import { FormKit } from '@formkit/vue';
    import { useRouter } from 'vue-router';
    import ClienteService from '@/services/ClienteService';
    import RouterLink  from '../components/UI/RouterLink.vue';
    import Heading from '../components/UI/Heading.vue';

    
    const router = useRouter()

    

    defineProps({
        titulo:{
        type: String
        }
    })

    const handleSubmit= (data) => {
        data.estado = 1
        ClienteService.agregarCliente(data)
            .then(respuesta => {
                console.log(respuesta)
                router.push('/')
            })
            .catch(error => console.log(error))
    }

</script>

<template>
    <div class="min-h-screen bg-gray-300 mb-5">
      <!-- Botón para volver -->
      <div class="flex justify-end p-4">
        <RouterLink
          to="inicio"
          class="px-4 py-2 text-sm font-semibold text-white bg-blue-500 rounded-md shadow hover:bg-blue-600 transition duration-300"
        >
          Volver
        </RouterLink>
      </div>
  
      <!-- Título -->
      <Heading class="text-center text-2xl font-bold text-gray-800">
        {{ titulo }}
      </Heading>
  
      <!-- Contenedor del formulario -->
      <div class="mx-auto mt-10 bg-[rgb(75,101,98)] shadow-lg rounded-lg md:w-2/3">
        <div class="py-10 px-6 md:px-10 text-white">
          <FormKit
            type="form"
            submit-label="Agregar censista"
            incomplete-message="No se pudo enviar, revisa los mensajes"
            @submit="handleSubmit"
            class="space-y-6"
          >
            <!-- Campo Nombre -->
            <FormKit
              type="text"
              label="Nombre"
              name="nombre"
              placeholder="Nombre del censista"
              help="Coloca el nombre del cliente que deseas registrar"
              validation="required"
              :validation-messages="{ required: 'El nombre del censista es obligatorio' }"
            />
        
            <FormKit
            type="password"
            label="Contraseña"
            name="password"
            placeholder="Contraseña"
            help="Introduce una contraseña segura"
            validation="required|min:8"
            :validation-messages="{
                required: 'La contraseña es obligatoria',
                min: 'La contraseña debe tener al menos 8 caracteres'
            }"
            />

            <FormKit
            type="password"
            label="Confirmar Contraseña"
            name="confirm_password"
            placeholder="Confirmar contraseña"
            help="Repite la contraseña para confirmarla"
            validation="required|same:password"
            :validation-messages="{
                required: 'La confirmación de la contraseña es obligatoria',
                same: 'Las contraseñas no coinciden'
            }"
            />

  
            <!-- Campo Email -->
            <FormKit
              type="email"
              label="Email"
              name="email"
              placeholder="Email del censista"
              validation="required|email"
              :validation-messages="{ required: 'El email del censista es obligatorio', email: 'Coloca un email válido' }"
              />
  
            <!-- Campo Rol -->
            <FormKit
              type="text"
              label="Rol"
              name="rol"
              placeholder="Rol del censista"
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
  