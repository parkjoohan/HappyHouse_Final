<template>
  <div>
    <b-container class="bv-example-row mt-3">
      <video muted autoplay loop>
        <source src="@/assets/login.mp4" type="video/mp4" />
      </video>
      <b-row>
        <b-col></b-col>
        <b-col cols="8" align="center">
          <b-card
            class="text-center mt-3"
            style="max-width: 30rem; max-height: 20rem"
            align="left"
          >
            <b-form class="text-left">
              <b-alert show variant="danger" v-if="isLoginError"
                >아이디 또는 비밀번호를 확인하세요.</b-alert
              >
              <b-form-group label="ID" label-for="userid">
                <b-form-input
                  id="userid"
                  v-model="user.userId"
                  required
                  placeholder="Id"
                  @keyup.enter="confirm"
                ></b-form-input>
              </b-form-group>
              <b-form-group label="PASSWORD" label-for="userpwd">
                <b-form-input
                  type="password"
                  id="userpwd"
                  v-model="user.userPwd"
                  required
                  placeholder="Password"
                  @keyup.enter="confirm"
                ></b-form-input>
              </b-form-group>
              <b-button
                type="button"
                variant="success"
                class="m-1"
                @click="confirm"
                ><b-icon icon="key"></b-icon><b> 로그인</b></b-button
              >
              <b-button
                type="button"
                variant="primary"
                class="m-1"
                @click="movePage"
                ><b-icon icon="person-plus"></b-icon><b> 회원가입</b></b-button
              >
              <b-button @click="goHome" variant="secondary" class="m-1"
                ><b-icon icon="box-arrow-left"></b-icon><b> 홈으로</b></b-button
              >
            </b-form>
          </b-card>
        </b-col>
        <b-col></b-col>
      </b-row>
    </b-container>
  </div>
</template>

<script>
import { mapState, mapActions } from "vuex";

const memberStore = "memberStore";

export default {
  name: "MemberLogin",
  data() {
    return {
      user: {
        userId: null,
        userPwd: null,
      },
    };
  },
  computed: {
    ...mapState(memberStore, ["isLogin", "isLoginError"]),
  },
  methods: {
    ...mapActions(memberStore, ["userConfirm", "getUserInfo"]),
    async confirm() {
      await this.userConfirm(this.user);
      let token = sessionStorage.getItem("access-token");
      if (this.isLogin) {
        await this.getUserInfo(token);
        this.$router.push({ name: "Home" });
      }
    },
    movePage() {
      this.$router.push({ name: "SignUp" });
    },
    goHome() {
      this.$router.push("/");
      [2];
    },
  },
};
</script>

<style scoped>
video {
  width: 50%;
}
</style>
