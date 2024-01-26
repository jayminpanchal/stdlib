<template>
  <div v-model="isHover">
    <button
      v-bind="variantsMapping"
      class="btn-style"
      depressed
      :large="$vuetify.breakpoint.mobile"
      min-width="0"
      v-on="$listeners"
    >
      <slot>Custom text</slot>
    </button>
  </div>
</template>

<script>
import style from "../../assets/scss/base/app.module.scss";

export default {
  name: "AppButton",
  props: {
    appBtnStyle: {
      type: String,
      default: "primary",
    },
  },
  data() {
    return {
      style,
      isHover: false,
    };
  },
  computed: {
    variantsMapping() {
      const props = {
        primary: {
          color: this.isHover
            ? this.style["blue_regular"]
            : this.style["deep-blue_regular"],
          dark: this.$attrs.disabled ? false : true,
          class: "px-6 py-2",
          ...this.$attrs,
        },
        secondary: {
          color: this.isHover
            ? this.style["deep-blue_light"]
            : this.style["white"],
          outlined: false,
          class: "secondary-btn px-6 py-2 ",
          ...this.$attrs,
        },
        tertiary: {
          color: this.isHover
            ? this.style["grey_lighter"]
            : this.style["white"],
          class: "tertiary-btn px-6 py-2 ",
          ...this.$attrs,
        },
        danger: {
          class: "danger-btn px-4 py-2",
          ...this.$attrs,
        },
        confirm: {
          class: "confirm-btn px-4 py-2",
          ...this.$attrs,
        },
        outlined: {
          class: "outlined-btn px-6 py-2",
          ...this.$attrs,
        },
        icon: {
          class: "icon-btn px-0 py-0",
          ...this.$attrs,
        },
        icon_outlined: {
          class: "icon-outlined-btn px-0 py-0",
          ...this.$attrs,
        },
      };
      return props[this.appBtnStyle];
    },
  },
};
</script>

<style lang="scss" scoped>
@import "../../assets/scss/main";

.btn-style {
  transition: 0.2s ease-in-out;
  text-indent: $text-indent--fix !important;
  &:focus {
    box-shadow: $border-focus !important;
  }
}

.danger-btn {
  background-color: $alert !important;
  color: white !important;
  :hover {
    color: white !important;
    cursor: pointer;
  }
}

.confirm-btn {
  background-color: $validate !important;
  color: white !important;
  :hover {
    color: white !important;
    cursor: pointer;
  }
}
.secondary-btn {
  &:has(.v-icon) {
    padding: 0px 16px !important;
  }
  box-shadow: $border-grey--thin !important;
  &:hover {
    box-shadow: $border-deep-blue--thin !important;
  }
  &:active {
    box-shadow: $border-deep-blue--large !important;
  }
}
.tertiary-btn {
  padding-left: $padding-left--8 !important;
  padding-right: $padding-right--8 !important;
  ::v-deep span.v-btn__content {
    .v-icon {
      &--left {
        margin-left: initial !important;
      }
      &--right {
        margin-right: initial !important;
      }
    }
  }
  &:active {
    background-color: $socotec-light-blue_light !important;
  }
}
.secondary-btn,
.tertiary-btn {
  &:hover {
    color: $socotec-deep-blue_regular !important;
  }
}

.outlined-btn {
  background-color: $white !important;
  border: 1px solid $grey_regular !important;
  &:hover {
    background-color: $socotec-deep-blue_light !important;
    border: 1px solid $socotec-deep-blue_regular !important;
  }
  &:active {
    background-color: $socotec-deep-blue_light !important;
  }
}

.icon-outlined-btn {
  width: 28px !important;
  max-width: 28px !important;
  max-height: 28px !important;
  background-color: $white !important;
  border: 1px solid $grey_regular !important;
  &:hover {
    background-color: $socotec-deep-blue_light !important;
    border: 1px solid $socotec-deep-blue_regular !important;
  }
  &:active {
    background-color: $socotec-deep-blue_light !important;
  }
}
</style>
