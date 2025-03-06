<template>
    <div class="list-item">
      <div class="left-column">
        <p class="time">{{ time }}</p>
      </div>
      <div class="divider divider-horizontal"></div>
      <div class="right-column">
        <p class="description">Lasts for {{ duration }} minutes.</p>
      </div>
    </div>
  </template>
  
  <script>
  export default {
    props: {
      date: {
        type: String,
        required: true
      },
      time: {
        type: String,
        required: true
      },
      duration: {
        type: Number,
        required: true
      }
    }
  }
  </script>
  
  <style scoped>
  .list-item {
    display: flex;
    align-items: center;
    padding: 10px;
  }
  
  .left-column {
    flex: 1;
  }
  
  .right-column {
    display: flex;
    gap: 10px;
  }
  
  .time {
    font-size: 1.5em;
    font-family: "Space Mono", monospace;
    font-weight: 400;
    font-style: normal;
  }
  
  .separator {
    width: 1px;
    background-color: #ccc;
    height: 30px;
    padding-left: 20px;
    padding-right: 20px;
  }
  
  .description {
    font-size: 1.2em;
    font-weight: 700;
    font-family: "Space Grotesk", sans-serif;
    font-optical-sizing: auto;
    font-style: normal;
  }
  </style>
  