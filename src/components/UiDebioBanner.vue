<template lang="pug">
  .banner(:class="classes")
    .banner__wrapper
      ui-debio-card.banner__card(block)
        template
          .banner__content
            .banner__illustrations
              .banner__illustration
                slot(v-if="hasIlustrationSlot" name="illustration")
              .banner__content-description(:class="{ 'banner__content-description--unset-margin': !hasIlustrationSlot }")
                .banner__title {{ title }}
                .banner__subtitle {{ subtitle }}

            .banner__cta
              .banner__cta-wrapper
                slot(name="cta")
              ui-debio-icon.banner__decoration(
                v-if="withDecoration"
                :icon="particleIllustration"
                width="350"
                height="270"
                color="red"
                view-box="0 0 390 235"
              )
</template>

<script>
import particleIllustration from "@debionetwork/ui-icons/src/particleIllustration"

const allowedGradients = /^(primary|secondary|tertiary|violet)$/

export default {
  name: "UiDebioBanner",
  props: {
    title: { type: String, default: "Default title" },
    subtitle: { type: String, default: "Default subtitle" },
    gradientColor: { type: String, default: null },
    withDecoration: Boolean
  },

  data: () => ({ particleIllustration }),

  computed: {
    hasIlustrationSlot() {
      return this.$slots["illustration"] || this.$scopedSlots["illustration"]
    },

    classes () {
      return [
        { "banner--with-gradient": this.gradientColor && allowedGradients.test(this.gradientColor) },
        { "banner--gradient-primary": this.gradientColor === "primary" },
        { "banner--gradient-secondary": this.gradientColor === "secondary" },
        { "banner--gradient-tertiary": this.gradientColor === "tertiary" },
        { "banner--gradient-violet": this.gradientColor === "violet" },
        { "banner--with-decoration": this.withDecoration }
      ]
    }
  }
}
</script>

<style lang="sass">
  .banner
    &__card

      .ui-debio-card__body
        background: #5640A5
        padding: 2.188rem 2rem 2.5rem
        border-radius: 0.25rem
        position: relative
        overflow: hidden

    &__content
      display: flex
      justify-content: space-between

    &__content-description
      margin-left: 13.25rem

    &__content-description--unset-margin
      margin-left: unset

    &__illustrations
      display: flex
      align-items: center
      gap: 0 1.875rem

    &__illustration
      position: absolute

    &__title
      font-size: 1.875rem
      font-weight: 600
      line-height: 2.813rem
      color: #FFFFFF

    &__subtitle
      max-width: 17.313rem
      font-size: 0.938rem
      font-weight: 700
      line-height: 1.438rem
      color: #FFFFFF

    &__cta-wrapper
      display: flex
      gap: 1.25rem

    &__decoration
      position: absolute
      top: -47px
      right: 67px
      transform: scale(1.2)

    &--gradient-primary
      .ui-debio-card__body
        background: linear-gradient(267.84deg, #FF83EB 18.61%, #FC5EFF 55.16%, #D045BA 93.27%)

    &--gradient-secondary
      .ui-debio-card__body
        background: linear-gradient(267.84deg, #9E83FF 18.61%, #815EFF 55.16%, #6345D0 93.27%)

    &--gradient-tertiary
      .ui-debio-card__body
        background: linear-gradient(267.84deg, #D783FF 18.61%, #AF5EFF 55.16%, #A445D0 93.27%)

    &--gradient-violet
      .ui-debio-card__body
        background: linear-gradient(91.73deg, #ff58ab -0.04%, #ffd0e7 100%)

    @media screen and (max-width: 959px)
      &__content,
      &__illustrations,
      &__cta-wrapper
        flex-direction: column

      &__content
        gap: 1.25rem

      &__content-description
        margin-left: unset
        text-align: center

      &__illustrations
        align-items: center

      &__illustration
        position: relative
        top: unset
</style>
