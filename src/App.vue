

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
          <th>Eliminar</th>
        </tr>
      </thead>
      <tbody>
        <tr v-for="(item, i) in registros" :key="i" :style="item.priority == 'alta' ? ' background-color:red; color:white' : ' '">
          <td>{{ item.activity }}</td>
          <td>{{ item.priority }}</td>
          <td>{{ item.date }}</td>
          <td>
            <button @click="eliminar(i)" class="eliminar">❌</button>
          </td>
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
function eliminar(i) {
  registros.value.splice(i, 1)
}

</script>

<style>
body {
  height: 120vh;
  display: grid;
  place-items: center;
}
.eliminar{
  width: 40%;
  height: auto;
  margin-left: 25%;
  border-radius: 5px;
  font-size: 120%;
padding: 1%;
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
