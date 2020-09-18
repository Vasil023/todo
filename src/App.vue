<template>
<div class="wrapper">
    <section>
      <div class="container">
         <NewNote 
         :note="note"
         @addNote="addNote" />
         <Notes :notes="notes" @remove="removeNote" />
      </div>
  <!-- /.container -->
    </section>
</div>
<!-- /.wrapper -->
</template>

<script>
import NewNote from '@/components/NewNote.vue'
import Notes from '@/components/Notes.vue'

export default {
  components: {
    NewNote,
    Notes
  },
  data () {
    return {
      notes: [],
      note: {
        title: ''
      }
    }
  },
  mounted() {
    if (localStorage.getItem('notes')) {
      try {
        this.notes = JSON.parse(localStorage.getItem('notes'));
      } catch(e) {
        localStorage.removeItem('notes')
      }
    }
  },
  methods: {
    addNote () {
      let {title} = this.note
      this.notes.push({
        title
      })
      this.note.title = '';
      this.saveNote();
    },
    removeNote (index) {
      this.notes.splice(index, 1)
      this.saveNote()
    },
    saveNote () {
      const parsed = JSON.stringify(this.notes);
      localStorage.setItem('notes', parsed)
    }
  }
}
</script>

<style>
#app {
  font-family: Avenir, Helvetica, Arial, sans-serif;
  -webkit-font-smoothing: antialiased;
  -moz-osx-font-smoothing: grayscale;
  text-align: center;
  color: #2c3e50;
  margin-top: 60px;
}
</style>
