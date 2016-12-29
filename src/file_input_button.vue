<template>
	<div>
		<input :id="id_prefix+'2'" class="fi_button" type="button" :value="name" @click="onButtonClick"></input>
		<input :id="id_prefix+'1'" type="file" accept="image/*" style="display: none;" @change="fileInputChange" :multiple="multiple"></input>	
	</div>
</template>

<script>
var $ = window.jQuery = require('jquery');

export default {
  name: 'app',
  
  props: {
  	multiple: {
  		type: String,
  		default: 'multiple',
  	},
  	name: {
		type: String,
		default: '更换图片1',
   },
   id_prefix: {
		type: String,
		default: 'fi_button',
   }
  },
  
  data () {
  	return {
  		msg: 'hello',
  	};
  },
  
  methods: {
  	onButtonClick: function() {
  		var $file_input = $('#' + this.id_prefix + '1');
  		$file_input.trigger('click');
  	},
   	fileInputChange: function () {
  		var ele = $('#' + this.id_prefix + '1').get(0);
  		this.$emit('dc', ele.files);
  	}
  }
};
</script>

<style scoped>
.fi_button {
    margin-left: 10px;
}
</style>