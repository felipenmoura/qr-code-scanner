## QRCodeScanner

This is a SIMPLE qr-code-scanner that will allow you to open the user's camera, scan it and match a pattern or read the string out of the QR Code.

It is highly customizable for you to use it within your page's styles.

### How it works

User will click a button, you will trigger the initiate method and a modal will open requesting permission to use the camera (only the first time).  
The user will see the camera's output.  
When a QRCode is found, it will trigger your _onResult_ method and close the modal.  
You can customize the modal and its layer.  
You can use a regex to match only what you expect, ensuring the result will not be garbage.

### How to use it:

You can require it, or use it as global:

```js
    require(['qr-code-scanner'], function (QRScanner) {...})
    // OR
    window.QRScanner
```

* The global _QRScanner_ will only be created IF there is not require/define available in the page.

### API

You will call the `initiate` method, sending the options, like so:

```js
    QRScanner.initiate({
        match: /^[a-zA-Z0-9]{16,18}$/, // optional
        onResult: function (result) { console.info('DONE: ', result); },
        onError: function (err) { console.error('ERR :::: ', err); }, // optional
        onTimeout: function () { console.warn('TIMEOUT'); } // optional
    })
```

#### Options

In the options object, you can send:

- onResult: A function to be triggered when a result is matched
- onError: A function to be called in case of an error (or device not supported) [optional]
- onTimeout: Your callback for the timeout event [optional]
- match: A regular Expression matching what you expect to find in the QRCode (if found something but it does not match what you expected, it will not trigger the onResult) [optional]
- timeout: A number in ms specifying for how long you will wait for a match. Default: 20000 [optional]
- parent: The container where the video(from the camera) should be appended to. Default: document.body [optional]
- lockLayerParent: The container on which the _lock-layer_ will be appended. Default: document.body [optional]
- className: A CSS class added to the video container. Default: QRScanner-container [optional]
- lockLayerClassName: A CSS class added to the lockLayer container. Default: QRScanner-lock-layer [optional]

* LockLayer is the darker layer behind the video.

### Example

```js
    import QRScanner from 'qr-code-scanner';

    QRScanner.initiate({
        onResult: (result) => { yourCustomCallback(result); },
        timeout: 10000,
    });
```

### Legacy

This lib uses some ES6 features like _let, const_ and _arrow functions_, but inherits the reader from Lazar Laszlo's port of ZXing Java library.
This project "cleans" some things like global variables and hardcoded ids from the previous projects, fixing some legacy problems.

