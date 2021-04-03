# Javascript Array 与 ArrayBuffer相互转换

两种常用的类型`ArrayBuffer`和`Array`。前者一般在IO时会用到，比如写文件时参数类型需要是这样的；后者是便于操作的Array可以push可以操作等等。所以需要两者相互转换。

ArrayBuffer to Array

```javascript
let arrayBuffer = new ArrayBuffer(10);
let array = Array.prototype.slice.call(new Uint8Array(arrayBuffer ));
```

Array to ArrayBuffer

```javascript
let array = [0x01, 0x02, 0x03, 0x04, 0x05, 0x06, 0x07];
let arrayBuffer = new Uint8Array(array).buffer;
```

注：我这里使用提`Uint8Array`作为中间量是结合具体项目选择的，可以根据数据类型选择`Int8Array Int16Array Uint16Array Int32Array Uint32Array Float32Array Float64Array`等等。

## 补充：

ArrayBuffer to AudioBuffer

```javascript
var audioCtx = new(window.AudioContext || window.webkitAudioContext)();
            audioCtx.decodeAudioData(arrayBuffer).then((data) => {
                console.log('data', data);
            })
```

- `length`: buffer中采样帧的长度.
- `numberOfChannels`: buffer的通道数. 默认值为1. 
- `sampleRate`: buffer的采样率 (Hz). 默认值为构造此对象时使用的 `context` 的采样率.

Blob to Array

```javascript
function blob2array(blob) {
        var reader = new FileReader();

        reader.onload = function() {
            console.log('buffer:', this.result);
        }

        reader.readAsArrayBuffer(blob);
    }
```

 File对象转base64

```javascript
  let reader = new FileReader();
  reader.readAsDataURL(file[0])
  console.log(reader)
```

base64 转成blob 上传

```javascript
function dataURItoBlob(dataURI) {  
    var byteString = atob(dataURI.split(',')[1]);  
    var mimeString = dataURI.split(',')[0].split(':')[1].split(';')[0];  
    var ab = new ArrayBuffer(byteString.length);  
    var ia = new Uint8Array(ab);  
    for (var i = 0; i < byteString.length; i++) {  
        ia[i] = byteString.charCodeAt(i);  
    }  
    return new Blob([ab], {type: mimeString});  
}
```