<script setup>
const props = defineProps({
    id: {
        type: String,
        required: true,
    },
    size: {
        type: String,
        default: null,
    }
});

const emit = defineEmits(['closeModal']);
</script>

<template>
    <div class="modal fade" tabindex="-1" :id="props.id">
        <div class="modal-dialog" :class="props.size">
            <div class="modal-content">
                <div class="modal-header">
                    <slot name="title"></slot>

                    <!--begin::Close-->
                    <div class="btn btn-icon btn-sm btn-active-light-primary ms-2" @click="emit('closeModal')"
                        aria-label="Close">
                        <i class="ki-duotone ki-cross fs-1"><span class="path1"></span><span class="path2"></span></i>
                    </div>
                    <!--end::Close-->
                </div>

                <div class="modal-body">
                    <slot name="body"></slot>
                </div>

                <div class="modal-footer">
                    <slot name="footer"></slot>
                </div>
            </div>
        </div>
    </div>
</template>
