<template>
    <div class="back-top" :style="{right:right + 'px',bottom:bottom + 'px'}" @click="backTop" v-if="showBackTop"></div>
</template>
<style>
    .back-top {
        position: fixed;
        width: 64px;
        height: 64px;
        cursor: pointer;
        background: url("../../src/assets/top.png") center no-repeat;
    }
</style>
<script>
    export default {
        name: 'back-top',
        data() {
            return {
                showBackTop: false,
                flag: true,
                timer: null,
                scrollTop: 0,
            }
        },
        mounted() {
            window.addEventListener('scroll',() => {
                //var height = document.documentElement.clientHeight || document.body.clientHeight;
                if (this.scrollTop >= this.height) {
                    this.showBackTop = true;
                } else {
                    this.showBackTop = false;
                }
                if (!this.flag) {
                    clearInterval(this.timer);
                }
                this.flag = false;
                this.scrollTop = document.documentElement.scrollTop || document.body.scrollTop;
            })
        },
        props: {
            duration: {
                type: Number,
                default: 30
            },
            spend:{
                type:Number,
                default:10
            },
            height: {
                type: Number,
                default: 200
            },
            right:{
                type:Number,
                default:30
            },
            bottom:{
                type:Number,
                default:30
            }

        },
        methods: {
            backTop() {
                clearInterval(this.timer);
                this.timer = setInterval(() => {
                    var now = this.scrollTop;
                    var speed = (0 - now) / this.spend;
                    speed = speed > 0 ? Math.ceil(speed) : Math.floor(speed);
                    if (this.scrollTop == 0) {
                        clearInterval(this.timer);
                    }
                    this.flag = true;
                    document.documentElement.scrollTop = this.scrollTop + speed;
                    document.body.scrollTop = this.scrollTop + speed;
                }, this.duration);
            }
        }
    };
</script>