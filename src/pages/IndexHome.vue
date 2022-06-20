<template>
  <q-page class="relative-position">
    <q-scroll-area class="absolute full-width full-height">
      <div class="q-py-lg q-px-md row items-end q-col-gutter-md">
        <div class="col">
          <q-input bottom-slots v-model="newTweetContent" class="q-tweet" placeholder="What's your tweets now?" counter maxlength="250" autogrow>
            <template v-slot:before>
              <q-avatar size="xl">
                <img src="https://i.pinimg.com/736x/d5/57/09/d55709eda0e977af153b3a4e381644a4.jpg">
              </q-avatar>
            </template>
          </q-input>
        </div>
        <div class="col col-shrink">
          <q-btn @click="addNewTweet" :disable="!newTweetContent" color="primary" label="Tweet" class="q-mb-lg" unelevated rounded no-caps/>
        </div>
      </div>
      <q-separator size="10px" color="grey-2" class="divider" />
      
      <q-list separator>
        <transition-group
          appear
          enter-active-class="animated fadeIn"
          leave-active-class="animated fadeOut"
        >
          <q-item v-for="tweet in tweets" :key="tweet.date" class="tweet q-py-md">
            <q-item-section avatar top>
              <q-avatar size="xl">
                <img src="https://i.pinimg.com/736x/d5/57/09/d55709eda0e977af153b3a4e381644a4.jpg">
              </q-avatar>
            </q-item-section>

            <q-item-section>
              <q-item-label class="text-subtitle1"><strong>Genshin Impact Official - ID</strong> <span class="text-grey-7">@GenshinImpactID &bull; {{tweet.date}}</span></q-item-label>
              <q-item-label class="tweet-content text-body1">
                {{tweet.content}}
              </q-item-label>

              <div class="tweet-icons row justify-between q-mt-sm">
                <q-btn flat round color="grey" icon="far fa-comment" size="sm" />
                <q-btn flat round color="grey" icon="fas fa-retweet" size="sm" />
                <q-btn flat round color="grey" icon="far fa-heart" size="sm" />
                <q-btn @click="deleteTweet(tweet)" flat round color="grey" icon="fas fa-trash" size="sm" />
              </div>
            </q-item-section>

            <!-- <q-item-section side top>
              {{tweet.date}}
            </q-item-section> -->
          </q-item>
        </transition-group>

        <q-separator inset="item" />
      </q-list>
    </q-scroll-area>
  </q-page>
</template>

<script>
// import { Datepicker } from '../src/datepicker/Datepicker.vue'
import { formatDistance } from 'date-fns'
import { defineComponent } from 'vue'

export default defineComponent({
  name: 'IndexHome',
  data() {
    return {
      newTweetContent: '',
      tweets: [
        {
          content: 'Genshin Impact Akan Segera Rilis di GeForce NOW ! Dear Traveler, Uji coba Genshin Impact di GeForce NOW akan segera selesai dan akan resmi dirilis sepenuhnya pada minggu depan. Traveler dapat memainkan Genshin Impact dari jarak jauh tanpa perlu mengunduh data game!',
          // date: new Date().getUTCSeconds()
          date: '2 Minutes'
        },
        {
          content: '[Event Berhadiah] Kontes Fan Art "Hanamizaka Heroics" Arataki Itto Dimulai! Dear Traveler, Kontes Fan Art Arataki Itto sudah dimulai! Siapkan alat gambarmu dan ikuti eventnya~ [Waktu Event] 15 Juni 2022 - 6 Juli 2022 23:59 (UTC+8) Lihat pengumuman di sini > > > https://genshin.hoyoverse.com/id/news/detail/21490 #GenshinImpact #HoYoverse #AratakiItto',
          date: '25 Minutes'
        },
        {
          content: 'Mini Album: Aspirasi Hanamizaka | Genshin Impact Hidup Arataki Itto itu sangat simpel. Dia melakukan apa saja sesuka hatinya, dan dia akan cuti tiga hari setelah bekerja satu hari. Hidup Arataki Itto juga sangat rumit. Karena seseorang yang sangat menarik perhatian seperti Itto akan sulit punya waktu yang tenang dan damai.',
          date: '1 Hour ago'
        },
        {
          content: 'Kuberi kalian dengar suara lagu terenak di dunia! Dengar-dengar hari ini ada yang dengar suara lagu aneh dari atas puncak gunung Siapa pula yang konser di atas puncak gunung ya?',
          date: '2 Hour ago'
        },
        {
          content: 'Event Petualangan Penuh Lumpur: Tantangan Membersihkan Jalur Tambang Selama event berlangsung, pergi ke Chasm dan bantu peneliti Sumeru untuk mengatasi krisis lumpur hitam yang merajalela dan membersihkan jalur tambang. Selesaikan misi yang ditentukan untuk mendapatkan Primogem, Hero Wit, Material Penguatan Talenta, Mystic Enhancement Ore, dan hadiah lainnya.',
          date: '1 day ago'
        }
      ]
    }
  },
  methods: {
    addNewTweet() {
      let newTweet = {
        content: this.newTweetContent,
        date: 'a few minutes ago'
      }
      this.tweets.unshift(newTweet)
      this.newTweetContent = ''
    },
    deleteTweet(tweet) {
      let dateToDelete = tweet.date
      let index = this.tweets.findIndex(tweet => tweet.date === dateToDelete)
      this.tweets.splice(index,1)
    }
  },
  filters: {
    relativeDate(value) {
      return formatDistance(value, new Date())
    }
  },
})
</script>

<style lang="sass">
.q-tweet
  textarea
    font-size: 19px
    line-height: 1.4 !important
.divider
 border-top: 1px solid
 border-bottom: 1px solid
 border-color: $grey-4
 .tweet-content
   white-space: pre-line 
.tweet-icons
  margin-left: 5px
.tweet:not(:first-child)
  border-top: 1px solid rgba(0, 0, 0, 0.12)
</style>
