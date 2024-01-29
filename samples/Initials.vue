<template>
  <Tooltip v-if="getInitials" :disabled="!getInitials" bottom>
    <template #activator="{ on }">
      <Avatar :color="getColor" :size="size" v-on="on">
        <span class="white--text" :style="{ 'font-size': fontSize }">
          {{ getInitials }}
        </span>
      </Avatar>
    </template>

    <slot name="tooltipContent">
      <span v-if="firstName || lastName"> {{ firstName }} {{ lastName }} </span>
      <span v-else-if="email">
        {{ email }}
      </span>
      <span v-else-if="user"> {{ user.firstName }} {{ user.lastName }} </span>
      <span v-else>{{ $t('project_manager_undefined') }}</span>
    </slot>
  </Tooltip>
</template>

<script>
import { getInitials } from '../../utils/formatting';
import { getAvatarColor } from '../../utils/avatars';

export default {
  name: 'Initials',
  props: {
    user: {
      type: Object,
      default: () => ({}),
    },
    firstName: {
      type: String,
      default: '',
    },
    lastName: {
      type: String,
      default: '',
    },
    email: {
      type: String,
      default: '',
    },
    color: {
      type: String,
      default: '#00ace8',
    },
    size: {
      type: [Number, String],
      default: '36',
    },
    fontSize: {
      type: String,
      default: '14px',
    },
  },
  computed: {
    getInitials() {
      if (this.email !== '') {
        const firstPart = this.email.substring(0, this.email.lastIndexOf('@'));
        const fields = firstPart.split('.');

        // Mail doesn't have the pattern first.last@test.com
        if (fields.length < 2) {
          return fields[0].toUpperCase;
        }
        return getInitials(fields[0].charAt(0), fields[1].charAt(0));
      }

      // Possible to get initials from props firstName and lastName specified directly
      // or using the user props that contain a full user object
      if (this.firstName || this.lastName) {
        return getInitials(this.firstName, this.lastName);
      }

      if (this.user) {
        return getInitials(this.user.firstName, this.user.lastName);
      }
      return '';
    },
    getColor() {
      if (this.user?.email) {
        return getAvatarColor(this.user.email);
      } else if (this.email) {
        return getAvatarColor(this.email);
      } else {
        return this.color;
      }
    },
  },

  // ----------------------- `i18n` option, setup locale info for component -----------------------
  i18n: {
    messages: {
      fr: {
        project_manager_undefined: 'Pilote non défini',
      },
      en: {
        project_manager_undefined: 'Project manager undefined',
      },
      nl: {
        project_manager_undefined: 'Projectmanager ongedefinieerd',
      },
    },
  },
};
</script>
