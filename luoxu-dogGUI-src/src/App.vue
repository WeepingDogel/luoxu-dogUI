<script lang="ts">
import axios from 'axios';

export default {
  data() {

    return {
      search_content: '',
      message_box_display: false,
    }
  },
  methods: {
    do_search() {
      this.message_box_display = !this.message_box_display;
    }
  }
}
</script>

<template>
  <div id="page">
    <div id="titleAndSearchBlock">
      <h1 id="title">LUOXU</h1>
      <p id="description">A web frontend for luoxu, but made by foolish dog. </p>
      <div class="search-bar">
        <select class="custom-select">
          <option class="select-options">#group_1</option>
          <option class="select-options">#group_2</option>
          <option class="select-options">#group_3</option>
        </select>
        <input class="input" id="contentSearch" type="text" placeholder="Search Content" v-model="search_content" />
      </div>
      <div class="search-bar" v-if="search_content != ''">
        <input class="input" id="userSearch" type="text" placeholder="Search Username" />
        <button id="searchButton" @click="do_search">Search</button>
      </div>
    </div>
    <div id="MessageBoxBlock">
      <div id="MessageBox" v-if="message_box_display && search_content != ''">
        <div class="single-message-data">
          <div class="avatar-area">
            <img class="avatar" />
          </div>
          <div class="text-area">
            <div class="username-and-datetime-area">
              <span class="user-name-text">username</span>
              <span class="date-time-text">datetime</span>
            </div>
            <span class="message-text">Message</span>
          </div>
        </div>

      </div>
    </div>
  </div>
</template>

<style scoped>
@keyframes FadeIn {
  from {
    opacity: 0;
    bottom: 100px;
  }

  to {
    opacity: 1;
    bottom: 0px;
  }
}

@keyframes typing {
  to {
    left: 100%;
  }
}

@keyframes blink {

  from,
  to {
    background: transparent;
  }

  50% {
    background: #212121;
  }
}

@keyframes BottomFadeIn {
  from{
    opacity: 0;
    bottom: 100%;
  }
  to {
    opacity: 1;
    bottom: 0%;
  }
}

#page {
  width: 100%;
  height: 100vh;
  display: flex;
  background-color: #f1f1f1;
  flex-direction: column;
  /* justify-content: center; */
  /* align-items: center; */
}

#titleAndSearchBlock {
  width: 100%;
  height: 500px;
  display: flex;
  justify-content: center;
  flex-direction: column;
  align-items: center;
}

#title {
  position: relative;
  font-family: "Lucida Console", Courier, monospace;
  font-weight: lighter;
  font-size: 90px;
  text-align: center;
  color: #212121;
  animation: FadeIn 1s;
}

#title::selection {
  background-color: #f1f1f1;
}

#description {
  margin: 0;
  padding: 0;
  font-family: 'Courier New', Courier, monospace;
  font-size: 22px;
  color: #212121;
  font-weight: lighter;
  text-align: center;
  position: relative;

}

#description::before,
#description::after {
  content: '';
  position: absolute;
  top: 0;
  left: 0;
  right: 0;
  bottom: 0;
}

#description::before {
  background-color: #f1f1f1;
  animation: 4s typing steps(50) 2s forwards;
}

#description::after {
  width: 2px;
  height: 22px;
  background-color: #212121;
  animation:
    4s typing steps(50) 2s forwards,
    500ms blink steps(2, jump-none) infinite;
}

.search-bar {
  position: relative;
  margin-top: 30px;
  width: 1280px;
  height: 60px;
  background-color: #fff;
  box-shadow: rgba(0, 0, 0, 0.2) 0 2px 1px;
  animation: 1s FadeIn;
  display: flex;
  flex-direction: row;
  justify-content: center;
  border-radius: 10px;
  border-bottom: solid 3px #e5e5e5;
}

.input {
  width: 1120px;
  font-family: 'Gill Sans', 'Gill Sans MT', Calibri, 'Trebuchet MS', sans-serif;
  font-weight: 500;
  font-size: 22px;
  height: 60px;
  padding-left: 10px;
  border: none;
  outline: none;
  transition: 0.5s;
  color: #212121;
}

.input:focus {
  border-bottom: 1px solid #212121;
  -webkit-transition: 0.1s;
  transition: 0.5s;
}

#contentSearch {
  border-top-right-radius: 10px;
  border-bottom-right-radius: 10px;
}

