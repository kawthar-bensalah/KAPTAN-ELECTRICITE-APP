<template>
    <div class="container" style="margin-top : 2%; margin-bottom : 2%;">
        <div id="page" >
             <img src="src/assets/img/kaptan-electric-logo.png">

            <transition name="fade">
                <router-view></router-view>
            </transition>
        </div>
    </div>
</template>

<style>
    .fade-enter-active, .fade-leave-active {
      transition: opacity .5s
    }
    .fade-enter, .fade-leave-active {
      opacity: 0
    }
</style>

<script>

    export default{
        data(){
            return{

            }
        }
    }
</script>
