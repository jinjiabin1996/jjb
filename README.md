<!DOCTYPE html>
<html>
	<head>
		<meta charset="UTF-8">
		<title></title>
		<style type="text/css">
			*{
				padding:0px;margin:0px;
			}
			.smallpic{
				width: 450px;
				height: 450px;
				border: 1px solid #ccc;
				position: relative;
			}
			.smallpic img{
				width: 450px;
				height: 450px;
			}
			.mask{
				position: absolute;
				left:0px;top:0px;
				width: 50px;
				height: 50px;
				background: rgba(169,255,0,0.5);
				visibility: hidden;
			}
			.bigpic{
				width: 600px;
				height: 600px;
				border: 1px solid #ccc;
				position: absolute;
				left:455px;
				top:0px;
				overflow: hidden;
				visibility: hidden;
			}
			.bigpic img{
				position: absolute;
				left:0px;
				top:0px;
			}
		</style>
	</head>
	<body>
		<div class="smallpic" id="smallpic">
			<img src="telphone.png"/>
			<div class="mask" id="mask"></div>
		</div>
		<div class="bigpic" id="bigpic">
			<img src="telphone.png" id="img1"/>
		</div>
		<script type="text/javascript">
			var oSmallPic=document.getElementById('smallpic');//小图
			var oMask=document.getElementById('mask');//小芳
			var oBigPic=document.getElementById('bigpic');//大芳
			var oImg1=document.getElementById('img1');//大图
			//小方/大方=小图/大图=scale
			oSmallPic.onmouseover=function(){
				//让小芳和大芳显示
				oMask.style.visibility='visible';
				oBigPic.style.visibility='visible';
				//求小芳的尺寸
				oMask.style.width=oBigPic.offsetWidth*oSmallPic.offsetWidth/oImg1.offsetWidth+'px';
				oMask.style.height=oBigPic.offsetHeight*oSmallPic.offsetHeight/oImg1.offsetHeight+'px';
				//求比例:倍数
				var scale=oBigPic.offsetWidth/oMask.offsetWidth;
				
				this.onmousemove=function(ev){
					var ev=ev||window.event;
					//让鼠标移动的放置在盒子的中间
					var l=ev.clientX-oMask.offsetWidth/2;
					var t=ev.clientY-oMask.offsetHeight/2;
					if(l<0){
						l=0;
					}else if(l>=oSmallPic.offsetWidth-oMask.offsetWidth){
						l=oSmallPic.offsetWidth-oMask.offsetWidth;
					}
					
					if(t<0){
						t=0;
					}else if(t>=oSmallPic.offsetHeight-oMask.offsetHeight){
						t=oSmallPic.offsetHeight-oMask.offsetHeight;
					}
					//判断小芳不能移出小图的范围。
					//赋值给小芳
					oMask.style.left=l+'px';
					oMask.style.top=t+'px';
					//将对应比例赋给大图
					oImg1.style.left=-l*scale+'px';
					oImg1.style.top=-t*scale+'px';
					
				}
			}
			
			oSmallPic.onmouseout=function(){
				oMask.style.visibility='hidden';
				oBigPic.style.visibility='hidden';
			}
		</script>
	</body>
</html>

