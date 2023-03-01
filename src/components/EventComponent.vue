<template>
    <div>
      <my-component :items="myItems"></my-component>
    </div>
  </template>
  


<script>
export default {
  components: {
    EventComponent
  },
  data() {
    return {
      myItems: [
        { eventDate: '2023-03-02', title: 'Event 1', info: 'Info 1' },
        { eventDate: '2023-03-03', title: 'Event 2', info: 'Info 2' },
        { eventDate: '2023-03-04', title: 'Event 3', info: 'Info 3' }
      ]
    };
  }
};
</script>