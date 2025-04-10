<template>
    <section  class="about-us">
      <div id = "about-section" class="about-content">
        <div class="text-content">
          <h1>{{ $t('aboutUsTitle') }}</h1>
          <p>{{ $t('aboutUsDescription') }}</p>
        </div>
        <div class="image-container">
          <img src="https://orchestra-website-5e76d.web.app/images/about-centered.webp" alt="About Us Image" class="about-image" />
        </div>
      </div>
    </section>
  </template>
  
  <script>
  export default {
    name: 'AboutUs',
  };
  </script>
  
  <style scoped>
  .about-us {
    display: flex;
    justify-content: center;
    align-items: center;
    background-color: black;
    color: white;
    padding: 60px 20px;
  }
  
  .about-content {
    display: flex;
    flex-direction: row;
    align-items: center;
    justify-content: center;
    width: 100%;
  }
  
  .text-content {
    flex: 1;
    padding-right: 30px;
    padding-left: 100px;
  }
  
  .text-content h1 {
    font-size: 3rem;
    margin-bottom: 20px;
  }
  
  .text-content p {
    font-size: 1.5rem;
    line-height: 1.6;
    color: #d3d3d3;
  }
  
  /*.image-container {
    flex: 1;
    max-width: 600px;
    width: 100%;
  }
*/
  .image-container {
  display: flex;
  justify-content: center;
  max-width: 600px;
}
  
  .about-image {
    width: 100%;
    height: auto;
    border-radius: 8px;
  }
  
  @media (max-width: 1080px) {
    .about-content {
      flex-direction: column;
      text-align: center;
    }
  
    .text-content {
      padding: 0 20px;
      margin-bottom: 20px;
      display: flex;
      flex-direction: column;
      align-items: center;
      text-align: center;
    }

  
    .about-image {
      width: 80%;
      margin-top: 20px;
    }
  
    .text-content h1 {
      font-size: 2.5rem;
    }
  
    .text-content p {
      font-size: 1.2rem;
    }
  }
  </style>
  