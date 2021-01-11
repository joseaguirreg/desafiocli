<template>
  <section>
      <h3 class="mb-2">{{ title }}</h3>
      <v-card
        v-for="(todo, index) in trash"
        :key="`${title}${index}`"
        class="px-8 mb-4 rounded-pill"
      >
        <v-card-text class="d-flex align-center">
          <span>
            {{ todo.title }}
          </span>
          <v-spacer />
          <slot name="buttons" :index="index"></slot>
          <!-- <v-btn color="primary" icon @click="restoreTodo(index)">
            <v-icon>mdi-delete-restore</v-icon>
          </v-btn>
          <v-btn color="error" icon @click="deleteForever(index)">
            <v-icon>mdi-delete-forever</v-icon>
          </v-btn> -->
        </v-card-text>
      </v-card>
    </section>
</template>

<script>
export default {
    props: {
        todos: {
            type: Array(),
            required: true
        },
        title: {
            type: String,
            default: "Completadas"
        }
    }
}
</script>

<style>

</style>