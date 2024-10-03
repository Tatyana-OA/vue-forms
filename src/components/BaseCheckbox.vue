<template>
  <div>
    <input
      type="checkbox"
      class="field"
      :checked="modelValue"
      @change="$emit('update:modelValue', $event.target.checked)"
      :id="uuid"
    />
    <label v-if="label" :for="uuid">{{ label }}</label>
  </div>
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
      type: Boolean,
      default: false
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
