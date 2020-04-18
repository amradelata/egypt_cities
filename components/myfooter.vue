<template>
  <div class="footer">
    <div class="content">
      <p>
        Made with love by
        <a href="https://amradelata.github.io/">Amr Adel Ata</a>
      </p>
    </div>
    <div class="layout"></div>
  </div>
</template>

<style scoped>
.footer {
  background-image: url("https://unforgettablecruises.com/wp-content/uploads/2019/05/2-min-1.png");
  background-size: cover;
  background-position: center;
  height: 30vh;
  position: relative;
  text-align: center;
}
.layout {
  position: absolute;
  top: 0;
  bottom: 0;
  right: 0;
  left: 0;
  background: gray;
  opacity: 0.7;
}
.content {
  position: absolute;
  top: 50%;
  left: 50%;
  transform: translate(-50%, -50%);
  z-index: 9999;
}
p {
  color: #fff;
  font-size: 20px;
}
a {
  color: #dcdde1;
  font-weight: bold;
}

@media screen and (max-width: 768px) {
  .footer {
    height: 50vh;
  }
}
</style>
