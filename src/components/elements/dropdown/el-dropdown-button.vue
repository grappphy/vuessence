<template>
    <button @click="clickHandler" class="vs-dropdown-button" :disabled="isDisabled">
        <!-- 슬롯: 텍스트 -->
        <slot name="text" :default-class="'vs-dropdown-button-text'">
            <!-- 텍스트 -->
            <vs-el-text v-if="text" class="vs-dropdown-button-text" :tag="'span'" :content="text" />
        </slot>

        <!-- 슬롯: 아이콘 -->
        <slot name="icon" :default-class="'vs-dropdown-button-icon'">
            <!-- 아이콘 -->
            <vs-el-icon v-if="icon" class="vs-dropdown-button-icon" :icon="icon" />
        </slot>

        <!-- 슬롯: 화살표 -->
        <slot name="arrow" :default-class="'vs-dropdown-button-arrow'">
            <!-- 화살표 -->
            <vs-el-icon v-if="arrow" class="vs-dropdown-button-arrow" :icon="arrow" />
        </slot>
    </button>
</template>

<script lang="ts">
import { defineComponent } from "vue";

// Elements
import VsElIcon from "../icon/el-icon.vue";
import VsElText from "../text/el-text.vue";

export default defineComponent({
    name: "vs-el-dropdown-button",
    components: {
        VsElIcon,
        VsElText
    },
    props: {
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
         * 화살표
         *
         * @type {String}
         */
        arrow: {
            type: String
        },
        /**
         * 사용불가 상태
         *
         * @type {Boolean}
         */
        isDisabled: {
            type: Boolean
        }
    },
    setup(props, { emit }) {
        // 버튼 클릭
        function clickHandler(): void {
            emit("on-click");
        }

        return {
            clickHandler
        };
    }
});
</script>
