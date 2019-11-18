<template>
    <div id="app">
        <img class="mx-auto mb-12" alt="Vue logo" src="./assets/logo.png">

        <div class="mb-12">
            <button @click.prevent="showModal = true" type="button" class="bg-gray-400 p-4 rounded">
                show modal
            </button>
            <modal v-if="showModal" @close="showModal = false">
                <h3 slot="title">Modal Title</h3>
                <div slot="body">
                    <p>this is the modal body</p>
                </div>
            </modal>
        </div>

        <div>
            <show-hide trigger-class="bg-gray-400 p-4 rounded" content-class="absolute bg-white shadow-lg px-8 py-6 rounded w-64">
                <div slot="content">
                    Show Hide Content
                </div>
            </show-hide>
        </div>

    </div>
</template>

<script>
    import Modal    from './components/Modal';
    import ShowHide from "./components/ShowHide";

    export default {
        name      : 'app',
        components: { ShowHide, Modal },

        data() {
            return {
                showModal: false,
            }
        },


    }
</script>

<style>
    #app {
        font-family: 'Avenir', Helvetica, Arial, sans-serif;
        -webkit-font-smoothing: antialiased;
        -moz-osx-font-smoothing: grayscale;
        text-align: center;
        color: #2c3e50;
        margin-top: 60px;
    }


    /***************************
    ******* Transitions ********
    ***************************/

    .fade-down-enter-active,
    .fade-down-leave-active,
    .fade-enter-active,
    .fade-leave-active {
        transition: all 225ms ease-in-out;
    }

    .fade-down-enter,
    .fade-down-leave-to {
        opacity: 0;
        transform: translateY(-50px);
    }

    .fade-enter,
    .fade-leave-to {
        opacity: 0;
    }

    .fade-scale-enter-active, .fade-scale-leave-active {
        transition: all 500ms ease;
        transform-origin: center;
    }

    .fade-scale-enter, .fade-scale-leave-to {
        transition: all 500ms ease;
        opacity: 0;
        transform-origin: center;
        transform: scale(1.05);
    }

</style>
