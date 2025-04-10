<template>
    <footer class="footer" id = "footer-section">
      <div class="footer-left">
        <img src="https://orchestra-website-5e76d.web.app/images/logo_gold.webp" alt="Logo" class="footer-logo" />
        <div class="footer-info">
          <h2 class="footer-title">NU ORCHESTRA</h2>
          <p>📧 Orchestra@nu.edu.kz</p>
          <p>📞 +7 (708) 092-68-77</p>
          <p>📞 +7 (707) 240-12-56</p>
        </div>
      </div>
  
      <div class="footer-socials">
        <a href="https://www.instagram.com/nuorchestra?igsh=a2ViYTE1dnd3dHhm" target="_blank" rel="noopener" class="social-link">
          <img src="@/assets/instagram.png" alt="Instagram" />
        </a>
        <a href="https://t.me/nuorchestra" target="_blank" rel="noopener" class="social-link">
          <img src="@/assets/telegram.png" alt="Telegram" />
        </a>
        <a href="https://wa.me/77080926877" target="_blank" rel="noopener" class="social-link">
          <img src="@/assets/whatsapp.png" alt="WhatsApp" />
        </a>
        <a href="mailto:Orchestra@nu.edu.kz" target="_blank" rel="noopener" class="social-link">
          <img src="@/assets/gmail.png" alt="Gmail" />
        </a>
      </div>
    </footer>
  </template>
  
  <script>
  export default {
    name: "FooterSection"
  };
  </script>
  
  <style scoped>
  .footer {
    display: flex;
    justify-content: space-between;
    align-items: flex-start;
    background: white;
    color: black;
    padding: 40px 60px;
    flex-wrap: wrap;
    gap: 30px;
  }
  
  .footer-left {
    display: flex;
    align-items: flex-start;
    gap: 20px;
  }
  
  .footer-logo {
    height: 160px;
    width: auto;
  }
  
  .footer-info {
    display: flex;
    flex-direction: column;
    font-size: 16px;
    gap: 6px;
  }

  .footer-info p{
    margin: 4px;
  }
  
  .footer-title {
    margin: 0;
    font-family: 'Playfair Display SC', serif;
    font-size: 24px;
    color: black;
  }
  
  .footer-socials {
    display: flex;
    gap: 20px;
    align-items: center;
    margin-left: auto;
  }
  
  .social-link img {
    width: 30px;
    height: 30px;
    transition: opacity 0.3s;
  }
  
  .social-link:hover img {
    opacity: 0.7;
  }

  @media (max-width: 768px){
    .footer {
      flex-direction: column;
    }
    .footer-socials {
      margin: 0;
    }
  }

  @media (max-width: 480px) {
    .footer-logo {
      height: 80px;
      width: auto;
    }
  }
  </style>
  
  