<template>
  <div class="ui vertical masthead center aligned" id="header">
    <div id="header-content">
      <h1 class="ui header">
        Server Status
      </h1>
    </div>
  </div>
</template>
<script lang="ts">
import { defineComponent } from 'vue';

export default defineComponent({
  name: 'TheHeader'
});
</script>
<style scoped>
#header {
  height: 15rem;
  position: relative;
  /*Replace your header image at this place!*/
  background: #21ba45!important;
}
.ui.header{
  color: #fff!important;
}
/* #header::after {
  content: 'Pixiv: 86597206';
  color: #CDCDCD;
  text-shadow: 1px 1px 1px #666;
  position: absolute;
  right: 15px;
  bottom: 0;
  z-index: 2;
} */

/*#header::after {
    content: '';
    display: inline-block;
    vertical-align: middle;
    height: 100%;
}*/
#header-content {
  position: absolute;
  z-index: 3;
  top: 50%;
  left: 50%;
  transform: translate(-50%, -50%);
  text-align: center;
}

#header h1 {
  font-size: 3.57rem;
  white-space: nowrap;
}

#header p {
  font-size: 1.5rem;
  color: #555;
  /*white-space: nowrap;*/
}
</style>
