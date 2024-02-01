<script setup>
  import { computed, ref } from 'vue'
  import axios from 'axios';
  import Select2 from 'vue3-select2-component'

  // reactive state
  const petType = ref('')
  const petName = ref('')
  const selectedBreed = ref('')
  const selectedGender = ref('')
  let petBreed = ref([])
  const stored = ref(false)
  const storedMessage = ref('')

  const props = defineProps({
    headerImage: String
  })
  const image = computed(() => props.headerImage)
  axios.post(`/registration/breeds`)
      .then((a) => {
        petBreed.value = a.data
      })
      .catch(error => {
        console.log(error)
      })

  function store() {
    axios.post(
        '/registration/store',
        {
          petType: petType.value,
          petName: petName.value,
          selectedBreed: selectedBreed.value,
          selectedGender: selectedGender.value
        })
        .then(response => {
          storedMessage.value = response.data
          stored.value = true
          petType.value = ''
          petName.value = ''
          selectedBreed.value = ''
          selectedGender.value = ''
        })
        .catch(error => {
          console.log(error)
        })
  }

  function refresh() {
    stored.value = false
    storedMessage.value = ''
    location.reload();
  }
</script>
<template>
  <div class="registration-form-page col-sm-6">
    <img :src="`${props.headerImage}`" alt="registration" class="image">
    <div
        class="registration-form"
    >
      <div
          id="v-model-pet-type"
          class="pet-type"
          :class="{ 'd-none': stored }"
      >
        <p>Select your pet type</p>
        <label for="cat">
          <input
              type="radio"
              id="Cat"
              value="Cat"
              v-model="petType"
          />
          <span>Cat</span>
        </label>
        <br />
        <label for="dog">
          <input
              type="radio"
              id="Dog"
              value="Dog"
              v-model="petType"
          />
          <span>Dog</span>
        </label>
        <br />
        <span :class="{ 'd-none': !petType }">
          Pet type: {{ petType }}
        </span>
      </div>
      <div
          class="main-form"
          :class="{ 'd-none': !petType }"
      >
        <h4 class="form-title-question">Tell as about your {{ petType.toLowerCase() }}</h4>
        <div
            id="v-model-name"
            class="pet-name"
        >
          <p>What is your {{ petType.toLowerCase() }}'s name?</p>
          <input v-model="petName" type="text" placeholder="Name" />
        </div>
        <p>What Breed are they?</p>
        <div class="breed">
          <Select2
              v-model="selectedBreed"
              :options="petBreed[petType.toLowerCase()]"
              placeholder="Can't find it?"
              :setting="{
                selectOnClose: true,
              }"
          />
        </div>

        <div
            id="v-model-pet-breed"
            class="additional-pet-breed"
        >
          <p>Choose one</p>
          <label for="unknown-breed">
            <input
                type="radio"
                id="unknown-breed"
                value="unknown"
                v-model="selectedBreed"
            />
            <span>I don't know</span>
          </label>
          <br />
          <label for="mix">
            <input
                type="radio"
                id="mix"
                value="mix"
                v-model="selectedBreed"
            />
            <span>It's a mix</span>
          </label>
          <div
              id="v-model-mix"
              class="pet-mix"
              :class="{ 'd-none': selectedBreed !== 'mix' }"
          >
            <input
                v-model="selectedBreed"
                type="text"
                placeholder="Collie, poodle, lab"
            />
          </div>
        </div>
        <div class="pet-gender">
          <p>What gender are they?</p>
          <input
              type="radio"
              id="male"
              value="male"
              v-model="selectedGender"
          />
          <label
              for="male"
              class="label-male"
          >
            Male
          </label>
          <input
              type="radio"
              id="female"
              value="female"
              v-model="selectedGender"
          />
          <label
              for="female"
              class="label-female"
          >
            Female
          </label>
        </div>
        <div class="registration-button">
          <button @click="store">Continue</button>
        </div>
      </div>
      <div :class="{ 'd-none': stored === false }">
        <h4 class="form-title-question">{{ storedMessage }}</h4>
        <div class="refresh-registration-button">
          <button @click="refresh">Need to register a new pet?</button>
        </div>
      </div>
    </div>
  </div>
</template>

