<template>
  <q-page padding>
        <q-list separator
        bordered>
      <q-separator spaced />
      <q-item  v-for="(task, index) in tasks"
      :key="task.id"
      @click="task.completed=!task.completed"
      class="!task.completed ? 'bg-orange-1' : 'bg-green'"
      clickable
        v-ripple>
        <q-item-section side top>
          <q-checkbox v-model="task.completed" />
        </q-item-section>

        <q-item-section>
          <q-item-label>{{task.name}}</q-item-label>
        </q-item-section>

              <q-item-section
              v-if="task.completed"
              side>
        <q-btn round color="red"
        @click.stop="deleteTask(index)"
        icon="delete" />
      </q-item-section>

      </q-item>
      <q-separator spaced />

    </q-list>
    <div class="row q-pa-sm bg-primary">
      <q-input class="col"
      @keyup.enter="addTask"
      square
      bg-color="white" filled bottom-slots v-model="newTask" label="ADD TASK">
        <template v-slot:before>
        </template>

        <template v-slot:hint>
        </template>

        <template v-slot:append>
          <q-btn @click="addTask" round dense flat icon="add" />
        </template>
      </q-input>
    </div>
    <div class="absolute-center" v-if="!tasks.length">
      <q-icon
      name="check"
      size="100px"
      color="primary" />
      <div class="text-5 text-primary text-center">
        NO Tasks
      </div>

    </div>
  </q-page>
</template>

<script>
export default {
  data () {
    return {
      newTask: '',
      tasks: [
        // {
        //   id: 1,
        //   name: 'krish',
        //   completed: false
        // },
        // {
        //   id: 2,
        //   name: 'pradeep',
        //   completed: false
        // },
        // {
        //   id: 3,
        //   name: 'mukesh',
        //   completed: false
        // }
      ]

    }
  },
  methods: {
    deleteTask (index) {
      this.$q.dialog({
        title: 'Confirm',
        message: 'Would you like to delete the task?',
        cancel: true,
        persistent: true
      }).onOk(() => {
        // console.log('>>>> OK')
        this.tasks.splice(index, 1)
        this.$q.notify('Task Deleted')
      })
    },
    addTask () {
      this.tasks.push(
        {
          name: this.newTask,
          completed: false
        }
      )
      this.newTask = ''
    }
  }
}
</script>
<style>

</style>
