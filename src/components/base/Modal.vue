<template>
    <aside>
        <div v-if="show" class="w-full h-full fixed top-0 left-0 bg-black opacity-75 cursor-pointer z-[1000]" @click="tryClose"></div>
        <transition name="modal">
            <dialog
                class="z-[1001] w-full p-0 shadow-sm max-h-full top-20 overflow-hidden fixed bg-white md:w-1/2 alert-modal right-0 left-0 mx-auto rounded-lg"
                v-if="show"
                open
            >
                <slot></slot>
            </dialog>
        </transition>
    </aside>
</template>

<script>
export default {
    props: {
        show: {
            type: Boolean,
            required: true
        }
    },
    emits: ["close"],
    methods: {
        tryClose() {
            this.$emit("close");
        }
    }
};
</script>

<style scoped>
/* 
dialog {
    top: 20vh;
    left: 10%;
} */

.modal-enter-active {
    animation: modal 0.3s ease-out;
}

.modal-leave-active {
    animation: modal 0.3s ease-in reverse;
}
.body {
    max-height: 450px;
    overflow-y: auto;
}

@keyframes modal {
    from {
        opacity: 0;
        transform: translateY(-50px) scale(0.9);
    }

    to {
        opacity: 1;
        transform: translateY(0) scale(1);
    }
}
@media (max-width: 767px) {
    /* dialog {
        top: 5%;
    } */
    /* .body {
        max-height: 320px;
    } */
    /* .modal-body, .user-image-modal .modal-footer,.user-image-modal .modal-footer {
        width: 100%!important;
    } */
}
</style>
