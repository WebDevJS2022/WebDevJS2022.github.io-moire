<template>
    <aside class="filter">
        <form class="filter__form form" action="#" method="get">
            <fieldset class="form__block">
                <legend class="form__legend">Цена</legend>
                <label class="form__label form__label--price" for=" ">
                    <input class="form__input" name="min-price"
                    :value="priceFrom" @input="updateInput">
                    <span class="form__value">От</span>
                </label>
                <label class="form__label form__label--price" for=" ">
                    <input class="form__input" name="max-price"
                    :value="priceTo" @input="updateInput2">
                    <span class="form__value">До</span>
                </label>
            </fieldset>

            <fieldset class="form__block">
                <legend class="form__legend">Категория</legend>
                <label class="form__label form__label--select" for=" ">
                    <select class="form__select" name="category"
                    :value="categoryId" @input="updateInput3">
                        <option value="0">Все категории</option>
                        <option :value="category.id" v-for="category in categories"
                        :key="category.id">
                            {{ category.title }}</option>
                    </select>
                </label>
            </fieldset>

            <fieldset class="form__block">
                <legend class="form__legend">Материал</legend>
                <ul class="check-list">
                    <li class="check-list__item">
                        <label class="check-list__label" for=" ">
                            <input class="check-list__check sr-only"
                            type="checkbox" name="material" value="лен">
                            <span class="check-list__desc">
                                лен
                                <span>(3)</span>
                            </span>
                        </label>
                    </li>
                    <li class="check-list__item">
                        <label class="check-list__label" for=" ">
                            <input class="check-list__check sr-only"
                            type="checkbox" name="material" value="хлопок">
                            <span class="check-list__desc">
                                хлопок
                                <span>(46)</span>
                            </span>
                        </label>
                    </li>
                    <li class="check-list__item">
                        <label class="check-list__label" for=" ">
                            <input class="check-list__check sr-only"
                            type="checkbox" name="material" value="шерсть">
                            <span class="check-list__desc">
                                шерсть
                                <span>(20)</span>
                            </span>
                        </label>
                    </li>
                    <li class="check-list__item">
                        <label class="check-list__label" for=" ">
                            <input class="check-list__check sr-only"
                            type="checkbox" name="material" value="шелк">
                            <span class="check-list__desc">
                                шелк
                                <span>(30)</span>
                            </span>
                        </label>
                    </li>
                </ul>
            </fieldset>

            <fieldset class="form__block">
                <legend class="form__legend">Коллекция</legend>
                <ul class="check-list">
                    <li class="check-list__item">
                        <label class="check-list__label" for=" ">
                            <input class="check-list__check sr-only"
                            type="checkbox" name="collection" value="лето"
                                checked="">
                            <span class="check-list__desc">
                                лето
                                <span>(2)</span>
                            </span>
                        </label>
                    </li>
                    <li class="check-list__item">
                        <label class="check-list__label" for=" ">
                            <input class="check-list__check sr-only"
                            type="checkbox" name="collection" value="зима">
                            <span class="check-list__desc">
                                зима
                                <span>(53)</span>
                            </span>
                        </label>
                    </li>
                    <li class="check-list__item">
                        <label class="check-list__label" for=" ">
                            <input class="check-list__check sr-only"
                            type="checkbox" name="collection" value="весна">
                            <span class="check-list__desc">
                                весна
                                <span>(24)</span>
                            </span>
                        </label>
                    </li>
                    <li class="check-list__item">
                        <label class="check-list__label" for=" ">
                            <input class="check-list__check sr-only"
                            type="checkbox" name="collection" value="осень">
                            <span class="check-list__desc">
                                осень
                                <span>(30)</span>
                            </span>
                        </label>
                    </li>
                </ul>
            </fieldset>

            <button class="filter__submit button button--primery" type="submit">
                Применить
            </button>
            <button class="filter__reset button button--second" type="button">
                Сбросить
            </button>
        </form>
    </aside>
</template>

<script>
import categories from '@/data/categories';

export default {
  data() {
    return {
      currentPriceFrom: 0,
      currentPriceTo: 0,
      currentCategoryId: 0,
    };
  },
  props: ['priceFrom', 'priceTo', 'categoryId'],
  methods: {
    updateInput(event) {
      this.$emit('update:priceFrom', event.target.value);
    },
    updateInput2(event) {
      this.$emit('update:priceTo', event.target.value);
    },
    updateInput3(event) {
      this.$emit('update:categoryId', event.target.value);
    },
  },
  computed: {
    categories() {
      return categories;
    },
  },
};
</script>
