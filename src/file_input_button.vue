<template>
	<div v-bind:class="width_value">
		<input :id="id_prefix+'2'" class="fi_button" type="button" :value="name" @click="onButtonClick"></input>
		<input :id="id_prefix+'1'" type="file" :accept="accept" style="display: none;" @change="fileInputChange" :multiple="multiple"></input>	
	</div>
</template>

<script>

export default {
	name: 'file_input',

	props: {
		multiple: {
			type: String,
			default: 'multiple',
		},
		name: {
			type: String,
			default: '选择文件',
		},
		id_prefix: {
			type: String,
			default: 'fi_button',
		},
		accept: {
			type: String,
			default: 'image/*',
		},
		width_value: {
			type: String,
			default: 'auto',
		}
	},

	data() {
		return {
			msg: 'hello',
		};
	},

	methods: {
		onButtonClick: function() {
			var $file_input = $('#' + this.id_prefix + '1');
			$file_input.trigger('click');
		},
		fileInputChange: function() {
			var ele = $('#' + this.id_prefix + '1').get(0);
			this.$emit('file_change', ele.files);
		}
	}
};

</script>

<style scoped>
.fi_button {
    width: 100%;
}
</style>