<template>
  <div class="home">
    <img alt="Vue logo" src="../assets/logo.png">
    <h1>Adopt a Best Friend.</h1>
    <button @click="togglePetForm" class="btn btn-primary">Add New Pet</button>

    <b-form @submit.prevent="handleSubmit" v-if="showPetForm">
      <b-form-group id="petNameGroup" label="Pet's Name:" label-for="petName">
        <b-form-input id="petName" type="text" v-model="formData.name" required placeholder="Enter name"></b-form-input>
      </b-form-group>
      <b-form-group id="petSpeciesGroup" label="Species:" label-for="petSpecie">
        <b-form-select id="petSpecies" :options="['cats', 'dogs']" required v-model="formData.species"></b-form-select>
      </b-form-group>
      <b-form-group id="petAgeGroup" label="Pet's Age:" label-for="petAge">
        <b-form-input id="petAge" type="number" v-model="formData.edad" required placeholder="Enter age"></b-form-input>
      </b-form-group>
      <button class="btn btn-primary">Submit</button>
    </b-form>
  </div>
</template>

<script>
import { mapActions } from 'vuex'
export default {
  name: 'home',
  data () {
    return {
      showPetForm: false,
      formData: {
        name: '',
        edad: 0,
        species: null
      }
    }
  },
  methods: {
    ...mapActions([
      'addPet'
    ]),
    togglePetForm () {
      this.showPetForm = !this.showPetForm
    },
    handleSubmit () {
      const { species, edad, name } = this.formData
      const payload = {
        species,
        pet: {
          name,
          edad
        }
      }
      this.addPet(payload)
      this.formData = {
        name: '',
        edad: 0,
        species: null
      }
    }
  }
}
</script>
