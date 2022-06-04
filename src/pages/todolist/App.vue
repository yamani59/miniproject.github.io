<script setup>
import { ref } from "vue"

const input = ref('')
const todos = ref([])

//custom directive
const vFocus = {
  mounted: el => el.focus()
}

// methods
const addList = () => {
  todos.value.unshift({ text: input.value, update: false, id: todos.value.length })
  input.value = ''
};

const deleteList = (id) => {
  todos.value = todos.value.filter(todo => todo.id != id)
}
</script>

<template>
  <div id="Todolist">
    <v-card evalation="20" class="pa-6 w-50 text-center mb-8 mt-10"><h1>TODOLIST</h1></v-card>
    <v-card evalation="20" class="pa-6 w-50 h-50 ">
      <v-text-field label="todo" variant="underlined" v-model="input" @keyup.enter="addList"></v-text-field>
      <div class="list">
      <TransitionGroup name="list">
        <v-banner v-for="(list) in todos" :key="list.id" lines="one" class="bg-red-lighten-1 mb-3">
          <v-banner-text v-if="list.update">
            <v-text-field v-model="list.text" v-focus @keyup.enter="list.update = false" variant="underlined"></v-text-field>
          </v-banner-text>
          <v-banner-text v-else @click.prevent="list.update = true">{{ list.text }}</v-banner-text>
          <v-banner-actions>
            <v-btn @click="deleteList(list.id)">hapus</v-btn>
          </v-banner-actions>
        </v-banner>
      </TransitionGroup>
    </div>
    </v-card>
  </div>
</template>