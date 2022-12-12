<template>
  <main id="main-container">
    <IconContainer />
    <CurrentData />
  </main>
</template>

<script>
import IconContainer from "../components/BarContainer.vue";
import CurrentData from "../components/CurrentData.vue";
export default {
  components: { IconContainer, CurrentData },
};
</script>

<style scoped lang="scss">
#main-container {
  width: 1176px;
  height: 900px;
  border-radius: 2rem;
  background: #fff;
  display: flex;
  flex-direction: column;
  padding: 3rem;
  overflow: hidden;
  @media screen and (max-width: 1130px) {
    width: 100%;
  }
  @media screen and (max-width: 899px) {
    height: 100%;
  }
}
</style>
