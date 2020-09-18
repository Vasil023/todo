<template>
    <div class="new-note">
			<input v-model="note.title" type="text">
			<button @click="addNote">Add Note</button>
    </div>
    <!-- /.new-note -->
		
</template>

<script>
export default {
	props: {
	note: {
		type: Object,
		required: true
	}
	},
	methods: {
		addNote () {
			this.$emit('addNote', this.note)
		}
	}
    
}
</script>