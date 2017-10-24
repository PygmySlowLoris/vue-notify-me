<template>
    <div class="notification-container">
        <notification
            v-for="(item,key) in list"
            :key="item.id"
            :permanent="item.permanent"
            :container="item.container"
            :status="item.status"
            :width="item.width"
            :timeout="item.timeout"
            :close="item.close"
            :content="item.content"
            @hide="hideChild(key)"
        >
            <template slot="content">
                <slot name="content" :data="item.content" />
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
            permanent: {
                default: false
            },
            close: {
                default: 'bulma'
            },
            container: {
                type: String,
                default: 'notification'
            },
            status: {
                type: String,
                default: 'is-success'
            },
            width: {
                type: String,
                default: '350px'
            },
            timeout: {
                type: Number,
                default: 4000
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
            }
        },
        data() {
            return {
                list: []
            };
        },
        methods: {
            showMe(obj) {
                const item = {
                    id: this.list.length,
                    permanent: obj.permanent || this.permanent,
                    close: obj.close || this.close,
                    content: obj.data,
                    container: obj.container || this.container,
                    status: obj.status || this.status,
                    width: obj.width || this.width,
                    timeout: obj.timeout || this.timeout
                };
                this.list.push(item);
            },
            hideMe() {
                this.list = [];
            },
            hideChild(key) {
                this.list.splice(key, 1);
            },
            // Register eventBus methods.
            registerBusMethods() {
                const bus =
                    this.eventBus ||
                    (this.$parent
                        ? this.$parent.bus || this.$parent
                        : null);

                if (bus) {
                    bus.$on(this.eventShow, this.showMe);
                    bus.$on(this.eventHide, this.hideMe);
                }
            }
        },
        created() {
            this.registerBusMethods();
        }
    };
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
        z-index: 9999;
    }
</style>
