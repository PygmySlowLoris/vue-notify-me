<template>
    <transition
            enter-active-class="animated quick fadeInRight"
            leave-active-class="animated quick fadeOutRight"
    >
        <div v-if="show" :class="[container,status, 'notify-me']" :style="{ width: width + 'px' }">
            <slot name="content"></slot>
            <button v-if="close === 'bulma'" class="delete" @click="hideMe"></button>
            <button v-else-if="close === 'bootstrap'" type="button" class="close" aria-label="Close" @click="hideMe">
                <span aria-hidden="true">&times;</span>
            </button>
            <i v-else :class="close + ' material-icons'" @click="hideMe">clear</i>
        </div>
    </transition>
</template>
<script>
    export default {
        props: {
            permanent: {
                default: false
            },
            close: '',
            content: {},
            container: {
                type: String,
                default: 'alert'
            },
            status: {
                type: String,
                default: 'alert-success'
            },
            width: {
                type: Number,
                default: 350
            }

        },
        data(){
            return {
                show:true
            }
        },
        methods: {
            hideMe(){
                this.$emit('hide');
            }
        },
        created(){
            if (!this.permanent) {
                setTimeout(() => {
                    this.hideMe();
                }, 4000)
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
        z-index: 9999;
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