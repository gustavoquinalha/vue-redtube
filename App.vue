<template>
  <Wrapper>
    <template slot-scope="{ videos }">
      <transition name="list">
        <Modal v-if="isModalVisible">
          <Embed :video="currentVideo" @close="isModalVisible = false" />
        </Modal>
      </transition>
      <transition-group name="list" class="list-container">
        <Card
          v-for="(video, index) in videos"
          :key="index"
          @play="play(video)"
          :items="video" />
      </transition-group>
    </template>
  </Wrapper>
</template>

<script>
import Wrapper from './components/Wrapper'
import Card from './components/Card'
import Modal from './components/Modal'
import Embed from './components/Embed'

export default {
  name: 'VueRedTube',
  components: { Wrapper, Card, Modal, Embed },
  data: () => ({
    currentVideo: {},
    isModalVisible: false
  }),
  methods: {
    play ({ video }) {
      this.currentVideo = video
      this.isModalVisible = true
      window.scrollTo(0, 0)
    }
  }
}
</script>

<style lang="scss">
* { margin: 0; padding: 0; box-sizing: border-box; }
html, body {
  width: 100%;
  height: 100%;
  font-family: 'Trebuchet MS', 'Lucida Sans Unicode', 'Lucida Grande', 'Lucida Sans', Arial, sans-serif;
}

.list-container {
  width: 100%;
  display: flex;
  flex-wrap: wrap;
  justify-content: space-around;
  padding-top: 10px;
}

.list-item {
  margin-right: 10px;
}
.list-enter-active, .list-leave-active {
  transition: all 1s;
}
.list-enter, .list-leave-to {
  opacity: 0;
  transform: translateY(30px);
}
</style>
