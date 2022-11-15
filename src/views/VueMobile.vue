<template>
  <div class="home">
    <v-text-field
    v-model="newNoteTitle"
    @click:append="addNote"
    @keyup.enter = "addNote"
            class="pa-2"
            outlined
            label="Add Notes..."
            append-icon="mdi-plus"
            hide-details
            clearable
          ></v-text-field>
    <v-list class="pt-0" flat>
      <div v-for="note in notes" :key="note.id">
        <v-list-item 
        @click="doneNote(note.id)"
        :class="{ 'yellow accent-1' : note.done }">
          <template v-slot:default>
            <v-list-item-action>
              <v-checkbox :input-value="note.done"></v-checkbox>
            </v-list-item-action>

            <v-list-item-content>
              <v-list-item-title
              :class="{ 'text-decoration-underline' : note.done }"
              >{{ note.title }}</v-list-item-title>
              <v-list-item-subtitle></v-list-item-subtitle>
            </v-list-item-content>
            <v-list-item-action>
          <v-btn 
          @click.stop="deleteNote(note.id)" 
          icon>
            <v-icon color="blue">mdi-delete</v-icon>
          </v-btn>
        </v-list-item-action>
        </template>
        </v-list-item>
        <v-divider></v-divider>
      </div>
    </v-list>
  </div>
</template>

<script>
export default {
  name: "Home",
  data() {
    return {
      newNoteTitle: '',
      notes: [
        {
          id: 1,
          title: "Wake up 2am",
          done: false,
        },
        {
          id: 2,
          title: "Theres nothing to do",
          done: false,
        },
        {
          id: 3,
          title: "Hello world",
          done: false,
        },
        {
          id: 4,
          title: "New task",
          done: false,
        },
      ],
    };
  },
  methods: {
    addNote() {
     let newNote = {
      id: Date.now(),
      title: this.newNoteTitle,
      done: false
     }
     this.notes.push(newNote)
     this.newNoteTitle = ''
    },
    doneNote(id) {
      let note = this.notes.filter((note) => note.id === id)[0];
      note.done = !note.done;
    },
    deleteNote(id) {
      this.notes = this.notes.filter(note => note.id !== id)
    }
  },
};
</script>
