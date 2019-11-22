 <template>
  <img class="heroImage" />
</template>

<script>
export default {
  name: 'HeroImage',
};
</script>
<style lang="scss" scoped>
  .heroImage {
    width: 100%;
    height: 100vh;
    top: 0;
    z-index: -1;
    position: fixed;
    background-image: url('../assets/heroimage.jpg');
    background-repeat: no-repeat;
    background-size: cover;
    background-position: 80% 0%;
  }

  .heroImage::after {
    content: '';
    background: rbga(0,0,0, .2);
    position: absolute;
    width: 100%;
    height: 100vh;
    z-index: 1;
    top: 0;
    left: 0;
  }
</style>
