<template>
  <n-form
    label-placement="left"
    label-width="auto"
    :style="{
      maxWidth: '640px',
    }"
  >
    <n-form-item
      :label="t('commons.canUsePaidModel')"
      path="can_use_paid"
    >
      <n-switch
        v-model:value="limit.can_use_paid"
        placeholder=""
      />
    </n-form-item>
    <n-form-item
      :label="t('commons.canUseGPT4Model')"
      path="can_use_paid"
    >
      <n-switch
        v-model:value="limit.can_use_gpt4"
        placeholder=""
      />
    </n-form-item>
    <n-form-item
      :label="t('commons.maxConversationCount')"
      path="max_conv_count"
    >
      <n-input-number
        v-model:value="limit.max_conv_count"
        :parse="parseValue"
        :format="formatValue"
      />
    </n-form-item>
    <n-form-item
      :label="t('commons.availableAskCount')"
      path="available_ask_count"
    >
      <n-input-number
        v-model:value="limit.available_ask_count"
        :parse="parseValue"
        :format="formatValue"
      />
    </n-form-item>
    <n-form-item
      :label="t('commons.availableGPT4AskCount')"
      path="available_gpt4_ask_count"
    >
      <n-input-number
        v-model:value="limit.available_gpt4_ask_count"
        :parse="parseValue"
        :format="formatValue"
      />
    </n-form-item>
  </n-form>
</template>

<script setup lang="ts">
import { computed } from 'vue';

import { i18n } from '@/i18n';
import { LimitSchema } from '@/types/schema';

const t = i18n.global.t as any;

const props = defineProps<{
  limit: LimitSchema;
}>();

const emits = defineEmits(['update:limit']);

const limit = computed({
  get: () => props.limit,
  set: (value) => {
    emits('update:limit', value);
  },
});

const formatValue = (value: number | null) => (value == -1 ? t('commons.unlimited') : value);
const parseValue = (value: string) => (value == t('commons.unlimited') ? -1 : parseInt(value));

</script>
