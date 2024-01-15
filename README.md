# Quiz-App
BHARAT INTERN

import 'package:flutter/material.dart';
import 'package:fluttertoast/fluttertoast.dart';

void main() {
  runApp(QuizApp());
}

class QuizApp extends StatelessWidget {
  @override
  Widget build(BuildContext context) {
    return MaterialApp(
      title: 'Quiz App',
      home: QuizScreen(),
    );
  }
}

class QuizScreen extends StatefulWidget {
  @override
  _QuizScreenState createState() => _QuizScreenState();
}

class _QuizScreenState extends State<QuizScreen> {
  int currentQuestionIndex = 0;
  List<Question> questions = [
    Question('Is Flutter a framework for web development?', false),
    Question('Is Dart the only programming language used in Flutter?', false),
    Question('Are widgets the core building blocks in Flutter?', true),
  ];

  @override
  Widget build(BuildContext context) {
    return Scaffold(
      appBar: AppBar(
        title: Text('Quiz App'),
      ),
      body: Padding(
        padding: const EdgeInsets.all(16.0),
        child: Column(
          crossAxisAlignment: CrossAxisAlignment.stretch,
          children: [
            Text(
              questions[currentQuestionIndex].text,
              style: TextStyle(fontSize: 18.0),
            ),
            SizedBox(height: 20.0),
            ElevatedButton(
              onPressed: () {
                checkAnswer(true);
              },
              child: Text('True'),
            ),
            SizedBox(height: 10.0),
            ElevatedButton(
              onPressed: () {
                checkAnswer(false);
              },
              child: Text('False'),
            ),
          ],
        ),
      ),
    );
  }

  void checkAnswer(bool userAnswer) {
    bool correctAnswer = questions[currentQuestionIndex].answer;

    if (userAnswer == correctAnswer) {
      showToast('Correct!');
    } else {
      showToast('Incorrect!');
    }

    // Move to the next question
    setState(() {
      currentQuestionIndex++;
      if (currentQuestionIndex >= questions.length) {
        currentQuestionIndex = 0; // Restart the quiz
      }
    });
  }

  void showToast(String message) {
    Fluttertoast.showToast(
      msg: message,
      toastLength: Toast.LENGTH_SHORT,
      gravity: ToastGravity.BOTTOM,
      backgroundColor: Colors.green,
      textColor: Colors.white,
    );
  }
}

class Question {
  String text;
  bool answer;

  Question(this.text, this.answer);
}
