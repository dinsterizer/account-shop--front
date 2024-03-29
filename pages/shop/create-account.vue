<template>
  <FrameBox>
    <div class="space-y-10">
      <div class="flex">
        <StepsCircles
          class="mx-auto"
          :current-step="currentStep"
          :last-step="7"
        />
      </div>

      <!-- STEP - 1: Select game -->
      <div v-if="currentStep === 1" class="space-y-8">
        <HeadingBase3 class="text-center">
          Vui lòng chọn game bạn muốn đăng
        </HeadingBase3>
        <GameFormSelectSelfs v-model="selectedGame" :games="games" />
      </div>

      <!-- STEP - 2: Select account type -->
      <div v-if="currentStep === 2" class="space-y-8">
        <HeadingBase3 class="text-center">
          Vui lòng chọn kiểu tài khoản
        </HeadingBase3>
        <AccountTypeFormSelectSelfs
          v-model="selectedAccountType"
          :account-types="usableAccountTypes"
        />
      </div>

      <!-- STEP - 3: Fill game info -->
      <div v-if="currentStep === 3" class="space-y-8">
        <HeadingBase3 class="text-center">
          Vui lòng điền thông tin game
        </HeadingBase3>
        <GameInfoFormFillSelfs
          v-model="filledGameInfos"
          :game-infos="selectedGame.gameInfos"
          @emit-panel="panelOfFilledGameInfos = $event"
        />
      </div>

      <!-- STEP - 4:  Perform account action -->
      <div v-if="currentStep === 4" class="space-y-8">
        <HeadingBase3 class="text-center">
          Vui lòng thực hiện các hành động dưới đây
        </HeadingBase3>
        <AccountActionFormPerformSelfs
          v-model="performedAccountActions"
          :account-actions="selectedAccountType.accountActions"
          @emit-panel="panelOfPerformedAccountActions = $event"
        />
      </div>

      <!-- STEP - 5: Fill account infos -->
      <div v-if="currentStep === 5" class="space-y-8">
        <HeadingBase3 class="text-center">
          Vui lòng điền thông tin tài khoản
        </HeadingBase3>
        <AccountInfoFormFillSelfs
          v-model="filledAccountInfos"
          :account-infos="selectedAccountType.accountInfos"
          @emit-panel="panelOfFilledAccountInfos = $event"
        />
      </div>

      <!-- STEP - 6: Fill base infos -->
      <div v-if="currentStep === 6" class="space-y-8">
        <HeadingBase3 class="text-center">
          Vui lòng điền thông tin tài khoản - II
        </HeadingBase3>
        <AccountFormFillBaseInfos
          v-model="filledBaseInfos"
          @emit-panel="panelOfFilledBaseInfos = $event"
        />
      </div>

      <!-- STEP - 7: Confirm -->
      <div v-if="currentStep === 7" class="space-y-8">
        <HeadingBase3 class="text-center"> Xác nhận nào </HeadingBase3>
        <AccountConfirmBase
          :game="selectedGame"
          :account-type="selectedAccountType"
          :base-infos="filledBaseInfos"
        />
      </div>

      <!-- Actions -->
      <div class="flex flex-row-reverse items-center gap-4">
        <!-- Next step -->
        <ButtonPrimary v-if="currentStep < 7" @click="hopNextStep">
          Tiếp theo
        </ButtonPrimary>
        <!-- Confirm -->
        <ButtonPrimary v-if="currentStep === 7" theme="green" @click="create">
          Xác nhận, và đăng nick lên shop
        </ButtonPrimary>
        <!-- Previous step -->
        <ButtonPrimary
          v-if="currentStep > 1"
          theme="yellow"
          @click="hopPreviousStep"
        >
          Quay lại
        </ButtonPrimary>
        <!-- Access created account -->
        <NuxtLink
          v-if="createdAccount"
          :to="{ name: 'account-id', params: { id: createdAccount.id } }"
        >
          <ButtonPrimary> Truy cập ngay </ButtonPrimary>
        </NuxtLink>
        <!-- Message -->
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
    </div>
  </FrameBox>
</template>

<script>
import { required } from 'vuelidate/lib/validators';

