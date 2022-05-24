<template>
  <main
    class="
      w-screen
      h-auto
      min-h-screen
      flex flex-column
      align-items-center
      justify-content-start
    "
  >
    <section
      class="
        banner
        w-screen
        flex flex-row
        align-items-center
        justify-content-center
      "
    >
      <div
        class="
          banner-info
          flex flex-row
          align-items-center
          justify-content-center
        "
      >
        <div
          class="
            info-content
            flex flex-column
            align-items-start
            justify-content-center
          "
        >
          <img :src="banner.logo" alt="Movie Logo" />
          <div
            class="
              rating
              flex flex-row
              align-items-center
              justify-content-start
            "
          >
            <i class="m-1 w-auto pi pi-star-fill"></i>
            <i class="m-1 w-auto pi pi-star-fill"></i>
            <i class="m-1 w-auto pi pi-star-fill"></i>
            <i class="m-1 w-auto pi pi-star-fill"></i>
            <i class="m-1 w-auto pi pi-star-fill"></i>
            <span>2016 2 seasons</span>
          </div>
          <!-- v-if serve para ser mostrado caso exista algum valor na variavel -->
          <p v-if="banner.description">{{ banner.description }}</p>
        </div>
      </div>

      <img class="logoManflix" src="manflix.png" alt="Manflix" />
      <div class="banner-image">
        <img :src="banner.image" alt="" />
        <!-- v-bind: é para classes etc, já o {{}} é para html em geral -->
      </div>
    </section>

    <section
      class="
        movies
        w-screen
        h-auto
        flex flex-column
        align-items-start
        justify-content-center
      "
    >
    <!-- ( ((index - 1) * noItems ) + (subIndex - 1) ) -->
      <!-- LISTAGEM CATEGORIA ACAO -->
      <div class="movies-category">
        <!-- o :key eh o item q vai mudar toda vez! -->
        <section v-for="index in noSection" :key="index" :id="'section' + index"> 

          <a :href="'#section' + (index - 1 <= 0 ? noSection : index - 1) "><</a>
          <div  v-for="subIndex in noItems" :key="subIndex" class="item" v-onClick="() =>{
            banner.image = $store.state.BASE_URL + movies[2].movies[( ((index - 1) * noItems ) + (subIndex - 1) )].image
            banner.logo = $store.state.BASE_URL + movies[2].movies[( ((index - 1) * noItems ) + (subIndex - 1) )].logo
            banner.description = $store.state.BASE_URL + movies[2].movies[( ((index - 1) * noItems ) + (subIndex - 1) )].descricao
            }">
            <img
              v-if="movies[2] !== undefined"
              :src="$store.state.BASE_URL + movies[2].movies[( ((index - 1) * noItems ) + (subIndex - 1) )].foto"
            />
          </div>
          
          <a :href="'#section' + (index + 1 > noSection? 1 : index + 1 )">></a>
        </section>

        <!-- <section id="section2">
          <a href="#section1"><</a>
           <div class="item">
            <img
              src="https://occ-0-185-1740.1.nflxso.net/dnm/api/v6/X194eJsgWBDE2aQbaNdmCXGUP-Y/AAAABTcOPiPTgagHms4XLYIkb8G-yA6SbMUzNrHPuR2Hh4HLckTllaAcELsvrESE3UweX-jDKYCpaVS3ADe6ETIZI7Htlm1IhchXFmM.webp?r=bb1"
            />
          </div>
          <div class="item">
            <img
              src="https://occ-0-185-1740.1.nflxso.net/dnm/api/v6/X194eJsgWBDE2aQbaNdmCXGUP-Y/AAAABY5IZ090i-iTHduH8ZluEULM4ONCW4CgRr3bFk2U1AVKZ7mVzVhxO6kw44126wC7IA6Q0nhols5baiicBDRBlbNzlLHA5HZ4SOpns91x98Hh7Be1rsTC_0azMZ7iDoCKeFGO.jpg?r=0dc"
            />
          </div>
          <div class="item">
            <img
              src="https://occ-0-185-1740.1.nflxso.net/dnm/api/v6/X194eJsgWBDE2aQbaNdmCXGUP-Y/AAAABcDwK_4UxlEq0Zqc6b_dfPz_0X9_iyBIH7gjMCp5zSlUiyEZTHbGBvQKrYHr8pbsgg63xyPKsP7Y_w07UXZ8liVmXfB5e7cKdNzVwE4zZiIAPgQOLkxLbXY-vPRRtr5rSm1V.jpg?r=cba"
            />
          </div>
          <div class="item">
            <img
              src="https://occ-0-185-1740.1.nflxso.net/dnm/api/v6/X194eJsgWBDE2aQbaNdmCXGUP-Y/AAAABbSwpZEHY1ihRrw4sJ8_neQQXpp6a3uk8g_17-giQgcqYv3BIREu_vuaJyTVH3AJ6AoVrVUY-HaKbJ0dcTDdY0IEfHTtd0xN1Nc.webp?r=7c1"
            />
          </div>
          <a href="#section3">></a>
        </section>

        <section id="section3">
          <a href="#section2"><</a>
           <div class="item">
            <img
              src="https://occ-0-185-1740.1.nflxso.net/dnm/api/v6/X194eJsgWBDE2aQbaNdmCXGUP-Y/AAAABTcOPiPTgagHms4XLYIkb8G-yA6SbMUzNrHPuR2Hh4HLckTllaAcELsvrESE3UweX-jDKYCpaVS3ADe6ETIZI7Htlm1IhchXFmM.webp?r=bb1"
            />
          </div>
          <div class="item">
            <img
              src="https://occ-0-185-1740.1.nflxso.net/dnm/api/v6/X194eJsgWBDE2aQbaNdmCXGUP-Y/AAAABY5IZ090i-iTHduH8ZluEULM4ONCW4CgRr3bFk2U1AVKZ7mVzVhxO6kw44126wC7IA6Q0nhols5baiicBDRBlbNzlLHA5HZ4SOpns91x98Hh7Be1rsTC_0azMZ7iDoCKeFGO.jpg?r=0dc"
            />
          </div>
          <div class="item">
            <img
              src="https://occ-0-185-1740.1.nflxso.net/dnm/api/v6/X194eJsgWBDE2aQbaNdmCXGUP-Y/AAAABcDwK_4UxlEq0Zqc6b_dfPz_0X9_iyBIH7gjMCp5zSlUiyEZTHbGBvQKrYHr8pbsgg63xyPKsP7Y_w07UXZ8liVmXfB5e7cKdNzVwE4zZiIAPgQOLkxLbXY-vPRRtr5rSm1V.jpg?r=cba"
            />
          </div>
          <div class="item">
            <img
              src="https://occ-0-185-1740.1.nflxso.net/dnm/api/v6/X194eJsgWBDE2aQbaNdmCXGUP-Y/AAAABbSwpZEHY1ihRrw4sJ8_neQQXpp6a3uk8g_17-giQgcqYv3BIREu_vuaJyTVH3AJ6AoVrVUY-HaKbJ0dcTDdY0IEfHTtd0xN1Nc.webp?r=7c1"
            />
          </div>
          <a href="#section1">></a>
        </section> -->
      </div>
    </section>
  </main>
