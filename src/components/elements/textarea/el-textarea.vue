<template>
    <div :class="classes">
        <!-- 시작 -->
        <div class="vs-textarea-start">
            <!-- 슬롯: 시작 이전 -->
            <slot name="start-before" />

            <!-- 컨트롤 -->
            <textarea
                @keydown="controlKeydownHandler"
                @input="controlChangeHandler"
                @focus="controlFocusHandler"
                @blur="controlBlurHandler"
                ref="controlRef"
                class="vs-textarea-control"
                :value="value"
                :maxlength="maxlength"
                :placeholder="placeholder"
                :autocomplete="autocomplete"
                :autofocus="autofocus"
                :readonly="isReadonly"
                :disabled="isDisabled"
                :style="controlStyles"
            />

            <!-- 슬롯: 시작 이후 -->
            <slot name="start-after" />
        </div>

        <!-- 종료 -->
        <div v-if="useEnd" class="vs-textarea-end">
            <!-- 슬롯: 종료 이전 -->
            <slot name="end-before" />

            <!-- 클리어 버튼 -->
            <button v-if="useClear" @click="clearButtonClickHandler" class="vs-textarea-clear-button">
                <vs-el-icon :icon="clearIcon" />
                <span class="vs-a11y">클리어</span>
            </button>

            <!-- 슬롯: 종료 이후 -->
            <slot name="end-after" />
        </div>
    </div>
</template>

<script lang="ts">
import { defineComponent, ref, computed, Ref } from "vue";

// Elements
import VsElIcon from "../icon/el-icon.vue";

export default defineComponent({
    components: {
        VsElIcon
    },
    props: {
        // 유형
        type: {
            type: String
        },
        // 크기
        size: {
            type: String
        },
        // 유효성
        validation: {
            type: String
        },
        // 자동 완성
        autocomplete: {
            type: String
        },
        // 자동 포커스
        autofocus: {
            type: Boolean
        },
        // 값
        value: {
            type: String
        },
        // 플레이스홀더
        placeholder: {
            type: String
        },
        // 최대 길이
        maxlength: {
            type: Number
        },
        // 컨트롤 높이
        controlHeight: {
            type: Number
        },
        // 클리어 아이콘
        clearIcon: {
            type: String
        },
        // 종료 영역 사용 여부
        useEnd: {
            type: Boolean
        },
        // 클리어 사용 여부
        useClear: {
            type: Boolean
        },
        // 읽기 전용 상태
        isReadonly: {
            type: Boolean
        },
        // 비활성화 상태
        isDisabled: {
            type: Boolean
        }
    },
    setup(props, { emit }) {
        // 레퍼런스
        const controlRef: Ref<HTMLTextAreaElement> = ref(null);

        // 클래스
        const classes = computed(() => {
            const defaultClass = "vs-textarea";

            const typeClass = props.type ? `${defaultClass}:${props.type}` : null;

            const sizeClass = props.size ? `${defaultClass}{${props.size}}` : null;

            const validationsClass = props.validation ? `${defaultClass}{${props.validation}}` : null;

            const readonlyClass = props.isReadonly ? "is-readonly" : null;

            const disabledClass = props.isDisabled ? "is-disabled" : null;

            return [defaultClass, typeClass, sizeClass, validationsClass, readonlyClass, disabledClass];
        });

        // 컨트롤 스타일
        const controlStyles = computed(() => {
            return {
                height: `${props.controlHeight}px`
            };
        });

        // 컨트롤 키다운
        function controlKeydownHandler(event: Event): void {
            emit("vs-on-keydown", (event.target as HTMLFormElement)?.value, event);
        }

        // 컨트롤 변경
        function controlChangeHandler(event: Event): void {
            emit("vs-on-change", (event.target as HTMLFormElement)?.value, event);
        }

        // 컨트롤 포커스
        function controlFocusHandler(event: Event): void {
            emit("vs-on-focus", (event.target as HTMLFormElement)?.value, event);
        }

        // 컨트롤 블러
        function controlBlurHandler(event: Event): void {
            emit("vs-on-blur", (event.target as HTMLFormElement)?.value, event);
        }

        // 클리어 버튼 클릭
        function clearButtonClickHandler(event: Event): void {
            emit("vs-on-clear-button-click", (event.target as HTMLFormElement)?.value, event, controlRef.value);
        }

        return {
            controlRef,

            classes,
            controlStyles,

            controlKeydownHandler,
            controlChangeHandler,
            controlFocusHandler,
            controlBlurHandler,
            clearButtonClickHandler
        };
    }
});
</script>
