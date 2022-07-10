# MessageChannel

The `MessageChaneel` interface allow us to create a message channel object and  send message through it via its two `MessagePort` properties.

## Properties

* MessageChannel.port1
* MessageChannel.port2

## Example

In the example below, we use `MessageChannel` constructor to create a message chaneel object. When `<iframe>` has loaded, we pass `port2` to `<iframe>` using `MessagePort.postMessage` along with a message. The `handleMessage` then responds to the message being sent back from `<iframe>` (using `onmessage`), putting it into output. The `handleMessage` method is associated to `port1` to listen when message arrives.

```js
const channel=new MessageChannel();
const output=document.querySelector(".output");
const ifr=document.querySelector("iframe");
const otherWindow=ifr.contentWindow;

ifr.addEventListener("load",onLoad);

function onLoad(){
  otherWindow.postMessage('Hello from the main page!', '*',[channel.port2]);
}

channel.port1.onmessage=handleMessage;
function handleMessage(e){
  output.innerHTML=e.data
}
```

