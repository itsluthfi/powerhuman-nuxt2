<template>
  <section class="py-[70px] flex flex-col items-center justify-center px-4">
    <div class="text-[32px] font-semibold text-dark">New Role</div>
    <p class="mt-4 text-base leading-7 text-center mb-[50px] text-grey">
      Manage your employees to achieve <br />
      a bigger goals for your company
    </p>
    <form class="w-full card" @submit.prevent="createRole">
      <div class="form-group">
        <label for="" class="text-grey">Role Name</label>
        <input
          type="text"
          class="input-field"
          value="Product Marketing"
          v-model="role.name"
        />
      </div>
      <div class="form-group">
        <label for="idRes" class="text-grey">Responsibility</label>
        <ul id="listResp" class="flex flex-col gap-4">
          <li class="inline-flex items-center w-full gap-5">
            <input
              type="text"
              id="idRes"
              name="responsibility"
              class="w-full input-field"
            />
            <a href="#" role="button" id="addRsp">
              <img src="/assets/svgs/ric-plus.svg" alt="" />
            </a>
          </li>
        </ul>
      </div>
      <button type="submit" class="w-full btn btn-primary mt-[14px]">
        Save Role
      </button>
    </form>
  </section>
</template>

<script>
export default {
  layout: 'form',
  middleware: 'auth',
  data() {
    return {
      role: {
        name: '',
        company_id: this.$route.params.id,
      },
    }
  },
  methods: {
    async createRole() {
      try {
        // Send Registration Data to Server
        let response = await this.$axios.post('/role', this.role)
        // Redirect to Company Roles Page
        this.$router.push({ name: 'companies-id-roles' })
        console.log(response)
      } catch (error) {
        console.log(error)
      }
    },
  },
}
</script>
