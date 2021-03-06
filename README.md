
# react-native-screen-listener
[![Build Status](https://travis-ci.org/tomas-paronai/react-native-screen-listener.svg?branch=master)](https://travis-ci.org/tomas-paronai/react-native-screen-listener)

This library was created to wrap previous and current pages under one callback.
**This library only works with** [react-native-navigation v1](https://github.com/wix/react-native-navigation).
You can find the original event listener if you search for `ScreenVisibilityListener` in the github repo
For deeper understanding of the navigation behavior please refer to library github pages.

## Getting started

`$ npm install react-native-screen-listener --save`

## Usage
```javascript
import ScreenListener from 'react-native-screen-listener';

const beforeCallback = screenData => {
  //TODO something with the previous and current screen before the update
}

const afterCallback = screenData => {
  //TODO something with the previous and current screen after update
}

//initialize reference
const listener = new ScreenListener({ beforeCallback, afterCallback });
//register event emitters
listener.register();

//unregister to avoid leaks
listener.unregister();
```

### Adding event listeners
Event listener is a callback which is executed when a certain navigation event happens for a certain screen.
For an example, lets say I want to print out message "Hello home_screen!" when ever *home_screen* appears.

```javascript
listener.registerEventCallback(ScreenListener.AFTER, 'home_screen', data => {
  console.log(`Hello ${data.screen}!`)
});
```

### ScreenData

Screen data returns an object with two keys: `previous` and `current`. Both these represent the screen data. 
They contain:

| Value | Description |
| --- | --- |
| commandType | Name of the command issued to get to this screen. Only at `current`. |
| endTime | Time when the new screen appeared/disappeared |
| screen | Name of the screen |
| startTime | Time when the screen started to initialize. Only at `current`. |
| status | What happen to the screen. This is only set when subscribing events. |
