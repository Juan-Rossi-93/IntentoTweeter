<template>
  <Menu :openCloseForm="openCloseForm" :showForm="showForm" />
  <TweetForm
    :showForm="showForm"
    :openCloseForm="openCloseForm"
    :reloadTweets="reloadTweets"
  />
  <TweetList :tweets="tweets" :reloadTweets="reloadTweets" />
</template>

<script>
import { ref } from "vue";
import Menu from "./components/Menu";
import TweetForm from "./components/TweetForm";
import useFormTweet from "./hooks/useFormTweet";
import TweetList from "./components/TweetList";
import { getTweetsApi } from "./api/tweet";

export default {
  name: "App",
  components: {
    Menu,
    TweetForm,
    TweetList,
  },
  setup() {
    let tweets = ref(getTweetsApi().reverse());

    //recarga los twitts
    const reloadTweets = () => {
      tweets.value = getTweetsApi().reverse();
    };

    return {
      ...useFormTweet(),
      tweets,
      reloadTweets,
      //sin los ... me retorna un objeto
    };
  },
};
</script>

<style></style>
