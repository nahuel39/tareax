<template>
  <q-page class="bg-grey-3 column">
    <div class="row q-pa-sm bg-primary">
      <q-input
        v-model="nuevaTarea"
        @keyup.enter="sumarTarea" 
        class="col" 
        square
        filled
        bg-color="white"
        placeholder="Añadir tarea" 
        dense>
        <template v-slot:append>
          <q-btn
          @click="sumarTarea" 
          round 
          dense 
          flat 
          icon="add" />
        </template>
      </q-input>
    </div>
    <q-list class="bg-white">
      <q-item 
        v-for="(task, index) in tasks"
        :key="task.title"
        @click="task.done = !task.done"
        :class="{ 'done bg-green-1' : task.done}"
        clickable
        v-ripple>
        <q-item-section avatar>
          <q-checkbox 
            v-model="task.done" 
            class="no-pointer-events"
            color="primary"/>
        </q-item-section>
        <q-item-section>
          <q-item-label>{{task.title}}</q-item-label>
        </q-item-section>
        <q-item-section
          v-if="task.done"
          side>
          <q-btn 
            @click.stop="deleteTask(index)"
            flat 
            round 
            dense
            color="primary" 
            icon="delete" />
        </q-item-section>
      </q-item>
    </q-list>
  </q-page>
</template>

<script>
export default {
  data(){
    return{
      nuevaTarea: '',
      tasks: []
    }
  },
  methods: {
    deleteTask(index){
      this.$q.dialog({
        title: '¡Atención!',
        message: '¿Desea eliminar esta tarea?',
        cancel: true,
        persistent: true
      }).onOk(() => {
        this.tasks.splice(index, 1)
        this.$q.notify('Tarea borrada')
      })
    },
    sumarTarea(){
        this.tasks.push({
          title: this.nuevaTarea,
          done: false
        })
        this.nuevaTarea = ''
    }
  }
}
</script>

<style lang="scss">
  .no-tasks{
    opacity: 0.5;
  }
</style>