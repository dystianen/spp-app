<template>
  <v-navigation-drawer
    :value="isDrawerOpen"
    app
    floating
    width="260"
    class="app-navigation-menu"
    :right="$vuetify.rtl"
    @input="val => $emit('update:is-drawer-open', val)"
  >
    <!-- Navigation Header -->
    <div class="vertical-nav-header d-flex items-center ps-6 pe-5 pt-5 pb-2">
      <router-link to="/" class="d-flex align-center text-decoration-none">
        <v-img
          :src="require('@/assets/images/logos/logo.svg')"
          max-height="30px"
          max-width="30px"
          alt="logo"
          contain
          eager
          class="app-logo me-3"
        ></v-img>
        <v-slide-x-transition>
          <h2 class="app-title text--primary">MY SPP</h2>
        </v-slide-x-transition>
      </router-link>
    </div>

    <!-- Navigation Items -->
    <v-list expand shaped class="vertical-nav-menu-items pr-5">
      <nav-menu-link title="Dashboard" :to="{ name: 'dashboard' }" :icon="icons.mdiHomeOutline"></nav-menu-link>
      <nav-menu-section-title title="USER INTERFACE"></nav-menu-section-title>
      <nav-menu-link
        v-if="role === 'admin'"
        title="Siswa"
        :to="{ name: 'student' }"
        :icon="icons.mdiAccountBoxMultiple"
      ></nav-menu-link>
      <nav-menu-link
        v-if="role === 'admin'"
        title="Kelas"
        :to="{ name: 'class' }"
        :icon="icons.mdiTable"
      ></nav-menu-link>
      <nav-menu-link
        v-if="role === 'admin'"
        title="Petugas"
        :to="{ name: 'petugas' }"
        :icon="icons.mdiAccountEditOutline"
      ></nav-menu-link>
      <nav-menu-link
        v-if="role === 'admin'"
        title="SPP"
        :to="{ name: 'spp' }"
        :icon="icons.mdiAndroidMessages"
      ></nav-menu-link>
      <nav-menu-link
        v-if="role === 'admin' || role === 'petugas'"
        title="Pembayaran"
        :to="{ name: 'pembayaran' }"
        :icon="icons.mdiAndroidMessages"
      ></nav-menu-link>
      <nav-menu-link
        v-if="siswa == 'true'"
        title="History"
        :to="{ name: 'history' }"
        :icon="icons.mdiAccountEditOutline"
      ></nav-menu-link>
    </v-list>
  </v-navigation-drawer>
</template>

<script>
// eslint-disable-next-line object-curly-newline
import {
  mdiHomeOutline,
  mdiAlphaTBoxOutline,
  mdiEyeOutline,
  mdiCreditCardOutline,
  mdiTable,
  mdiFileOutline,
  mdiFormSelect,
  mdiAccountCogOutline,
  mdiAccountBoxMultiple,
  mdiAccountEditOutline,
  mdiAndroidMessages,
} from '@mdi/js'
import NavMenuSectionTitle from './components/NavMenuSectionTitle.vue'
import NavMenuGroup from './components/NavMenuGroup.vue'
import NavMenuLink from './components/NavMenuLink.vue'

export default {
  components: {
    NavMenuSectionTitle,
    NavMenuGroup,
    NavMenuLink,
  },
  props: {
    isDrawerOpen: {
      type: Boolean,
      default: null,
    },
  },
  setup() {
    return {
      role: '',
      siswa: '',
      icons: {
        mdiHomeOutline,
        mdiAlphaTBoxOutline,
        mdiEyeOutline,
        mdiCreditCardOutline,
        mdiTable,
        mdiFileOutline,
        mdiFormSelect,
        mdiAccountCogOutline,
        mdiAccountBoxMultiple,
        mdiAccountEditOutline,
        mdiAndroidMessages,
      },
    }
  },

  mounted() {
    this.siswa = localStorage.getItem('isSiswa')
    this.role = localStorage.getItem('role')
  },
}
</script>

<style lang="scss" scoped>
.app-title {
  font-size: 1.25rem;
  font-weight: 700;
  font-stretch: normal;
  font-style: normal;
  line-height: normal;
  letter-spacing: 0.3px;
}

// ? Adjust this `translateX` value to keep logo in center when vertical nav menu is collapsed (Value depends on your logo)
.app-logo {
  transition: all 0.18s ease-in-out;

  .v-navigation-drawer--mini-variant & {
    transform: translateX(-4px);
  }
}

@include theme(app-navigation-menu) using($material) {
  background-color: map-deep-get($material, 'background');
}

.app-navigation-menu {
  .v-list-item {
    &.vertical-nav-menu-link {
      ::v-deep .v-list-item__icon {
        .v-icon {
          transition: none !important;
        }
      }
    }
  }
}

// You can remove below style
// Upgrade Banner
.app-navigation-menu {
  .upgrade-banner {
    position: absolute;
    bottom: 13px;
    left: 50%;
    transform: translateX(-50%);
  }
}
</style>
