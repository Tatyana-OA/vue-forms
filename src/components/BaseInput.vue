<template>
  <label v-if="label" :for="uuid">
    {{ label }}
  </label>
  <input
    class="field"
    v-bind="{
      ...$attrs,
      onInput: updateValue
    }"
    :id="uuid"
    :value="modelValue"
    :placeholder="label"
    :aria-describedby="error ? `${uuid}-error` : null"
    :aria-invalid="error ? true : false"
    :class="{ error }"
  />
  <BaseErrorMessage v-if="error" :id="`${uuid}-error`" className="errorMessage">
    {{ error }}
  </BaseErrorMessage>
</template>

<script>
import SetupFormComponent from '@/util/SetupFormComponent'
import UniqueID from '@/util/getID'
import BaseErrorMessage from './BaseErrorMessage.vue'

export default {
  props: {
    label: {
      type: String,
      default: ''
    },
    error: {
      type: String,
      default: ''
    },
    modelValue: {
      type: [String, Number],
      default: ''
    }
  },
  components: {
    BaseErrorMessage
  },
  setup(props, context) {
    const { updateValue } = SetupFormComponent(props, context)
    const uuid = UniqueID().getID()

    return {
      updateValue,
      uuid
    }
  }
}
</script>
