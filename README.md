## Listeleme
import 'package:flutter/material.dart';

void main() {
  runApp(MyApp());
}

class MyApp extends StatelessWidget {
  @override
  Widget build(BuildContext context) {
    return MaterialApp(
      title: 'Sevilen Öğretmenler',
      theme: ThemeData(
        primarySwatch: Colors.pink,
      ),
      home: TeacherListPage(),
    );
  }
}

class TeacherListPage extends StatefulWidget {
  @override
  _TeacherListPageState createState() => _TeacherListPageState();
}

class _TeacherListPageState extends State<TeacherListPage> {
  List<String> teachers = ['ayşegül', 'veysel', 'emre', 'rıdvan'];
  TextEditingController controller = TextEditingController();
  int? editingIndex;

  void addOrUpdateTeacher() {
    String name = controller.text.trim();
    if (name.isEmpty) return;

    setState(() {
      if (editingIndex == null) {
        teachers.add(name);
      } else {
        teachers[editingIndex!] = name;
        editingIndex = null;
      }
      controller.clear();
    });
  }

  void editTeacher(int index) {
    controller.text = teachers[index];
    setState(() {
      editingIndex = index;
    });
  }

  void deleteTeacher(int index) {
    setState(() {
      teachers.removeAt(index);
      if (editingIndex == index) {
        controller.clear();
        editingIndex = null;
      }
    });
  }

  @override
  Widget build(BuildContext context) {
    return Scaffold(
      appBar: AppBar(
        title: Text('Sevilen Öğretmenler'),
      ),
      body: Padding(
        padding: const EdgeInsets.all(16.0),
        child: Column(
          children: [
            Row(
              children: [
                Expanded(
                  child: TextField(
                    controller: controller,
                    decoration: InputDecoration(
                      labelText: 'Öğretmen adı',
                    ),
                  ),
                ),
                SizedBox(width: 10),
                ElevatedButton(
                  onPressed: addOrUpdateTeacher,
                  child: Text(editingIndex == null ? 'Ekle' : 'Güncelle'),
                ),
              ],
            ),
            SizedBox(height: 20),
            Expanded(
              child: ListView.builder(
                itemCount: teachers.length,
                itemBuilder: (context, index) {
                  return ListTile(
                    title: Text(teachers[index]),
                    trailing: Row(
                      mainAxisSize: MainAxisSize.min,
                      children: [
                        IconButton(
                          icon: Icon(Icons.edit),
                          onPressed: () => editTeacher(index),
                        ),
                        IconButton(
                          icon: Icon(Icons.delete),
                          onPressed: () => deleteTeacher(index),
                        ),
                      ],
                    ),
                  );
                },
              ),
            ),
          ],
        ),
      ),
    );
  }
}




## SAyfalar Arası Gecis
import 'package:flutter/material.dart';
import 'package:sayfalar_arasi_gecis/ucuncu.dart';
import 'ikinci.dart'; // artık kullanılacak!

void main() {
  runApp(MaterialApp(
    initialRoute: '/ana',
    routes: {
      '/ana': (context) => const AnaEkran(),
      '/ikinci': (context) => const ikinciEkran(), 
      '/ucuncu': (context) => const ucuncuEkran(), 
    },
  ));
}

class AnaEkran extends StatefulWidget {
  const AnaEkran({super.key});

  @override
  State<AnaEkran> createState() => _AnaEkranState();
}

class _AnaEkranState extends State<AnaEkran> {
  @override
  Widget build(BuildContext context) {
    return Scaffold(
      appBar: AppBar(
        title: Text("Ana Ekran"),
        backgroundColor: Colors.red,
      ),
      body: Center(
        child: Row(
         mainAxisAlignment: MainAxisAlignment.center,
          children: [
            ElevatedButton(
              onPressed: () {
                Navigator.pushNamed(context, '/ikinci');
              },
              child: Text("İkinci Ekrana Git"),
            ),
            SizedBox(width: 20), 
            ElevatedButton(
              onPressed: () {
                Navigator.pushNamed(context, '/ucuncu');
              },
              child: Text("Üçüncü Ekrana Git"),
            ),
          ],
        ),
      ),
    );
  }
}


## Metin Yazdırma
import 'package:flutter/material.dart';

void main() {
  runApp(const AnaEkran());
}

class AnaEkran extends StatefulWidget {
  const AnaEkran({super.key});

  @override
  State<AnaEkran> createState() => _AnaEkranState();
}

class _AnaEkranState extends State<AnaEkran> {
  final TextEditingController kutu=TextEditingController();
  String girilenmetin="";


  @override
  Widget build(BuildContext context) {
    return MaterialApp(
      home: Scaffold(
        appBar: AppBar(
          title: Text("Değer Alma Uygulaması"),
          backgroundColor: const Color.fromARGB(255, 255, 0, 0),
          
        ),
        body: Column(children: [
          Text("Selam :$girilenmetin"),
          TextField(controller: kutu,),
          ElevatedButton(
            onPressed: () { 
              setState(() {
                
                girilenmetin=kutu.text;
              });
            },
           
            child: Text("Ekranda Göster "),
            ),
        ],),
      ),
    );
  }
}
