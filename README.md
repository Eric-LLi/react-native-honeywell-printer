# React Native Honeywell Scanner

This package works with Honeywell devices that have an integrated barcode scanner, like the Honeywell Dolphin CT50. This package was fully tested with a CT50, since the SDK is not specific to the CT50 other devices will likely work as well but this is not guaranteed.

TODO:

- Find out how printerprofiles.json works
- Properly rotate text on PB50 printer
- Make sure printer is stable
- Cleanup printerprofiles
- Write documentation

## Installation

```
yarn add react-native-honeywell-scanner
```

To install the native dependencies:

```
react-native link react-native-honeywell-scanner
```

## Usage

First you'll want to check whether the device is a Honeywell scanner:

```js
import HoneywellPrinter from 'react-native-honeywell-scanner';

HoneywellPrinter.isCompatible // true or false
```

The barcode reader needs to be "claimed" by your application; meanwhile no other application can use it. You can do that like this:

```js
HoneywellPrinter.startReader().then((claimed) => {
    console.log(claimed ? 'Barcode reader is claimed' : 'Barcode reader is busy');
});
```

To free the claim and stop the reader, also freeing up resources:

```js
HoneywellPrinter.stopReader().then(() => {
    console.log('Freedom!');
});
```

To get events from the barcode scanner:

```js
HoneywellPrinter.on('barcodeReadSuccess', event => {
    console.log('Received data', event);
});

HoneywellPrinter.on('barcodeReadFail', () => {
    console.log('Barcode read failed');
});
```

To stop receiving events:

```js
function barcodeReadFail = () => console.log('Barcode read failed');
HoneywellPrinter.off('barcodeReadFail', handler);
```


## Inspiration

The [react-native-bluetooth-serial](https://github.com/rusel1989/react-native-bluetooth-serial) project was used as inspiration. [cordova-honeywell](https://github.com/icsfl/cordova-honeywell) also served as some inspiration.