<template>
  <router-view />
</template>

<style lang="scss">
@font-face {
  font-family: "SF Pro Display";
  src: local("SF Pro Display"),
    url(./fonts/SFPRODISPLAYREGULAR.OTF) format("truetype");
}
* {
  margin: 0;
  padding: 0;
  box-sizing: border-box;
  font-family: "SF Pro Display", Helvetica, Arial;
}
#app {
  display: flex;
  justify-content: center;
  align-items: center;
  background: black;
  min-height: 100vh;
}
h2 {
  font-style: normal;
  font-weight: 500;
  font-size: 20px;
  line-height: 24px;
  color: #0a041c;
}
h3 {
  font-style: normal;
  font-weight: 500;
  font-size: 16px;
  line-height: 24px;
  color: #0a041c;
}
.invest-button-box {
  margin-top: 6rem;
  display: flex;
  .violet-button {
    width: 109px;
    background: #7445fb;
    border-radius: 4px;
    font-weight: 400;
    font-size: 14px;
    line-height: 24px;
    padding: 0.5rem;
    color: #fff;
    border: 1px solid #7445fb;
    transition: all 0.4s ease-in-out;
  }
  .white-button {
    width: 109px;
    background: #fff;
    border-radius: 4px;
    font-weight: 400;
    font-size: 14px;
    line-height: 24px;
    padding: 0.5rem;
    color: #7445fb;
    border: 1px solid #ebebf3;
    transition: all 0.4s ease-in-out;
  }
  .violet-button,
  .white-button {
    margin-left: 1rem;
    &:hover {
      cursor: pointer;
      opacity: 0.5;
    }
  }
}
.button-box {
  display: flex;
  align-items: center;
  .sell-button {
    width: 55px;
    height: 40px;
    background: #ffffff;
    border: 1px solid #ebebf3;
    border-radius: 4px;
    font-style: normal;
    font-weight: 600;
    font-size: 14px;
    line-height: 24px;
    color: #7445fb;
    margin-right: 1rem;
    transition: all 0.4s ease-in-out;
    @media screen and (max-width: 655px) {
      font-size: 11px;
      width: 45px;
      height: 30px;
    }
  }
  .buy-button {
    background: #7445fb;
    border: solid #7445fb 1px;
    border-radius: 4px;
    width: 56px;
    height: 40px;
    color: #ffffff;
    font-style: normal;
    font-size: 14px;
    line-height: 24px;
    transition: all 0.4s ease-in-out;
    @media screen and (max-width: 655px) {
      font-size: 11px;
      width: 45px;
      height: 30px;
    }
  }
  .buy-button:hover {
    cursor: pointer;
    opacity: 0.4;
  }
  .sell-button:hover {
    cursor: pointer;
    opacity: 0.4;
  }
}
</style>
