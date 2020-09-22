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

<style scoped>
.new-note {
	width: 409px;
	margin: auto;
	margin-bottom: 30px;
}
input {
	border-radius: 50px;
	width: 280px;
	padding-top: 5px;
	border: 2px solid #ff0000;
	font-size: 18px;
	outline:none;
	margin-top: 10px;
	padding-left: 22px;
}
button {
	border-radius: 50px;
	border: none;
	outline:none;
	background: #ff0000;
	padding-top: 10px;
	padding-bottom: 10px;
	padding-right: 15px;
	padding-left: 15px;
	margin-left: 15px;
	color: white;
}
</style>