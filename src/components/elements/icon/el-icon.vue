<template>
    <i :class="classes">
        <slot />
    </i>
</template>

<script lang="ts">
import { defineComponent, computed } from "vue";

export default defineComponent({
    name: "vs-el-icon",
    props: {
        /**
         * 크기
         *
         * @type {String}
         */
        size: {
            type: String
        },
        /**
         * 색상
         *
         * @type {String}
         */
        color: {
            type: String
        },
        /**
         * 아이콘
         *
         * @type {string}
         */
        icon: {
            type: String
        }
    },
    setup(props) {
        const classes = computed(() => {
            const defaultClass = "vs-icon";

            const sizeClass = props.size ? `vs-icon{${props.size}}` : null;

            const colorClass = props.color ? `vs-color{${props.color}}` : null;

            const iconClass = props.icon ? props.icon : null;

            return [defaultClass, sizeClass, colorClass, iconClass];
        });

        return {
            classes
        };
    }
});
</script>
