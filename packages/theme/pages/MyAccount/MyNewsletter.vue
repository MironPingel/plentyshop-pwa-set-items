<template>
  <SfTabs
    :open-tab="1"
    class="tab-orphan"
  >
    <SfTab :title="$t('MyNewsletter.My newsletter')">
      <p class="message">
        {{ $t('MyNewsletter.Set up newsletter') }}
      </p>
      <div class="form">
        <p class="form__title">
          {{ $t('MyNewsletter.Sections that interest you') }}
        </p>
        <div class="form__checkbox-group">
          <SfCheckbox
            v-model="newsletter"
            :label="$t('MyNewsletter.Women')"
            value="woman"
            class="form__element"
          />
          <SfCheckbox
            v-model="newsletter"
            :label="$t('MyNewsletter.Men')"
            value="man"
            class="form__element"
          />
          <SfCheckbox
            v-model="newsletter"
            :label="$t('MyNewsletter.Kids')"
            value="kids"
            class="form__element"
          />
        </div>
        <SfButton class="form__button">
          {{ $t('MyNewsletter.Save changes') }}
        </SfButton>
      </div>
      <p class="notice">
        {{ $t('MyNewsletter.I have read and understand') }} <SfLink
          class="notice__link"
          link="#"
        >
          {{ $t('MyNewsletter.Privacy policy') }}
        </SfLink> and
        <SfLink
          class="notice__link"
          link="#"
        >
          {{ $t('MyNewsletter.Cookies policy') }}
        </SfLink> {{ $t('MyNewsletter.Commercial information') }}
      </p>
    </SfTab>
  </SfTabs>
</template>

<script>
import { SfTabs, SfCheckbox, SfButton, SfLink } from '@storefront-ui/vue';
export default {
  name: 'MyNewsletter',
  components: {
    SfTabs,
    SfCheckbox,
    SfButton,
    SfLink
  },
  data() {
    return { newsletter: [] };
  }
};
</script>

<style lang='scss' scoped>
.tab-orphan {
  @include for-mobile {
    --tabs-title-display: none;
    --tabs-content-padding: 0;
    --tabs-conent-border-width: 0;
  }
}
.form {
  &__element {
    margin: 0 0 var(--spacer-base) 0;
    &:last-child {
      margin: 0;
    }
  }
  &__checkbox-group {
    margin: 0 0 var(--spacer-xl) 0;
  }
  &__title {
    margin: 0 0 var(--spacer-base) 0;
  }
  &__button {
    --button-width: 100%;
    @include for-desktop {
      --button-width: 17.5rem;
    }
  }
}
.message {
  margin: 0 0 var(--spacer-xl) 0;
  color: var(--c-dark-variant);
}
.notice {
  margin: var(--spacer-base) 0 0 0;
  font-size: var(--font-size--xs);
  &__link {
  color: var(--c-primary);
  text-decoration: none;
    &:hover {
      color: var(--c-text);
    }
  }
}

</style>
