<template>
  <div class="oyasumi-result">
    <div class="oyasumi-result_main">
      <img src="@/assets/waku_up.gif" alt>
      <div style="display: flex;align-items: stretch">
        <img src="@/assets/waku_left.gif" alt>
        <div class="oyasumi-result__message">
          <p v-if="step">
            {{questions.name}} {{titleList[questions.title-1]}}
          </p>
          <template v-for="(results, questionNumber) in resultsList">
            <p v-if="step > questionNumber+1" :key="questionNumber">
              <template v-for="(result, resultIndex) in results">
                <span :key="result" v-if="questions[`q${questionNumber+1}`] === resultIndex+1">{{result}}</span>
              </template>
            </p>
          </template>
        </div>
        <img src="@/assets/waku_left.gif" alt>
      </div>
      <img src="@/assets/waku_down.gif" alt>
    </div>
    <template v-if="step >= 7">
      <p class="oyasumi-result_build">
        <button type="button" @click="handleClickRestart">もう一度つくる</button>
      </p>
      <p class="oyasumi-result_share">
        <input type="text" class="oyasumi-result_shareurl" readonly :value="shareUrl">
        <a target="_blank" :href="twitterUrl">つぶやく</a>
      </p>
    </template>
  </div>
</template>

<script>
import { stringify } from 'querystring'

export default {
  props: {
    questions: Object,
    step: Number
  },
  computed: {
    titleList() {
      return [ 'さま', '様', '殿', 'さん', 'くん', 'ちゃん' ]
    },
    resultsList() {
      return [
        [
          'おはようございます',
          'ういーっす！（カラ元気で）',
          'グッモーニン エブリワン、ってひとりか。',
          'げほげほげほ、おばようごじゃいます'
        ],
        [
          'すいません。風邪をひいてしまいました。',
          '風邪をひきました。自己管理ができていないのは社会人としてお恥ずかしい限りです。',
          'なんか調子悪くってー、たぶん風邪だと思うのよ',
          'ゲホ！？げろげろげろ（吐いてる音）昨日から風邪をひいたみたいです。'
        ],
        [
          'きょうはお休みさせてください',
          'とりあえず午前中、お休みさせてください。体調が戻りしだい出社したいと思います。',
          'きょうはお休みさせてください。ただ、症状がひどいのであしたもお休みさせていただくかもしれません。',
          '辛くていつ会社にいけるかわかりません。あきらめてください。'
        ],
        [
          '先週末から風邪っぽかったのですが、無理をしてこじらせてしまいました。',
          '先日の残業時間に寒気を感じたのですが、仕事の締め切りがあったため無理をしてしまいました。それが原因かもしれません。',
          '飼っている猫が鼻をぐずぐずさせていたのですが、まさか人間にうつるとは思いませんでした。',
          'いつ風邪をひくか、いつ治るかと言うのはすべて決まっていることなのではありますが。'
        ],
        [
          '仕事でなにかありましたら、家で寝てますので携帯にかけてください（聞き苦しい声かもしれませんが）',
          '仕事で不明な点がありましたら、自宅に電話をかけてくださってもいいのですが、寝込んでいるため対応できないことがあるかと思います。',
          '仕事の件に関しては同じグループのものに聞いてもらえればわかると思います。',
          'いまは仕事とかどうでもいい気分です。自分の体をなおすことが先決です。'
        ],
        [
          'ご迷惑をおかけしますが、よろしくおねがいします。',
          'よろしくおねがいします。げほげほ、病院いってきます。',
          'では、よろしく。給食のプリンは食べてけっこうです。',
          'というか風邪というのは嘘です。遊びに行ってきます。チャオ！'
        ]
      ]
    },
    shareUrl() {
      const shareData = {
        ...this.questions.target,
        ...this.questions,
        target: null,
        share: 1
      }
      delete shareData.target
      return `https://dailyportalz.jp/kiji/kaze-mail-generator?${stringify(
        shareData
      )}`
    },
    twitterUrl() {
      return `https://twitter.com/intent/tweet?text=風邪でお休みメールジェネレーター&url=${encodeURIComponent(
        this.shareUrl
      )}`
    }
  },
  methods: {
    handleClickRestart() {
      location.href = location.href.replace(location.search, '')
    }
  }
}
</script>

<style scoped>
img {
  user-select: none;
}

.oyasumi-result {
  width: 526px;
  margin: 0 auto;
}

.oyasumi-result_main {
  font-size: 0;
}

.oyasumi-result__message {
  padding: 16px;
  font-size: 12px;
  flex: 1;
  min-height: 150px;
}

.oyasumi-result__message p:first-child {
  margin-top: 0;
}

.oyasumi-result_build {
  text-align: right;
}

.oyasumi-result_share {
  font-size: 12px;
}

.oyasumi-result_shareurl {
  width: 100%;
}

.oyasumi-result_share {
  display: flex;
  align-items: center;
}

input {
  margin: 4px 10px 4px 0;
  flex: 1;
}
</style>
