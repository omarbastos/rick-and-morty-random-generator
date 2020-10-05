<template>
  <div class="container portal mt-12">
    <div class="bg-gray-900 shadow overflow-hidden sm:rounded-lg">
      <div class="px-4 py-5 border-b border-gray-200 sm:px-6">
        <div class="flex items-baseline justify-center">
          <span :class="statusClass(character.status)">
            {{ character.status }}</span
          >
          <div
            class="text-3xl leading-6 font-medium text-gray-200 text-center my-4"
          >
            {{ character.name }}
          </div>
        </div>
        <div class="container justify-center flex">
          <img
            class="h-52 w-52 object-center rounded-full border-2 border-gray-100"
            :src="character.image"
            :alt="character.name"
          />
        </div>
      </div>
      <div>
        <dl>
          <div
            class="bg-gray-50 px-4 py-5 sm:grid sm:grid-cols-3 sm:gap-4 sm:px-6"
          >
            <dt class="text-xl leading-5 font-medium text-gray-500 text-center">
              <div class="tooltip">
                Species
                <span
                  class="tooltip-text text-sm bg-green-500 p-3 mt-1 lg:mt-8 text-white rounded"
                  >The species of the character.</span
                >
              </div>
            </dt>
            <dd
              class="mt-1 text-xl leading-5 text-gray-500 sm:mt-0 sm:col-span-2 text-center"
            >
              {{
                character.species && character.species.length > 0
                  ? character.species
                  : 'N/A'
              }}
            </dd>
          </div>
          <div
            class="bg-gray-50 px-4 py-5 sm:grid sm:grid-cols-3 sm:gap-4 sm:px-6"
          >
            <dt class="text-xl leading-5 font-medium text-gray-500 text-center">
              <div class="tooltip">
                Type
                <span
                  class="tooltip-text text-sm bg-green-500 p-3 mt-1 lg:mt-8 text-white rounded"
                  >The type or subspecies of the character.</span
                >
              </div>
            </dt>
            <dd
              class="mt-1 text-xl leading-5 text-gray-500 sm:mt-0 sm:col-span-2 text-center"
            >
              {{
                character.type && character.type.length > 0
                  ? character.type
                  : 'N/A'
              }}
            </dd>
          </div>
          <div
            class="bg-gray-50 px-4 py-5 sm:grid sm:grid-cols-3 sm:gap-4 sm:px-6"
          >
            <dt class="text-xl leading-5 font-medium text-gray-500 text-center">
              <div class="tooltip">
                Gender
                <span
                  class="tooltip-text text-sm bg-green-500 p-3 mt-1 lg:mt-8 text-white rounded"
                  >The gender of the character ('Female', 'Male', 'Genderless'
                  or 'unknown').</span
                >
              </div>
            </dt>
            <dd
              class="mt-1 text-xl leading-5 text-gray-500 sm:mt-0 sm:col-span-2 text-center"
            >
              <span :class="genderClass(character.gender)">
                {{ character.gender }}</span
              >
            </dd>
          </div>
          <div
            class="bg-gray-50 px-4 py-5 sm:grid sm:grid-cols-3 sm:gap-4 sm:px-6"
          >
            <dt class="text-xl leading-5 font-medium text-gray-500 text-center">
              <div class="tooltip">
                Origin
                <span
                  class="tooltip-text text-sm bg-green-500 p-3 mt-1 lg:mt-8 text-white rounded"
                  >Character's origin location.</span
                >
              </div>
            </dt>
            <dd
              class="mt-1 text-xl capitalize leading-5 text-gray-500 sm:mt-0 sm:col-span-2 text-center"
            >
              {{
                character.origin &&
                character.origin.name &&
                character.origin.name.length > 0
                  ? character.origin.name
                  : 'N/A'
              }}
            </dd>
          </div>
          <div
            class="bg-gray-50 px-4 py-5 sm:grid sm:grid-cols-3 sm:gap-4 sm:px-6"
          >
            <dt class="text-xl leading-5 font-medium text-gray-500 text-center">
              <div class="tooltip">
                Last Known Location
                <span
                  class="tooltip-text text-sm bg-green-500 p-3 mt-1 lg:mt-8 text-white rounded"
                  >Character's last known location endpoint.</span
                >
              </div>
            </dt>
            <dd
              class="mt-1 text-xl capitalize leading-5 text-gray-500 sm:mt-0 sm:col-span-2 text-center"
            >
              {{
                character.location &&
                character.location.name &&
                character.location.name.length > 0
                  ? character.location.name
                  : 'N/A'
              }}
            </dd>
          </div>
        </dl>
      </div>
    </div>
  </div>
</template>

<script lang="ts">
import { Vue, Component, Prop } from 'nuxt-property-decorator'

// Define the component in class-style
@Component
export default class RandomCharacter extends Vue {
  // Class properties will be component data
  character = []
  MAX = 671
  async fetch() {
    this.character = await fetch(
      `https://rickandmortyapi.com/api/character/${this.randomNumber()}`
    ).then((res) => res.json())
  }
  randomNumber(): number {
    return Math.floor(Math.random() * this.MAX) + 1
  }
  // Methods will be component methods

  statusClass(status: string): string {
    switch (status) {
      case 'Alive':
        return `inline-block bg-green-500 mx-2 text-green-100 text-xl px-2 rounded-full uppercase font-semibold tracking-wide`
      case 'Dead':
        return `inline-block bg-red-700 mx-2 text-red-100 text-xl px-2 rounded-full uppercase font-semibold tracking-wide`
      case 'unknown':
        return `inline-block bg-blue-700 mx-2 text-blue-100 text-xl px-2 rounded-full uppercase font-semibold tracking-wide`
      default:
        return `inline-block bg-blue-700 mx-2 text-blue-100 text-xl px-2 rounded-full uppercase font-semibold tracking-wide`
    }
  }
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
/* Sample `apply` at-rules with Tailwind CSS
.container {
@apply min-h-screen flex justify-center items-center text-center mx-auto;
}
*/

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
