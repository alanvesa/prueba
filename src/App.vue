

<template>
  <div class="Principal">
    <div class="detalles">
      <h1 class="titulo">Agenda</h1>
      <div class="contenedor_dentro">
        <div class="cont_doc">
          <label for="activity">Actividad</label>
          <input type="text" class="form" name="activity" id="activity" placeholder="Ingrese su tarea" v-model="activity" />
        </div>
       
        <label>
        <p>Prioridad </p>
        <label>
          <input type="radio" v-model="check" name="check" value="alta">Alta
        </label>
        <label>
          <input type="radio" v-model="check" name="check" value="baja">Baja
        </label>

      </label>
        <label for="">Fecha</label>
        <input type="date" class="boton" name="date_register" id="date_register" placeholder="Fecha de la tarea"
          v-model="date" />
        <button @click="agregar()" class="add">✅</button>
        <button @click="ordenar()" class="ordenar">Ordenar</button>
      </div>
    </div>

    <table>
      <thead>
        <tr>
          <th>Actividad</th>
          <th>Prioridad</th>
          <th>Fecha</th>
        </tr>
      </thead>
      <tbody>
        <tr v-for="(item, i) in registros" :key="i" :style="item.priority == 'alta' ? ' background-color:red; color:white' : ' '">
          <td>{{ item.activity }}</td>
          <td>{{ item.priority }}</td>
          <td>{{ item.date }}</td>
        </tr>
      </tbody>
    </table>
    <div class="alerta"><h3 :style="alerta === 'Tarea agregada correctamente' ? 'color:green' : 'color:red'">
      {{ alerta }}
    </h3></div>
  </div>
</template>

<script setup>
import { ref } from "vue";

const registros = ref([]);
const activity = ref("");
const check = ref("");
const date = ref("");
const alerta = ref("");

const ocultarAlerta = () => {
  setTimeout(() => {
    alerta.value = "";
  }, 3500);
};

const agregar = () => {
  if (activity.value === "") {
    alerta.value = "Ingrese una actividad";
    ocultarAlerta();
  } else if (date.value === "") {
    alerta.value = "Ingrese una fecha";
    ocultarAlerta();
  } else {
    alerta.value = "Tarea agregada correctamente";
    ocultarAlerta();
    registros.value.push({
      activity: activity.value,
      priority: check.value,
      date: date.value,
    });
    limpiar();
    console.log(registros.value);
  }

};


function limpiar() {
    activity.value = "";
    check.value = "";
    date.value = "";
  }

function ordenar() {
    registros.value.sort((a, b) => {
    if (a.priority === b.priority) {
      return new Date(a.date) - new Date(b.date);
    }
    return a.priority === 'alta' ? -1 : 1;
  });
}

</script>

<style>
body {
  height: 120vh;
  display: grid;
  place-items: center;
}


input{
  padding: 17px 25px;
  margin-bottom: 20px;
  background-color: #E6E6E6;
  border: 3px solid #f0faf1;
  color: #362928;
  outline: none;
}

label{
  color: #3D3D3D;
  font-size: 15px;
  font-weight: 600;
  margin-bottom: 30px;
}

.Principal {
  border: solid 4px gray;
  width: 1020px;
  height: 520px;
  display: flex;
  flex-direction: column;
  color: rgb(20, 20, 21)
}

button{
  border: none;
  font-size: 15px;
  margin-left: 20px;

}
.cont_doc{
  display: flex;
}

.contenedor_dentro {
  display: flex;
  flex-direction: row;
  margin: 20px;
}

.add{
  background: green;
  color: white;
height: 70px;
width: 50px;
font-size: 30px;
}

.alerta{
  text-align: center;
}

.titulo{
  text-align: center;
}
</style>

