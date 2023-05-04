<template>
<ul class="catalog__pagination pagination">
          <li class="pagination__item">
            <button class="pagination__link pagination__link--arrow"
            :disabled="modelValue === 1" aria-label="Предыдущая страница"
            @click.prevent="prevPage()">
              <svg width="8" height="14" fill="currentColor">
                <use xlink:href="#icon-arrow-left"></use>
              </svg>
            </button>
          </li>
          <li class="pagination__item" v-for="pageNumber in pages" :key="pageNumber">
            <a href="#" class="pagination__link"
            :class="{'pagination__link--current': pageNumber === modelValue}"
            @click.prevent="paginate(pageNumber)">
              {{ pageNumber }}
            </a>
          </li>
          <li class="pagination__item">
            <button class="pagination__link pagination__link--arrow"
            :disabled="modelValue === 4" href="#" aria-label="Следующая страница"
            @click.prevent="nextPage()">
              <svg width="8" height="14" fill="currentColor">
                <use xlink:href="#icon-arrow-right"></use>
              </svg>
            </button>
          </li>
        </ul>
</template>

<script>
export default {
//   model: {
//     prop: 'modelValue', // свойство
//     event: 'paginate', // событие
//   },
  props: ['modelValue', 'count', 'perPage'],
  computed: {
    pages() { // количество страниц
      return Math.ceil(this.count / this.perPage);
    },
  },
  methods: {
    paginate(modelValue) {
      this.$emit('update:modelValue', modelValue);
    },
    nextPage() {
      this.$emit('update:modelValue', (this.modelValue + 1));
    },
    prevPage() {
      this.$emit('update:modelValue', (this.modelValue - 1));
    },
  },
};
</script>
