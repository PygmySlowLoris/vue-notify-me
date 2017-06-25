<template>
    <transition
            enter-active-class="animated quick fadeInRight"
            leave-active-class="animated quick fadeOutRight"
    >
        <div v-if="showing" :class="[containerClass,statusClass, 'notify-me']" :style="{ width: width + 'px' }">
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
            show: {
                default: false
            },
            close:'',
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
            },
            // central event bus
            eventBus: {
                default: null
            },
            eventShow: {
                default: 'notify-me'
            },
            eventHide: {
                default: 'hide-notify-me'
            },

        },
        data(){
            return{
                showing: false,
                permanent:false,
                content: {}
            }
        },
        watch: {
            show(val){
                this.showMe(val);
            }
        },
        methods:{
            showMe(obj){
                this.permanent = obj.permanent || this.permanent;
                this.content = obj.data;
                this.showing = true;

                if(!this.permanent)
                    setTimeout(() => {
                        this.hideMe()
                    }, 4000);
            },
            hideMe(){
                this.showing = false;
                this.permanent = false;

                this.$emit('hide');
            },
            // Register eventBus methods.
            registerBusMethods()
            {
                this.eventBus.$on(this.eventShow, this.showMe);
                this.eventBus.$on(this.eventHide, this.hideMe);
            }
        },
        created(){
            // If event bus, register methods.
            if (this.eventBus)
                this.registerBusMethods();
        }

    }
</script>
<style scoped>
    .notify-me {
        display: flex;
        align-items: center;
        justify-content: space-between;
        position: fixed;
        bottom: 2rem;
        right: 2rem;
        z-index:9999;
    }

    .notify-me i {
        cursor: pointer;
        align-self: flex-start;
    }
</style>