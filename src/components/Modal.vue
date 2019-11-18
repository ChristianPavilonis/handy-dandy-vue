<template>
    <transition name="fade-scale" appear>
        <div class="modal" @click="close">
            <div class="modal-overlay">
                <div class="modal-content" @click.stop>
                    <div class="modal-header">
                        <div class="modal-title">
                            <slot name="title"></slot>
                        </div>

                        <button class="close-button" @click="close">
                            <svg class="fill-current" xmlns="http://www.w3.org/2000/svg" viewBox="0 0 20 20">
                                <path d="M10 8.586L2.929 1.515 1.515 2.929 8.586 10l-7.071 7.071 1.414 1.414L10 11.414l7.071 7.071 1.414-1.414L11.414 10l7.071-7.071-1.414-1.414L10 8.586z"/>
                            </svg>
                        </button>
                    </div>
                    <div class="modal-body flex justify-center">
                        <slot name="body"></slot>
                    </div>
                </div>
            </div>
        </div>
    </transition>
</template>

<script>
    export default {
        name : "Modal",

        computed: {},

        data() {
            return {};
        },

        methods: {
            close() {
                this.$emit('close');
            }
        },

        mounted() {
            document.body.classList.toggle('modal-open')
        },
        beforeDestroy() {
            document.body.classList.toggle('modal-open')
        }
    }
</script>

<style>
    body.modal-open {
        overflow: hidden;
    }

    .modal {
        position: fixed;
        z-index: 1;
        left: 0;
        top: 0;
        overflow: auto;
        width: 100%;
        height: 100%;
    }

    .modal-overlay {
        background-color: rgba(0, 0, 0, .1);

        width: 100%;
        height: 100%;
        display: flex;
        justify-content: center;
        align-items: center;
    }

    .modal-content {
        background-color: #fff;
        border: 1px solid #fff;
        border-radius: 5px;
        width: 80%;
        max-width: 900px;
        box-shadow: 0 1px 3px 0 rgba(0, 0, 0, 0.1), 0 1px 2px 0 rgba(0, 0, 0, 0.06);
        padding: 20px;
    }

    .close-button {
        width: 32px;
        background-color: transparent;
        border: none;
        margin-top: -8px;
    }

    .modal-header {
        display: flex;
        align-items: center;
        justify-content: space-between;

    }
</style>
