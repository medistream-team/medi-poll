<template>
  <v-app :style="{ width: '600px', margin: '50px auto' }">
    <div
      v-if="isAdmin || isPublic"
      class="survey-results-container"
      :style="{ width: '600px', margin: '50px auto' }"
    >
      <SurveyInfo
        :surveyId="surveyData._id"
        :totalCount="surveyData.participantCount"
        :expiryDate="surveyData.closeAt"
        :hasExpiry="surveyData.hasExpiry"
      />
      <SurveyQuestion
        v-for="page in pages"
        :key="page._id"
        :page="page"
        :showResult="showResult"
      />
    </div>
  </v-app>
</template>

<script>
import { USER_SURVEY_API } from "../config";
import SurveyInfo from "../components/UserView/SurveyInfo";
import SurveyQuestion from "../components/UserView/SurveyQuestion";
import vuetify from "../plugins/vuetify";

const axios = require("axios");

export default {
  name: "SurveyResults",
  vuetify,
  components: { SurveyInfo, SurveyQuestion },
  props: {
    surveyId: {
      type: String,
      required: true,
    },
    userKey: {
      type: String,
      required: true,
    },
  },
  data() {
    return {
      surveyData: null,
      isAdmin: null,
      isPublic: null,
      pages: null,
      showResult: true,
    };
  },
  computed: {
    headers() {
      return {
        Authorization: this.userKey,
      };
    },
  },
  created() {
    axios
      .get(`${USER_SURVEY_API}/${this.surveyId}`, {
        headers: this.headers,
      })
      .then((res) => {
        this.isAdmin = res.data.isAdmin;
        this.isPublic = res.data.survey.isPublic;
        this.surveyData = res.data.survey;
        this.pages = res.data.survey.pages;

        if (!this.isPublic && !this.isAdmin) {
          alert("Results cannot be loaded");
        }
      })
      .catch((err) => console.log(err));
  },
};
</script>

<style lang="scss" scoped>
.survey-results-container {
  width: 100%;
  max-width: 600px;
  margin: 50px auto;
  padding: 10px;
}
</style>
