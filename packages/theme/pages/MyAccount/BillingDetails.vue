<template>
  <MyAccountAddressDetails
    v-if="!loading"
    :tab-title="$t('BillingDetails.Billing details')"
    :addresses="billing"
    :countries="countries"
    :type="'billing'"
    @set-default-address="setDefaultAddress({address: $event })"
    @delete-address="deleteAddress({address: $event})"
    @update-address="addAddress({address: $event})"
  />
</template>
<script>
import MyAccountAddressDetails from '~/components/MyAccount/MyAccountAddressDetails';
import { useUserBilling, useActiveShippingCountries } from '@vue-storefront/plentymarkets';
import { onSSR } from '@vue-storefront/core';

export default {
  name: 'BillingDetails',
  components: {
    MyAccountAddressDetails
  },
  setup() {
    const { billing, load, loading, addAddress, deleteAddress, setDefaultAddress } = useUserBilling();
    const { load: loadActiveShippingCountries, result: countries } = useActiveShippingCountries();

    onSSR(async () => {
      await load();
      await loadActiveShippingCountries();
    });

    return {
      billing,
      countries,
      loading,
      addAddress,
      deleteAddress,
      setDefaultAddress
    };
  }
};
</script>

<style lang='scss' scoped>
</style>
