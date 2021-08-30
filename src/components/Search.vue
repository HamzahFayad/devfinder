<template>
  <div id="search">
    <input
      type="text"
      placeholder="Search Github username..."
      v-model="username"
      @keydown.enter="search()"
    />

    <div class="userCard" v-if="userInfos">
      <div class="userCard__img">
        <img :src="userInfos.avatar_url" alt="" />
      </div>
      <div class="userCard__content">
        <div class="c1">
          <h2>{{ userInfos.login }}</h2>
          <p>Joined: 25 Jan 2018</p>
        </div>
        <a :href="userInfos.html_url" target="_black">@{{ userInfos.login }}</a>
        <p class="bio" v-if="userInfos.bio">{{ userInfos.bio }}</p>
        <p v-else>This profile has no bio</p>
        <div class="infos">
          <div>
            <p>Repos</p>
            <h3>{{ userInfos.public_repos }}</h3>
          </div>
          <div>
            <p>Followers</p>
            <h3>{{ userInfos.followers }}</h3>
          </div>
          <div>
            <p>Following</p>
            <h3>{{ userInfos.following }}</h3>
          </div>
        </div>
        <div class="infos2">
          <div>
            <div class="logo1"></div>
            <svg
              aria-hidden="true"
              focusable="false"
              data-prefix="fas"
              data-icon="map-marker-alt"
              class="svg-map fa-map-marker-alt fa-w-12"
              role="img"
              xmlns="http://www.w3.org/2000/svg"
              viewBox="0 0 384 512"
            >
              <path
                fill="currentColor"
                d="M172.268 501.67C26.97 291.031 0 269.413 0 192 0 85.961 85.961 0 192 0s192 85.961 192 192c0 77.413-26.97 99.031-172.268 309.67-9.535 13.774-29.93 13.773-39.464 0zM192 272c44.183 0 80-35.817 80-80s-35.817-80-80-80-80 35.817-80 80 35.817 80 80 80z"
              ></path>
            </svg>
            <p v-if="userInfos.location">{{ userInfos.location }}</p>
            <p style="color: gray" v-else>No location</p>
          </div>
          <div>
            <svg
              aria-hidden="true"
              focusable="false"
              data-prefix="fab"
              data-icon="twitter"
              class="svg-twitter fa-w-16"
              role="img"
              xmlns="http://www.w3.org/2000/svg"
              viewBox="0 0 512 512"
            >
              <path
                fill="currentColor"
                d="M459.37 151.716c.325 4.548.325 9.097.325 13.645 0 138.72-105.583 298.558-298.558 298.558-59.452 0-114.68-17.219-161.137-47.106 8.447.974 16.568 1.299 25.34 1.299 49.055 0 94.213-16.568 130.274-44.832-46.132-.975-84.792-31.188-98.112-72.772 6.498.974 12.995 1.624 19.818 1.624 9.421 0 18.843-1.3 27.614-3.573-48.081-9.747-84.143-51.98-84.143-102.985v-1.299c13.969 7.797 30.214 12.67 47.431 13.319-28.264-18.843-46.781-51.005-46.781-87.391 0-19.492 5.197-37.36 14.294-52.954 51.655 63.675 129.3 105.258 216.365 109.807-1.624-7.797-2.599-15.918-2.599-24.04 0-57.828 46.782-104.934 104.934-104.934 30.213 0 57.502 12.67 76.67 33.137 23.715-4.548 46.456-13.32 66.599-25.34-7.798 24.366-24.366 44.833-46.132 57.827 21.117-2.273 41.584-8.122 60.426-16.243-14.292 20.791-32.161 39.308-52.628 54.253z"
              ></path>
            </svg>
            <p v-if="userInfos.twitter_username">
              {{ userInfos.twitter_username }}
            </p>
            <p style="color: gray" v-else>Not Available</p>
          </div>
          <div>
            <svg
              aria-hidden="true"
              focusable="false"
              data-prefix="fas"
              data-icon="link"
              class="svg-link"
              role="img"
              xmlns="http://www.w3.org/2000/svg"
              viewBox="0 0 512 512"
            >
              <path
                fill="currentColor"
                d="M326.612 185.391c59.747 59.809 58.927 155.698.36 214.59-.11.12-.24.25-.36.37l-67.2 67.2c-59.27 59.27-155.699 59.262-214.96 0-59.27-59.26-59.27-155.7 0-214.96l37.106-37.106c9.84-9.84 26.786-3.3 27.294 10.606.648 17.722 3.826 35.527 9.69 52.721 1.986 5.822.567 12.262-3.783 16.612l-13.087 13.087c-28.026 28.026-28.905 73.66-1.155 101.96 28.024 28.579 74.086 28.749 102.325.51l67.2-67.19c28.191-28.191 28.073-73.757 0-101.83-3.701-3.694-7.429-6.564-10.341-8.569a16.037 16.037 0 0 1-6.947-12.606c-.396-10.567 3.348-21.456 11.698-29.806l21.054-21.055c5.521-5.521 14.182-6.199 20.584-1.731a152.482 152.482 0 0 1 20.522 17.197zM467.547 44.449c-59.261-59.262-155.69-59.27-214.96 0l-67.2 67.2c-.12.12-.25.25-.36.37-58.566 58.892-59.387 154.781.36 214.59a152.454 152.454 0 0 0 20.521 17.196c6.402 4.468 15.064 3.789 20.584-1.731l21.054-21.055c8.35-8.35 12.094-19.239 11.698-29.806a16.037 16.037 0 0 0-6.947-12.606c-2.912-2.005-6.64-4.875-10.341-8.569-28.073-28.073-28.191-73.639 0-101.83l67.2-67.19c28.239-28.239 74.3-28.069 102.325.51 27.75 28.3 26.872 73.934-1.155 101.96l-13.087 13.087c-4.35 4.35-5.769 10.79-3.783 16.612 5.864 17.194 9.042 34.999 9.69 52.721.509 13.906 17.454 20.446 27.294 10.606l37.106-37.106c59.271-59.259 59.271-155.699.001-214.959z"
              ></path>
            </svg>
            <a v-if="userInfos.blog" :href="userInfos.blog" target="_black">{{
              userInfos.blog
            }}</a>
            <p style="color: gray" v-else>No blog link</p>
          </div>
          <div>
            <svg
              aria-hidden="true"
              focusable="false"
              data-prefix="fas"
              data-icon="user"
              class="svg-user fa-w-14"
              role="img"
              xmlns="http://www.w3.org/2000/svg"
              viewBox="0 0 448 512"
            >
              <path
                fill="currentColor"
                d="M224 256c70.7 0 128-57.3 128-128S294.7 0 224 0 96 57.3 96 128s57.3 128 128 128zm89.6 32h-16.7c-22.2 10.2-46.9 16-72.9 16s-50.6-5.8-72.9-16h-16.7C60.2 288 0 348.2 0 422.4V464c0 26.5 21.5 48 48 48h352c26.5 0 48-21.5 48-48v-41.6c0-74.2-60.2-134.4-134.4-134.4z"
              ></path>
            </svg>
            <a :href="userInfos.html_url" target="_black">@github</a>
          </div>
        </div>
      </div>
    </div>
  </div>
