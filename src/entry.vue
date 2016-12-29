<template>
<div id="app">
  <div class="image_bundle" v-if="multiple_imgs" v-for="img in multiple_imgs">
  	<div class="preview">
  		<img :src="img" alt="placeholder of img"/>
  	</div>
  	<input type="button" value="更换" class="replace" id="replace">
  	<input type="button" value="删除" class="delete" id="delete">
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
  <div style="clear:both;">
  	<file_input_button :name="buttonText" v-on:dc="fileInputChange"></file_input_button>
</div>  
</template>

<script>
import file_input_button from "./file_input_button.vue"

var selected_img_list = [];
var ident = 0;

export default {
  name: 'app',
  data () {
    return {
      multiple_imgs: selected_img_list,
      in_uploading: false,
      name: 'fileupload',
      ident: ident,
      accept: 'images/*',
      multiple: 'multiple',  
		  buttonText: '选择文件',
		  show_submit: false,
    }
  },
  components: {file_input_button},  // 局部注册
  methods: {
		fileUpload: function () {
			
		},
		fileInputChange: function (param) {
			if (param) {
				for (var i = 0; i < param.length; i++) {
					var img = param[i];
					var reader = new FileReader();
					reader.onload = (e => {
						selected_img_list.push(e.target.result);
					});
					
					reader.readAsDataURL(img);			
				}
				
				
			}
		},
		fileInputClick: function () {
		}
  }
}
</script>

<style>
.progress_container {
	border: 1px black solid;
	height: 3px;
}

.progress_indicator {
	background-color: green;
	height: 100%;
	width: 50%;
}

.image_bundle {
	margin: 20px;
	width: 200px;
	float: left;
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
