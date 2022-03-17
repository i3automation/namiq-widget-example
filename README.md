## NamiQ Chat Widget

Use to embed NamiQ chat widget to your web site.

1. **Installation**
In your `<body/>`:

```html
<script>
      function addLoadEvent(e) {
        if (document.readyState === "complete") {
          e();
        } else {
          var t = window.onload;
          if (typeof window.onload != "function") {
            window.onload = e;
          } else {
            window.onload = function () {
              if (t) {
                t();
              }
              e();
            };
          }
        }
      }

      addLoadEvent(function () {
        setTimeout(function () {
          (function () {
            var e = document.createElement("script"),
              t = document.head || document.getElementsByTagName("head")[0];
            e.src =
              "https://d30y08pk6dssu7.cloudfront.net/namiq-widget-0.0.2.js";
            e.async = !0;
            e.onload = function () {
              window.WebChat.default.init({
                selector: "#chat-widget",
                socketUrl: "<SOCKET_URL>",
                language: "vi",
                apiKey: "<API_KEY>",
                onWidgetEvent: function (event, payload) {
                  console.log(event, payload);
                },
              });
            };
            t.insertBefore(e, t.firstChild);
          })();
        }, 3000);
      });
    </script>    
```

    | Props/params                    | Description                            |
    | ------------------------------- | -------------------------------------- |
    | namiq-widget-0.0.1.js           | NamiQ Chat widget Library              |

2. **Usage**

- Insert to HTML

  ```html
  <div id="chat-widget"></div>
  ```

- Init widget

  ```javascript

  WebChat.default.init({
    selector: '#chat-widget',
    socketUrl: '<YOUR_SOCKET_URL>',
  } as any);

  ```

3. **Options**

| Props/params                | Default value  | Description                                        |
| --------------------------- | -------------- | -------------------------------------------------- |
| selector                    | undefined      | Where chat widget will be render.                  |
| initPayload                 | undefined      | Payload sent to server when conversation starts    |
| socketUrl                   | undefined      | Socket URL                                         |
| socketPath                  | /socket.io     | Socket Path                                        |
| showCloseButton             | true           | Show close button in header                        |
| showFullScreenButton        | false          | Show full screen button in header                  |
| hideWhenNotConnected        | true           | Hide widget when server is not available           |
| language                    | en             | Widget text language (not bot language)            |
| defaultProductID            | -1             | Product ID send to server when conversation starts |
| logoUrl                     | NamiQ Logo URL | Logo URL                                           |
| mainColor                   | #3366ff        | Primary color                                      |
| conversationBackgroundColor | #ffffff        | Background of conversation area                    |
| userTextColor               | #FBFBFF        | Color of message from user                         |
| userBackgroundColor         | #6F54FF        | Background of message from user                    |
| assistTextColor             | #0D0054        | Color of message from bot or agent                 |
| assistBackgroundColor       | #EDEAFF        | Background of message from bot or agent            |
| onWidgetEvent               | func           | Widget event Callback function.                    |

- onWidgetEvent callback function

```javascript
onWidgetEvent = function (eventName: string, payload: any) {
  // TODO: Implement you logic
};
```

### Event list

| Event             | Payload | Description                                               | Example                              |
| ----------------- | ------- | --------------------------------------------------------- | ------------------------------------ |
| initialized       | string  | Chat widget initialize success. And return conversion id. | 1baf83d2-8e1a-48de-9a30-0ca79afbb419 |
| add_to_cart       | object  | Request add item to cart.                                 | { "id": 2810, "quantity": 2 }        |
| update-quantity   | object  | Request update quantity of an item in cart.               | { "sku": 2810, "quantity": 2 }       |
| remove-item       | string  | Request remove an item in cart.                           | 2807                                 |

### Method list

| Method              | Params | Description                                               |
| ------------------- | ------ | --------------------------------------------------------- |
| openChat            | None   | Open Chat widget programmatic.                            |
| closeChat           | None   | Close Chat widget programmatic.                           |
| toggleChat          | None   | Toggle Chat widget programmatic.                          |
| hideChat            | None   | Hide Chat widget programmatic.                            |
| toggleInputDisabled | None   | Toggle Disable Chat Input programmatic.                   |
| showChat            | None   | Show Chat widget programmatic.                            |
| setProductId        | id     | Update Product ID value.                                  |
| openBanner          | html   | Open widget banner by provide a HTML string or plaintext. |
| setConsumer         | Object | Update consumer data                                      |
| sendCustomEvent     | Object | Send an event with payload to widget.                     |
| isCartExist         | None   | Check cart is existed or not.                             |

- setConsumer parameters

```json
{
  "provider": "string",
  "profile": "Object"
}
```

### sendCustomEvent list

Name: cart-created
Payload: cart id as string
Ex:

```js
WebChat.default.sendCustomEvent({
  name: "cart-created",
  payload: "XXXXXXX-XXXXXXX",
});
```

Name: cart-created-failed
Payload: None
Ex:

```js
WebChat.default.sendCustomEvent({
  name: "cart-created",
  payload: null,
});
```