export default {
  async asyncData({ $axios }) {
    const { data: games } = await $axios.$get('game/all/usable', {
      params: {
        _requiredModelRelationships: [
          'accountTypes.usableUsers',
          'accountTypes.accountInfos.rule',
          'accountTypes.accountActions.rule',
          'gameInfos.rule',
          'representativeImage',
        ],
      },
    });
    return {
      // game
      games,
      selectedGame: undefined,
      // account type
      selectedAccountType: undefined,
      // game infos
      filledGameInfos: undefined,
      panelOfFilledGameInfos: [],
      // account actions
      performedAccountActions: {},
      panelOfPerformedAccountActions: undefined,
      // account infos
      filledAccountInfos: {},
      panelOfFilledAccountInfos: undefined,
      // base infos
      filledBaseInfos: {},
      panelOfFilledBaseInfos: undefined,
      // others
      createdAccount: undefined,
      // Support
      currentStep: 1,
      message: {
        error: undefined,
        success: undefined,
      },
    };
  },
  computed: {
    // Include account types auth can use it to create account
    // Change according to selectedGame
    // Used in step 2 - select account type
    usableAccountTypes() {
      return this.selectedGame.accountTypes.filter((accountType) =>
        accountType.usableUsers.find(
          (user) => user.id === this.$store.state.auth.profile.id
        )
      );
    },
  },
  validations: {
    selectedGame: {
      required,
    },
    selectedAccountType: {
      required,
    },
    stepOne: ['selectedGame'],
    stepTwo: ['selectedAccountType'],
  },
  methods: {
    hopNextStep() {
      this.message.error = null;
      this.message.success = null;

      // Validate step 1
      if (this.currentStep === 1) {
        this.$v.stepOne.$touch();

        if (this.$v.stepOne.$error) {
          this.message.error = 'Vui lòng chọn một game.';
          return;
        }
      }

      // Validate step 2
      else if (this.currentStep === 2) {
        this.$v.stepTwo.$touch();

        if (this.$v.stepTwo.$error) {
          this.message.error = 'Vui lòng kiểu tài khoản mà bạn muốn đăng.';
          return;
        }
      }

      // Validate step 3 - fill game infos
      else if (this.currentStep === 3) {
        const validatedStep4Result = this.panelOfFilledGameInfos.check();
        if (validatedStep4Result.isPending) {
          this.message.warn = 'Hãy đợi thêm trước khi tiếp tục.';
          return;
        } else if (validatedStep4Result.isInvalid) {
          this.message.error = 'Vui lòng kiểm tra lại thông tin vừa nhập.';
          return;
        }
      }

      // Validate step 4 - perform account actions
      else if (this.currentStep === 4) {
        const validatedStep5Result =
          this.panelOfPerformedAccountActions.check();
        if (validatedStep5Result.isPending) {
          this.message.warn = 'Hãy đợi thêm trước khi tiếp tục.';
          return;
        } else if (validatedStep5Result.isInvalid) {
          this.message.error = 'Vui lòng thực hiện các hành động bắt buộc.';
          return;
        }
      }

      // Validate step 5 - fill account infos
      else if (this.currentStep === 5) {
        const validatedStep6Result = this.panelOfFilledAccountInfos.check();
        if (validatedStep6Result.isPending) {
          this.message.warn = 'Hãy đợi thêm trước khi tiếp tục.';
          return;
        } else if (validatedStep6Result.isInvalid) {
          this.message.error = 'Vui lòng kiểm tra lại thông tin vừa nhập.';
          return;
        }
      }

      // Validate step 6 - fill account infos
      else if (this.currentStep === 6) {
        const validatedStep7Result = this.panelOfFilledBaseInfos.check();
        if (validatedStep7Result.isPending) {
          this.message.warn = 'Hãy đợi thêm trước khi tiếp tục.';
          return;
        } else if (validatedStep7Result.isInvalid) {
          this.message.error = 'Vui lòng kiểm tra lại thông tin vừa nhập.';
          return;
        }
      }

      this.currentStep++;
    },
    hopPreviousStep() {
      this.currentStep--;
    },
    create() {
      const data = this.$withFile({
        ...this.filledBaseInfos,
        rawAccountInfos: this.filledAccountInfos,
        rawAccountActions: this.performedAccountActions,
        rawGameInfos: this.filledGameInfos,
        _requiredModelRelationships: [
          'accountInfos',
          'gameInfos',
          'accountActions',
        ],
      });
      this.$axios
        .$post(`account/${this.selectedAccountType.id}`, data)
        .then(({ data }) => {
          this.createdAccount = data;
          this.message.error = null;
          this.message.success = 'Nick đã được đăng lên thành công!';
        })
        .catch(() => {
          this.message.error =
            'Thất bại, thông tin bạn cung cấp không hợp lệ hoặc lỗi hệ thống.';
          this.message.success = null;
        });
    },
  },
};
</script>