<!-- <template>
  <div id="padre">
    <h1>{{ parseInt(num) / parseInt(num2==0?1:num2) }}</h1>
    <input type="text" placeholder="Telefono..." v-model.trim="num">
    <input type="text" placeholder="Telefono..." v-model="num2"> --> -->

   <!--  <h1>{{ contador }}</h1>
    <button @click="contar()">Cambiar</button>
    <h2 v-if="contador<21">Hola soy el msj q van a desaparecer</h2>
    <h2 v-else>hola yo voy aparecer</h2>
    <h2 > {{contador<21?"Hola soy el msj q van a desaparecer":"hola yo voy aparecer"}}</h2> -->

    <!-- <h3 :style="alerta==='Formulario enviado correctamente'?'color:green':''">{{ alerta }}</h3>
    <h1>Formulario</h1>
    <form>
      <label for="nombre">Nombre:</label>
      <input type="text" id="nombre" name="nombre" v-model="nombre">
      <label for="apellidos">Apellidos:</label>
      <input type="text" id="apellidos" name="apellidos" v-model="apellidos">
      <label for="tipo_documento">Tipo documento:</label>
      <select id="tipo_documento" name="tipo_documento" v-model="tipo_documento">
        <option value="cedula">Cédula</option>
        <option value="tarjeta_identidad">Tarjeta de identidad</option>
        <option value="pasaporte">Pasaporte</option>
      </select>
      <label for="numero_documento">Número de documento:</label>
      <input type="text" id="numero_documento" name="numero_documento" v-model="numero_documento">
      <label for="genero">Genero:</label>
      <select id="genero" name="genero" v-model="genero">
        <option value="masculino">Masculino</option>
        <option value="femenino">Femenino</option>
        <option value="otro">Otro</option>
      </select>
      <label for="correo">Correo:</label>
      <input type="email" id="correo" name="correo" v-model="correo">
      <label for="telefono">Teléfono:</label>
      <input type="text" id="telefono" name="telefono" v-model="telefono">
      <label for="fecha_nacimiento">Fecha de nacimiento:</label>
      <input type="date" id="fecha_nacimiento" name="fecha_nacimiento" v-model="fecha_nacimiento">
      <label for="telefono">Edad:</label>
      <input type="number" id="telefono" name="telefono" v-model="edad1">
    </form>
    <button @click="validar()">enviar</button>

    <table>
      <thead>
        <tr>
          <th>Nombre</th>
          <th>Apellido</th>
          <th>Tipo de documento</th>
          <th>Numero de documento</th>
          <th>Telefono</th>
          <th>Correo</th>
          <th>Genero</th>
          <th>Fecha de nacimiento</th>
          <th>edad</th>
          <th>Opciones</th>
        </tr>
      </thead>
      <tbody>
        <tr v-for="(item, i) in registros" :key="i" :style="item.edad>17?'color:pink':'color:purple'">
          <td>{{ item.nombre }}</td>
          <td>{{ item.apellidos }}</td>
          <td>{{ item.tipo_documento }}</td>
          <td>{{ item.numero_documento }}</td>
          <td>{{ item.telefono }}</td>
          <td>{{ item.correo }}</td>
          <td>{{ item.genero }}</td>
          <td>{{ item.fecha_nacimiento }}</td>
          <td>{{ item.edad }}</td>
          <td>
            <button @click="eliminar(i)">❌</button>
            <button @click="editar(item, i)">📝</button>
          </td>
        </tr>

      </tbody>

    </table> 

    <!-- <img :src="image" alt="" :style="{borderRadius:num}"> -->
    <!-- <h1 :style="{borderRadius:12}">hola a todos</h1> -->
    <!-- <h1 :style="num>18?'color:salmon':'color:green'">mi edad es {{ num }}</h1> -->

  <!-- </div> -->
<!-- </template>

<script setup>
import {ref} from "vue"
let num = ref(19)
let color = ref("yellow")
let image = ref("https://adrianalonso.es/wp-content/uploads/2018/01/vue.jpg")

let bd=true

const registros = ref([{
  nombre: "jose",
  apellidos: "HOla",
  tipo_documento: "CC",
  numero_documento:"123123123",
  telefono: "123123213",
  correo: "asdas",
  genero: "m",
  fecha_nacimiento: "12312",
  edad: "12"
},
{
  nombre: "jmiguel",
  apellidos: "HOla",
  tipo_documento: "CC",
  numero_documento: "123123123",
  telefono: "123123213",
  correo: "asdas",
  genero: "m",
  fecha_nacimiento: "12312",
  edad: "12"
},
{
  nombre: "cvcijiase",
  apellidos: "HOla",
  tipo_documento: "CC",
  numero_documento: "123123123",
  telefono: "123123213",
  correo: "asdas",
  genero: "m",
  fecha_nacimiento: "12312",
  edad: "12"
},
{
  nombre: "jadasdnsae",
  apellidos: "HOla",
  tipo_documento: "CC",
  numero_documento: "123123123",
  telefono: "123123213",
  correo: "asdas",
  genero: "m",
  fecha_nacimiento: "12312",
  edad: "12"
}])

