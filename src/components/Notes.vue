<template>
	<div class="notes">
			<div class="note" v-for="(note, index) in notes" :key="index">
				<div class="note-title">
					{{note.title}}
						<p  style="cursor: pointer;" @click="removeNote(index)" >x</p>
				</div>
				<!-- /.note-title -->
			</div>
			<!-- /.note -->
	</div>
	<!-- /.notes -->
</template>

<script>
export default {
  props: {
		notes: {
			type: Array,
			required: true
		}
	},
	methods: {
		removeNote (index) {
			this.$emit('remove', index)
		}
	}
	
}
</script>