<template>
  <DaCard class="card--a" :class="ad.source" :title="ad.description" :url="ad.link"
          :image="ad.image" :placeholder="ad.placeholder" :size="size"
          :image-background="ad.backgroundColor" @click="$emit('click', ad)"
          :lines="4">
    <template slot="content">
      <img v-for="(item, index) in pixel" :key="index" :src="item" class="card__pixel"/>
    </template>
    <a slot="footer" class="card__footer__promoted micro2" target="_blank"
       :href="ad.referralLink" v-if="ad && ad.referralLink">/* {{ promoted }} */</a>
    <span slot="footer" class="card__footer__promoted micro2" v-else>/* {{ promoted }} */</span>
  </DaCard>
</template>

<script>
import DaCard from './DaCard.vue';

export default {
  name: 'DaCardAd',
  components: { DaCard },
  props: {
    ad: {
      type: Object,
      required: true,
    },
  },

  computed: {
    size() {
      return this.ad.size || 'small';
    },

    pixel() {
      return this.ad.pixel || [];
    },

    promoted() {
      if (this.ad.company) {
        return `Promoted by ${this.ad.company}`;
      }

      return 'Promoted';
    },
  },

  mounted() {
    this.$emit('impression', this.ad);
  },
};
</script>
<style>
.card--a .card__footer {
  justify-content: center;
}

.card--a.BSA .card__background__image {
  left: 0;
  right: 0;
  top: 0;
  bottom: 0;
  max-width: 250px;
  max-height: 100px;
  margin: auto;
}

.card__footer__promoted {
  color: var(--theme-secondary);
  text-transform: uppercase;
  text-decoration: none;
}

.card__pixel {
  display: none;
  width: 0;
  height: 0;
}
</style>
