import 'package:flutter/material.dart';

void main() {
  runApp(const MyApp());
}

class MyApp extends StatelessWidget {
  const MyApp({super.key});

  @override
  Widget build(BuildContext context) {
    return MaterialApp(
      title: 'Gestão de Abrigos',
      debugShowCheckedModeBanner: false,
      theme: ThemeData(
        primarySwatch: Colors.blue,
      ),
      home: SheltersPage(),
    );
  }
}

class Shelter {
  String name;
  String address;
  int maxCapacity;
  int currentCapacity;

  Shelter({
    required this.name,
    required this.address,
    required this.maxCapacity,
    required this.currentCapacity,
  });

  bool get isFull => currentCapacity >= maxCapacity;
}

class SheltersPage extends StatefulWidget {
  @override
  State<SheltersPage> createState() => _SheltersPageState();
}

class _SheltersPageState extends State<SheltersPage> {
  final List<Shelter> shelters = [
    Shelter(
      name: "Ginásio Municipal",
      address: "Rua das Flores, 123 - Centro",
      maxCapacity: 200,
      currentCapacity: 150,
    ),
    Shelter(
      name: "Escola Central",
      address: "Av. Brasil, 456 - Centro",
      maxCapacity: 100,
      currentCapacity: 100,
    ),
    Shelter(
      name: "Igreja São Pedro",
      address: "Praça da Matriz, 10 - Bairro Velho",
      maxCapacity: 80,
      currentCapacity: 77,
    ),
    Shelter(
      name: "Clube Recreativo",
      address: "Rua do Lazer, 200 - Jardim",
      maxCapacity: 150,
      currentCapacity: 149,
    ),
    Shelter(
      name: "Associação de Moradores",
      address: "Rua União, 50 - Vila Nova",
      maxCapacity: 90,
      currentCapacity: 80,
    ),
    Shelter(
      name: "Centro Comunitário",
      address: "Rua Esperança, 333 - Esperança",
      maxCapacity: 120,
      currentCapacity: 120,
    ),
  ];

  void incrementCapacity(int index) {
    setState(() {
      if (shelters[index].currentCapacity < shelters[index].maxCapacity) {
        shelters[index].currentCapacity++;
      }
    });
  }

  void decrementCapacity(int index) {
    setState(() {
      if (shelters[index].currentCapacity > 0) {
        shelters[index].currentCapacity--;
      }
    });
  }

  @override
  Widget build(BuildContext context) {
    return Scaffold(
      appBar: AppBar(
        title: const Text("Gestão de Abrigos"),
      ),
      body: ListView.builder(
        itemCount: shelters.length,
        itemBuilder: (context, index) {
          final shelter = shelters[index];
          return Card(
            margin: const EdgeInsets.symmetric(horizontal: 12, vertical: 8),
            child: Padding(
              padding: const EdgeInsets.all(12.0),
              child: Column(
                crossAxisAlignment: CrossAxisAlignment.start,
                children: [
                  Row(
                    children: [
                      Expanded(
                        child: Text(
                          shelter.name,
                          style: const TextStyle(
                            fontSize: 18,
                            fontWeight: FontWeight.bold,
                          ),
                        ),
                      ),
                      Icon(
                        shelter.isFull
                            ? Icons.cancel
                            : Icons.check_circle_outline,
                        color: shelter.isFull ? Colors.red : Colors.green,
                        size: 28,
                      ),
                      const SizedBox(width: 8),
                    ],
                  ),
                  const SizedBox(height: 6),
                  Text(
                    shelter.address,
                    style: const TextStyle(fontSize: 15),
                  ),
                  const SizedBox(height: 10),
                  Row(
                    children: [
                      Text(
                        "Capacidade Atual: ${shelter.currentCapacity}",
                        style: const TextStyle(fontSize: 15),
                      ),
                      const SizedBox(width: 16),
                      Text(
                        "Máx: ${shelter.maxCapacity}",
                        style: const TextStyle(fontSize: 15),
                      ),
                    ],
                  ),
                  const SizedBox(height: 8),
                  Row(
                    mainAxisAlignment: MainAxisAlignment.end,
                    children: [
                      IconButton(
                        onPressed: () => decrementCapacity(index),
                        icon: const Icon(Icons.remove_circle),
                        color: Color.fromARGB(255, 235, 19, 19),
                        tooltip: "Remover pessoa",
                      ),
                      IconButton(
                        onPressed: () => incrementCapacity(index),
                        icon: const Icon(Icons.add_circle),
                        color: Colors.blue,
                        tooltip: "Adicionar pessoa",
                      ),
                    ],
                  )
                ],
              ),
            ),
          );
        },
      ),
    );
  }
}
