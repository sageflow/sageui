<template lang="pug">
aside#activity-bar
  //- Brand.
  .brand
    brand-image
    //- img(src="~@/assets/images/avatar-gigamono.svg" alt="gigamono brand image")

  .layout-divider

  //- Main shortcuts.
  ul.main-shortcuts
    li(v-for="shortcut in mainShortcuts")
      activity-bar-shortcut.activity-bar-shortcut(:iconName="shortcut.iconName", :route="shortcut.route")

  .layout-divider

  //- Spaces shortcuts.
  ul.space-shortcuts
    //- li(v-for="")

  .layout-divider

  //- Other system shorrtcuts.
  ul.other-shortcuts
    li(v-for="shortcut in otherShortcuts")
      activity-bar-shortcut.activity-bar-shortcut(:iconName="shortcut.iconName", :route="shortcut.route")
</template>

<script>
  import BrandImage from "@/components/ui/BrandImage"
  import ActivityBarShortcut from "@/components/layout/ActivityBarShortcut"
  import { reactive, computed, toRefs } from "vue"
  import store from "@/store"

  export default {
    components: {
      BrandImage,
      ActivityBarShortcut,
    },
    setup() {
      const event = reactive({
        mainShortcuts: computed(() => store.getters["user/mainShortcuts"]),
        otherShortcuts: computed(() => store.getters["user/otherShortcuts"]),
      })

      return { ...toRefs(event) }
    },
  }
</script>

<style lang="scss" scoped>
  #activity-bar {
    height: inherit;
    width: var(--width-activity-bar);
    background-color: var(--color-bg);
    display: flex;
    flex-direction: column;
    justify-content: center;
    align-items: center;
    padding: var(--spacing-gutter-primary);

    > .brand {
      height: 3rem;
      width: 100%;
      background-color: var(--color-bg-8);
      cursor: pointer;
      display: flex;
      align-items: center;
      justify-content: center;

      > #brand-svg {
        height: 1.9rem;
        width: 1.9rem;
      }
    }

    > ul {
      width: 100%;
      display: flex;
      flex-direction: column;
      background-color: var(--color-bg-8);

      > li {
        width: 100%;
        display: flex;
        justify-content: center;

        &:first-child > a {
          padding-top: 0.9rem;
        }

        &:last-child > a {
          padding-bottom: 1rem;
        }
      }

      &.space-shortcuts {
        flex-grow: 1;
      }
    }
  }
</style>
