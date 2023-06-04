<template>
  <footer class="footer">
    <div class="container">
      <div class="level">
        <div class="level-left">
          <div class="level-item is-column">
            <div class="level-subitem footer-address">
              <div class="footer-address__name">
                <!-- {{ $t('donationsAddress') }} -->
              </div>
              <!-- <a
                class="footer-address__value"
                target="_blank"
                :href="addressExplorerUrl(donationsAddress)"
                rel="noopener noreferrer"
                >{{ donationsAddress }}</a
              > -->
            </div>
          </div>
        </div>
        <div class="level-right">
          <div class="level-item is-column">
            <div class="level-subitem">
              <div class="buttons">
                <a href="https://twitter.com/whiteethtoken/" class="footer-links-xee">Twitter</a>
                <!-- <a href="#" class="footer-links-xee">Github</a> -->
                <a href="https://t.me/White_ETH" class="footer-links-xee">Telegram</a>
              </div>
            </div>
          </div>
        </div>
      </div>
    </div>
  </footer>
</template>

<script>
import { mapGetters } from 'vuex'

// import { FlagIcon } from '@/components/icons'
import { LOCALES_NAMES, DONATIONS_ADDRESS } from '@/constants'

export default {
  data() {
    return {
      commit: process.env.commit,
      donationsAddress: DONATIONS_ADDRESS
    }
  },
  computed: {
    ...mapGetters('metamask', ['networkConfig', 'netId']),
    ...mapGetters('txHashKeeper', ['addressExplorerUrl']),
    duneLink() {
      const mainnetNetworks = [1, 5]

      if (mainnetNetworks.includes(Number(this.netId))) {
        return 'https://dune.xyz/poma/white-cash_1'
      }

      return 'https://dune.xyz/fennec/Tornado-Cash-Cross-chain-Dashboard'
    },
    locales() {
      return this.$i18n.availableLocales
    }
  },
  methods: {
    langChange(lang) {
      localStorage.setItem('lang', lang)

      if (lang === 'zh') {
        lang += '-cn'
      }

      this.$moment.locale(lang)
      this.$numbro.setLanguage(LOCALES_NAMES[lang])
    },
    printLang(lang) {
      let code = lang
      switch (code) {
        case 'zh':
          code = 'cn'
          break
      }
      return code.toUpperCase()
    }
  }
}
</script>
