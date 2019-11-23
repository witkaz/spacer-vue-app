 <template>
  <!-- <img :src="photo" :alt="title"> -->
  <div :style="style" class="item"></div>
</template>

<script>
export default {
  name: 'ResultsItem',
  props: {
    item: {
      type: Object,
      required: true,
    },
  },
  data() {
    return {
      photo: this.item.links[0].href,
      title: this.item.data[0].title,
    };
  },
  // computed aktualizuje wartość style, jesli obiekt data się zmieni, dlatego photo
  // juz nie bedzie undefined
  computed: {
    style() {
      return `background-image: url("${this.photo}")`;
    },
  },
};
</script>
<style lang="scss" scoped>
  .item {
    width: 40vw;
    height: 250px;
    background-repeat: no-repeat;
    background-size: cover;
    background-position: 50%;

    @media (min-width: 768px) {
      width: 25vw;
    }
  }
</style>
