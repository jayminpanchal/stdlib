<template>
  <Menu v-if="displayLink && menus.length" open-on-hover offset-y>
    <template #activator="{ on, attrs }">
      <span :class="linkClass" class="menus-btn" v-bind="attrs" v-on="on">
        {{ text }}
        <VIcon right size="16" color="#333333" class="pl-2 ma-0"> mdi-menu-down </VIcon>
      </span>
    </template>

    <List class="pa-0">
      <ListItem
        v-for="(item, index) in menus"
        :key="index"
        :to="{ name: item.routeName, params: item.params, query: item.query }"
      >
        <Icon v-if="icon" size="18" class="mr-1">
          {{ icon }}
        </Icon>
        {{ item.textLabel }}
      </ListItem>
    </List>
  </Menu>
  <RouterLink
    v-else-if="displayLink"
    :to="{ name: routeName, params, query }"
    active-class="active"
    :class="linkClass"
    :exact="exact"
    :exact-path="exactPath"
  >
    <Icon v-if="icon" size="18" class="mr-1">
      {{ icon }}
    </Icon>
    {{ text }}
  </RouterLink>
</template>
<script>
export default {
  name: 'NavigationLink',
  props: {
    linkClass: {
      type: String,
      default: 'navbar-item-link',
    },
    text: {
      type: String,
      default: '',
    },
    routeName: {
      type: String,
      default: '',
    },
    displayLink: {
      type: Boolean,
      default: false,
    },
    exact: {
      type: Boolean,
      default: true,
    },
    exactPath: {
      type: Boolean,
      default: false,
    },
    icon: {
      type: String,
      default: '',
    },
    params: {
      type: Object,
      default: () => ({}),
    },
    query: {
      type: Object,
      default: () => ({}),
    },
    menus: {
      type: Array,
      default: () => [],
    },
  },
};
</script>

<style lang="scss" scoped>
.menus-btn {
  margin: 0;
  height: 100%;
  font-size: 1.125rem;
}
.tab-link {
  height: 40px;
  min-width: 96px;
  justify-content: center;
  font-size: 1rem;
  font-weight: normal;
  display: flex;
  align-items: center;
  text-decoration: none;
  color: #333333 !important;
  padding: 0 16px;
  border-bottom: 3px solid transparent;
  &:hover,
  &.active {
    color: #333333;
    text-decoration: none;
    border-bottom: 3px solid #fcb902;
    background-color: #fff8e6;
  }
}
</style>
