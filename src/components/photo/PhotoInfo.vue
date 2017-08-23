<template>
	<div class="templateDiv">
		<h3>{{photoinfo.title}}</h3>
		<div>
			{{photoinfo.add_time | dateFmt('YYYY/MM/DD HH:mm:SS')}}  {{photoinfo.click}}次浏览
		</div>
		<p class="line"></p>

		<div class="mui-content">
			<ul class="mui-table-view mui-grid-view mui-grid-9">
				<li class="mui-table-view-cell mui-media mui-col-xs-4 mui-col-sm-4" v-for="item in imgDetail">
					<router-link to="/news/newlist">
						<img src="../../../static/test.jpg">
					</router-link>
				</li>
			</ul>
		</div>

		<p v-html="photoinfo.content"></p>
		<comment v-bind:myNewsId="photoinfo.id"></comment>
	</div>
</template>

<script>
	import Comment from "../../subcomponents/Comment.vue";
	export default{
		components:{
			comment :Comment
		},
		data(){
			return {
				id:0,
				photoinfo:[],
				imgDetail:[]
			}
		},
		created(){
			this.id=this.$route.params.id;
			this.getImgInfo();
			this.getImgDetail();
		},
		methods:{
			getImgInfo(){
				var url = this.$urlPrefix+"/api/getimageInfo/"+this.id;
				this.$http.get(url).then(function(response){
					 this.photoinfo = response.body.message[0];
					console.log(response.body);
				});
			},
			getImgDetail(){
				var url = this.$urlPrefix+"/api/getthumimages/"+this.id;
				this.$http.get(url).then(function(response){
					 this.imgDetail = response.body.message;
					console.log(response.body);
				});
			}
		}
	}
</script>
<style scoped>
	.line{
		width: 100%;
		height: 1px;
		background-color: rgba(0,0,0,0.2);
		margin: 5px 0;
	}
	ul li img{
		width: 50px;
		height: 50px;
	}
	.mui-content{
		background-color: #fff;
	}
	.mui-content ul{
		background-color: #fff;
	}
	.mui-grid-view.mui-grid-9 .mui-table-view-cell{
		border: 0;
	}
	.mui-grid-view.mui-grid-9{
		border: 0;
	}
</style>
