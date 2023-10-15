<template>
    <v-container fluid>
        <h1 class="text-purple-darken-2">Estudiante</h1>
        <v-row>
            <v-col cols="4">
                <v-text-field
                label="Nombre"
                placeholder="Escriba su nombre"
                color="purple"
                clearable
                v-model="nombre"></v-text-field>
                <v-text-field
                label="Edad"
                placeholder="Escriba su edad"
                color="purple"
                clearabletype="number"
                v-model="edad"></v-text-field>
                <v-btn block color="purple-darken-2" prepend-icon="mdi-check" @click="guardar">Guardar</v-btn>
            </v-col>
            <v-col>
                <v-card title="Equipo">
                     <v-card-text>
                    <v-btn color="red" append-icon="mdi-delete-forever" size="small" @click="eliminarTodo">Borrar todo</v-btn>
                        <v-table>
                            <thead>
                            <tr>
                                <th>Nombre</th>
                                <th>Edad</th>
                                <th>Acciones</th>
                            </tr>
                            </thead>
                            <tbody>
                                <tr v-for="(persona, i) in equipo" :key="i">
                                    <td>{{ persona.nombre }}</td>
                                    <td>{{ persona.edad }}</td>
                                    <td>
                                <v-btn icon="mdi-delete" color="red" size="x-small" @click="eliminar(i)">
                                </v-btn>
                                    </td>
                                    </tr>
                                <!-- Se mostrará si el arreglo está vacío -->
                                <tr v-if="equipo.length === 0">
                                <td colspan="3">No hay estudiantes</td></tr>                        
                            </tbody>
                        </v-table>
                    </v-card-text>
                </v-card>
            </v-col>
        </v-row>
    </v-container>
</template>
<script>
export default{
    name: 'PersonaView',
    data(){
        return {
        // Estas variables guardarán los datos del formulario
            nombre: '',
            edad: 0,
            // Este arreglo guardará a todos los estudiantes
            equipo: []
        }
    },
    methods: {
    // Este método guarda el arreglo equipo al localStorage
        guardar(){
            let persona = { 'nombre': this.nombre, 'edad': this.edad }
            // Se agrega el objeto persona al arreglo
            this.equipo.push(persona)
        // Se guarda el arreglo al local Storage
        localStorage.setItem('equipo', JSON.stringify(this.equipo))
            // Se limpian las variables del formulario
            this.nombre = ''
            this.edad = 0
        },
        // Este método obtiene el arreglo equipo del localStorage
        leer(){
            let data = JSON.parse(localStorage.getItem('equipo'))
            if(data){
            this.equipo = data
            }
        },
        // Este método elimina al estudiante
        eliminar(i){
            // Elimina al estudiante del arreglo
            this.equipo.splice(i,1)// Actualiza el elemento en el localStoraga
            localStorage.setItem('equipo', JSON.stringify(this.equipo))
        },
        // Este método elimina a todo el equipo del localStorage
        eliminarTodo(){
            localStorage.removeItem('equipo')
            this.equipo = []
        }
    },
    // Se invoca al método cuando el componente se está
    // creando para extraer los datos del localStorage
    created(){
        this.leer()
    }
};
</script>