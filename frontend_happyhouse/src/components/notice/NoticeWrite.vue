<template>
  <b-container class="bv-example-row mt-3">
    <b-row>
      <b-col>
        <b-alert show
          ><h3><b>글쓰기</b></h3></b-alert
        >
      </b-col>
    </b-row>
    <notice-write-form type="register" />
  </b-container>
</template>

<script>
import NoticeWriteForm from "./child/NoticeWriteForm.vue";

export default {
  name: "NoticeWrite",
  components: {
    NoticeWriteForm,
  },
};
</script>

<style></style>
