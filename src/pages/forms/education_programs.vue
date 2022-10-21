<template>
  <div>
    <q-card flat>
      <q-card-section style="padding-bottom: 0px">
        <div class="text-h5">Загрузка образовательных программ</div>
      </q-card-section>
      <q-form>
      <q-card-section>
        <div v-for="program in education_programs">
        <hr>


        <div v-if="education_programs.indexOf(program) !== education_programs.length-1">
          <q-checkbox v-model="program.check" label="Изменить"/>
          <q-input outlined :disable="(education_programs.indexOf(program) !== education_programs.length-1 && !program.check)" v-model="program.title" label="Название"></q-input>
          <q-input outlined :disable="(education_programs.indexOf(program) !== education_programs.length-1 && !program.check)" v-model="program.direction" label="Направление"></q-input>
          <q-input outlined :disable="(education_programs.indexOf(program) !== education_programs.length-1 && !program.check)" v-model="program.code_direction" label="Код направления"></q-input>
          <q-input outlined :disable="(education_programs.indexOf(program) !== education_programs.length-1 && !program.check)" v-model="program.start_year" label="Год начала обучения"></q-input>
          <q-input outlined :disable="(education_programs.indexOf(program) !== education_programs.length-1 && !program.check)" v-model="program.end_year" label="Год окончания обучения"></q-input>
        </div>
        <div v-if="education_programs.indexOf(program) === education_programs.length-1">
            <q-input lazy-rules :rules="[ val => val && val.length > 0 || 'Обязательное поле']" v-model="program.title" label="Название"></q-input>
            <q-input lazy-rules :rules="[ val => val && val.length > 0 || 'Обязательное поле']" v-model="program.direction" label="Направление"></q-input>
            <q-input lazy-rules :rules="[ val => val && val.length > 0 || 'Обязательное поле']" v-model="program.code_direction" label="Код направления"></q-input>
            <q-input lazy-rules :rules="[ val => val && val.length > 0 || 'Обязательное поле']" v-model="program.start_year" label="Год начала обучения"></q-input>
            <q-input lazy-rules :rules="[ val => val && val.length > 0 || 'Обязательное поле']" v-model="program.end_year" label="Год окончания обучения"></q-input>
        </div>

        <div class="flex justify-around">
          <q-btn v-if="education_programs.indexOf(program) === education_programs.length-1" round color="primary" icon="add" @click="validate(program)"/>
          <q-btn v-if="education_programs.indexOf(program) === education_programs.length-1 && education_programs.indexOf(program) !== 0" round color="primary" icon="remove" @click="education_programs.splice(education_programs.indexOf(program),1)"/>
        </div>

        </div>
        <div style="padding-top: 20px" >
<!--          <q-btn round color="primary" icon="add" @click="addProgram"/>-->

        </div>

      </q-card-section>
      <q-card-actions>
        <q-btn label="Отправить" type="submit" @click="onSubmit" color="primary" class="full-width text-white"/>
      </q-card-actions>
      </q-form>
    </q-card>
  </div>
</template>

<script>
import {useQuasar} from "quasar";

export default {
  name: "education_programs",
  setup () {
    // const $q = useQuasar()
  },
  data: () => ({
    $q: useQuasar(),
    education_programs: [
      {
        title: null,
        direction: null,
        code_direction: null,
        start_year: null,
        end_year: null,
        check: false
      }
    ]
  }),
  methods: {
    validate(obj){
      if(obj.direction && obj.end_year && obj.start_year && obj.title && obj.code_direction){
        this.addProgram();
      }
      else {
        this.$q.notify({
          type: 'negative',
          icon: 'warning',
          message: 'Обнаружено пустное поле'
        })
      }

    },
    onSubmit () {
      console.log(this.education_programs)
    },
    addProgram(){
      this.education_programs.push({
        title: null,
        direction: null,
        code_direction: null,
        start_year: null,
        end_year: null,
        check: false
      })
    }
  }
}
</script>

<style scoped>

</style>
