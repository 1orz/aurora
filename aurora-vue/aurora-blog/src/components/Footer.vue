<template>
  <div id="footer" class="relative w-full pt-1" :style="gradientBackground">
    <span class="bg-ob-deep-900 flex justify-center">
      <div
        class="bg-ob-deep-900 rounded-lg max-w-10/12 lg:max-w-screen-2xl text-sm text-ob-normal w-full py-6 px-6 grid grid-rows-1 lg:grid-rows-none lg:grid-cols-4 justify-center items-center gap-8 h-36 mx-auto">
        <div
          class="flex flex-col lg:flex-row gap-6 lg:gap-12 row-span-1 lg:col-span-5 text-center lg:text-left mx-auto">
          <ul class="flex flex-col gap-2 mx-auto">
            <li class="flex flex-row mx-auto">
              Copyright © {{ currentYear }}
              <b class="font-extrabold">&nbsp;{{ websiteConfig.author }}</b>
            </li>
            <li v-if="websiteConfig.gonganBeianNumber != '' && websiteConfig.gonganBeianNumber != undefined" class="flex flex-row mx-auto">
              <a href="http://www.beian.gov.cn/portal/registerSystemInfo?recordcode=11011402013558" target="_blank">
                <img src="https://oss.supermouse.cn/aurora/config/gongan-beian-icon.png" style="float:left;"/> &nbsp;
                <b class="font-extrabold border-b-2 border-ob hover:text-ob"> {{ websiteConfig.gonganBeianNumber }} </b>
              </a>
            </li>
            <li v-if="websiteConfig.beianNumber != '' && websiteConfig.beianNumber != undefined" class="flex flex-row mx-auto">
              <a href="https://beian.miit.gov.cn/" target="_blank">
                <b class="font-extrabold border-b-2 border-ob hover:text-ob"> {{ websiteConfig.beianNumber }} </b>
              </a>
            </li>
          </ul>
        </div>
      </div>
    </span>
  </div>
</template>

<script lang="ts">
import { computed, defineComponent } from 'vue'
import { useAppStore } from '@/stores/app'
import { useI18n } from 'vue-i18n'

export default defineComponent({
  name: 'Footer',
  setup() {
    const appStore = useAppStore()
    const { t } = useI18n()
    return {
      avatarClass: computed(() => {
        return {
          'footer-avatar': true,
          [appStore.themeConfig.profile_shape]: true
        }
      }),
      gradientText: computed(() => appStore.themeConfig.background_gradient_style),
      gradientBackground: computed(() => {
        return { background: appStore.themeConfig.header_gradient_css }
      }),
      currentYear: computed(() => new Date().getUTCFullYear()),
      websiteConfig: computed(() => appStore.websiteConfig),
      t
    }
  }
})
</script>
