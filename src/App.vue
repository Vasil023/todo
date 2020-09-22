<template>
<div class="wrapper">
    <section>
      <div class="container">
         <NewNote 
         :note="note"
         @addNote="addNote" />
         <Notes :notes="notes"
          @remove="removeNote"
           />
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
      },
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
      if (!this.note.title) {
              return;
      }
      let {title} = this.note
      this.notes.push({
        title,
        id: Math.floor(Math.random() * 100)
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
    },
  }
}
</script>

