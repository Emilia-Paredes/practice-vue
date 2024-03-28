<template>
  <section>
    <h3>Añadir Profesor</h3>
    <div><label>Nombre:</label><input type="text" v-model="teacher.teacherName"></div>
    <div><label>Apellido:</label><input type="text" v-model="teacher.surname"></div>
    <div><label>DNI:</label><input type="text" v-model="teacher.dni"></div>
    <div><label>Materias:</label><input type="text" v-model="subject"><button @click="handlerSubject()">Agregar</button>
    </div>
    <div>
      <ul>
        <li v-for="(subj, index) in teacher.subjects" :key="index">{{ subj }}</li>
      </ul>
    </div>
    <input type="checkbox" v-model="teacher.doc" />Documentacion entregada
    <button @click="handerlAddTeacher()">Agregar</button>
  </section>

  <section>
    <h3>Listado de profesores:</h3>
    <table>
      <tr>
        <th>Nombre</th>
        <th>Apellido</th>
        <th>DNI</th>
        <th>Materias</th>
        <th>Documentacion Entregada</th>
      </tr>
      <tr v-for="elem in teachers" :key="elem.dni">
        <th>{{ elem.teacherName }}</th>
        <th>{{ elem.surname }}</th>
        <th>{{ elem.dni }}</th>
        <th>
          <ul>
            <li v-for="(item, index) in elem.subjects" :key="index">{{ item }}</li>
          </ul>
        </th>
        <th v-if="elem.doc">Entregada</th>
        <th v-else>No Entregada</th>
      </tr>
    </table>
  </section>
</template>

<script lang="ts" setup>
import { Ref, ref } from 'vue';

interface ITeacher {
  teacherName: string,
  surname: string,
  dni: string,
  subjects: Array<string>,
  doc: boolean
}

let teacher: Ref<ITeacher> = ref({
  teacherName: '',
  surname: '',
  dni: '',
  subjects: [],
  doc: false
})

let teachers: Ref<Array<ITeacher>> = ref([])

let subject: Ref<string> = ref('')

// insercion de subject dentro de obj.teacher
const handlerSubject = () => {
  teacher.value.subjects.push(subject.value)
  subject.value = ''
}

const handerlAddTeacher = () => {
  teachers.value.push({
    teacherName: teacher.value.teacherName,
    surname: teacher.value.surname,
    dni: teacher.value.dni,
    subjects: teacher.value.subjects,
    doc: teacher.value.doc
  })

  teacher.value.teacherName = ""
  teacher.value.surname = ""
  teacher.value.dni = ""
  teacher.value.subjects = []
  teacher.value.doc = false
}

</script>

<style scoped></style>
