<template>
    <div class="notification-container">
        <notification v-for="item,key in list" :key="item.id"
                      :permanent="item.permanent"
                      :container-class="item.containerClass"
                      :status-class="item.statusClass"
                      :width="item.width"
                      :show="item.show"
                      :close="item.close"
                      :content="item.content"
                      @hide="hideChild(key,item)">

            <template slot="content" scope="props">
                <slot name="content" :data="item.content"></slot>
            </template>

        </notification>
    </div>
</template>
<script>
    import Notification from './Notification.vue';

    export default {
        components: {
            notification: Notification
        },
        props: {
            close: '',
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
            return {
                list: [],
                permanent: false,
            }
        },
        watch: {
            show(val){
                this.showMe(val);
            }
        },
        methods: {
            showMe(obj){
                const item = {
                    id: this.list.length,
                    show: true,
                    permanent: obj.permanent || this.permanent,
                    close: this.close,
                    content: obj.data,
                    containerClass: this.containerClass,
                    statusClass: obj.status,
                    width: this.width
                };
                this.list.push(item);
            },
            hideChild(key,item){
                console.log(key);
                item.show = false;
                this.list.splice(key,1);
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
    .notification-container {
        display: flex;
        flex-direction: column-reverse;
        align-items: flex-end;
        position: fixed;
        right: 0;
        bottom: 0;
        width: auto;
        height: auto;
    }
</style>