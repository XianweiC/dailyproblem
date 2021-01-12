# python Socket.send()编码问题

**解决问题**

```
当我使用socket.send(data)时报错
TypeError: a bytes-like object is required, not 'str'
```

**解决思路**

```
问题出在python3.5和Python2.7在套接字返回值解码上有区别:
 python bytes和str两种类型可以通过函数encode()和decode()相互转换，
 str→bytes：encode()方法。str通过encode()方法可以转换为bytes。
 bytes→str：decode()方法。如果我们从网络或磁盘上读取了字节流，那么读到的数据就是bytes。要把bytes变为str，就需要用decode()方法。
```

**解决方法**

```
socket.send(data.decode("UTF-8"))
```

大功告成！

**正确写法：**（字符串转16进制）

```
server_reply = binascii.hexlify(s.recv(1024)).decode()
print(server_reply
```
**总结一下：**

```
str→bytes：encode()方法。str通过encode()方法可以转换为bytes。
bytes→str：decode()方法。如果我们从网络或磁盘上读取了字节流，那么读到的数据就是bytes。要把bytes变为str，就需要用decode()方法。
```
