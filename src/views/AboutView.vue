<script setup>
import MainLayout from '../components/MainLayout.vue';

// Page Title of Views
const pageTitle = 'About'
</script>

<template>
  <MainLayout :pageTitle="pageTitle">
    <section class="about-us">
    <div class="about">
          <img src="../assets/elden.jpg" class="h-48 mr-10 overflow-hidden rounded-lg bg-gray-100 shadow-lg lg:h-auto xl:w-5/12">
      <div class="text">
        <h2>About Me</h2>
        <h5>Keth Elden Mondejar <span>BSIT  </span></h5>
        <p class="mb-5">As a fourth-year student pursuing a Bachelor of Science in Information Technology (BSIT) at Cordova Public College, I am deeply passionate about the ever-evolving realm of technology. My enthusiasm lies in absorbing and applying avant-garde concepts within software development, network administration, and IT management. </p>
        <p>Driven by a keen desire to contribute my skills and knowledge to real-world challenges, I am committed to refining my expertise and staying abreast of the latest industry trends. Outside the academic sphere, I actively participate in hands-on projects, collaborate with peers, and actively seek opportunities for personal and professional growth in the dynamic field of information technology.</p>
      </div>
    </div>
  </section>
  </MainLayout>
</template>
<style>
@import url('https://fonts.googleapis.com/css2?family=Poppins:wght@200;300;400;500&display=swap');
*{
  margin: 0;
  padding: 0;
  box-sizing: border-box;
  font-family: -apple-system, BlinkMacSystemFont, "Segoe UI", Roboto, Helvetica, Arial, sans-serif, "Apple Color Emoji", "Segoe UI Emoji", "Segoe UI Symbol";
}
.about-us{
  height: 100vh;
  width: 100%;
  padding: 90px 0;
}
.pic{
  height: auto;
  width:  302px;
}
.about{
  width: 1130px;
  max-width: 85%;
  margin: 0 auto;
  display: flex;
  align-items: center;
  justify-content: space-around;
}
.text{
  width: 540px;
}
.text h2{
  font-size: 40px;
  font-weight: 400;
  margin-bottom: 10px;

}
.text h5{
  font-size: 22px;
  font-weight: 500;
  margin-bottom: 20px;
}
span{
  color: #f49440;
}
.text p{
  font-size: 18px;
  line-height: 25px;
  letter-spacing: 1px;
}
.data{
  margin-top: 30px;
}


</style>