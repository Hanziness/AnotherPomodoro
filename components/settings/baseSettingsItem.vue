<template>
  <settings-resolver :settings-key="settingsKey" :custom-value="customValue" :custom-set-function="customSetFunction">
    <base-settings-item-bare
      slot-scope="{ value, update, error, lastError, translationKey }"
      :disabled="disabled"
      :settings-key="settingsKey"
      :settings-value="value"
      :error-value="lastError"
      :translation-key="translationKey"
    >
      <template #content-action="{ settingsValue }">
        <slot
          name="content-action"
          :settingsValue="settingsValue"
          :update="update"
          :error="error"
          :lastError="lastError"
        />
      </template>

      <template #content-main="{ settingsValue }">
        <slot
          name="content-main"
          :settingsValue="settingsValue"
          :translation-key="translationKey"
          :values="values"
          :selected="settingsValue"
          :update="update"
        />
      </template>
    </base-settings-item-bare>
  </settings-resolver>
</template>

<script>
import settingsInputMixin from '@/assets/mixins/settings/settingsItemBase'

export default {
  components: {
    SettingsResolver: () => import(/* webpackMode: "eager" */ '@/components/settings/renderlessSettingsResolver.vue'),
    BaseSettingsItemBare: () => import(/* webpackMode: "eager" */ '@/components/settings/baseSettingsItemBare.vue')
  },

  mixins: [settingsInputMixin],

  props: {
    values: {
      type: Object,
      default: () => {}
    },

    customValue: {
      type: [Number, String, Object],
      default: undefined
    }
  }
}
</script>
