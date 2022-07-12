<template>
  <div class="wrapper">
    <div class="wrapper-content">
      <section>
          <div class="container">
            <h1> {{ title }} </h1>

            <Message v-if="message" :message="message"/>

            <NewNote
            :note="note"
            @addNote="addNote"/>

             <!-- search -->
            <Search
                :value="search"
                placeholder="Find your note"
                @search="search = $event"
            />

            <Notes
            :notes="notesFilter"
            @remove="removeNote"/>

          </div>
      </section>
    </div>
  </div>
</template>

<script>
import Message from '@/components/Message.vue'
import NewNote from './components/NewNote.vue'
import Search from "@/components/Search";
import Notes from './components/Notes.vue'
export default {
  components: {
    Message,
    NewNote,
    Search,
    Notes
},
  data () {
    return {
      title: 'Notes App',
      search: '',
      message: null,
      note: {
          title: '',
          descr: '',
      },
      notes: [
          {
              title: 'First note',
              descr: 'Description for first note',
              date: new Date(Date.now()).toLocaleString()
          },
          {
              title: 'Second note',
              descr: 'Description for second note',
              date: new Date(Date.now()).toLocaleString()
          },
          {
              title: 'Third note',
              descr: 'Description for third note',
              date: new Date(Date.now()).toLocaleString()
          }
      ]
    }
  },
  computed: {
    notesFilter () {
      let array = this.notes,
          search = this.search
      if (!search) return array
      search = search.trim().toLowerCase()
      array = array.filter(function (item) {
        if (item.title.toLowerCase().indexOf(search) !== -1) {
          return item
        }
      })
      return array
    }
  },
  methods: {
    addNote() {
      let {title, descr} = this.note

      if (title === '') {
          this.message = 'Title can`t be blank!!!'
          return false
      }
      this.notes.push({
          title,
          descr,
          date: new Date(Date.now()).toLocaleString()
      })
      this.message = null
      this.note.title = ''
      this.note.descr = ''
    },
    removeNote(index) {
      this.notes.splice(index, 1)
    }
  }
}
</script>

<style>
</style>
