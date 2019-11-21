 <template>
  <div class="searchWrapper">
    <input id="search" name="search" v-model="searchValue" @input="handleInput">
  </div>
</template>

<script>
export default {
  name: 'SearchInput',
};
</script>
<style lang="scss" scoped>
  .searchWrapper {
    width: 250px;
    display: flex;
    flex-direction: column;
    margin-top: 50px;
    input {
      height: 30px;
      border: 0;
      border-bottom: 1px solid black;
      background: none;
    }
  }
</style>