const nombre = ref("")
const apellidos = ref("")
const tipo_documento = ref("")
const numero_documento = ref("")
const genero = ref("")
const correo = ref("")
const telefono = ref("")
const fecha_nacimiento = ref("")
const edad1 = ref(0)
let alerta = ref("")
let index = null

function eliminar(i){
  registros.value.splice(i,1)
}

function editar(item, i){
  console.log(item);
  console.log(i);
  nombre.value = item.nombre
  apellidos.value = item.apellidos
bd = false
index=i

}

function ocultarAlerta() {
  setTimeout(() => {
  alerta.value = "";
}, 3500)
}


const validar = () => {
  if (bd==true){
    if (nombre.value === "") {
    alerta.value = "El campo nombre no puede estar vacio" -->
    <!-- ocultarAlerta()
  }
  else if (apellidos.value === "") {
    alerta.value = "El campo apellidos no puede estar vacio"
    ocultarAlerta()
  }
  else if (tipo_documento.value === "") {
    alerta.value = "El campo tipo de documento no puede estar vacio"
    ocultarAlerta()
  }
  else if (numero_documento.value === "") {
    alerta.value = "El campo número de documento no puede estar vacio"
    ocultarAlerta()
  }
  else if (isNaN(numero_documento.value)) {
    alerta.value = "El campo número de documento solo puede contener números"
    ocultarAlerta()
  }
  else if (genero.value === "") {
    alerta.value = "El campo genero no puede estar vacio"
    ocultarAlerta()
  }
  else if (correo.value === "") {
    alerta.value = "El campo correo no puede estar vacio"
    ocultarAlerta()
  }
  else if (!correo.value.includes("@")) {
    alerta.value = "El campo correo debe ser un correo valido"
    ocultarAlerta()
  }
  else if (telefono.value === "") {
    alerta.value = "El campo teléfono no puede estar vacio"
    ocultarAlerta()
  }
  else if (telefono.value.length < 10) {
    alerta.value = "El campo teléfono debe tener al menos 10 números"
    ocultarAlerta()
  }
  else if (fecha_nacimiento.value === "") {
    alerta.value = "El campo fecha de nacimiento no puede estar vacio"
    ocultarAlerta()
  }
  else {
    const fecha = new Date();
    const fechaActual = fecha.toISOString().split('T')[0];
    let edad = fechaActual.split("-")[0] - fecha_nacimiento.value.split("-")[0];
    if (fechaActual.split("-")[1] < fecha_nacimiento.value.split("-")[1]) {
      edad--;
    }
    if (edad < 18) {
      alerta.value = "Debe ser mayor de 18 años para registrarse";
      ocultarAlerta()
    } else {
      alerta.value = "Formulario enviado correctamente"
      ocultarAlerta()
      registros.value.push({
        nombre: nombre.value,
        apellidos: apellidos.value,
        tipo_documento: tipo_documento.value,
        numero_documento: numero_documento.value,
        genero: genero.value,
        correo: correo.value,
        telefono: telefono.value,
        fecha_nacimiento: fecha_nacimiento.value,
        edad:edad1.value
      })
      console.log(registros.value)
    }
  }
  } else {
registros.value [index].nombre= nombre.value
registros.value [index].apellidos= apellidos.value
bd=true
  }
  
} 





/* let contador=ref(0)
function contar(){
  contador.value+=1
} */


/* let num =ref(0)
let num2 =ref(0)
let telefono = ref("312446579")
telefono.value="345"
let nombre = ref("Contreras")
nombre.value = telefono.value */

</script>

<style scoped>
h3 {
  color: red;
}

#padre {
  display: flex;
  flex-direction: column;
  align-items: center;
  justify-content: space-between;
  width: 100%;
  padding: 10px;
}

th, tr, td{
  border: 2px solid blue;
}

form {
  display: flex;
  flex-direction: column;
  align-items: center;
  justify-content: space-between;
  width: 80%;
  margin-bottom: 20px;
  background-color: #5a007d;
  padding: 10px;
}

input{
  width: 100%;
}

select {
  width: 100%;
  padding: 2px;
} 
</style> -->