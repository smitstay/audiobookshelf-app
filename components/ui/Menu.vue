<template>
  <div class="relative" v-click-outside="clickOutside">
    <button type="button" class="relative w-full bg-fg border border-border rounded shadow-sm pl-3 pr-10 py-2 text-left focus:outline-none sm:text-sm cursor-pointer" aria-haspopup="listbox" aria-expanded="true" @click.stop.prevent="showMenu = !showMenu">
      <span class="flex items-center">
        <span class="block truncate">{{ label }}</span>
      </span>
      <span class="ml-3 absolute inset-y-0 right-0 flex items-center pr-2 pointer-events-none">
        <span class="material-symbols text-fg">person</span>
      </span>
    </button>

    <transition name="menu">
      <ul v-show="showMenu" class="absolute z-10 -mt-px w-full bg-primary border bordesr-border shadow-lg max-h-56 rounded-b-md py-1 text-base ring-1 ring-bg ring-opacity-5 overflow-auto focus:outline-none sm:text-sm" tabindex="-1" role="listbox" aria-activedescendant="listbox-option-3">
        <template v-for="item in items">
          <nuxt-link :key="item.value" v-if="item.to" :to="item.to">
            <li :key="item.value" class="text-fg select-none relative py-2" id="listbox-option-0" role="option" @click="clickedOption(item.value)">
              <div class="flex items-center">
                <span class="font-normal ml-3 block truncate font-sans">{{ item.text }}</span>
              </div>
            </li>
          </nuxt-link>
          <li v-else :key="item.value" class="text-fg select-none relative py-2" id="listbox-option-0" role="option" @click="clickedOption(item.value)">
            <div class="flex items-center">
              <span class="font-normal ml-3 block truncate font-sans">{{ item.text }}</span>
            </div>
          </li>
        </template>
      </ul>
    </transition>
  </div>
</template>

<script>
export default {
  props: {
    label: {
      type: String,
      default: 'Menu'
    },
    items: {
      type: Array,
      default: () => []
    }
  },
  data() {
    return {
      showMenu: false
    }
  },
  methods: {
    clickOutside() {
      this.showMenu = false
    },
    clickedOption(itemValue) {
      this.$emit('action', itemValue)
      this.showMenu = false
    }
  },
  mounted() {}
}
</script>
