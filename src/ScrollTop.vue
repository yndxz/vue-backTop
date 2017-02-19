<template>
	<div class="scroll-top" @click="top"></div>
</template>
<style>
	.scroll-top{
    position: fixed;
    top: 80%;
    right: 10%;
    width: 64px;
    height: 64px;
    cursor:pointer;
    display:none;
    background: url("../src/assets/top.png") center no-repeat;
  }
</style>
<script>
  export default {
  		name:'scroll-top',
	    mounted() {
	        var self = this;
	        window.onscroll=function(){
		        	var height = document.documentElement.clientHeight || document.body.clientHeight;
	        		if(self.scrollTop >= height){
	      				self.$el.style.display = "block";
	        		}else{
	        			self.$el.style.display = "none";
	        		}
	            if(!self.flag){
	                clearInterval(self.timer);
	            }
	            self.flag = false;
	            self.scrollTop=document.documentElement.scrollTop || document.body.scrollTop;
	        };
	    },
	    props:{
	        spend:{
	            type:Number,
	            default:30
	        }
	    },
	    data() {
	      return {
	          flag:true,
	          timer:null,
	          scrollTop:null,
	      }
	    },
	    methods:{
	        top() {
            clearInterval(this.timer);
            var self = this;
            this.timer=setInterval(function(){
                var now=self.scrollTop;
                var speed=(0-now)/10;
                speed=speed>0?Math.ceil(speed):Math.floor(speed);
                if(self.scrollTop==0){
                    clearInterval(self.timer);
                }
                self.flag = true;
                document.documentElement.scrollTop = self.scrollTop + speed;
                document.body.scrollTop = self.scrollTop + speed;
            }, this.spend);
	        }
	    }
	};
</script>