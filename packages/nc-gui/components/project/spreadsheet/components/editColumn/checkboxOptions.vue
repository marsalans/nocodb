<template>
  <div>
    <div class="nc-rating-wrapper ui-type">
      <v-select
        v-model="colMeta.icon"
        label="Icon"
        :items="icons"
        dense
        outlined
        class="caption"
        :item-value="v=>v"
        :value-comparator="(a,b) => a && b && a.checked === b.checked && a.unchecked === b.unchecked"
      >
        <template #item="{ item }">
          <v-icon small :color="colMeta.color">
            {{ item.checked }}
          </v-icon>
          <v-icon class="ml-2" small :color="colMeta.color">
            {{ item.unchecked }}
          </v-icon>
        </template>
        <template #selection="{ item }">
          <v-icon small :color="colMeta.color">
            {{ item.checked }}
          </v-icon>
          <v-icon class="ml-2" small :color="colMeta.color">
            {{ item.unchecked }}
          </v-icon>
        </template>
      </v-select>
    </div>
    <v-color-picker
      v-model="colMeta.color"
      class="mx-auto"
      hide-inputs
    />
  </div>
</template>

<script>

export default {
  name: 'CheckboxOptions',
  props: ['column', 'meta', 'value'],
  data: () => ({
    colMeta: {
      icon: {
        checked: 'mdi-check-bold',
        unchecked: 'mdi-crop-square'
      },
      color: '#777'
    },
    icons: [{
      checked: 'mdi-check-bold',
      unchecked: 'mdi-crop-square'
    }, {
      checked: 'mdi-check-circle-outline',
      unchecked: 'mdi-checkbox-blank-circle-outline'
    }, {
      checked: 'mdi-star',
      unchecked: 'mdi-star-outline'
    }, {
      checked: 'mdi-heart',
      unchecked: 'mdi-heart-outline'
    }, {
      checked: 'mdi-moon-full',
      unchecked: 'mdi-moon-new'
    }, {
      checked: 'mdi-thumb-up',
      unchecked: 'mdi-thumb-up-outline'
    }, {
      checked: 'mdi-flag',
      unchecked: 'mdi-flag-outline'
    }]
  }),
  watch: {
    value() {
      this.colMeta = this.value || {}
    },
    colMeta(v) {
      this.$emit('input', v)
    }
  },
  created() {
    this.colMeta = this.value || { ...this.colMeta }
  }
}
</script>

<style scoped lang="scss">
.nc-rating-wrapper {
  display: flex;
  gap: 16px
}
</style>
