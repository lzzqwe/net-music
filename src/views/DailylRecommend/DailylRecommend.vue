<template>
  <div v-if="token" class="daily-recommend">
    <recommend-content></recommend-content>
  </div>
  <div v-else>
    <net-login></net-login>
  </div>
</template>

<script>
import NetLogin from "../NetLogin/NetLogin";
import RecommendContent from "@/components/RecommendContent";
import { mapGetters } from "vuex";
export default {
   metaInfo() {
      return {
        title:"每日推荐"
      }
    },
  name: "DailyRecommend",
  data() {
    return {
      dailySongs: [],
    };
  },
  components: {
    NetLogin,
    RecommendContent,
  },
  computed: {
    ...mapGetters(["user","token"]),
  },
  created() {
    const token = this.token;
    if (!token) {
      this.$dialog.alert({
        message: "必须要登录后才可以获取每日推荐内容",
      });
    }
  },
};
</script>

<style lang="less" scoped>
.daily-recommend {
  font-size: 40px;
}
</style>