</template>

<script>
import axios from "axios";
export default {
  components: {},
  data() {
    return {
      username: "",
      userInfos: "",
    };
  },
  methods: {
    search() {
      axios
        .get("https://api.github.com/users/" + this.username)
        .then((res) => {
          console.log(res.data);
          this.userInfos = res.data;
        })
        .catch((err) => console.log(err));
    },
  },
};
</script>

<style lang="scss">
input {
  border: none;
  box-shadow: 1px 3px 9px #1c1c1c8c;
  outline: none;
  color: var(--text-color);
  width: 800px;
  height: 50px;
  border-radius: 8px;
  padding: 0 6px;
  margin-top: 25px;
  background-color: var(--cards-color);
}
input::placeholder {
  color: var(--text-color);
  //padding: 0 12px;
}
.userCard {
  margin-top: 25px;
  box-shadow: 1px 3px 9px #1c1c1c8c;
  background: var(--cards-color);
  width: 800px;
  border-radius: 8px;
  padding: 20px 6px;
  margin: 25px auto;
  display: flex;
  flex-flow: row wrap;
  justify-content: center;
  gap: 20px;
  transition: background 200ms;
  img {
    border-radius: 50%;
    max-width: 120px;
    height: 120px;
  }
  h2 {
    margin: 3% 0;
  }
  &__content {
    text-align: left;
    width: 70%;
    h1,
    p {
      padding: 0;
      margin: 0;
    }
    .c1 {
      display: flex;
      flex-flow: row nowrap;
      justify-content: space-between;
      align-items: center;
    }
    .bio {
      padding: 8px 0;
    }
    a {
      color: var(--accent-color);
    }
  }
  .infos {
    display: flex;
    flex-flow: row nowrap;
    justify-content: space-around;
    background: var(--background-color);
    border-radius: 8px;
    height: 75px;
    transition: background 500ms;
    margin: 12px 0;
    div {
      align-self: center;
    }
    h3 {
      margin: 1% 0;
      font-weight: 800;
      font-size: 1.4rem;
    }
  }
  .infos2 {
    display: grid;
    grid-template-columns: repeat(2, 1fr);
    grid-gap: 20px;
    padding: 12px 0;
    div {
      display: flex;
      flex-flow: row nowrap;
      justify-content: flex-start;
      p,
      a {
        padding-left: 8px;
      }
      a {
        color: var(--text-color);
        font-weight: 500;
      }
    }
    img,
    svg {
      max-width: 18px;
      height: 18px;
    }
    .svg-link,
    .svg-twitter,
    .svg-map,
    .svg-user {
      fill: var(--background-color);
    }
  }
}
a {
  text-decoration: none;
  font-weight: 600;
  color: var(--text-color);
}

@media only screen and (max-width: 825px) {
  input,
  .userCard {
    width: 350px;
  }
  .userCard {
    &__content {
      text-align: center;
      width: 100%;
      margin: 0 auto;
      img {
        display: block;
        margin: 0 auto;
      }
      .c1 {
        flex-flow: column nowrap;
        h2 {
          order: 2;
        }
      }
    }
    .infos2 {
      grid-template-columns: repeat(1, 1fr);
      grid-gap: 0;
      div {
        display: block;
        padding: 6px 0;
      }
    }
  }
}
</style>