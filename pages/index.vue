<template>
  <div class="container">
    <div
      v-for="(character, index) in characters"
      :key="index"
      class="my-12 justify-center w-full lg:max-w-full lg:flex"
    >
      <div
        class="h-48 lg:h-auto lg:w-48 flex-none bg-cover rounded-t lg:rounded-t-none lg:rounded-l text-center overflow-hidden"
        :style="`background-image: url('${character.image}')`"
        :title="character.name"
      ></div>
      <div
        class="lg:w-1/3 sm:w-4/5 bg-gray-900 border-r border-b border-l border-gray-900 lg:border-l-0 lg:border-t lg:border-gray-900 bg-white rounded-b lg:rounded-b-none lg:rounded-r p-4 flex flex-col justify-between leading-normal"
      >
        <div class="mb-8">
          <div class="text-center text-yellow-400 font-bold text-2xl mb-2">
            <span :class="statusClass(character.status)">
              {{ character.status }}</span
            >
            {{ character.name }}
          </div>
          <p class="py-2 text-lg text-white font-semibold">
            Gender: {{ character.gender }}<br />
            Type:
            {{
              character.type && character.type.length > 0
                ? character.type
                : 'N/A'
            }}<br />
            Species:
            {{
              character.species && character.species.length > 0
                ? character.species
                : 'N/A'
            }}<br />
            <!--   First seen in:
            {{ character.episode[0] }}
            <br /> -->
          </p>
        </div>
      </div>
    </div>
    <div class="flex justify-center my-12">
      <button
        @click="getCharacters"
        class="mx-auto bg-green-500 hover:bg-green-400 text-white font-bold py-2 px-4 hover:border-green-500 rounded text-2xl"
      >
        Get new Random Characters!
      </button>
    </div>
  </div>
</template>

<script lang="ts">
import { Vue, Component, Prop } from 'nuxt-property-decorator'

// Define the component in class-style
@Component
export default class RandomCharacter extends Vue {
  // Class properties will be component data
  characters = []
  MAX = 671

  //Initial Fetch
  async fetch() {
    await this.getCharacters()
  }
  // Get Characters from API
  async getCharacters() {
    this.characters = await fetch(
      `https://rickandmortyapi.com/api/character/${this.randomNumbers()}`
    ).then((res) => res.json())
  }
  //Get Random Numbers from 1 to MAX
  randomNumbers(): number[] {
    return [
      Math.floor(Math.random() * this.MAX) + 1,
      Math.floor(Math.random() * this.MAX) + 1,
      Math.floor(Math.random() * this.MAX) + 1,
    ]
  }
  // Methods will be component methods
  // Switch Case for Status, getting right color
  statusClass(status: string): string {
    switch (status) {
      case 'Alive':
        return `inline-block bg-green-500 mx-2 text-green-100 px-2 rounded-full  font-semibold tracking-wide`
      case 'Dead':
        return `inline-block bg-red-700 mx-2 text-red-100 px-2 rounded-full  font-semibold tracking-wide`
      case 'unknown':
        return `inline-block bg-blue-700 mx-2 text-blue-100  px-2 rounded-full  font-semibold tracking-wide`
      default:
        return `inline-block bg-blue-700 mx-2 text-blue-100 px-2 rounded-full  font-semibold tracking-wide`
    }
  }
  //Switch Case for Gender
  genderClass(gender: string): string {
    switch (gender) {
      case 'Female':
        return `inline-block bg-pink-200  text-black  px-2 rounded-full uppercase font-semibold tracking-wide`
      case 'Male':
        return `inline-block bg-blue-700 text-blue-100  px-2 rounded-full uppercase font-semibold tracking-wide`
      case 'Genderless':
        return `inline-block bg-green-700 text-green-100 px-2 rounded-full uppercase font-semibold tracking-wide`
      case 'unknown':
        return `inline-block bg-yellow-500 text-black  px-2 rounded-full uppercase font-semibold tracking-wide`
      default:
        return `inline-block bg-yellow-500 text-black  px-2 rounded-full uppercase font-semibold tracking-wide`
    }
  }
}
</script>

<style>
.tooltip .tooltip-text {
  visibility: hidden;
  text-align: center;
  padding: 2px 6px;
  position: absolute;
  z-index: 100;
}
.tooltip:hover .tooltip-text {
  visibility: visible;
}
</style>
