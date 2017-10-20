<template>
    <div id="app">
        <!--Example dependecies-->
        <link rel="stylesheet" href="https://cdnjs.cloudflare.com/ajax/libs/bulma/0.4.4/css/bulma.min.css">
        <link href="https://fonts.googleapis.com/icon?family=Material+Icons" rel="stylesheet">
        <a :href="repoUrl" class="github-corner" aria-label="View source on Github">
            <svg width="80" height="80" viewBox="0 0 250 250"
                 style="fill:#151513; color:#fff; position: absolute; top: 0; border: 0; right: 0;" aria-hidden="true">
                <path d="M0,0 L115,115 L130,115 L142,142 L250,250 L250,0 Z"></path>
                <path d="M128.3,109.0 C113.8,99.7 119.0,89.6 119.0,89.6 C122.0,82.7 120.5,78.6 120.5,78.6 C119.2,72.0 123.4,76.3 123.4,76.3 C127.3,80.9 125.5,87.3 125.5,87.3 C122.9,97.6 130.6,101.9 134.4,103.2"
                      fill="currentColor" style="transform-origin: 130px 106px;" class="octo-arm"></path>
                <path d="M115.0,115.0 C114.9,115.1 118.7,116.5 119.8,115.4 L133.7,101.6 C136.9,99.2 139.9,98.4 142.2,98.6 C133.8,88.0 127.5,74.4 143.8,58.0 C148.5,53.4 154.0,51.2 159.7,51.0 C160.3,49.4 163.2,43.6 171.4,40.1 C171.4,40.1 176.1,42.5 178.8,56.2 C183.1,58.6 187.2,61.8 190.9,65.4 C194.5,69.0 197.7,73.2 200.1,77.6 C213.8,80.2 216.3,84.9 216.3,84.9 C212.7,93.1 206.9,96.0 205.4,96.6 C205.1,102.4 203.0,107.8 198.3,112.5 C181.9,128.9 168.3,122.5 157.7,114.1 C157.9,116.9 156.7,120.9 152.7,124.9 L141.0,136.5 C139.8,137.7 141.6,141.9 141.8,141.8 Z"
                      fill="currentColor" class="octo-body"></path>
            </svg>
        </a>
        <!--Example Elements-->
        <section class="hero">
            <div class="hero-body" style="padding: 1rem 0">
                <div class="container">
                    <div class="columns">
                        <div class="column is-8 is-offset-3" style="display: flex; align-items: center;">
                            <div class="is-pulled-left">
                                <img width="350px" src="./assets/logo.png">
                            </div>
                            <div class="is-pulled-left" style="text-align: left">
                                <h1 class="title text-medium-grey" style="margin-bottom: .5rem">
                                    {{componentName}}
                                </h1>
                                <hr class="is-marginless">
                                <h2 class="subtitle text-light-grey" style="margin-top: .5rem">
                                    A Vue Component
                                    <span class="is-pulled-right">
                                        <!-- Place this tag where you want the button to render. -->
