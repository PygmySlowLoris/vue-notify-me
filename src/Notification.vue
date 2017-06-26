<template>
    <transition
            enter-active-class="animated quick fadeInRight"
            leave-active-class="animated quick fadeOutRight"
    >
        <div v-if="show" :class="[containerClass,statusClass, 'notify-me']" :style="{ width: width + 'px' }">
            <slot name="content" :data="content"></slot>
            <button v-if="close === 'bulma'" class="delete" @click="hideMe"></button>
            <button v-else-if="close === 'bootstrap'" type="button" class="close" aria-label="Close" @click="hideMe">
                <span aria-hidden="true">&times;</span>
            </button>
            <i v-else class="notify-close material-icons" @click="hideMe">clear</i>
        </div>
    </transition>
</template>
<script>
    export default {
        props:{
            show: false,
            permanent:false,
            close:'',
            content: {},
            containerClass: {
                type: String,
                default: 'alert'
            },
            statusClass: {
                type: String,
                default: 'alert-success'
            },
            width: {
                type: Number,
                default: 350
            }

        },
        methods:{
            hideMe(){

                this.$emit('hide');
                setTimeout(() => {
                    this.$destroy();
                },1000)

            }
        },
        created(){
            if(!this.permanent){
                setTimeout(() => {
                    this.hideMe();
                },4000)
            }

        }

    }
</script>
<style scoped>
    .notify-me {
        display: flex;
        align-items: center;
        justify-content: space-between;
        position: relative;
        bottom: 2rem;
        right: 2rem;
        z-index:9999;
        margin-bottom: 1.5rem;
    }

    .notify-me i {
        cursor: pointer;
        align-self: flex-start;
    }

    .notify-me:first-child {
        margin-bottom: 0;
    }
</style>