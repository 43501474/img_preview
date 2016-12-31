<template>
<div id="app">
	<div v-for="(img,idx) in multiple_imgs">
		<img_preview 
			v-bind:id_prefix="multiple_imgs.length + 'img_preview_'+idx" 
			v-bind:placeholder="img.data.name" 
			v-bind:img_blob="img.data" 
			v-if="img.visible"
			@delimg="doDel">
		</img_preview>
	</div>

  	<div style="clear:both;">
  		<file_input_button :name="buttonText" v-on:dc="fileInputChange"></file_input_button>
	</div>  
</template>

<script>

import file_input_button from "./file_input_button.vue"
import img_preview from "./img_preview.vue"

export default {
	name: 'app',
	props: {
		id_prefix: {
			type: String,
			default: 'fi_button',
		}
	},
	data() {
		return {
			multiple_imgs: [],
			buttonText: '选择文件',
		}
	},
	components: {
		file_input_button,
		img_preview
	}, // 局部注册
	methods: {
		fileUpload: function() {

		},
		fileInputChange: function(param) {
			if(param) {
				for(var i = 0; i < param.length; i++) {
					var img = param[i];
					this.multiple_imgs.push({'data': img, 'visible': true});
				}
			}
		},
		fileInputClick: function() {},
		doDel: function(img) {
			// 这里只是把需要删除的sub component隐藏起来。
			// 直接从数组multiple_imgs中删除对应元素的办法行不通，问题在于multiple_imgs更新后，img_preview中的img_url没有重新生成。
			this.multiple_imgs.forEach(function(ele) {
				if (ele['data'] === img)
					ele['visible'] = false;
			});
		},
	}
};

</script>

<style>

</style>
