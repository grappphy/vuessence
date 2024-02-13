<template>
    <component
        @click="clickHandler"
        @mouseenter="mouseenterHandler"
        @mouseleave="mouseleaveHandler"
        @mousedown="mousedownHandler"
        @mouseup="mouseupHandler"
        :class="classes"
        :is="tag"
        :to="to"
        :href="href"
        :target="linkTarget"
        :disabled="isDisabled"
    >
        <!-- 슬롯: 아이콘-->
        <slot name="icon" :default-class="'vs-button-icon'">
            <vs-el-icon v-if="icon" class="vs-button-icon" :icon="icon" />
        </slot>

        <!-- 슬롯: 텍스트 -->
        <slot name="text" :default-class="'vs-button-text'">
            <vs-el-text v-if="text" class="vs-button-text" :tag="'span'" :content="text" />
        </slot>

        <!-- 슬롯: 화살표 -->
        <slot name="arrow" :default-class="'vs-button-arrow'">
            <vs-el-icon v-if="arrow" class="vs-button-arrow" :icon="arrow" />
        </slot>
    </component>
</template>

<script lang="ts">
import { defineComponent, computed } from "vue";

// Elements
import VsElText from "../text/el-text.vue";
import VsElIcon from "../icon/el-icon.vue";

export default defineComponent({
    name: "vs-el-button",
    components: {
        VsElText,
        VsElIcon
    },
    props: {
        /**
         * 태그
         *
         * @type {String}
         */
        tag: {
            type: String
        },
        /**
         * 유형
         *
         * @type {String}
         */
        type: {
            type: String
        },
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
         * 형태
         *
         * @type {String}
         */
        shape: {
            type: String
        },
        /**
         * 아이콘
         *
         * @type {String}
         */
        icon: {
            type: String
        },
        /**
         * 텍스트
         *
         * @type {String}
         */
        text: {
            type: String
        },
        /**
         * 화살표
         *
         * @type {String}
         */
        arrow: {
            type: String
        },
        /**
         * 링크 URL
         *
         * @type {String}
         */
        href: {
            type: String
        },
        /**
         * 라우터 링크 URL
         *
         * @type {String}
         */
        to: {
            type: String
        },
        /**
         * 링크 타겟
         *
         * @type {String}
         */
        linkTarget: {
            type: String
        },
        /**
         * 비활성화 상태
         *
         * @type {Boolean}
         */
        isDisabled: {
            type: Boolean
        }
    },
    setup(props, { emit }) {
        const classes = computed(() => {
            const defaultClass = "vs-button";

            const typeClass = props.type ? `${defaultClass}:${props.type}` : null;

            const sizeClass = props.size ? `${defaultClass}{${props.size}}` : null;

            const colorClass = props.color ? `vs-button{${props.color}}` : null;

            const shapeClass = props.shape ? `vs-button{${props.shape}}` : null;

            const disabledClass = props.isDisabled ? "is:disabled" : null;

            return [defaultClass, typeClass, sizeClass, colorClass, shapeClass, disabledClass];
        });

        function clickHandler(event: Event): void {
            emit("on-click", event);
        }

        function mouseenterHandler(event: Event): void {
            emit("on-mouseenter", event);
        }

        function mouseleaveHandler(event: Event): void {
            emit("on-mouseleave", event);
        }

        function mousedownHandler(event: Event): void {
            emit("on-mousedown", event);
        }

        function mouseupHandler(event: Event): void {
            emit("on-mouseup", event);
        }

        return {
            classes,

            clickHandler,
            mouseenterHandler,
            mouseleaveHandler,
            mousedownHandler,
            mouseupHandler
        };
    }
});
</script>
