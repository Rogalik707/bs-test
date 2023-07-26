<template>
  <div class="navbar">
    <b
        v-for="item in list"
        :key="item.value"
        class="navbar__item"
        @click="changeOption(item)"
    >
      {{ item.label }} <arrow-down-icon class="navbar__arrow" :class="getArrowClass(item.value)"/>
    </b>
  </div>
</template>

<script>
import ArrowDownIcon from "@/components/icons/ArrowDownIcon";
export default {
  name: "CustomNavbar",
  components: {ArrowDownIcon},
  props: {
    selectedValue: {
      type: Object,
      required: true
    },
    list: {
      type: Array,
      required: true
    }
  },
  methods: {
    getArrowClass(value) {
      return value === this.selectedValue.sort && this.selectedValue.order === 'desc' ? 'navbar__arrow--rotate' : ''
    },
    changeOption(item){
      let order = 'desc'
      if (item.value === this.selectedValue.sort && this.selectedValue.order === 'desc') {
        order = 'asc'
      }
      this.$emit('change', { sort: item.value, order })
    },
  }
}
</script>

<style lang="scss" scoped>
.navbar {
  display: flex;
  background-color: #474955;
  margin-top: 15px;
  padding: 18px;
  &__item {
    cursor: pointer;
    padding-right: 120px;
    font-weight:  600;
    font-size: 14px;
    color: #FFFFFF;
  }
  &__item:last-child{
    padding-left: 290px;
  }

  &__arrow {
    margin-left: 10px;
    &--rotate {
      transform: rotate(180deg);
    }
  }
}
@media (max-width: 1234px) {
  .navbar {
    margin: 15px 34px 0 34px;
  }
}
</style>
