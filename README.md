#   vue-notify-me

<p align="center">
<img src="https://media.giphy.com/media/GoTlxRAapcEVy/giphy.gif" />
</p>

Notification Alert for Vue.

## Features

* Customizable template
* Stackable notifications

<a href="https://pygmyslowloris.github.io/vue-notify-me/"> Live Demo</a>

##  Installation

```
npm install vue-notify-me --save
```

##  Properties

| Properties                    | Type      | Values     |
| :---------------              | :-------  | :--------- |
|  `event-bus`                  | Object    | <b>Central event Bus </b>|
|  `event-show` (not required)  | String    | <b>Default </b> 'notify-me'|
|  `event-hide` (not required)  | String    | <b>Default </b> 'hide-notify-me'|
|  `close` (not required)       | String    | <b>Default </b>'bulma', options: bootstrap or any other class for the closing icon|
|  `permanent` (not required)   | Bool      | <b>Default </b>false|
|  `container` (not required)   | String    | <b>Default </b>'notification', (Class for the notification container)|
|  `status` (not required)      | String    | <b>Default </b>'alert-success', (Class for the notification status)|
|  `width` (not required)       | String    | <b>Default </b>'350'    |

##  Examples

Include the component in your .vue file.

```
<template>
  <notify-me
        :event-bus="bus">
      <template slot="content" scope="{data}">
          <div style="width: 100%; word-break: break-all; text-align: left">
              <h4><b>{{data.title}}</b></h4>
              <p style="margin: 0">{{data.text}}</p>
          </div>
      </template>
  </notify-me>
</template>
```

If you'd like to use the component in a SPA set a single template on your layout application
and fire your notification through your central event bus.
Set any available prop for the component like this:

```
<notify-me
    container="notification"
    status="alert-success"
    :width="300"
    close="bulma"
    :event-bus="bus"
>
      <template slot="content" scope="{data}">
          <div style="width: 100%; word-break: break-all; text-align: left">
              <h4><b>{{data.title}}</b></h4>
              <p style="margin: 0">{{data.text}}</p>
          </div>
      </template>
  </notify-me>
```

To show a notification just fire an event like this:
 
```
<script>
import Notify from 'vue-notify-me'

const bus = new Vue();

export default {
  components: {
    'notify-me': Notify
  },
  data(){
      return {
          bus
      }
  },
  mounted(){
      this.bus.$emit('notify-me', {
        data: {
            title: 'The pygmy team :)',
            text: 'this is my notification'
        }
  
      });
  }
  
}
</script>
```

You may also add any available prop through the event emitter:

```
this.bus.$emit('notify-me', {
    permanent: true,
    status: this.status,
    data: {
        title: 'The pygmy team :)',
        text: this.text
    }

});
```

Enjoy :)
