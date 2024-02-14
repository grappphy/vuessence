<template>
    <vs-el-menu-item :class="classes">
        <slot />
    </vs-el-menu-item>
</template>

<script lang="ts">
import { computed, defineComponent } from "vue";

// Elements
import VsElMenuItem from "../menu/el-menu-item.vue";

export default defineComponent({
    name: "vs-el-dropdown-menu-item",
    components: {
        VsElMenuItem
    },
    props: {
        /**
         * 활성화 상태
         *
         * @type {Boolean}
         */
        isActive: {
            type: Boolean
        }
    },
    setup(props) {
        const classes = computed(() => {
            const defaultClass = "vs-dropdown-menu-item";

            const activeClass = props.isActive ? `${defaultClass}:active` : null;

            return [defaultClass, activeClass];
        });

        return {
            classes
        };
    }
});
</script>
