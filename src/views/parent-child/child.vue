<script setup>
import { useLockScreen } from 'viy-ui';
import { useI18n } from 'vue-i18n';

const props = defineProps(['lastNameParent', 'parentInput']);
const emit = defineEmits(['onChildEmit']);
const { t } = useI18n();
const lockScreenUtils = useLockScreen();
const lockScreen = lockScreenUtils.lockScreen;

defineOptions({
  name: 'child',
});

const form = ref();
const childfield = ref();
const receiveBtn = ref();
const sendBtn = ref();

const formData = reactive({
  childTextInput: '',
});

const receiveBtnClick = () => {
  getValueFromParent();
};
const sendBtnClick = () => {
  sendValueFromChild();
};

function getValueFromParent() {
  console.log(props);
  console.log(props.lastNameParent);
  console.log(props.parentInput);
}

function sendValueFromChild() {
  emit('onChildEmit', formData.childTextInput);
}
</script>

<template>
  <VueForm ref="form" v-loading="lockScreen" :model="formData">
    <VueFormItem

      label="Child Input"

      prop="childTextInput"
    >
      <VueInput

        id="childfield"

        ref="childfield"
        v-model="formData.childTextInput"

        data-type="string"
      />
    </VueFormItem>

    <VueButton id="receiveBtn" ref="receiveBtn" icon-position="left" @click="receiveBtnClick">
      Get Value From Parent
    </VueButton>
    <VueButton id="sendBtn" ref="sendBtn" icon-position="left" @click="sendBtnClick">
      Send Value From Child
    </VueButton>
  </VueForm>
</template>
