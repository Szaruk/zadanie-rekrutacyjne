<template>
  <div class="icon-container">
    <div class="search-input-box">
      <input class="search-input" type="search" placeholder="Search" />
      <img class="search-icon" src="../assets/icons/search_icon.svg" alt="" />
    </div>
    <div class="info-container">
      <div class="info-icon-box">
        <img src="../assets/icons/info_icon.svg" alt="" />
      </div>
      <div class="info-icon-box">
        <img src="../assets/icons/hamburger_icon.svg" alt="" />
      </div>
    </div>
  </div>
</template>

<script>
export default {};
</script>

<style lang="scss" scoped>
.icon-container {
  display: flex;
  justify-content: space-between;
  .search-input-box {
    position: relative;
    .search-input {
      width: 232px;
      height: 48px;
      border-radius: 8px;
      background: #f7f7f9;
      color: #9896a1;
      border: none;
      padding-left: 3rem;
      font-weight: 400;
      font-size: 14px;
      line-height: 24px;
      &:focus {
        color: #9896a1;
      }
      &:hover {
        cursor: pointer;
      }
    }
    .search-icon {
      position: absolute;
      content: "";
      top: 1.2rem;
      left: 1rem;
      &:hover {
        cursor: pointer;
      }
    }
  }
  .info-container {
    display: flex;
    .info-icon-box {
      display: flex;
      justify-content: center;
      align-items: center;
      width: 48px;
      height: 48px;
      background: #f7f7f9;
      border-radius: 8px;
      margin-left: 1rem;
      margin-right: 1rem;
      &:hover {
        cursor: pointer;
        img {
          transition: opacity 0.3s ease-in-out;
          opacity: 0.4;
        }
      }
      &:first-child {
        position: relative;
        &::after {
          position: absolute;
          border-radius: 2rem;
          top: -0.3rem;
          right: -0.5rem;
          content: "";
          width: 12px;
          height: 12px;
          background: #ea4d4d;
          border: 2px solid #ffffff;
        }
      }
    }
  }
}
</style>
