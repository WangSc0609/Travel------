<template>
  <div id="app">
    <!--除了名为Detail的组件，其他组件都进行缓存-->
    <keep-alive exclude="Detail">
      <router-view/>
    </keep-alive>
  </div>
</template>