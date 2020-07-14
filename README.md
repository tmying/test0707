# 简介(vue.js + 原生js)

## 1 项目描述

1. 制作html静态页面
2. 使用vue.js在个人信息列表中实现数据绑定
3. 点击修改按钮弹出修改模态框，自动显示当前修改的个人信息，修改内容后点击保存，刷新个人信息列表
4. 编辑页点击取消或“x”，个人信息不做修改

## 2 技术难点

### 2.1 css样式
1. 实现精灵图
	.aside li>div {
		width: 30px;
		height: 30px;
		margin: 0 8px 0 56px;
	}

	.aside li:first-child>div {
		background: url('./imgs/aside.png') no-repeat 0px -36px;
	}
2. 使用阿里矢量图标
	先找图并加入购物车，然后创建项目，下载包到本地  font文件夹(5)
	<span class="iconfont">&#xe60a;</span>
3. 实现蒙层
	<div class="disnone" id="special" ref="special"></div>
	#special {
		width: 100%;
		height: 100%;
		position: absolute;
		top: 0;
		left: 0;
		background: black;
		opacity: 0.6;
		z-index: 1;
		/* display: none; */
	}

	/* 默认隐藏 */
	.disnone {
		display: none;
	}
	
	#edit {
		width: 560px;
		height: 220px;
		position: absolute;
		top: 50%;
		left: 50%;
		transform: translate(-50%, -50%);
		background: #fff;
		border-radius: 5px;
		z-index: 2;
		/* display: none; */
	}
### 2.2 js编写
1. button按钮点击不起作用
	原因：IE中button的默认值是 "button"，而其他浏览器中的默认值是 "submit"
	解决：在<button>中添加属性 type="button"
2. vue.js的下拉框获取值和传值
	<p><span class="iconfont">&#xe635;</span>性&emsp;别：<select name="" id="" v-model="form2.sex">
		<option :value="0">男</option>
		<option :value="1">女</option>
	</select></p>
	/* 计算属性 */  !重点(对值进行加工，直接返回值)
	computed: {
		handleSex() {
			if (this.form1.sex === '男') {
				return 0;
			} else if (this.form1.sex === '女') {
				return 1;
			} else if (this.form1.sex === 0) {
				return "男";
			} else {
				return "女";
			}
		}
	}
3. 为符合实际应用情景，在编辑页进行修改时，避免form1的值跟着变动，故在切换时进行浅拷贝
	点击修改：this.form1.sex = this.handleSex;
			  this.form2 = Object.assign({}, this.form1);
	点击保存：this.form1 = Object.assign({}, this.form2);
			  this.form1.sex = this.handleSex;

## 3 额外说明
注意：不使用脚手架或者webpack，直接srcipt标签引入vue.js
此项目为**成都青云之上信息科技有限公司**的上机测试题，要求2小时完成
