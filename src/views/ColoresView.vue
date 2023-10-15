<template>
    <v-container fluid>
        <h1 class="text-purple-darken-2">Color</h1>
        <v-row>
            <v-col>
            <v-text-field label="Color" placeholder="Ingresa un color" color="purple" v-model="color"></v-text-field>
            <v-btn prepend-icon="mdi-check" color="purple-darken-2" block @click="agregarColor">Guardar color</v-btn>
            </v-col>
        <v-col>
            <v-card title="Color" color="deep-purple-lighten-4" :text="colorGuardado" v-if="colorGuardado!==''">
                <v-card-actions>
                <v-btn icon="mdi-delete" color="red" @click="eliminarColor"></v-btn>
                </v-card-actions>
            </v-card>
        </v-col>
        </v-row>
    </v-container>
</template>
<script>
export default{
name: 'ColoresView',
    data(){
        return {
    // Esta variable guarda el color que se ingresa en la caja de texto
        color: '',
    // Esta variable guarda el color obtenido del local storage
        colorGuardado: ''
        }
    },
    methods: {
    // Este método agrega los colores al localStorage
        agregarColor(){
    // Agrega un item al local storage
        localStorage.setItem('color', this.color)
    // Invoca al método leerColor
        this.leerColor()
    // Se vacia la variable color
        this.color = ''
    },
    // Este método obtiene el color del localStorage
        leerColor(){
    // Obtiene el item del local storage
        let data = localStorage.getItem('color')
    // Si no es null ses guarda en la variable colorGuardado
        if(data){
            this.colorGuardado = data
        } else {
            this.colorGuardado = ''
        }
    },
    // Este método elimina el color del localStorage
    eliminarColor(){
    // Elimina el item del local storage
        localStorage.removeItem('color')
            this.leerColor()
    }
    },
    created(){
    // Se invoca al método cuando el componente se está
    // creando, para extraer el dato del localStorage
        this.leerColor()
    }
};
</script>

