<template>
  <div>
    <FrameBox>
      <AccountTypeForm
        :account-type="accountType"
        :can-edit="canUpdateAccountType"
      >
        <template #title> Thông tin kiểu tài khoản </template>
        <template #description> </template>
        <template #actions>
          <div class="flex flex-row-reverse gap-4 items-center">
            <ButtonPrimary v-if="canUpdateAccountType" @click="update">
              Cập nhật
            </ButtonPrimary>
            <p
              class="text-sm"
              :class="{
                'text-green-500': !message.error,
                'text-red-500': message.error,
              }"
            >
              {{ message.error || message.success }}
            </p>
          </div>
        </template>
      </AccountTypeForm>

      <!-- List account infos -->
      <div class="mt-8">
        <div class="flex items-center justify-between mb-4">
          <HeadingBase3>Danh sách thông tin tài khoản</HeadingBase3>
          <NuxtLink
            v-if="canCreateAccountAction"
            :to="{
              name: 'account-type-id-create-account-info',
              params: { id: accountType.id },
            }"
          >
            <ButtonPrimary>Thêm</ButtonPrimary>
          </NuxtLink>
        </div>

        <AccountInfoList :account-infos="accountInfos" />
      </div>

      <!-- List account actions -->
      <div class="mt-16">
        <div class="flex items-center justify-between mb-4">
          <HeadingBase3>Danh sách hành động tài khoản</HeadingBase3>
          <NuxtLink
            v-if="canCreateAccountInfo"
            :to="{
              name: 'account-type-id-create-account-action',
              params: { id: accountType.id },
            }"
          >
            <ButtonPrimary>Thêm</ButtonPrimary>
          </NuxtLink>
        </div>

        <AccountActionList :account-actions="accountActions" />
      </div>
    </FrameBox>
  </div>
</template>

<script>
export default {
  layout: 'admin',
  async asyncData({ $axios, $auth, params }) {
    const [
      { data: accountType },
      canUpdateAccountType,
      canCreateAccountInfo,
      canCreateAccountAction,
    ] = await Promise.all([
      $axios.$get(`account-type/${params.id}`),
      $auth.can('update', `AccountType:${params.id}`),
      $auth.can('create', `AccountInfo,AccountType:${params.id}`),
      $auth.can('create', `AccountAction,AccountType:${params.id}`),
    ]);

    accountType.rolesCanUsedAccountType =
      accountType.rolesCanUsedAccountType.map((role) => ({
        key: role.key,
        statusCode: role.pivot.status_code,
      }));

    return {
      canUpdateAccountType,
      canCreateAccountInfo,
      canCreateAccountAction,
      accountType,
      accountInfos: accountType.accountInfos,
      accountActions: accountType.accountActions,
      message: {
        error: undefined,
        success: undefined,
      },
    };
  },

  methods: {
    update() {
      this.$axios
        .$put(`account-type/${this.accountType.id}`, {
          name: this.accountType.name,
          description: this.accountType.description,
          rolesCanUsedAccountType: this.accountType.rolesCanUsedAccountType,
        })
        .then(() => {
          this.message.error = null;
          this.message.success = 'Thành công!!';
        })
        .catch(() => {
          this.message.error = 'Thất bại :((';
          this.message.success = null;
        });
    },
  },
};
</script>