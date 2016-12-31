<template>
	<div class="image_bundle">
	  	<div class="preview">
	  		<img :src="img_url" :alt="placeholder" :key="id_prefix + '_img'"/>
	  	</div>
	  	<file_input_button width_value="replace_component" name="更换" :id_prefix="id_prefix+'replace_img'" multiple="false" v-on:file_change="onReplace" ></file_input_button>
	  	<input type="button" value="删除" class="delete" :id="id_prefix+'1'" @click="onDel" style="display:inline">
	  	<div v-if="in_uploading" style="display:none">
			<div class="progress_container">
				<div class="progress_indicator">
				</div>
			</div>
	  	</div>
		<div v-else>
			<textarea placeholder="请在这里输入对图片的备注说明" class="remark" id="remarks"></textarea>
		</div>	
	</div>
</template>

<script>
import file_input_button from "./file_input_button.vue"

export default {
  name: 'img_preview',
  components: {file_input_button},
  props: {
	id_prefix: {
		type: String,
		default: 'img_preview_btn',
	},
	img_blob: {
		type: File,
	},
	placeholder: {
		type: String,
		default: '',
	}
  },
  beforeMount: function() {
  	console.log('beforemount');
  	self = this;
	var reader = new FileReader();
	reader.onload = function(evt) {
		console.log('old data is ' + this.img_url.length);
		this.img_url = evt.target.result;
		console.log('old data is ' + this.img_url.length);
	}.bind(this);
	reader.readAsDataURL(this.img_blob);
  },
  
  
  data () {
  	return {
		name: 'fileupload',
		in_uploading: false,
		show_submit: false,
		img_url: '',
  	}
  },
  
  methods: {
	onDel: function() {
		this.$emit('delimg', this.img_blob);
	},
	onReplace: function(file_list) {
		console.log('replacing...')
		console.log('file number should be 1: ' + file_list.length)
		console.log(file_list[0].name);
		self = this;
		
		var ele = file_list[0];
		var reader = new FileReader();
		reader.onload = function(evt) {
			console.log('old data is ' + self.img_url.length);
			self.img_url = evt.target.result;
			console.log('new data is ' + self.img_url.length);
		};
		reader.readAsDataURL(ele);
	}
  }
};

</script>

<style scoped>
.image_bundle {
	margin: 20px;
	width: 200px;
	float: left;
}

.progress_container {
	border: 1px black solid;
	height: 3px;
}

.progress_indicator {
	background-color: green;
	height: 100%;
	width: 50%;
}

.preview {
	width: 100%;
	height: 200px;
}

.image_bundle .delete {
	width: 45%;
	margin: 0 2px;
}

.image_bundle .remark {
	width: 100%;
	min-height: 3em;
	text-wrap: ;
}

.image_bundle img {
	width: 200px;
	height: 200px;
}

.image_bundle .replace_component {
	display: inline-block;
	width: 45%;
	margin: 0 2px;
}
</style>