</template>

<script>
export default {
  name: "home",
  // proteger essa tela somente para usuarios logados
  // middleware: 'auth',
  data() {
    return {
      banner: {
        image: "https://images8.alphacoders.com/934/thumb-1920-934722.jpg",
        logo: "https://occ-0-185-1740.1.nflxso.net/dnm/api/v6/tx1O544a9T7n8Z_G12qaboulQQE/AAAABdlLaSHqUMLyPj3keradZBjfSo_4grbDXwLkconYHhSQHiX_8u0HPYPhVwdOvphjGLdo-PzZr7a1Hqv9mPhnQbPuPGZuAfm9mG3lNMhK85g.webp?r=71a",
        description:
          "Lorem Ipsum is simply dummy text of the printing and typesetting industry. Lorem Ipsum has been the industrys standard dummy text ever since the 1500s, when an unknown printer took a galley of type and scrambled it to make a type specimen book.",
      },
      movies: [],
      categories: [],
      noSection: 2,
      noItems: 4
    };
  },
  methods: {
    getCategories: async function () {
      await this.$axios
        .get(this.$store.state.BASE_URL + "/categoria")
        .then((response) => {
          console.log("categorias:", response.data);
          this.categories = response.data;
        })
        .catch((error) => {
          console.log("categorias erro:", error);
        });
    },
    getMovie: async function () {
      //map -> loop e retornar o objeto
      //forEach -> loop funciona da msm forma, mas n retorna

      this.categories.map((category) => {
        this.$axios
          .get(this.$store.state.BASE_URL + "/filmes?categoria=" + category.id)
          .then((response) => {
            console.log(response.data);
            //push nao reescreve, ele serve para adicionar as categorias sem apagar as anteriores.
            this.movies.push({
              category: category,
              movies: response.data,
            });
            console.log("this.movies", this.movies);
          })
          .catch((error) => {
            console.log(error);
          });
      });
    },
  },
  async created() {
    // esse await é esperar essas funcoes serem concluidas para ir para a proxima!
    // no created a ordem importa!
    await Promise.all([this.getCategories()]);
    this.getMovie();
  },
};
</script>