<a class="github-button" :href="repoUrl" data-icon="octicon-star" data-size="large"
   :aria-label="'Star' + repoFullName + 'on GitHub'">Star</a>
                                    </span>
                                </h2>
                            </div>
                        </div>
                    </div>
                </div>
            </div>
        </section>

        <section class="section" style="padding-top: .5rem">
            <div class="container">
                <div class="columns">
                    <div class="column is-8 is-offset-2">
                        <div class="box formated">
                            <div class="heading">
                                <div class="columns">
                                    <div class="column">
                                        <i class="material-icons top-left">code</i>
                                        <span class="is-pulled-right"><b>Example</b></span>
                                    </div>
                                </div>
                            </div>
                            <div class="content">
                                <div class="columns">
                                    <div class="column">
                                        <div class="field">
                                            <label class="label">Text to show</label>
                                            <div class="control">
                                                <input v-model="text" class="input" type="text">
                                            </div>
                                        </div>
                                    </div>
                                    <div class="column">
                                        <div class="field">
                                            <label class="label">Notification Status</label>
                                            <div class="control is-expanded">
                                                <span class="select is-fullwidth">
                                                  <select v-model="status">
                                                    <option value="is-success">success</option>
                                                    <option value="is-info">info</option>
                                                    <option value="is-warning">warning</option>
                                                    <option value="is-danger">danger</option>
                                                  </select>
                                                </span>
                                            </div>
                                        </div>
                                    </div>
                                    <div class="column">
                                        <div class="field">
                                            <label class="label">Permanent</label>
                                            <div class="control is-expanded">
                                                <p class="control">
                                                    <label class="radio">
                                                        <input type="radio" name="question" :value="true"
                                                               v-model="permanent">
                                                        Yes
                                                    </label>
                                                    <label class="radio">
                                                        <input type="radio" name="question" :value="false"
                                                               v-model="permanent">
                                                        No
                                                    </label>
                                                </p>
                                            </div>
                                        </div>
                                    </div>
                                    <div class="column">
                                        <div class="field">
                                            <label class="label">Timeout</label>
                                            <div class="control">
                                                <input v-model="timeout" class="input" type="number">
                                            </div>
                                        </div>
                                    </div>
                                </div>
                                <div class="columns">
                                    <div class="column">
                                        <button class="button is-primary" style="width: 100%" @click="showMe">
                                            Show Notification
                                        </button>
                                    </div>
                                    <div class="column">
                                        <button class="button is-warning" style="width: 100%" @click="hideMe">
                                            Hide Notifications
                                        </button>
                                    </div>
                                </div>
                                <div class="columns">
                                    <div class="column has-text-centered">
                                        <a :href="repoUrl">Installation & Code usage</a>
                                    </div>
                                </div>
                            </div>
                        </div>
                    </div>
                </div>
            </div>
        </section>

        <footer class="footer">
            <div class="container">
                <div class="content has-text-centered">
                    <p>
                        <strong>Floating Action Button Vue Component</strong> by <a
                            :href="teamUrl">Pygmy Team</a>.
                    </p>
                    <p>
                        <small>Used dependencies for this demo: <a href="http://bulma.io">bulma</a></small>
                    </p>
                </div>
            </div>
        </footer>
        <notify-me
            :event-bus="bus">
            <template slot="content" slot-scope="{data}">
                <div style="width: 100%; word-break: break-all; text-align: left">
                    <h4><b>{{data.title}}</b></h4>
                    <p style="margin: 0">{{data.text}}</p>
                </div>
            </template>
        </notify-me>
    </div>
</template>

<script>
    import Notify from '../src/Notify.vue';
    import Vue from 'vue';

    const componentName = 'vue-notify-me';
    const teamUrl = 'https://github.com/PygmySlowLoris';
    const repoUrl = 'https://github.com/PygmySlowLoris/vue-notify-me';
    const repoFullName = 'PygmySlowLoris/vue-notify-me';

    const bus = new Vue();

    export default {
        name: 'app',
        components: {
            'notify-me': Notify
        },
        data(){
            return {
                repoUrl,
                teamUrl,
                componentName,
                repoFullName,
                status: 'is-success',
                permanent: false,
                text: 'Coded slow but effective',
                timeout: 4000,
                bus
            }
        },
        methods: {
            showMe(){
                this.bus.$emit('notify-me', {
                    permanent: this.permanent,
                    status: this.status,
                    timeout: parseInt(this.timeout),
                    data: {
                        title: 'The pygmy team :)',
                        text: this.text
                    }

                });
            },
            hideMe()
            {
                this.bus.$emit('hide-notify-me');
            }
        }
    }
</script>

<style scoped>
    #app {
        -webkit-font-smoothing: antialiased;
        -moz-osx-font-smoothing: grayscale;
        color: #2c3e50;
    }

    .pointer {
        cursor: pointer;
    }

    h1, h2 {
        font-weight: normal;
    }

    hr {
        background-color: transparent;
        border: none;
        display: block;
        height: inherit;
        margin: 1.5rem 0;
        border-top: dashed 1px;
    }

    li {
        display: inline-block;
        margin: 0 10px;
    }

    a {
        color: #0b99b9;
        text-decoration: underline;
    }

    .text-medium-grey {
        color: #333;
    }

    .text-light-grey {
        color: #888;
    }

    .box.formated {
        position: relative;
        padding: 0;
    }

    .box.formated .heading {
        font-size: 1rem;
        text-transform: capitalize;
        padding: .8rem 1.5rem;
        background-color: #fafafa;
    }

    .box.formated .content {
        padding: 1rem 2rem;
    }

    i.top-left {
        position: absolute;
        left: 1.5rem;
        top: 0.8rem;
    }

    .vertical-separator {
        display: flex;
        justify-content: space-around;
    }

    .vertical-separator .line {
        border-right: 1px solid #cccccc;
    }

    .github-corner:hover .octo-arm {
        animation: octocat-wave 560ms ease-in-out
    }

    @keyframes octocat-wave {
        0%, 100% {
            transform: rotate(0)
        }
        20%, 60% {
            transform: rotate(-25deg)
        }
        40%, 80% {
            transform: rotate(10deg)
        }
    }

    @media (max-width: 500px) {
        .github-corner:hover .octo-arm {
            animation: none
        }

        .github-corner .octo-arm {
            animation: octocat-wave 560ms ease-in-out
        }
    }
</style>
