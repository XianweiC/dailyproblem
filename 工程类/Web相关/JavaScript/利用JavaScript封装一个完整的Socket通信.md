# 利用`JavaScript`封装一个完整的Socket通信

**引言：**在项目与服务器进行交互的过程中，需要采用websocket保持连接，因此将代码整理出来便于日后使用，避免重复造轮子。

```javascript
/**
此处引入了项目所需的几个函数
*/
//import { noticePath } from "../api/getData.js";
//import { Notification } from 'element-ui';
//import { MessageBox } from 'element-ui';


// 建立Socket
let Socket = ''
let setIntervalWesocketPush = null
let URL = '';

// 创建socket连接
export const createSocket = userId => {
    Socket && Socket.close()
    if (!Socket) {
        console.log('建立websocket连接');

        // 根据不同的userId生成socket地址，并保存到全局变量
        URL = noticePath(userId);

        Socket = new WebSocket(URL);

        Socket.onopen = onopenWS;
        Socket.onmessage = onmessageWS;
        Socket.onerror = onerrorWS;
        Socket.onclose = oncloseWS;

        return Socket;

    } else {
        console.log('websocket已连接');
    }
}

/*需要重连时调用此方法，
由于当时需要绑定至全局socket变量，
因此采用重新创建的方法，
如果是正常使用，只需要复用createSocket方法即可*/
const recoverSocket = () => {
    Socket && Socket.close()
    if (!Socket) {
        console.log('建立websocket连接');

        Socket = new WebSocket(URL);

        Socket.onopen = onopenWS;
        Socket.onmessage = onmessageWS;
        Socket.onerror = onerrorWS;
        Socket.onclose = oncloseWS;

        return Socket;

    } else {
        console.log('websocket已连接');
    }
}


/**打开WS之后发送心跳 */
const onopenWS = () => {
    sendPing();
}

/**连接失败重连 */
const onerrorWS = () => {
    Socket.close();
    clearInterval(setIntervalWesocketPush);
    console.log('连接失败重连中');
    if (Socket.readyState !== 3) {
        Socket = null;
        createSocket();
    }
}

/**WS数据接收统一处理 */
const onmessageWS = e => {
    Notification({
        title: "闹钟",
        type: "info",
        message: e.data
    });
    // MessageBox
    console.log('Notify');
    window.dispatchEvent(new CustomEvent('onmessageWS', {
        detail: {
            data: e.data
        }
    }))
}

/**
 * 发送数据但连接未建立时进行处理等待重发
 * @param {any} message 需要发送的数据
 */
const connecting = message => {
    setTimeout(() => {
        if (Socket.readyState === 0) {
            connecting(message);
        } else {
            Socket.send(JSON.stringify(message));
        }
    }, 1000)
}

/**
 * 发送数据
 * @param {any} message 需要发送的数据
 */
export const sendWSPush = message => {
    if (Socket !== null && Socket.readyState === 3) {
        Socket.close();
        // 恢复连接
        createSocket();
    } else if (Socket.readyState === 1) {
        Socket.send(JSON.stringify(message));
    } else if (Socket.readyState === 0) {
        connecting(message);
    }
}

/**断开重连 */
const oncloseWS = () => {
    clearInterval(setIntervalWesocketPush);
    console.log('websocket已断开....正在尝试重连');
    if (Socket.readyState !== 2) {
        Socket = null;
        createSocket();
    }
}

/**发送心跳
 * @param {number} time 心跳间隔毫秒 默认5000
 * @param {string} ping 心跳名称 默认字符串ping
 */
export const sendPing = (time = 30000, ping = 'ping') => {
    clearInterval(setIntervalWesocketPush);
    Socket.send(ping);
    setIntervalWesocketPush = setInterval(() => {
        Socket.send(ping);
    }, time);
}
```

下面将此方法重新组织，便于重新使用

```javascript
// 建立Socket
let Socket = ''
let setIntervalWesocketPush = null
let URL = '';

// 创建socket连接
export const createSocket = userId => {
    Socket && Socket.close()
    if (!Socket) {
        console.log('建立websocket连接');

        // 根据不同的userId生成socket地址，并保存到全局变量
        URL = noticePath(userId);

        Socket = new WebSocket(URL);

        Socket.onopen = onopenWS;
        Socket.onmessage = onmessageWS;
        Socket.onerror = onerrorWS;
        Socket.onclose = oncloseWS;

        return Socket;

    } else {
        console.log('websocket已连接');
    }
}

/**打开WS之后发送心跳 */
const onopenWS = () => {
    sendPing();
}

/**连接失败重连 */
const onerrorWS = () => {
    Socket.close();
    clearInterval(setIntervalWesocketPush);
    console.log('连接失败重连中');
    if (Socket.readyState !== 3) {
        Socket = null;
        createSocket();
    }
}

/**WS数据接收统一处理 */
const onmessageWS = e => {
    Notification({
        title: "闹钟",
        type: "info",
        message: e.data
    });
    // MessageBox
    console.log('Notify');
    window.dispatchEvent(new CustomEvent('onmessageWS', {
        detail: {
            data: e.data
        }
    }))
}

/**
 * 发送数据但连接未建立时进行处理等待重发
 * @param {any} message 需要发送的数据
 */
const connecting = message => {
    setTimeout(() => {
        if (Socket.readyState === 0) {
            connecting(message);
        } else {
            Socket.send(JSON.stringify(message));
        }
    }, 1000)
}

/**
 * 发送数据
 * @param {any} message 需要发送的数据
 */
export const sendWSPush = message => {
    if (Socket !== null && Socket.readyState === 3) {
        Socket.close();
        // 恢复连接
        createSocket();
    } else if (Socket.readyState === 1) {
        Socket.send(JSON.stringify(message));
    } else if (Socket.readyState === 0) {
        connecting(message);
    }
}

/**断开重连 */
const oncloseWS = () => {
    clearInterval(setIntervalWesocketPush);
    console.log('websocket已断开....正在尝试重连');
    if (Socket.readyState !== 2) {
        Socket = null;
        createSocket();
    }
}

/**发送心跳
 * @param {number} time 心跳间隔毫秒 默认5000
 * @param {string} ping 心跳名称 默认字符串ping
 */
export const sendPing = (time = 30000, ping = 'ping') => {
    clearInterval(setIntervalWesocketPush);
    Socket.send(ping);
    setIntervalWesocketPush = setInterval(() => {
        Socket.send(ping);
    }, time);
}
```

