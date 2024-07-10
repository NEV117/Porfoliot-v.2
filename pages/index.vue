<template>
  	<main v-if="!loading" id="hello">

    	<!-- gradients -->
    	<div class="css-blurry-gradient-blue"></div>
    	<div class="css-blurry-gradient-green"></div>

		<section class="hero">
		
			<div class="head">
				<span>
					Hi all, I am
				</span>
				<h1>{{ config.dev.name }}</h1>
				<h2>> {{ config.dev.role }}</h2>

        <br><br>
        <button class="button" @click="downloadFile">
          <span class="button_lg">
              <span class="button_sl"></span>
              <span class="button_text">Download CV</span>
          </span>
      </button>
			</div>

			<div id="info">
				<span class="action">
					// complete the game to continue
				</span>
				<span :class="{hide: isMobile}">
					// you can also see it on my Github page
				</span>
				<span :class="{hide: !isMobile}">
					// find my profile on Github:
				</span>
				<p class="code">
					<span class="identifier">
						const
					</span>
					<span class="variable-name">
						githubLink
					</span>
					<span class="operator">
						=
					</span>
					<a class="string" :href="'https://github.com/' + config.public.dev.contacts.social.github.user">
						"https://github.com/{{ config.public.dev.contacts.social.github.user }}"
					</a>
				</p>
			</div>
		</section>

		<section data-aos="fade-up" class="game" v-if="!isMobile">
			<SnakeGame />
		</section>

	</main>
</template>

<style>

#hello { 
  display: flex;
  height: 100%;
  width: 100%;
  flex: 1 1 auto;
  padding-left: 275px;
  overflow: hidden;
  /* padding-top: 5rem; */ /* 80px */
}
.hero {
	width: 100%;
	justify-content: center;
	
}
.game {
	display: flex;
	flex-direction: column;
	width: 100%;
	height: 100%;
	justify-content: center;
/* 	align-items: center; */
	z-index: 20;
}

#hello .hero {
	display: flex;
	flex-direction: column;
	/* display: grid;
	grid-template-columns: repeat(12, minmax(0, 1fr)); */
	margin: 0rem;
}


#hello .head span {
  font-size: 18px;
  line-height: 1;
  color: #E5E9F0;
  font-family: 'Fira Code Retina';
}

#hello .head h1 {
  font-size: 48px;
  line-height: 1;
  color: #E5E9F0;
  font-family: 'Fira Code Regular';
  padding-top: 1rem; /* 16px */
  padding-bottom: 1rem; /* 16px */
}

#hello .head h2 {
  font-size: 22px;
  line-height: 1;
  color: #4D5BCE;
  font-family: 'Fira Code Retina';
}

.head {
  padding-bottom: 3rem;
}

#info {
	display: flex;
	flex-direction: column;
}

#info > span {
  font-size: 14px;
  line-height: 1;
  color: #607B96;
  font-family: 'Fira Code Retina';
  padding-bottom: 1rem; /* 16px */
}

.code {
  font-family: 'Fira Code Medium';
  color: #E5E9F0;
}

.code .identifier {
  color: #4D5BCE;
}

.code .variable-name {
  color: #43D9AD;
}

.code .operator {
  color: white;
}

.code .string {
  color: #E99287;
  text-decoration-line: underline;
  text-underline-offset: 4px;
}

#info {
	padding-block: 2.5rem;
}

#info .action {
	display: flex
}

.hide {
  display: none;
}

.css-blurry-gradient-blue {
  position: fixed;
  bottom: 25%;
  right: 5%;
  width: 300px;
  height: 300px;
	border-radius: 0% 0% 50% 50%;
  rotate: 10deg;
	filter: blur(70px);
  background: radial-gradient(circle at 50% 50%,rgba(77, 91, 206, 1), rgba(76, 0, 255, 0));
  opacity: 0.5;
  z-index: 10;
}

.css-blurry-gradient-green {
  position: absolute;
  top: 20%;
  right: 30%;
  width: 300px;
  height: 300px;
	border-radius: 0% 50% 0% 50%;
	filter: blur(70px);
  background: radial-gradient(circle at 50% 50%,rgba(67, 217, 173, 1), rgba(76, 0, 255, 0));
  opacity: 0.5;
  z-index: 10;
}

#info {
  font-size: 14px;
}


/* mobile */
@media (max-width: 768px) {

	#hello {
		padding-left: 0;
	}

	#hello .hero {
		display: flex;
		flex-direction: column;
		justify-content: space-between;
		margin: 1.75rem; /* 28px */
	}
	.head {
		padding-top: 4rem; /* 40px */
	}

	#hello .head h2 {
		font-size: 20px;
		color: #43D9AD;
	}
	
	#info .action {
		display: none;
	}

}

