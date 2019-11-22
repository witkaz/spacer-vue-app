 <template>
  <div class="searchWrapper">
    <input id="search" name="search" :value="value" @input="handleChange">
  </div>
</template>

<script>
export default {
  name: 'SearchInput',
  props: {
    value: {
      type: String,
      required: true,
    },
  },
  methods: {
    // emituje event do rodzica App.vue
    handleChange(e) {
      this.$emit('input', e.target.value);
    },
  },
};
</script>
<style lang="scss" scoped>
  .searchWrapper {
    width: 250px;
    display: flex;
    flex-direction: column;
    margin-top: 50px;
    input {
      color: #fff;
      text-align: center;
      font-size: 18px;
      font-weight: 300;
      height: 30px;
      border: 0;
      border-bottom: 1px solid #fff;
      background: none;
      transition: box-shadow .3s ease-out;

      @media (min-width: 1024px) {
        font-weight: 400;
      }
    }

    input:focus {
      outline: none;
      box-shadow: 0 10px 20px -8px rgba(255,255,255, .5);
    }
  }
</style>
