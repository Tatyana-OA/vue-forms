<template>
  <label v-if="label" :for="uuid">
    {{ label }}
  </label>
  <select
    class="field"
    v-bind="{
      ...$attrs,
      onChange: updateValue
    }"
    :value="modelValue"
    :id="uuid"
    :aria-describedby="error ? `${uuid}-error` : null"
    :aria-invalid="error ? true : false"
    :class="{ error }"
  >
    <option
      v-for="option in options"
      :value="option"
      :key="option"
      :selected="option === modelValue"
    >
      {{ option }}
    </option>
  </select>
  <BaseErrorMessage v-if="error" :id="`${uuid}-error`">
    {{ error }}
  </BaseErrorMessage>
</template>

<script>
import UniqueID from '@/util/getID'
import SetupFormComponent from '@/util/SetupFormComponent'
import BaseErrorMessage from './BaseErrorMessage.vue'

export default {
  props: {
    options: {
      type: Array,
      required: true
    },
    label: {
      type: String,
      default: ''
    },
    error: {
      type: String,
      default: ''
    },
    modelValue: {
      type: [String, Number]
    }
  },
  setup(props, context) {
    const { updateValue } = SetupFormComponent(props, context)
    const uuid = UniqueID().getID()

    return {
      updateValue,
      uuid
    }
  },
  components: {
    BaseErrorMessage
  }
}
</script>
