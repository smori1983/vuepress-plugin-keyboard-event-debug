# vuepress-plugin-keyboard-event-debug

Debugging keyboard events (especially for Japanese IME).


## Usage

`.vuepress/config.js`

```js
module.exports = {
  plugins: [
    ['keyboard-event-debug'],
  ],
};
```


## Predefined global component

In arbitrary markdown file,

```html
<PluginKeyboardEventDebug/>
```

See: `example/README.md`.


## Capture

![](https://cdn.jsdelivr.net/gh/smori1983/vuepress-plugin-keyboard-event-debug@master/doc/capture.01.png)
