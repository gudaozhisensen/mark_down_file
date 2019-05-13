# mark_down_file
book_mark


学习中遇到的问题和记录的笔记
```
// 服务端接收
const http = require('http');
const io = require('socket.io');
const fs = require('fs');
let httpServer = http.createServer();
httpServer.listen(8080);
let wsServer = io.listen(httpServer);
let aSock=[];
wsServer.on('connection',sock=>{
aSock.push(sock);
sock.on('msg',str=>{ 
aSock.forEach(s=>{
if (s!=sock) {
sock.emit('msg',str);//发送给非自己的客户端数据
}
})
})
});
sock.on('disconnect',()=>{
var n = aSock.indexOf(sock);
if (n>-1) {
aSock.splice(n,1);//当客户端断开连接时从第n位删除一个元素
}
})
//客户端发送和接收
const http = require('http');
const io = require('socket.io');
const fs = require('fs');
sock.emit('msg',oTxt.value);//把填入的数据发给服务端
sock.on('msg',str=>{
...
})//接收服务端发送过来的数据
//客户端判断连接状态
sock.on('connect',()=>{
console.log('已连接');
})
sock.on('disconnect',()=>{
console.log('连接断开');
})
```