<style lang="scss" scoped>
$height-banner: 52vh;
$width-banner-image: 55vw;

main {
  background-color: var(--background-banner);
  color: var(--placeholder-field-color);
  .banner {
    height: $height-banner;
    background-color: var(--background-banner);

    .banner-info {
      height: 100%;
      width: calc(100vw - $width-banner-image);

      .info-content {
        /* background-color: red; */
        width: 80%;
        img {
          width: 390px;
          height: 170px;
        }
        i {
          color: var(--background-btn-color);
        }
      }
    }
    .banner-image {
      width: $width-banner-image;
      height: 100%;
      img {
        width: 100%;
        height: 100%;
        /* PARA NAVEGADORES COMO OPERA, BRAVE */
        -webkit-mask-image: linear-gradient(
          to right,
          transparent 0%,
          black 11%
        );
        /* PARA NAVEGADORES COMUNS */
        mask-image: linear-gradient(to right, transparent 0%, black 11%);
      }
    }
    .logoManflix {
      /* esqueça as estruturas,vá para onde eu te falei: */
      position: absolute;
      top: 10px;
      right: 50vw;
      width: 180px;
      height: 55px;
      z-index: 100; /* trabalha na profundidade */
    }
  }
  .movies {
    $itemGrow: 1.2;
    $duration: 250ms;
    min-height: calc(100vh - $height-banner);
    scroll-behavior: smooth;

    .movies-category {
      width: 100vw;
      display: grid; //para dividir em colunas, para DIVIDIR AS PAGINAZINHAS DE SCROLL
      grid-template-columns: repeat(3, 100%);
      overflow: hidden;
      scroll-behavior: smooth; //EFEITO DE SLIDER
      
      section {
        width: 100%;
        position: relative;
        display: grid;
        grid-template-columns: repeat(4, auto);
        margin: 20px 0; // x e y
        .item {
          cursor: pointer;
          padding: 0 20px;
          transition: $duration all;
          &:hover {
            margin: 0 40px;
            transform: scale($itemGrow);
          }
        }
        i {
          color: white;
        }
        a {
          position: absolute;
          color: white;
          text-decoration: none;
          font-size: 6rem;
          background-color: black;
          width: 80px;
          padding: 20px;
          text-align: center;
          z-index: 1;

          &:nth-of-type(1) {
            top: 0;
            bottom: 0;
            left: 0;
            background: linear-gradient(
              -90deg,
              rgba(0, 0, 0, 0) 0%,
              rgba(0, 0, 0, 0) 100%
            );
          }

          &:nth-of-type(2) {
            top: 0;
            bottom: 0;
            right: 0;
            background: linear-gradient(
              90deg,
              rgba(0, 0, 0, 0) 0%,
              rgba(0, 0, 0, 0) 100%
            );
          }
        }
      }
    }
  }
}
</style>