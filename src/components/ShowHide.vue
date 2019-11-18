<template>
    <div class="show-hide-wrapper">
        <button :id="'show-trigger-' + uid" :class="triggerClass" @click.prevent="toggle" type="button">
            <slot name="trigger-text">Show</slot>
        </button>
        <transition name="fade-down">
            <div :id="'content-' + uid" :class="contentClass" v-show="showContent">
                <slot name="content"></slot>
            </div>
        </transition>
    </div>
</template>

<script>
    export default {
        name: "ShowHide",

        props: {
            triggerClass: {
                default: 'show-hide-trigger',
            },
            contentClass: {
                default: 'show-hide-content'
            },
        },

        computed: {
            uid() {
                return Math.floor(1 + Math.random() * 0x10000).toString(16).substring(1);
            }
        },

        data() {
            return {
                showContent: false,
            };
        },

        methods: {
            toggle() {
                this.showContent = !this.showContent;

                if(this.showContent) {
                    this.$emit('show');
                }
                else {
                    this.$emit('hide');
                }
            },
        },

        mounted() {
            new ClickOffHandler('#show-trigger-' + this.uid, () => this.showContent = false, '#content-' + this.uid);
        }
    }


    class ClickOffHandler {

        constructor(selector, callback, stopOn = null) {
            this.selector = selector;
            this.callback = callback;
            this.stopOn   = stopOn;

            this.handler = null;

            this.setOnFirstClickEvent();
            this.setStopEvent();
        }

        removeListener() {
            document.removeEventListener('click', this.handler);
        }

        setOnFirstClickEvent() {
            document.querySelector(this.selector).addEventListener('click', (event) => {
                this.setClickOffEvent(event.target)
            });
        }

        setClickOffEvent(firstClickTarget) {
            this.handler = (secondClick) => {
                if(firstClickTarget !== secondClick.target) {
                    this.callback();
                    this.removeListener();
                }
            };

            document.addEventListener('click', this.handler);
        }

        setStopEvent() {
            if(this.stopOn) {
                document.querySelector(this.stopOn).addEventListener('click', (e) => e.stopPropagation());
            }
        }
    }

</script>

<style scoped>
    .show-hide-wrapper {
        display: inline-block;
        position: relative;
    }
</style>
