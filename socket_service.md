# Add socket service

<li>This is the service: </li>

```dart
import 'dart:convert';
import 'package:get/get.dart';
import 'package:socket_io_client/socket_io_client.dart' as IO;

class SocketService { 
  SocketService._privateConstructor();
  static final SocketService _instance = SocketService._privateConstructor();
  static SocketService get instance => _instance;

  late IO.Socket _socket;

  void connect() {
    _socket = IO.io(
      AppUrls.socketUrl,
      IO.OptionBuilder().setTransports(['websocket']).build(),
    );

    _socket.onConnect((_) {
      print('Socket connected');
    });

    _socket.onDisconnect((_) {
      print('Socket disconnected');
    });
  }

  // Method to send investment data
  void sendInvest(String userName, int amount) {
    if (!_socket.connected) {
      print("Socket is not connected. Connecting...");
      connect();
    }

    final data = {
      "userName": userName,
      "result": {"amount": amount}
    };

    _socket.emit('invest', data);
    print('Sent invest data: $data');
  }

  void createTicket(String userName, Map<String, dynamic> result) {
    if (!_socket.connected) {
      appLog("Socket is not connected. Connecting...");
      connect();
    }
    appLog(result);
    final data = {
      "result": jsonEncode(result),
      "userName": userName,
    };

    _socket.emit('new tickets', data);
    appLog('Sent invest data: $data');
  }

  void sendReportData(
      String userName, String email, Map<String, dynamic> result) {
    if (!_socket.connected) {
      appLog("Socket is not connected. Connecting...");
      connect();
    }
    appLog(result);
    final data = {
      "result": jsonEncode(result),
      "user": {"name": userName, "email": email}
    };
// result, user: { name: user.name, email: user.email }
    _socket.emit('report', data);
    appLog('Sent report data: $data');
  }

// Method to listen for 'new invest message received' event
  void onNewInvestMessageReceived(
      void Function(RecentActivityReceiveModel) callback) {
    _socket.on('new invest message received', (data) {
      appLog('Received invest message: $data');
      Get.find<NotificationController>().increment();
      callback(RecentActivityReceiveModel.fromJson(data));
    });
  }

  void onCreatingTicketResponse(void Function(TicketWonSocketModel) callback) {
    _socket.on('ticket message received', (data) {
      appLog('Received invest message: $data');
      Get.find<NotificationController>().increment();
      callback(TicketWonSocketModel.fromJson(data));
    });
  }

  void dispose() {
    _socket.dispose();
  }
}

```
<li>Add this in init where this service will be used</li>

```dart
 SocketService.instance.connect();
```

<li>Then write this method to use the service</li>

```dart
void sendData() {
    SocketService.instance.sendInvest("Aurnab 420", 200);
  }

  void receiveData() {
    SocketService.instance.onNewInvestMessageReceived((p0) {
      final time = DateFormat('mm').format(DateTime.parse(p0.createdAt));
      recentActivity.insert(0, [p0.title, p0.subTitle, time]);
    });
    SocketService.instance.onCreatingTicketResponse(
      (p0) {
        final time = DateFormat('mm').format(DateTime.parse(p0.createdAt));
        recentActivity.insert(0, [p0.title, p0.text, time]);
      },
    );
  }
```
