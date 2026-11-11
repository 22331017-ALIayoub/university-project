import 'package:flutter/material.dart';

void main() => runApp(const MaterialApp(home: TaskMateApp()));

class TaskMateApp extends StatefulWidget {
  const TaskMateApp({super.key});
  @override
  State<TaskMateApp> createState() => _TaskMateAppState();
}

class _TaskMateAppState extends State<TaskMateApp> {
  final List> _tasks = [];
  final _controller = TextEditingController();

  void _addTask() {
    if (_controller.text.isNotEmpty) {
      setState(() => _tasks.add({'title': _controller.text, 'done': false}));
      _controller.clear();
    }
  }

  @override
  Widget build(BuildContext context) {
    return Scaffold(
      appBar: AppBar(title: const Text('TaskMate - ToDo App')),
      body: Column(
        children: [
          Padding(
            padding: const EdgeInsets.all(8.0),
            child: Row(
              children: [
                Expanded(child: TextField(controller: _controller, decoration: const InputDecoration(labelText: 'New Task'))),
                IconButton(icon: const Icon(Icons.add), onPressed: _addTask),
              ],
            ),
          ),
          Expanded(
            child: ListView.builder(
              itemCount: _tasks.length,
              itemBuilder: (_, i) => CheckboxListTile(
                title: Text(_tasks[i]['title']),
                value: _tasks[i]['done'],
                onChanged: (v) => setState(() => _tasks[i]['done'] = v),
              ),
            ),
          ),
        ],
      ),
    );
  }
}
