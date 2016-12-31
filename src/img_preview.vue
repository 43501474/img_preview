<template>
	<div class="image_bundle">
	  	<div class="preview">
	  		<img :src="img_url" :alt="placeholder" :id="id_prefix+'2'"" key="id_prefix+'2'"/>
	  	</div>
	  	<input type="button" value="更换" class="replace" id="replace">
	  	<input type="button" value="删除" class="delete" :id="id_prefix+'1'" @click="onDel">
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
function asyncLoadImg() {

}

export default {
  name: 'img_preview',
  
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
		this.img_url = evt.target.result;
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
		console.dir(this.img_blob);
		this.$emit('delimg', this.img_blob);
	},
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

.image_bundle .replace {
	width: 45%;
	margin: 0 2px;
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
</style>