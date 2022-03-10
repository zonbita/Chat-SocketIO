# Chat-SocketIO
io.on('connect', onConnect);

function onConnect(socket){

  // Gửi cho tất cả client
  socket.emit('hello', 'can you hear me?', 1, 2, 'abc');

  // Gửi cho tất cả client ngoại trừ người gửi
  socket.broadcast.emit('broadcast', 'hello friends!');

  // Gửi cho tất cả client trong room 'game' ngoại trừ người gửi
  socket.to('game').emit('nice game', "let's play a game");

  // Gửi cho tất cả client trong room 'game1' và room 'game2' ngoại trừ người gửi
  socket.to('game1').to('game2').emit('nice game', "let's play a game (too)");

  //  Gửi cho tất cả client trong room 'game' bao gồm cả người gửi
  io.in('game').emit('big-announcement', 'the game will start soon');

  // Gửi cho tất cả client trong namespace 'myNamespace', bao gồm cả người gửi
  io.of('myNamespace').emit('bigger-announcement', 'the tournament will start soon');

  // Gửi cho room 'room' trong namespace 'myNamespace', bao gồm cả người gửi
  io.of('myNamespace').to('room').emit('event', 'message');

  // Gửi tin nhắn riêng cho socket đó qua socketId
  io.to(`${socketId}`).emit('hey', 'I just met you');

  // Gửi không đính kèm file nén
  socket.compress(false).emit('uncompressed', "that's rough");

  // Việc gửi tin nhắn này cần sự chấp nhận từ client thì mới có thể đến được client
  socket.volatile.emit('maybe', 'do you really need it?');

  // Gửi dữ liệu liên quan đến hệ nhị phân
  socket.binary(false).emit('what', 'I have no binaries!');

  // Gửi dữ liệu cho tất cả client sử dụng node
  io.local.emit('hi', 'my lovely babies');

  // Gửi đến tất cả client kết nối đến
  io.emit('an event sent to all connected clients');

};