#userSearch {
  border-top-left-radius: 10px;
  border-bottom-left-radius: 10px;
}

#searchButton {
  width: 160px;
  height: 60px;
  border-top-right-radius: 10px;
  border-bottom-right-radius: 10px;
  outline: none;
  border: none;
  font-family: 'Gill Sans', 'Gill Sans MT', Calibri, 'Trebuchet MS', sans-serif;
  font-weight: 500;
  font-size: 22px;
  background-color: #212121;
  color: #FFFFFF;
  transition: 200ms ease-in-out background-color, 0.5s ease-in-out color, 1s ease-in-out border-color;
  cursor: pointer;
}

#searchButton:hover {
  color: #212121;
  background-color: #FFFFFF;
  border: solid 1px #212121;
  transition: 200ms ease-in-out background-color, 0.5s ease-in-out color, 1s ease-in-out border-color;
}

#searchButton:active {
  filter: brightness(.7);
  transform: scale(0.95);
}

.custom-select {
  -webkit-appearance: none;
  -moz-appearance: none;
  appearance: none;
  height: 60px;
  width: 160px;
  color: #212121;
  background: #fff;
  background-size: 10px;
  transition: border-color .1s ease-in-out;
  border: none;
  border-top-left-radius: 10px;
  border-bottom-left-radius: 10px;
  text-align: center;
  font-family: 'Gill Sans', 'Gill Sans MT', Calibri, 'Trebuchet MS', sans-serif;
  font-weight: 500;
  font-size: 20px;
  cursor: pointer;
}


/* remove default arrow in IE */
select::-ms-expand {
  display: none;
}

.select-options {
  font-family: 'Gill Sans', 'Gill Sans MT', Calibri, 'Trebuchet MS', sans-serif;
  font-weight: 500;
  font-size: 20px;
  color: #212121;
}

#MessageBoxBlock {
  width: 100%;
  height: auto;
  display: flex;
  justify-content: center;
}

#MessageBox {
  width: 1280px;
  height: 550px;
  /* height: auto; */
  overflow-x: scroll;
  /* scrollbar-width: none; */
  background-color: #fff;
  box-shadow: rgba(0, 0, 0, 0.2) 0 2px 1px;
  animation: 1s FadeIn;
  border-radius: 10px;
  margin-bottom: 50px;
  margin-top: 15px;
  position: relative;
  display: flex;
  flex-direction: column;
  justify-content: flex-start;
  align-items: center;
  border-bottom: solid 3px #e5e5e5;
}

.single-message-data {
  width: 100%;
  height: auto;
  min-height: 100px;
  display: flex;
  justify-content: flex-start;
  flex-direction: row;
  /* background-color: #f3d3d3; */
  border-bottom: solid #dbdbdb 1px;
  position: relative;
  animation: BottomFadeIn 500ms;
}

.avatar-area {
  width: 80px;
  height: 80px;
  background-color: #F1F1F1;
  border-radius: 100%;
  justify-content: center;
  margin-left: 10px;
  margin-top: 10px;
  margin-bottom: 10px;
}

.avatar {
  width: 100%;
  height: auto;
}

.text-area {
  width: 1180px;
  height: auto;
  min-height: 100px;
  /* background-color: yellow; */
  display: flex;
  justify-content: flex-start;
  flex-direction: column;
}

.username-and-datetime-area {
  width: 100%;
  height: auto;
  display: flex;
  margin-top: 10px;
  flex-direction: row;
  justify-content: space-around;
}

.user-name-text {
  font-family: 'Gill Sans', 'Gill Sans MT', Calibri, 'Trebuchet MS', sans-serif;
  font-weight: 800;
  font-size: 22px;
  margin-left: 20px;
  margin-right: auto;
  line-height: 40px;
  color: #212121;
}

.date-time-text {
  font-family: 'Gill Sans', 'Gill Sans MT', Calibri, 'Trebuchet MS', sans-serif;
  font-weight: 800;
  font-size: 22px;
  margin-right: 20px;
  margin-left: auto;
  line-height: 40px;
  color: #212121;
}

.message-text {
  font-family: 'Gill Sans', 'Gill Sans MT', Calibri, 'Trebuchet MS', sans-serif;
  font-weight: 500;
  font-size: 20px;
  line-height: 30px;
  color: #212121;
  padding-left: 25px;
  padding-right: 25px;
  padding-bottom: 25px;
}
</style>
