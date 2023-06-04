<template>
  <b-navbar wrapper-class="container" class="header">
    <template slot="brand">
      <b-navbar-item tag="router-link" to="/" data-test="tornado_main_page" active-class="">
        <Logo />
      </b-navbar-item>
    </template>
    <template slot="start">
      <b-navbar-item
        v-if="isEnabledGovernance"
        tag="router-link"
        to="/governance"
        data-test="voting_link"
        :active="$route.path.includes('governance')"
        class="has-tag"
      >
        {{ $t('governance') }} <span v-if="hasActiveProposals" class="navbar-item--tag"></span>
      </b-navbar-item>
    </template>
    <template slot="end">
      <b-navbar-item tag="div">
        <div class="buttons">
          <network-navbar-icon />
          <metamask-navbar-icon data-test="metamask_connection_state" />
        </div>
      </b-navbar-item>
    </template>
  </b-navbar>
</template>

<script>
import { mapState, mapGetters } from 'vuex'
import Logo from '@/components/Logo'
import MetamaskNavbarIcon from '@/components/MetamaskNavbarIcon'
import NetworkNavbarIcon from '@/components/NetworkNavbarIcon'

export default {
  components: {
    Logo,
    NetworkNavbarIcon,
    MetamaskNavbarIcon
  },
  data() {
    return {
      isActive: false
    }
  },
  computed: {
    ...mapGetters('metamask', ['netId', 'isLoggedIn']),
    ...mapGetters('governance/gov', ['isEnabledGovernance']),
    ...mapState('governance/gov', ['hasActiveProposals'])
  },
  methods: {
    onAccount() {
      this.$router.push('/account')
    }
  }
}
</script>
