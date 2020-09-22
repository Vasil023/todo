<template>
	<div class="notes">
			<div class="note" v-for="(note, index) in notes" :key="note.id" @click="doneTask(note.id)" >
				<div class="note-title" style="cursor: pointer;" @click="toggle">
					<span>
						{{note.title}}
					</span>
				</div>
				<!-- /.note-title -->
					<div class="delite">
						<p style="cursor: pointer;" @click="removeNote(index)" >
          <svg height="20pt" viewBox="0 0 512 512" width="20pt" xmlns="http://www.w3.org/2000/svg"><path d="m256 0c-141.164062 0-256 114.835938-256 256s114.835938 256 256 256 256-114.835938 256-256-114.835938-256-256-256zm0 0" fill="#f44336"/><path d="m350.273438 320.105469c8.339843 8.34375 8.339843 21.824219 0 30.167969-4.160157 4.160156-9.621094 6.25-15.085938 6.25-5.460938 0-10.921875-2.089844-15.082031-6.25l-64.105469-64.109376-64.105469 64.109376c-4.160156 4.160156-9.621093 6.25-15.082031 6.25-5.464844 0-10.925781-2.089844-15.085938-6.25-8.339843-8.34375-8.339843-21.824219 0-30.167969l64.109376-64.105469-64.109376-64.105469c-8.339843-8.34375-8.339843-21.824219 0-30.167969 8.34375-8.339843 21.824219-8.339843 30.167969 0l64.105469 64.109376 64.105469-64.109376c8.34375-8.339843 21.824219-8.339843 30.167969 0 8.339843 8.34375 8.339843 21.824219 0 30.167969l-64.109376 64.105469zm0 0" fill="#fafafa"/></svg>
            </p>
					</div>
					<!-- /.delite -->
			</div>
			<!-- /.note -->
      <div class="done-notes" v-for="(not, index) in todo" :key="'not'+index">
        <div class="note-title text">
           <span>
          {{not}}
        </span>
        </div>
        <!-- /.note-title -->
        	<div class="delite">
						<p style="cursor: pointer;" @click="removeNote(index)" >
          <svg height="20pt" viewBox="0 0 512 512" width="20pt" xmlns="http://www.w3.org/2000/svg"><path d="m256 0c-141.164062 0-256 114.835938-256 256s114.835938 256 256 256 256-114.835938 256-256-114.835938-256-256-256zm0 0" fill="#f44336"/><path d="m350.273438 320.105469c8.339843 8.34375 8.339843 21.824219 0 30.167969-4.160157 4.160156-9.621094 6.25-15.085938 6.25-5.460938 0-10.921875-2.089844-15.082031-6.25l-64.105469-64.109376-64.105469 64.109376c-4.160156 4.160156-9.621093 6.25-15.082031 6.25-5.464844 0-10.925781-2.089844-15.085938-6.25-8.339843-8.34375-8.339843-21.824219 0-30.167969l64.109376-64.105469-64.109376-64.105469c-8.339843-8.34375-8.339843-21.824219 0-30.167969 8.34375-8.339843 21.824219-8.339843 30.167969 0l64.105469 64.109376 64.105469-64.109376c8.34375-8.339843 21.824219-8.339843 30.167969 0 8.339843 8.34375 8.339843 21.824219 0 30.167969l-64.109376 64.105469zm0 0" fill="#fafafa"/></svg>
            </p>
					</div>
					<!-- /.delite -->
      </div> 
     <!-- .done-notes -->
	</div>
	<!-- /.notes -->
</template>

<script>
export default {
	data () {
	return {
    todo: []
	}
},
  props: {
		notes: {
			type: Array,
			required: true
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
		removeNote (index) {
      this.$emit('remove', index)
    },
		toggle: function (e) {
		  e.target.classList.toggle('active')
    },
    doneTask: function (index) {
		for(let i = 0; i<this.notes.length; i++){
			if(index === this.notes[i].id) {
				this.todo.push(
					this.notes[i].title
				)
        this.notes.splice(i, 1)
        this.saveNote()
			}
		  }
    },
     saveNote () {
      const parsed = JSON.stringify(this.notes);
      localStorage.setItem('notes', parsed)
    },
  }
}
</script>

<style scoped>
.note {
	width: 500px;
	display: flex;
	justify-content: space-between;
	margin: auto;
	border-radius: 50px;
  box-shadow: 0px 2px 10px 1px rgba(0,0,0,0.35);
	margin-bottom: 15px;
}
.note-title {
  width: 500px;
  padding-top: 18px;
  padding-left: 30px;
}
span {
  font-size: 17px;
  text-align: center;
  font-family: 'Montserrat';
}
.active {
  text-decoration: line-through;
}
.delite {
  padding-right: 15px;
}
.done-notes {
  text-decoration: line-through;
  width: 500px;
	display: flex;
	justify-content: space-between;
	margin: auto;
  border-radius: 50px;
  box-shadow: 0px 2px 10px 1px rgba(0,0,0,0.35);
	margin-bottom: 15px;
	margin-bottom: 5px;
}
.text span{
  font-size: 20px;
  color: #7f7f7f;
}
</style>