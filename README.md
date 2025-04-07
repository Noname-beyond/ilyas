call.dart 
class Call {
String image;
String name;
String statusDate;
Call({required this.name, required this.statusDate, required
this.image});
}
var callList = [
Call(name: "Bapak Mirza", image: "", statusDate: "hari ini, 12.00"),

Call(name: "Ibu rina", image: "images/P2.jpg", statusDate: "hari ini,
10.00"),
Call(name: "Bapak Rizha", image: "", statusDate: "kemarin, 13.30"),
Call(name: "ibu intan", image: "images/P4.jpg", statusDate:
"kemarin, 09.00"),
];

chat.dart
class Chat {
String image;
String name;
String messageDate;
String mostRecentMessage;
Chat({
required this.image,
required this.name,
required this.messageDate,
required this.mostRecentMessage,
});
}
var chatList = [
Chat(
name: 'Avril',
image: 'images/P1.jpg',
messageDate: '07/11/2024',
mostRecentMessage: 'Ayo Belajar Flutter',
),
Chat(
name: 'Rosa',
image: 'images/P3.jpg',
messageDate: '10/11/2024',
mostRecentMessage: 'Belajar Flutter itu Menyenangkan',
),
Chat(
name: 'Johan',
image: 'images/L1.png',
messageDate: '15/11/2024',
mostRecentMessage: 'Apakah Kuliah Sudah Dimulai',
),
];

status.dart
class Status {

String image;
String name;
String statusDate;
Status({required this.name, required this.statusDate, required
this.image});
}
var statusList = [
Status(
name: "Bapak ucup",
image: "images/L2.jpg",
statusDate: "Hari ini, 19.00",
),
Status(
name: "pak Bondan",
image: "images/L3.png",
statusDate: "Hari ini, 21.00",
),
Status(name: "pak Sugeng", image: "", statusDate: "Hari ini, 22.00"),
Status(name: "bu rudi", image: "", statusDate: "Hari ini, 22.15"),
];

call_view.dart
import 'package:flutter/material.dart';
import 'package:whatsapp_clone/models/call.dart';
import 'package:whatsapp_clone/theme.dart';
class CallList extends StatelessWidget {
const CallList({super.key});
@override
Widget build(BuildContext context) {
return ListView.builder(
itemCount: callList.length,
itemBuilder: (context, index) {
final call = callList[index];
return ListTile(
leading: call.image.isNotEmpty
? CircleAvatar(
radius: 29,
backgroundImage: AssetImage(call.image),
)
: const Icon(

Icons.account_circle,
color: Colors.black45,
size: 58,
),
title: Text(call.name, style: customTextStyle),
subtitle: Text(
call.statusDate,
style: const TextStyle(color: Colors.black45, fontSize: 16),
),
trailing: const Icon(Icons.call, color: whatsAppLightGreen, size:
24),
);
},
);
}
}

chat_view.dart
import 'package:flutter/material.dart';
import 'package:whatsapp_clone/models/chat.dart';
import 'package:whatsapp_clone/theme.dart';
class ChatView extends StatelessWidget {
const ChatView({super.key});
@override
Widget build(BuildContext context) {
return ListView.builder(
itemCount: chatList.length,
itemBuilder: (context, index) {
final chat = chatList[index];
return ListTile(
leading: CircleAvatar(
radius: 29,
backgroundImage: AssetImage(chat.image),
),
title: Text(chat.name, style: customTextStyle),
subtitle: Text(
chat.mostRecentMessage,
style: const TextStyle(color: Colors.black45, fontSize: 15),
),
trailing: Padding(
padding: const EdgeInsets.only(bottom: 25),
child: Text(
chat.messageDate,
style: const TextStyle(color: Colors.black45),
),
),

);
},
);
}
}

status_view.dart
import 'package:flutter/material.dart';
import 'package:whatsapp_clone/models/status.dart';
import 'package:whatsapp_clone/theme.dart';
class StatusView extends StatelessWidget {
const StatusView({super.key});
@override
Widget build(BuildContext context) {
return ListView.builder(
itemCount: statusList.length,
itemBuilder: (context, index) {
final status = statusList[index];
return ListTile(
leading: status.image.isNotEmpty
? CircleAvatar(
radius: 29,
backgroundImage: AssetImage(status.image),
)
: const Icon(
Icons.account_circle,
color: Colors.black45,
size: 58,
),
title: Text(status.name, style: customTextStyle),
subtitle: Text(
status.statusDate,
style: const TextStyle(color: Colors.black45, fontSize: 16),
),
);
},
);
}
}

main.dart
import 'package:flutter/material.dart';
import 'package:whatsapp_clone/whatsapp_page.dart';
void main() {
runApp(const MainApp());
}

class MainApp extends StatelessWidget {
const MainApp({super.key});
@override
Widget build(BuildContext context) {
return MaterialApp(
theme: ThemeData(useMaterial3: false),
home: const WhatsAppPage(),
);
}
}

theme.dart
import 'package:flutter/material.dart';
const Color whatsAppGreen = Color.fromRGBO(18, 140, 126, 1.0);
const Color whatsAppLightGreen = Color.fromRGBO(37, 211, 102,
1.0);
const TextStyle customTextStyle = TextStyle(
fontSize: 20.0,
fontWeight: FontWeight.w600,
);

whatsapp_page.dart
import 'package:flutter/material.dart';
import 'package:whatsapp_clone/widgets/chat_view.dart';
import 'package:whatsapp_clone/widgets/status_view.dart';
import 'package:whatsapp_clone/widgets/call_view.dart';
class WhatsAppPage extends StatefulWidget {
const WhatsAppPage({super.key});
@override
State<WhatsAppPage> createState() => _WhatsAppPageState();
}
class _WhatsAppPageState extends State<WhatsAppPage>
with SingleTickerProviderStateMixin {
late TabController tabController;
final List<Tab> tabs = [
const Tab(icon: Icon(Icons.camera_alt)),
const Tab(text: "CHATS"),
const Tab(text: "STATUS"),
const Tab(text: "CALLS"),
];
IconData? fabIcon;
@override
void initState() {
super.initState();
tabController = TabController(length: tabs.length, vsync: this);
fabIcon = Icons.message; // Default to tab CHATS
tabController.addListener(() {
switch (tabController.index) {
case 0:
fabIcon = Icons.camera;
break;
case 1:
fabIcon = Icons.message;
break;
case 2:
fabIcon = Icons.camera_alt;
break;
case 3:
fabIcon = Icons.call;
break;
}
setState(() {});
});
}

@override
Widget build(BuildContext context) {
return Scaffold(
appBar: AppBar(
title: const Text("WhatsApp"),
backgroundColor: Colors.teal,
actions: [
const Icon(Icons.search),
Padding(
padding: const EdgeInsets.symmetric(horizontal: 15),
child: const Icon(Icons.more_vert),
),
],
bottom: TabBar(
controller: tabController,
tabs: tabs,
indicatorColor: Colors.white,
),
),
body: TabBarView(
controller: tabController,
children: const [
Center(child: Icon(Icons.camera_alt)), // Camera View
ChatView(), // Chat List
StatusView(), // Status List
CallsView(), // Call List
],
),
floatingActionButton: FloatingActionButton(
onPressed: () {},
backgroundColor: Colors.tealAccent[700],
child: Icon(fabIcon),
),
);
}
}
