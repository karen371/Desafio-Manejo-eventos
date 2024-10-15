<script>
import { ref } from 'vue';

export default {
    setup() {
        // Declarar los refs
        const nombre = ref('');
        const fecha = ref('');
        const hora = ref('');
        const gravedad = ref('');
        const motivo = ref('');
        const pacientes = ref([]);

        // Función para agregar paciente (aquí se puede añadir la lógica)
        const agregarPaciente = () => {
           // Crear un objeto con los datos del paciente
            const paciente = {
                nombre: nombre.value,
                fecha: fecha.value,
                hora: hora.value,
                gravedad: gravedad.value,
                motivo: motivo.value,
            };
            // Agregar el paciente al array
            pacientes.value.push(paciente);
            console.log(pacientes.value);
            // Limpiar el formulario después de agregar el paciente
            limpiarFormulario();
        };

        // Función para limpiar el formulario
        const limpiarFormulario = () => {
            nombre.value = '';
            fecha.value = '';
            hora.value = '';
            gravedad.value = '';
            motivo.value = '';
        };
        // Computar si el formulario es válido
        const isFormValid = () => {
            return nombre.value && fecha.value && hora.value && gravedad.value && motivo.value;
        };
        return {
            nombre,
            fecha,
            hora,
            gravedad,
            motivo,
            pacientes,
            agregarPaciente,
            limpiarFormulario,
            isFormValid
        };
    },
};
</script>
<template>
    <form @submit.prevent="agregarPaciente" class="d-flex flex-column justify-content-center">
    <div class=" d-flex flex-row justify-content-between">
        <div class="mb-3">
            <label for="" class="form-label" :class="{'text-danger': !nombre}">Paciente</label>
            <input type="text" v-model="nombre" class="form-control"/>
        </div>
        <div class="mb-3">
            <label for="" class="form-label" :class="{'text-danger': !fecha}">Fecha</label>
            <input type="date" v-model="fecha" class="form-control" />
        </div>
        <div class="mb-3">
            <label for="" class="form-label" :class="{'text-danger': !hora}">Hora</label>
            <input type="time" v-model="hora" class="form-control" />
        </div>
        <div class="mb-3">
            <label for="" class="form-label" :class="{'text-danger': !gravedad}">Gravedad</label>
            <select v-model="gravedad" class="form-select">
            <option disabled value="">Por favor seleccione una opción</option>
            <option>Baja</option>
            <option>Media</option>
            <option>Alta</option>
            </select>
        </div>
        <div class="mb-3">
            <label for="" class="form-label" :class="{'text-danger': !motivo}">Motivo</label>
            <input type="text" v-model="motivo" class="form-control" />
        </div>
    </div>
    <div class="d-flex justify-content-center">
        <button type="submit" class="btn btn-primary btn-lg" :disabled="!isFormValid()">Agregar</button>
    </div>
    </form>
</template>

<style scoped>
.empty-input {
    color: red;
}
</style>
