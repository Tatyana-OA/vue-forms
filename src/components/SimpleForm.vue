<template>
  <div>
    <h1>Create an event</h1>
    <form @submit.prevent="sendForm">
      <BaseSelect
        label="Select a category"
        :options="categories"
        v-model="event.category"
        name="select"
      />

      <fieldset>
        <legend>Name & describe your event</legend>

        <BaseInput label="Title" v-model="event.title" type="text" />

        <BaseInput label="Description" v-model="event.description" type="text" />
      </fieldset>

      <fieldset>
        <legend>Where is your event?</legend>

        <BaseInput label="Location" v-model="event.location" type="text" />
      </fieldset>

      <fieldset>
        <legend>Pets</legend>
        <p>Are pets allowed?</p>

        <div>
          <BaseRadioGroup v-model="event.pets" name="pets" :options="petOptions" />
        </div>
      </fieldset>

      <fieldset>
        <legend>Extras</legend>
        <BaseCheckbox label="Catering" v-model="event.extras.catering" />

        <BaseCheckbox label="Live Music" v-model="event.extras.music" />
      </fieldset>

      <button type="submit">Submit</button>
    </form>
  </div>
</template>

<script>
import axios from 'axios'
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
  },
  methods: {
    sendForm() {
      //  Mock Requests to: https://my-json-server.typicode.com/Code-Pop/Vue-3-Forms/
      axios
        .post('https://my-json-server.typicode.com/Code-Pop/Vue-3-Forms/events', this.event)
        .then((res) => console.log('Response: ', res))
        .catch((err) => console.log('Error: ', err))
    }
  }
}
</script>

<style>
fieldset {
  border: 0;
  margin: 0;
  padding: 0;
}

legend {
  font-size: 28px;
  font-weight: 700;
  margin-top: 20px;
}
</style>
