<template>
  <label v-if="label" :for="uuid">{{ label }}</label>
  <input
    :placeholder="label"
    class="field"
    :value="modelValue"
    @input="$emit('update:modelValue', $event.target.value)"
    v-bind="$attrs"
    :id="uuid"
  />
</template>

<script>
import UniqueID from '@/util/getID'
export default {
  props: {
    label: {
      type: String,
      default: ''
    },
    modelValue: {
      type: [String, Number],
      default: ''
    }
  },
  setup() {
    const uuid = UniqueID().getID()

    return {
      uuid
    }
  }
}
</script>
