<template>
  <SfModal
    :visible="isNewsletterModalOpen"
    class="modal"
    @close="closeModal"
  >
    <template #modal-bar>
      <SfBar
        class="modal__title smartphone-only"
        :close="true"
        :title="$t('NewsletterModal.Subscribe to newsletter')"
        @click:close="closeModal"
      />
    </template>
    <transition
      name="sf-fade"
      mode="out-in"
    >
      <div>
        <SfHeading
          :level="3"
          :title="$t('NewsletterModal.Subscribe to newsletter')"
          class="modal__title desktop-only"
        />
        <form @submit.prevent="$emit('email-submitted', emailAddress)">
          <SfInput
            v-model="emailAddress"
            type="email"
            :label="$t('NewsletterModal.Email address')"
            class="modal__input"
          />
          <SfButton
            class="modal__button"
            type="submit"
          >
            {{ $t('NewsletterModal.Confirm subscription') }}
          </SfButton>
        </form>
        <SfHeading
          :description="$t('NewsletterModal.You can unsubscribe at any time')"
          :level="3"
        />
        <SfScrollable
          max-content-height="3.75rem"
          :class="{ 'is-open': !isHidden }"
        >
          <i18n
            tag="p"
            class="modal__content"
            path="NewsletterModal.subscribeToNewsletterModalContent"
          >
            <SfLink link="https://www.vuestorefront.io/privacy-policy">
              {{ $t('NewsletterModal.Privacy policy') }}
            </SfLink>
          </i18n>
          <template #view-all>
            <SfButton
              class="sf-button--text sf-scrollable__view-all desktop-only"
              @click="isHidden = !isHidden"
            >
              <span>{{ isHidden ? $t('NewsletterModal.Show more') : $t('NewsletterModal.Hide') }}</span>
            </SfButton>
          </template>
        </SfScrollable>
      </div>
    </transition>
  </SfModal>
</template>
<script>
import { SfModal, SfHeading, SfInput, SfButton, SfScrollable, SfBar, SfLink } from '@storefront-ui/vue';
import { ref } from '@nuxtjs/composition-api';
import { useUiState } from '~/composables';

export default {
  name: 'NewsletterModal',
  components: {
    SfModal,
    SfHeading,
    SfInput,
    SfButton,
    SfScrollable,
    SfBar,
    SfLink
  },
  setup() {
    const { isNewsletterModalOpen, toggleNewsletterModal } = useUiState();

    const isHidden = ref(true);
    const emailAddress = ref('');

    const closeModal = () => {
      toggleNewsletterModal();
    };

    return {
      isNewsletterModalOpen,
      toggleNewsletterModal,
      isHidden,
      emailAddress,
      closeModal
    };
  }
};
</script>

  <style lang="scss" scoped>

  .modal {
    display: flex;
    justify-content: center;
    --modal-index: 30;
    --overlay-z-index: 30;
    --modal-content-padding: var(--spacer-xl);
    &__input,
    .sf-input__label {
      --input-font-size: var(--font-size--base);
      --input-label-font-size: var(--font-size--base);
    }
    &__button {
      margin: 0 auto;
    }
    &__content {
      font-size: var(--font-size--sm);
      font-weight: var(--font-weight--light);
    }
    .sf-scrollable__view-all.sf-button {
      font-weight: var(--font-weight--light);
    }
  }

  </style>
