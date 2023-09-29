---
title: "How I created a dictionary app using Flutter"
datePublished: Fri Sep 29 2023 12:13:00 GMT+0000 (Coordinated Universal Time)
cuid: cln4kenl5000s08l2h7zdhgaa
slug: how-i-created-a-dictionary-app-using-flutter
cover: https://cdn.hashnode.com/res/hashnode/image/upload/v1695989558595/9306499e-e785-4485-9142-649da558eb3d.png
tags: app-development, flutter

---

Hello everyone. I recently created a Dictionary App using Flutter called "Word Lock". That app is freely available for anyone to use and is created with the Merriam-Webster API. In this tutorial, I will teach you how I achieved that.

Play Store Link to the app: [https://play.google.com/store/apps/details?id=com.dhruvbadaya.dictionary](https://play.google.com/store/apps/details?id=com.dhruvbadaya.dictionary&hl=en_IN&gl=US)

Before we begin, since most of you were asking me where I learned Flutter from, I am providing a link to a free certified Flutter course that I took when I started learning Flutter here: [https://crookshanksacademy.com/flutter](https://crookshanksacademy.com/flutter).

Here's the screenshot of the app we are going to create.

![](https://user-images.githubusercontent.com/97734029/253754210-b5ad51c9-7bc4-43da-8ade-fbeb1eee8a64.png align="left")

So start by creating an empty Flutter project.

```python
flutter create appname
```

Next, open `lib/main.dart` and delete the code there. After that, add the following code:

```dart
import 'package:dictionary/ui/home.dart';
import 'package:flutter/material.dart';

void main() {
  runApp(const MyApp());
}

class MyApp extends StatelessWidget {
  const MyApp({super.key});

  // This widget is the root of your application.
  @override
  Widget build(BuildContext context) {
    return MaterialApp(
      title: 'Dictionary',
      debugShowCheckedModeBanner: false,
      theme: ThemeData(
        colorScheme: ColorScheme.fromSeed(seedColor: Colors.black),
        primaryColor: Colors.black,
        secondaryHeaderColor: Colors.black,
        canvasColor: Colors.black,
        useMaterial3: true,
      ),
      home: const Home(),
    );
  }
}
```

The first thing we will add is a widget called Easy\_Loading. This will allow us to show a loading widget while we are fetching data from the internet. This will provide a clean interface for the users.

So let us start by adding all the dependencies. Go to `pubspec.yaml` file. Then add the following dependencies:

```yaml
  cupertino_icons: ^1.0.2
//...

//add the following:
  http: ^1.1.0
  flutter_easyloading: ^3.0.5
  just_audio: ^0.9.34
  url_launcher: ^6.0.3

//...
dev_dependencies:
  flutter_test:
```

Next, run the following command:

```bash
flutter pub get
```

Now, in `main.dart` file add the following piece of code:

```dart
      home: const Home(),
//add this:
      builder: EasyLoading.init(),
```

Now the last thing we need to do is import the easy\_loading library like this:

```dart
import 'package:flutter_easyloading/flutter_easyloading.dart';
```

Great. Now we are all set up. Let us start by creating the homepage. In `lib` folder, create another folder called `ui` and create a file `home.dart` in it. Write the following code in it:

```dart
import 'package:dictionary/ui/constants/colors.dart';
import 'package:flutter/material.dart';
import '../methods/find_word.dart';
import 'about.dart';

// ignore: must_be_immutable
class Home extends StatefulWidget {
  const Home({super.key});

  @override
  State<Home> createState() => _HomeState();
}

class _HomeState extends State<Home> {
  TextEditingController word = TextEditingController();

  int _selectedIndex = 0;
 //New
  @override
  Widget build(BuildContext context) {
    return Scaffold(
      appBar: AppBar(backgroundColor: Colors.black,elevation: 0,toolbarHeight: 0,),
      backgroundColor: backgroundColor,
      bottomNavigationBar: BottomNavigationBar(
        currentIndex: _selectedIndex, //New
        onTap: _onItemTapped,         //New
        backgroundColor: backgroundColor,
        elevation: 0,
        selectedIconTheme: const IconThemeData(
          color: Colors.black,
        ),
        selectedItemColor: Colors.black,
        selectedLabelStyle: const TextStyle(color: Colors.black),
        items:  const <BottomNavigationBarItem>[
                  //New
          BottomNavigationBarItem(

            icon: Icon(Icons.home),
            label: 'Home',
          ),

          BottomNavigationBarItem(
            icon: Icon(Icons.info),
            label: 'About',
          ),
        ],
      ),
      body: Padding(
        padding: const EdgeInsets.symmetric(horizontal: 28),
        child: Column(
          mainAxisAlignment: MainAxisAlignment.center,
          crossAxisAlignment: CrossAxisAlignment.start,
          children: [
            const Text(
              "Word Lock",
              style: TextStyle(
                  fontFamily: "Title",
                  fontSize: 40,
                  fontWeight: FontWeight.w900,),
              textAlign: TextAlign.left,
            ),
            const Text(
              "Over 100,000 Definitions and Pronunciations",
              style: TextStyle(
                  fontFamily: "SansSerif",
                  fontSize: 18,
                  fontWeight: FontWeight.w400,
              color: Colors.grey,),
              textAlign: TextAlign.left,
            ),
            const SizedBox(
              height: 20,
            ),
            TextField(
              decoration: InputDecoration(
                hintText: 'search word',
                prefixIcon: IconButton(
                  icon: const Icon(
                    Icons.search,
                    color: Colors.grey,
                  ),
                  onPressed: () {
                    if(word.text.replaceAll(" ", "").isNotEmpty) findWord(word.text, context);
                  },
                ),
                filled: true,
                fillColor: searchBackground,
                border: InputBorder.none,
                contentPadding: const EdgeInsets.only(top: 10, bottom: 10),
              ),
              style: const TextStyle(
                  fontFamily: "SansSerif", fontWeight: FontWeight.w500),
              textInputAction: TextInputAction.search,
              controller: word,
              onSubmitted: (value) {
                if(word.text.replaceAll(" ", "").isNotEmpty) findWord(word.text, context);
              },
            ),
            const SizedBox(height: 25),
        const Text(
          "Powered by Merriam Webster © 2023",
          style: TextStyle(
            fontFamily: "SansSerif",
            fontSize: 12,
            fontWeight: FontWeight.w400,
            color: Colors.grey,),),
          ],
        ),
      ),
    );

  }

  void _onItemTapped(int index) {
    setState(() {
      _selectedIndex = index;
    });
    if(index==1){
      goTo(const About());
    }
    setState(() {
      _selectedIndex=0;
    });
  }

  void goTo(var className){
    Navigator.push(
      context,
      MaterialPageRoute(builder: (context) => className),
    );
  }
}
```

Here, if you observe, we used three constants in place of colors. So let us create those constants now. Inside your `lib/ui` folder, create another folder called `constants` and inside it create a file called `colors.dart`. Type in the following:

```dart
import 'package:flutter/material.dart';
const Color backgroundColor=Colors.white;
const Color searchBackground=Color(0xFFebebeb);
const Color appBarColor=Colors.black;
```

Next, we need functions to fetch data from the API. The first thing you need to do is get your API Key from Merriam Webster's website. After that, create a folder called `fetch` inside `lib` and add the following in a file named `constants.dart`:

```dart
const apiKey1="we are removing the api key from here for privacy reasons";

String fetchURL(String word,String apiKey){
  return "https://www.dictionaryapi.com/api/v3/references/collegiate/json/$word?key=$apiKey";
}

String fetchAudioURL(String audioName){
  return "https://media.merriam-webster.com/audio/prons/en/us/mp3/${audioName[0]}/$audioName.mp3";
}
```

Next, inside the same folder create a file named `fetch_data.dart` and add the following code to it:

```dart
import 'dart:convert';
import 'package:dictionary/fetch/constants.dart';
import 'package:http/http.dart' as http;
import 'package:url_launcher/url_launcher.dart';

Future<List<dynamic>> fetchData(String word, String apiKey) async {
  var result = await http.get(Uri.parse(fetchURL(word, apiKey)));
  return (jsonDecode(result.body));
}

Future<void> launchUrlInBrowser(Uri url) async {
  if (!await launchUrl(url, mode: LaunchMode.externalApplication)) {
    throw Exception('Could not launch $url');
  }
}
```

In the same folder, create a file called `fetch_meaning.dart` and write the following code in it:

```dart
import 'dart:math';

import 'package:dictionary/fetch/constants.dart';
import 'package:dictionary/fetch/fetch_data.dart';

Future<List> getWordMeanings(String word) async {
  List getData=(await fetchData(word, (Random().nextBool())?apiKey1:apiKey2));


  //finding if the word exists or not
  try{
    getData[0]["meta"];
  }catch(e){
    return ["notfound",getData];
  }

  //this will be executed if the word exists
  return ["found",getData];
}
```

Next, we need two methods which you can store anywhere. I am providing you with the code of both the methods here:

```dart
import 'package:flutter/material.dart';
import 'package:flutter_easyloading/flutter_easyloading.dart';
import '../fetch/fetch_meaning.dart';
import '../ui/word.dart';
import '../ui/wordnotfound.dart';

Future<void> findWord(String text, BuildContext context) async {
  EasyLoading.show(status: 'looking up...');
  List meaning = await getWordMeanings(text);
  EasyLoading.dismiss();
  if (meaning[0] == "found") {
    // ignore: use_build_context_synchronously
    Navigator.push(
      context,
      MaterialPageRoute(builder: (context) => Word(text, [meaning[1]])),
    );
  } else {
    // ignore: use_build_context_synchronously
    Navigator.push(
      context,
      MaterialPageRoute(builder: (context) => WordNotFound([meaning[1]])),
    );
  }
}
```

```dart
import 'package:flutter/material.dart';

import 'find_word.dart';

class SimilarWord extends StatelessWidget {
  const SimilarWord({
    super.key,
    required this.words,
    required this.index,
    required this.easteregg,
  });

  final List words;
  final int index;
  final String easteregg;

  @override
  Widget build(BuildContext context) {
    return GestureDetector(
      onTap: () {
        findWord((words[0].length > 0) ? words[0][index] : easteregg, context);
      },
      child: Text(
        (words[0].length > 0) ? words[0][index] : easteregg,
        style: const TextStyle(fontWeight: FontWeight.w800, fontSize: 25),
      ),
    );
  }
}
```

Lastly, we need two pages: one that we will show when word is found and the other we will show when word is not found. If the word is found, we will show the following page:

```dart
import 'package:dictionary/ui/constants/colors.dart';
import 'package:flutter/material.dart';
import 'package:just_audio/just_audio.dart';

import '../fetch/constants.dart';

// ignore: must_be_immutable
class Word extends StatefulWidget {
  String word;
  List list;

  Word(this.word, this.list, {super.key});

  @override
  State<Word> createState() => _WordState();
}

final player1 = AudioPlayer();
int listLength = 1;
int selectedMeaning = 0;
List loopingList = [];
String pronunciation = " ";
String audioURL = "notexisting";
bool partOfSpeechDoesNotExist = false;

class _WordState extends State<Word> {
  @override
  void initState() {
    try {
      if (widget.list[0][0]["fl"] == null) {
        widget.list[0][0]["fl"] = widget.list[0][1]["fl"];
      }
    } catch (e) {
      partOfSpeechDoesNotExist = true;
    }
    loopingList = [];
    pronunciation = " ";
    listLength = 1;
    selectedMeaning = 0;
    audioURL = "notexisting";
    for (int i = 0; i < 2; i++) {
      try {
        // ignore: unused_local_variable
        String a = widget.list[0][i + 1]["fl"];
        if ((widget.list[0][i + 1]["fl"]) == null) {
          throw Exception();
        }
        loopingList.add(i + 1);
      } catch (e) {
        break;
      }
    }

    try {
      pronunciation = widget.list[0][0]["hwi"]["prs"][0]["mw"];
      // ignore: empty_catches
    } catch (e) {}

    try {
      audioSetter();
      // ignore: empty_catches
    } catch (e) {}
    super.initState();
  }

  Future<void> audioSetter() async {
    audioURL =
        fetchAudioURL(widget.list[0][0]["hwi"]["prs"][0]["sound"]["audio"]);
    await player1.setUrl(audioURL);
  }

  @override
  Widget build(BuildContext context) {
    return Scaffold(
      backgroundColor: backgroundColor,
      appBar: AppBar(
        backgroundColor: appBarColor,
        iconTheme: const IconThemeData(color: backgroundColor),
      ),
      body: SafeArea(
        child: Padding(
          padding: const EdgeInsets.symmetric(horizontal: 28),
          child: Column(
            mainAxisAlignment: MainAxisAlignment.center,
            crossAxisAlignment: CrossAxisAlignment.start,
            children: [
              Text(
                widget.word,
                style: const TextStyle(
                    fontFamily: "Title",
                    fontSize: 48,
                    fontWeight: FontWeight.w800),
              ),
              (pronunciation != " ")
                  ? Row(
                      children: [
                        Text(
                          pronunciation,
                          style: const TextStyle(
                              fontFamily: "SansSerifReg",
                              fontWeight: FontWeight.w600,
                              fontSize: 18,
                              fontStyle: FontStyle.italic),
                        ),
                        const SizedBox(
                          width: 5,
                        ),
                        IconButton(
                          onPressed: () async {
                            if (audioURL != "notexisting") {
                              await player1.setClip(
                                  start: const Duration(seconds: 0));
                              await player1.play();
                              await player1.stop();
                            }
                          },
                          icon: const Icon(
                            Icons.volume_up,
                          ),
                        )
                      ],
                    )
                  : const SizedBox(
                      height: 0,
                    ),
              const SizedBox(
                height: 12,
              ),
              SingleChildScrollView(
                scrollDirection: Axis.horizontal,
                child: Row(
                  children: [
                    (partOfSpeechDoesNotExist)
                        ? const SizedBox(
                            height: 0,
                          )
                        : GestureDetector(
                            onTap: () {
                              setState(() {
                                selectedMeaning = 0;
                              });
                            },
                            child: Container(
                              decoration: BoxDecoration(
                                  color: (selectedMeaning == 0)
                                      ? Colors.black
                                      : Colors.transparent,
                                  border:
                                      Border.all(color: Colors.black, width: 1),
                                  borderRadius: const BorderRadius.only(
                                      topLeft: Radius.circular(10),
                                      bottomLeft: Radius.circular(10))),
                              child: Padding(
                                padding: const EdgeInsets.symmetric(
                                    vertical: 5, horizontal: 10),
                                child: Text(
                                  widget.list[0][0]["fl"],
                                  style: TextStyle(
                                      color: (selectedMeaning == 0)
                                          ? Colors.white
                                          : Colors.black),
                                ),
                              ),
                            ),
                          ),
                    (loopingList.contains(2))
                        ? GestureDetector(
                            onTap: () {
                              setState(() {
                                selectedMeaning = 2;
                              });
                            },
                            child: Container(
                              decoration: BoxDecoration(
                                border: const Border.symmetric(
                                    vertical: BorderSide.none,
                                    horizontal: BorderSide(width: 1)),
                                color: (selectedMeaning == 2)
                                    ? Colors.black
                                    : Colors.transparent,
                              ),
                              child: Padding(
                                padding: const EdgeInsets.symmetric(
                                    vertical: 5, horizontal: 10),
                                child: Text(widget.list[0][2]["fl"],
                                    style: TextStyle(
                                        color: (selectedMeaning == 2)
                                            ? Colors.white
                                            : Colors.black)),
                              ),
                            ),
                          )
                        : const SizedBox(
                            height: 0,
                          ),
                    (loopingList.contains(1))
                        ? GestureDetector(
                            onTap: () {
                              setState(() {
                                selectedMeaning = 1;
                              });
                            },
                            child: Container(
                              decoration: BoxDecoration(
                                color: (selectedMeaning == 1)
                                    ? Colors.black
                                    : Colors.transparent,
                                border:
                                    Border.all(color: Colors.black, width: 1),
                                borderRadius: const BorderRadius.only(
                                  topRight: Radius.circular(10),
                                  bottomRight: Radius.circular(10),
                                ),
                              ),
                              child: Padding(
                                padding: const EdgeInsets.symmetric(
                                    vertical: 5, horizontal: 10),
                                child: Text(widget.list[0][1]["fl"],
                                    style: TextStyle(
                                        color: (selectedMeaning == 1)
                                            ? Colors.white
                                            : Colors.black)),
                              ),
                            ),
                          )
                        : const SizedBox(
                            height: 0,
                          ),
                  ],
                ),
              ),
              const SizedBox(
                height: 20,
              ),
              ListView.builder(
                  shrinkWrap: true,
                  itemCount: widget.list[0][selectedMeaning]["shortdef"].length,
                  itemBuilder: (BuildContext context, int index) {
                    return ListTile(
                      leading: Text("${index + 1}"),
                      title: SelectableText(
                        widget.list[0][selectedMeaning]["shortdef"][index],
                        style: const TextStyle(
                            fontFamily: "sansSerif", fontSize: 16),
                      ),
                    );
                  }),
              const SizedBox(
                height: 40,
              )
            ],
          ),
        ),
      ),
    );
  }
}
```

If word is not found, we will show the following page:

```dart
import 'package:flutter/material.dart';
import '../methods/similar_word.dart';

// ignore: must_be_immutable
class WordNotFound extends StatelessWidget {
  List words;
  WordNotFound(this.words, {super.key});

  @override
  Widget build(BuildContext context) {
    return Scaffold(
      appBar: AppBar(
        backgroundColor: Colors.black,
        iconTheme: const IconThemeData(
          color: Colors.white,
        ),
      ),
      body: Padding(
        padding: const EdgeInsets.all(
          30.0,
        ),
        child: Column(
          mainAxisAlignment: MainAxisAlignment.center,
          children: [
            const Text(
              "Sorry Buddy, We did not find your word. 🥺",
              style: TextStyle(
                fontSize: 35,
                fontFamily: "Title",
              ),
              textAlign: TextAlign.left,
            ),
            const SizedBox(
              height: 20,
            ),
            const Text(
              "However, here are three words with similar spellings:",
              style: TextStyle(
                fontSize: 20,
                fontFamily: "sansSerif",
              ),
            ),
            const SizedBox(
              height: 20,
            ),
            Padding(
              padding: const EdgeInsets.symmetric(
                horizontal: 10.0,
              ),
              child: Row(
                mainAxisAlignment: MainAxisAlignment.spaceBetween,
                children: [
                  SimilarWord(
                    words: words,
                    index: 0,
                    easteregg: 'what',
                  ),
                  SimilarWord(
                    words: words,
                    index: 1,
                    easteregg: 'the',
                  ),
                  SimilarWord(
                    words: words,
                    index: 2,
                    easteregg: 'word',
                  ),
                ],
              ),
            ),
          ],
        ),
      ),
    );
  }
}
```

And we are done. Here are more screenshots of the app:

![](https://user-images.githubusercontent.com/97734029/253754734-610f01d5-e7b1-4766-9d1f-2ccd6e90350f.png align="left")

![](https://user-images.githubusercontent.com/97734029/253754212-93ac52fe-4cdb-475a-b7af-e77ff4f78d22.png align="left")