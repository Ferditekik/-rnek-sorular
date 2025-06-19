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

## Snake bar
import 'package:flutter/material.dart';

void main() {
  runApp(const MyApp());
}

class MyApp extends StatelessWidget {
  const MyApp({super.key});

  @override
  Widget build(BuildContext context) {
    return MaterialApp(
      debugShowCheckedModeBanner: false,
      home: const HomePage(),
    );
  }
}

class HomePage extends StatelessWidget {
  const HomePage({super.key});

  @override
  Widget build(BuildContext context) {
    return Scaffold(
      appBar: AppBar(
        title: const Text('Snackbar Örneği'),
        centerTitle: true,
        backgroundColor: Colors.teal,
      ),
      body: Center(
        child: ElevatedButton(
          onPressed: () {
            // Snackbar'ı göster
            ScaffoldMessenger.of(context).showSnackBar(
              const SnackBar(
                content: Text('Butona tıkladın!'),
                duration: Duration(seconds: 2),
                backgroundColor: Colors.teal,
              ),
            );
          },
          child: const Text('Snackbar Göster'),
        ),
      ),
    );
  }
}


##Kaydırmalı Sekme
import 'package:flutter/material.dart';

void main() {
  runApp(MyApp());
}

class MyApp extends StatelessWidget {
  @override
  Widget build(BuildContext context) {
    return MaterialApp(
      home: TrendyolStyleTabs(),
    );
  }
}

class TrendyolStyleTabs extends StatefulWidget {
  @override
  _TrendyolStyleTabsState createState() => _TrendyolStyleTabsState();
}

class _TrendyolStyleTabsState extends State<TrendyolStyleTabs>
    with SingleTickerProviderStateMixin {
  late TabController _tabController;

  final List<String> categories = [
    'Kadın',
    'Erkek',
    'Çocuk',
    'Spor',
    'Elektronik',
    'Ev & Yaşam',
    'Kozmetik',
    'Süpermarket',
    'Kitap',
  ];

  @override
  void initState() {
    super.initState();
    _tabController = TabController(length: categories.length, vsync: this);
  }

  @override
  void dispose() {
    _tabController.dispose();
    super.dispose();
  }

  @override
  Widget build(BuildContext context) {
    return Scaffold(
      appBar: AppBar(
        title: Text('Trendyol Tarzı Sekmeler'),
        bottom: TabBar(
          isScrollable: true, // Kaydırma özelliği
          controller: _tabController,
          tabs: categories.map((category) => Tab(text: category)).toList(),
        ),
      ),
      body: TabBarView(
        controller: _tabController,
        children: categories.map((category) {
          return Center(
            child: Text(
              '$category Sayfası',
              style: TextStyle(fontSize: 24),
            ),
          );
        }).toList(),
      ),
    );
  }
}

##Sayaç
import 'package:flutter/material.dart';

void main() {
  runApp(const MyApp());
}

class MyApp extends StatelessWidget {
  const MyApp({super.key});

  @override
  Widget build(BuildContext context) {
    return MaterialApp(
      debugShowCheckedModeBanner: false,
      home: const CounterPage(),
    );
  }
}

class CounterPage extends StatefulWidget {
  const CounterPage({super.key});

  @override
  State<CounterPage> createState() => _CounterPageState();
}

class _CounterPageState extends State<CounterPage> {
  int _counter = 0;

  void _increment() {
    setState(() {
      _counter++;
    });
  }

  void _decrement() {
    setState(() {
      _counter--;
    });
  }

  void _reset() {
    setState(() {
      _counter = 0;
    });
  }

  @override
  Widget build(BuildContext context) {
    return Scaffold(
      appBar: AppBar(
        title: const Text('Sayaç Uygulaması'),
        centerTitle: true,
        backgroundColor: Colors.deepPurple,
      ),
      body: Column(
        mainAxisAlignment: MainAxisAlignment.center,
        children: [
          const Text(
            'Sayacın değeri:',
            style: TextStyle(fontSize: 24),
          ),
          Text(
            '$_counter',
            style: const TextStyle(fontSize: 48, fontWeight: FontWeight.bold),
          ),
          const SizedBox(height: 30),
          Row(
            mainAxisAlignment: MainAxisAlignment.center,
            children: [
              ElevatedButton(
                onPressed: _increment,
                child: const Text('+ Artır'),
              ),
              const SizedBox(width: 10),
              ElevatedButton(
                onPressed: _decrement,
                child: const Text('- Azalt'),
              ),
              const SizedBox(width: 10),
              ElevatedButton(
                onPressed: _reset,
                style: ElevatedButton.styleFrom(backgroundColor: Colors.red),
                child: const Text('Sıfırla'),
              ),
            ],
          ),
        ],
      ),
    );
  }
}
