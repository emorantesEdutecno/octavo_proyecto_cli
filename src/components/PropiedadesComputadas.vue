<template>
    <div id="PropiedadesComputadas">
        <h2>Componente Propiedades Computadas</h2>

        <h3 id="tituloProp">{{  titulo  }}</h3>
        <p id="parrafoProp">{{  parrafo }}</p>
        <hr>
        <h3>{{  mensaje  }}</h3>
        <p>{{  mensaje  }}</p>
        <input type="text" v-bind:value="mensaje">
        <button v-on:click="saludar">Saluda</button>
        <hr>
        <input type="text" v-model="datosAEnviar">
        <button @:click="enviar">Enviar datos al padre</button>
        <hr>
        <p>Propiedades del modelo de datos mediante interpolacion</p>
        <p>{{  nombre }}</p>
        <p>{{  apellido }}</p>
        <label for="txtNombre">Nombre:</label>
        <input type="text" id="txtNombre" v-model="nombre"><br>
        <label for="txtApellido">Apellido:</label>
        <input type="text" id="txtApellido" v-model="apellido"><br>
        <hr>
        <p>Propiedad Computada</p>
        <p> {{  getFullName }}</p>
        <hr>
            <div id="seccionProductos">
                <h1>Cantidad de Productos: {{  getQuantity }}</h1>
                    <ul>
                        <li v-for="(producto,index) in productos" v-bind:key="index">{{ producto.name }} - {{ producto.price }}</li>
                    </ul>
                <h2>Precio Total de los Productos: {{ getTotal }}</h2>
            </div>
            <div id="seccionIngreso">
                <label for="txtIdIngresado">Ingrese Id:</label>
                <input type="text" id="txtIdIngresado" v-model="form.id"><br>
                <label for="txtNombreIngresado">Ingrese Nombre:</label>
                <input type="text" id="txtNombreIngresado" v-model="form.name"><br>
                <label for="txtPrecioIngresado">Ingrese Precio:</label>
                <input type="text" id="txtPrecioIngresado" v-model="form.price" ><br>
                <input type="submit" value="Enviar" v-on:click.prevent="guardarRefresco">
            </div>
        <hr>
        <p>Datos del form</p>
        <p>id: {{  form.id }}</p>
        <p>nombre: {{  form.name }}</p>
        <p>precio: {{  form.price }}</p>
    </div>
</template>

<script>
export default{
    name:'PropiedadesComputadas',
    props:{
        titulo:{
            type: String,
            required: true,
        },
        parrafo:{
            type: String,
            required: false,
        },
    },
    data: function(){
        return{
            mensaje: '',
            datosAEnviar: '',
            nombre: 'Alejandro',
            apellido: 'Perez',
            productos:[
                {id:1, name:'Coca Cola', price:1000},
                {id:2, name:'Pesi Cola', price:1000},
                {id:3, name:'Sprite', price: 1000},
                {id:4, name:'Fanta', price: 1100}
            ],
            form:{
                id:'',
                name:'',
                price:0,
            },
        }
    },
    methods:{
        saludar: function(){
            this.mensaje = 'Hola Mundo !!!';
        },
        enviar: function(){
            this.$emit('eventoEmitidoPorElHijo', this.datosAEnviar );
        },
        guardarRefresco:function(){
            //cambiamos a numero el price del modelo de datos
            this.form.price = Number(this.form.price);
            this.productos.push(this.form);
            // limpiamos para proxima insercion
            this.form.id='';
            this.form.name='';
            this.form.price='';
        },
    },
    computed:{
        getFullName: function(){
            return this.nombre.toUpperCase() + " "+this.apellido.toUpperCase();
        },
        getQuantity: function(){
            return this.productos.length;
        },
        getTotal: function(){
            let total = this.productos.reduce((acumulador, producto)=>{
                return acumulador+producto.price;
            }, 0);
            return total;
        }, 
    }

}
</script>


<style scoped>
    #PropiedadesComputadas{
        background-color: aquamarine;
        color: blue;
    }

    #tituloProp{
        color: brown;
    }
    #parrafoProp{
        color:darkred;
    }
    #seccionProductos{
        margin: 2%;
        background-color:greenyellow;
        text-align: justify;
    }

    #seccionIngreso{
        margin: 2%;
        background-color:lightskyblue;
        text-align: right;
    }
</style>