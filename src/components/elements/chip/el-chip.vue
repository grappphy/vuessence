<template>
    <span :class="classes">
        <component
            v-if="useButton"
            @click="clickHandler"
            class="vs-chip-button"
            :is="tag"
            :to="to"
            :href="href"
            :target="linkTarget"
            :disabled="isDisabled"
        >
            <vs-el-a11y :text="text" />
        </component>

        <!-- 슬롯: 아이콘 -->
        <slot name="icon" :default-class="'vs-chip-icon'">
            <vs-el-icon v-if="icon" class="vs-chip-icon" :icon="icon" />
        </slot>

        <!-- 슬롯: 텍스트 -->
        <slot name="text" :default-class="'vs-chip-text'">
            <vs-el-text v-if="text" class="vs-chip-text" :tag="'span'" :content="text" />
        </slot>

        <!-- 슬롯: 삭제 -->
        <slot name="delete" :default-class="'vs-chip-delete'">
            <button v-if="useDelete" @click="deleteHandler" class="vs-chip-delete">
                <vs-el-icon :icon="deleteIcon" />
                <vs-el-a11y :text="'삭제'" />
            </button>
        </slot>
    </span>
</template>

<script lang="ts">
import { defineComponent, computed } from "vue";

// Elements
import VsElIcon from "../icon/el-icon.vue";
import VsElText from "../text/el-text.vue";
import VsElA11y from "../a11y/el-a11y.vue";

export default defineComponent({
    name: "vs-el-chip",
    components: {
        VsElIcon,
        VsElText,
        VsElA11y
    },
    props: {
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
         * 태그
         *
         * @type {String}
         */
        tag: {
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
         * 아이콘
         *
         * @type {String}
         */
        icon: {
            type: String
        },
        /**
         * 삭제 아이콘
         *
         * @type {String}
         */
        deleteIcon: {
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
         * 버튼 사용 여부
         *
         * @type {Boolean}
         */
        useButton: {
            type: Boolean
        },
        /**
         * 삭제 사용 여부
         *
         * @type {Boolean}
         */
        useDelete: {
            type: Boolean
        },
        /**
         * 읽기전용 상태
         *
         * @type {Boolean}
         */
        isReadonly: {
            type: Boolean
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
        // 클래스
        const classes = computed(() => {
            const defaultClass = "vs-chip";

            const typeClass = props.type ? `${defaultClass}<${props.type}>` : null;

            const sizeClass = props.size ? `${defaultClass}{${props.size}}` : null;

            const readonlyClass = props.isReadonly ? `${defaultClass}:readonly` : null;

            const disabledClass = props.isDisabled ? `${defaultClass}:disabled` : null;

            return [defaultClass, typeClass, sizeClass, readonlyClass, disabledClass];
        });

        // 클릭
        function clickHandler(event: Event): void {
            emit("on-click", event);
        }

        // 삭제
        function deleteHandler(event: Event): void {
            emit("on-delete", event);
        }

        return {
            classes,

            clickHandler,
            deleteHandler
        };
    }
});
</script>
