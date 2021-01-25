<template>
  <div class="container">
    <h1 class="text-center">Lista de Tweets</h1>
    <p class="notice" v-if="tweets.length === 0">
      No hay Tweets en este momento, Puedes crear uno desde el boton azul "Nuevo
      Tweet"
    </p>
    <div class="tweet" v-for="tweet in tweets" :key="tweet.id">
      <p class="tweet__title">{{ tweet.username }}</p>
      <p class="tweet__text">{{ tweet.tweet }}</p>
      <span>{{ formatDate(tweet.createdAt) }}</span>
      <Close @click="deleteTeet(tweet.id)" />
    </div>
  </div>
</template>

<script>
import moment from "moment";
import "moment/locale/es";
import { Close } from "./Icons/index";
import { deleteTweetApi } from "../api/tweet";
export default {
  props: {
    tweets: Array,
    reloadTweets: Function,
  },

  components: {
    Close,
  },
  setup(props) {
    const formatDate = (date) => {
      return moment(date).fromNow();
    };

    const deleteTeet = (idTweet) => {
      deleteTweetApi(idTweet);
      props.reloadTweets();
    };
    console.log(props.tweets);
    return {
      formatDate,
      deleteTeet,
    };
  },
};
</script>

<style lang="scss">
.notice {
  font-size: 30px;
  color: grey;
}
.tweet {
  position: relative;
  border: 1px solid #ccc;
  padding: 20px;
  margin-bottom: 20px;
  display: flex;
  justify-content: space-between;
  align-items: center;

  p {
    margin: 0;
  }
  &__title {
    position: absolute;
    top: -12px;
    left: 10px;
    background-color: #fff;
    padding: 0 10px;
    font-weight: bold;
  }

  &__text {
    color: gray;
  }

  span {
    position: absolute;
    right: 10px;
    bottom: -9px;
    font-size: 12px;
    color: gray;
    background-color: #fff;
    padding: 0 20px;
    border: 1px solid #ccc;
  }
  svg {
    width: 20px;
    height: 20px;
    &:hover {
      cursor: pointer;
      color: red;
    }
  }
}
</style>
