<template>
  <div>
    <h1>Create an event</h1>
    <form>
      <BaseSelect label="Select a category" :options="categories" v-model="event.category" />

      <h3>Name & describe your event</h3>

      <BaseInput label="Title" v-model="event.title" type="text" />

      <BaseInput label="Description" v-model="event.description" type="text" />

      <h3>Where is your event?</h3>

      <BaseInput label="Location" v-model="event.location" type="text" />

      <h3>Are pets allowed?</h3>

      <div>
        <BaseRadioGroup v-model="event.pets" name="pets" :options="petOptions" />
      </div>

      <h3>Extras</h3>
      <BaseCheckbox label="Catering" v-model="event.extras.catering" />

      <BaseCheckbox label="Live Music" v-model="event.extras.music" />
      <button type="submit">Submit</button>
    </form>
  </div>
</template>

<script>
import BaseCheckbox from './BaseCheckbox.vue'
import BaseInput from './BaseInput.vue'
import BaseRadioGroup from './BaseRadioGroup.vue'
import BaseSelect from './BaseSelect.vue'

export default {
  components: {
    BaseInput,
    BaseSelect,
    BaseCheckbox,
    BaseRadioGroup
  },
  data() {
    return {
      categories: [
        'sustainability',
        'nature',
        'animal welfare',
        'housing',
        'education',
        'food',
        'community'
      ],
      event: {
        category: '',
        title: '',
        description: '',
        location: '',
        pets: 1,
        extras: {
          catering: false,
          music: false
        }
      },
      petOptions: [
        { label: 'Yes', value: 1 },
        { label: 'No', value: 0 }
      ]
    }
  }
}
</script>
