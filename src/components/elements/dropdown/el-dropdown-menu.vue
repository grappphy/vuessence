<template>
    <vs-el-menu class="vs-dropdown-menu" :placement="placement">
        <template #body="{ defaultClass, listClass }">
            <div :class="['vs-dropdown-menu-body', defaultClass]">
                <div :class="['vs-dropdown-menu-list', listClass]">
                    <slot />
                </div>
            </div>
        </template>
    </vs-el-menu>
</template>

<script lang="ts">
import { defineComponent } from "vue";

// Elements
import VsElMenu from "../menu/el-menu.vue";

export default defineComponent({
    name: "vs-el-dropdown-menu",
    components: {
        VsElMenu
    },
    props: {
        /**
         * 배치
         *
         * @type {String}
         */
        placement: {
            type: String
        }
    }
});
</script>
