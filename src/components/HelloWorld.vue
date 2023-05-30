<script setup>
import { ref, toRefs, onMounted } from 'vue';
import { createPopup } from '@picmo/popup-picker';

const props = defineProps({
    postId: {
        type: Number,
        required: false,
    },
    replyInfo: {
        type: Object,
        default: null,
    },
    showInputPadding: {
        type: Boolean,
        default: true,
    },
});
const postId  = 1;
const emit = defineEmits(['on-comment-added', 'cancel-reply', 'emoji:select']);

const picker = ref();
function togglePicker() {
    console.log('togglePicker');
    picker.value.toggle();
}
const emojiButtonId = `emoji-button-${postId.value}`;
console.dir(emojiButtonId);
onMounted(() => {
    const triggerButton = document.getElementById(`#${emojiButtonId}`);
    console.dir(triggerButton);
    // Create the picker
    picker.value = createPopup(
        {},
        {
            isOpen: true,
            // The element that triggers the popup
            triggerElement: triggerButton,
            // The element to position the picker relative to - often this is also the trigger element,
            referenceElement: triggerButton,
            position: 'auto',
            showCloseButton: false,
        },
    );
    // The picker emits an event when an emoji is selected. Do with it as you will!
    picker.value.addEventListener('emoji:select', (event) => {
        console.log('Emoji selected:', event.emoji);
    });
});

</script>

<template>
  <div>
    <div :class="$style.component">
            <div :class="$style.inputComment">
                <input
                    type="text"
                    :placeholder="write_comment"
                    maxlength="250"
                    :class="$style.inputClass"
                >

                <button
                    :id="emojiButtonId"
                    :class="emojiBnt"
                    type="button"
                    @click="togglePicker"
                >
                    <img
                        src="images/icons/chat/icon_emoji.svg"
                        alt="emoji"
                    >
                </button>
            </div>
            <button @click="() => addComment()">
                <img
                    src="images/icons/comments/send.svg"
                    alt="Send message"
                >
            </button>
    </div>
  </div>
</template>

<style lang="scss" module>
.component {
    margin: 0;
    display: flex;
    flex-direction: column;
    justify-content: end;
    gap: 4px;
    height: 100%;

    button {
        background: transparent;
        padding: 0;
        outline: none;
        border: none;
    }

    .replyToContainer {
        padding: 4px 24px;
        display: flex;
        justify-content: space-between;
        background: rgba(247, 179, 43, 0.2);

        .replyUser {
            span {
                font-weight: 400;
                font-size: 14px;
                line-height: 19px;
                color: #343840;
            }

            img {
                margin-right: 4px;
                width: 16px;
                height: 16px;
            }
        }

        .cancelBtn {
            span {
                font-weight: 500;
                font-size: 14px;
                line-height: 19px;
                color: #343840;
            }

            img {
                margin-left: 4px;
                width: 16px;
                height: 16px;
            }
        }
    }

    .inputContainer {
        display: flex;
        flex-direction: row;
        justify-content: center;
        align-items: center;
        gap: 16px;

        &.inputMargin {
            margin: 0 16px 0 16px;
        }

        .inputComment {
            flex: none;
            order: 0;
            flex-grow: 1;
            border: 1px solid rgba(52, 56, 64, 0.2);
            border-radius: 100px;
            padding: 12px 1px;
            font-weight: 400;
            font-size: 16px;
            line-height: 24px;
            color: #343840;
            position: relative;
        }

        .inputComment:focus {
            outline: none;
            border: 1px solid rgba(52, 56, 64, 0.3);
        }

        .inputComment::placeholder {
            color: rgba(52, 56, 64, 0.5);
        }

        input {
            margin-left: 10px;
            border: none;
        }
        input:focus {
            outline: none;
        }
        .emojiBnt{
            position: absolute;
            padding-right: 20px;
            right: 0px;
            margin-left: 10px;
        }
        .inputClass{
            border-style: none;
            width: 90%;
            padding-left: 10px;
            padding-right: 15px;
        }

    }
}
</style>