/* tablet */
@media (min-width: 768px) and (max-width: 1024px) {
	#hello {
		padding-left: 0;
	}
	#hello .hero {
		display: flex;
		flex-direction: column;
		justify-content: center;
		margin: 1.75rem; /* 28px */
	}
	.head {
		padding-top: 4rem; /* 40px */
	}

}

@media (min-width: 1024px) and (max-width: 1320px) {
	#hello {
		padding-left: 135px;
	}
}


/* LG */

@media (min-width: 1024px) {

  .css-blurry-gradient-blue {
    position: fixed;
    bottom: 10%;
    right: 10%;
    width: 500px;
    height: 500px;
    opacity: 0.7;
    border-radius: 100% 50% 100% 0%;
  }

  .css-blurry-gradient-green {
    position: fixed;
    top: 10%;
    right: 35%;
    filter: blur(100px);
    rotate: 10deg;
    width: 400px;
    height: 400px;
    opacity: 0.5;
    border-radius: 100% 0% 0% 0%;
    rotate: 20deg;
  }
}

@media (min-width: 1920px){
	#hello {
		padding-left: 310px;
	}
	#hello .head h1 {
		font-size: 62px;
	}
}

.button {
  -moz-appearance: none;
  -webkit-appearance: none;
  appearance: none;
  border: none;
  background: none;
  color: #0f1923;
  cursor: pointer;
  position: relative;
  padding: 8px;
  margin-bottom: 20px;
  text-transform: uppercase;
  font-weight: bold;
  font-size: 14px;
  transition: all .15s ease;
  z-index: 99;
}

.button::before,
.button::after {
  content: '';
  display: block;
  position: absolute;
  right: 0;
  left: 0;
  height: calc(50% - 5px);
  border: 1px solid #7D8082;
  transition: all .15s ease;
}

.button::before {
  top: 0;
  border-bottom-width: 0;
}

.button::after {
  bottom: 0;
  border-top-width: 0;
}

.button:active,
.button:focus {
  outline: none;
}

.button:active::before,
.button:active::after {
  right: 3px;
  left: 3px;
}

.button:active::before {
  top: 3px;
}

.button:active::after {
  bottom: 3px;
}

.button_lg {
  position: relative;
  display: block;
  padding: 10px 20px;
  color: #fff;
  background-color: #0f1923;
  overflow: hidden;
  box-shadow: inset 0px 0px 0px 1px transparent;
  z-index: 99;
}

.button_lg::before {
  content: '';
  display: block;
  position: absolute;
  top: 0;
  left: 0;
  width: 2px;
  height: 2px;
  background-color: #0f1923;
}

.button_lg::after {
  content: '';
  display: block;
  position: absolute;
  right: 0;
  bottom: 0;
  width: 4px;
  height: 4px;
  background-color: #0f1923;
  transition: all .2s ease;
}

.button_sl {
  display: block;
  position: absolute;
  top: 0;
  bottom: -1px;
  left: -8px;
  width: 0;
  background-color: #ff4655;
  transform: skew(-15deg);
  transition: all .2s ease;
}

.button_text {
  position: relative;
}

.button:hover {
  color: #0f1923;
}

.button:hover .button_sl {
  width: calc(100% + 15px);
}

.button:hover .button_lg::after {
  background-color: #fff;
}


</style>

<script>
export default {
  name: 'Hello',
  setup() {
    const config = useRuntimeConfig()
    return {
      config
    }
  },
  data() {
    return {
      isMobile: false,
      loading: true
    }
  },
  mounted() {
    // Detectamos si es mobile
    if (window.innerWidth <= 1024) {
      this.isMobile = true
    }

    // Escuchamos los cambios de tamaño de pantalla
    window.addEventListener('resize', this.handleResize)

    // When the component is mounted, we can remove the loader.
    this.loading = false
  },
  beforeDestroy() {
    // Remove the event listener when the component is destroyed.
    window.removeEventListener('resize', this.handleResize)
  },
  methods: {
    handleResize() {
      if (window.innerWidth <= 1024) {
        this.isMobile = true
      } else {
        this.isMobile = false
      }
    },
    downloadFile() {
      var fileUrl = '/files/NicolasEscandon.docx';
      // Crea un elemento <a> invisible
      var a = document.createElement('a');
      a.href = fileUrl;
      a.download = 'NicolasEscandon.docx'; // Nombre con el que se descargará el archivo

      // Agrega el elemento <a> al DOM
      document.body.appendChild(a);

      // Simula el clic en el enlace para iniciar la descarga
      a.click();

      // Elimina el elemento <a> del DOM después de la descarga
      document.body.removeChild(a);
    }
  }
}
</script>

