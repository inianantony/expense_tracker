# Agenda
- Installation & Tools​
- An App to enter expense​
    - Button ​
    - Text​
    - Image​
    - ListView​
    - Column​
    - GestureDetector​
    - BottomNavBar​
    - StateLess & StateFull​
    - A Simple Chart

# Prerequisites

1. Download Flutter and extract to the specific location
![alt text](https://github.com/inianantony/expense_tracker/blob/master/readme_images/fultter_path.png)
2. Install Dart and Flutter extension in Visual Studio Code

Dart Ext             |  Flutter Ext
:-------------------------:|:-------------------------:
![alt text](https://github.com/inianantony/expense_tracker/blob/master/readme_images/dart_ext.png) | ![alt text](https://github.com/inianantony/expense_tracker/blob/master/readme_images/flutter_ext.png)


3. Set up the location of Flutter in Visual Studio Code if prompted
4. Install Android Studio and Open any one Android Emulator
5. Visual Studio Code should be linked to the Emulator

# Create New Project

1. Visual Studio Code -> View -> Command Palette -> Flutter: New Project
2. Set the name of project as `expense_tracker`
3. Chosse the main.dart file and hit the debug button in Visual Studio Code to see your default app on screen
4. Optionally open the Dart dev tools to explore ( Similar to Chrome dev tools )

# Knowing the Folder Structure

1. .dart_tool directory, which is new in Dart 2, is used by pub and other tools
2. .idea -> all the project specific settings for project are stored under the .idea folder
3. android -> files and configurations specific for android
4. build -> build versions reside on this folder
5. ios -> files and configurations specific to ios
6. lib -> is our play ground, or where the app source code resides
6. test -> where the test related code is placed
7. pubspec.yaml -> same use as package.json file to specify dependencies and some configurations

# Code and Demo

1. NOTE : In Flutter the casing is very sensitive, like starting from folder naming to method namings, should start with small letter
2. NOTE : However dont worry, visual studio will guide you.

## Clean up the default code

1. Open the main.dart file under lib folder
2. Delete all the comments

## Default code explanation

```dart
void main() => runApp(MyApp());
``` 
- Entry point is the main method, and its call the runApp method and passes the widget class that holds the application

```dart
class MyApp extends StatelessWidget {
  @override
  Widget build(BuildContext context) {
    return MaterialApp(
      title: 'Expense_Tracker',
      theme: ThemeData(
        primarySwatch: Colors.blue,
      ),
      home: MyHomePage(title: 'Flutter Demo Home Page'),
    );
  }
}
``` 
- A class extends StatelessWidget
    - Stateless widgets are that that dont hold any data
    - It forces to implement build method
    - Flutter automatically calls the build method when this widget is loaded
- The build method returns MaterialApp widget
    - MaterialApp is the starting point of your app, it tells Flutter that you are going to use Material components and follow material design in your app.
    - set properties like the Theme and title
    - most importantly, the home, which bootstraps our App

```dart
class MyHomePage extends StatefulWidget {
  MyHomePage({Key key, this.title}) : super(key: key);
  final String title;

  @override
  _MyHomePageState createState() => _MyHomePageState();
}
``` 
- A Class extends StatefullWidget
    - The widget holds data
    - It forces to implement the createState method
    - Flutter automatically calls the createState method when this widget is loaded
- The createState method initializes a new state called _MyHomePageState();
    - files starting with _ means they are private and accessible to only this file
- The class also accepts two optional parameters Key key and String title
    - The Key is used to track the state from its creator ( framework handels it)
    - title is passed from class initialization

```dart
class _MyHomePageState extends State<MyHomePage> {
  int _counter = 0;

  void _incrementCounter() {
    setState(() {
      _counter++;
    });
  }

  @override
  Widget build(BuildContext context) {
    return Scaffold(
      appBar: AppBar(
        title: Text(widget.title),
      ),
      body: Center(
        child: Column(
          mainAxisAlignment: MainAxisAlignment.center,
          children: <Widget>[
            Text(
              'You have pushed the button this many times:',
            ),
            Text(
              '$_counter',
              style: Theme.of(context).textTheme.display1,
            ),
          ],
        ),
      ),
      floatingActionButton: FloatingActionButton(
        onPressed: _incrementCounter,
        tooltip: 'Increment',
        child: Icon(Icons.add),
      ),
    );
  }
}
``` 
- The state extends State class and links to MyHomePage
- Has a state property called _counter initialized to 0
- Has a method that changes the state data by calling setState method
- By extending State class, you are forced to implement the build method
    - The build method will be auto called by framework when the widget for this state is loaded
- The build method returs a Scaffold widget
    - Scaffold is used under MaterialApp, it gives you many basic functionalities, like AppBar, BottomNavigationBar, Drawer, FloatingActionButton etc.
    - appBar is the top bar of the application
    - body is the main area of the application
    - floatingActionButton is a button shown at the bottom of the screen
- Body contains 2 Text Widgets, enclosed in Column Widget which is enclosed in Center widget
- https://flutter.dev/docs/development/ui/widgets for more reference

## How the app works

- when user clicks the floating action button the state is updated by incrementing the counter
- The UI is updated with the new value

## What we are going to Build

Home Page             |  Chart Page
:-------------------------:|:-------------------------:
![alt text](https://github.com/inianantony/expense_tracker/blob/master/readme_images/home.png)   |  ![alt text](https://github.com/inianantony/expense_tracker/blob/master/readme_images/chart.png)


## Add New functionality

1. Delete floatingActionButton, _incrementCounter, _counter, and Text widget showing the counter
2. See the hot reload in action
3. Change the title to Expense Tracker
4. Wrap the AppBar title text with Center widget

### Add a new button for left arrow

```dart
RaisedButton(
    onPressed: () => {
        setState(() {
        
        }),
    },
    shape: RoundedRectangleBorder(
        borderRadius: BorderRadius.circular(5)),
    color: Colors.grey[100],
    child: Text(
        "<",
        style: TextStyle(
            color: Colors.black,
            fontFamily: 'FonsecaRounded',
            fontSize: 20),
    ),
),
``` 
- Add this button inside Column widget
- Add button height and width
```dart
ButtonTheme(
    minWidth: 25.0,
    height: 30.0,
)
```

### Delete the default text widget

- Delete the text widget for `You have pushed the button this many times:`

### Add a Text widget next to button

```dart
Text(
    "dd-MM-yyyy",
    textAlign: TextAlign.center,
),
```


### Add a new button for right arrow

```dart
ButtonTheme(
    minWidth: 25.0,
    height: 30.0,
    child: RaisedButton(
        onPressed: () => {
            setState(() {
            
            }),
        },
        shape: RoundedRectangleBorder(
            borderRadius: BorderRadius.circular(5)),
        color: Colors.grey[100],
        child: Text(
            ">",
            style: TextStyle(
                color: Colors.black,
                fontFamily: 'FonsecaRounded',
                fontSize: 20),
        ),
    ),
),
``` 
- Add this button inside Column widget

### Add a dropdown with some default shopping categories

```dart
String category = 'Grocery';
```
- Add a property category inside `_MyHomePageState` 

```dart
DropdownButton<String>(
    isExpanded: true,
    value: category,
    icon: Icon(Icons.arrow_downward),
    iconSize: 30,
    elevation: 16,
    style: TextStyle(color: Colors.black),
    underline: Container(
    height: 2,
    color: Colors.grey,
    ),
    onChanged: (String newValue) {
    setState(() {
        
    });
    },
    items: <String>[
    'Grocery',
    'Electronics',
    'Fashion',
    'Travel'
    ].map<DropdownMenuItem<String>>((String value) {
    return DropdownMenuItem<String>(
        value: value,
        child: Text(value),
    );
    }).toList(),
),
```

### Add a textfield to capture the amount

```dart
final amountController = TextEditingController();
```
- Add TextEditingController to capture the value from TextField inside `_MyHomePageState` 


```dart
TextField(
    decoration: new InputDecoration(
        labelText: "Enter your expense amount"),
    keyboardType: TextInputType.number, //
    controller: amountController,
),
```

- Add dispose function to dispose of the controller when widget is offloaded

```dart
  @override
  void dispose() {
    // Clean up the controller when the widget is disposed.
    amountController.dispose();
    super.dispose();
  }
```

### Add a button to save the value to DB

```dart
ButtonTheme(
    minWidth: 25.0,
    height: 30.0,
    child: RaisedButton(
        onPressed: () => {
            setState(() {
            
            }),
        },
        shape: RoundedRectangleBorder(
            borderRadius: BorderRadius.circular(5)),
        color: Colors.grey[100],
        child: Text(
            "Add Expense",
            style: TextStyle(
                color: Colors.black,
                fontFamily: 'FonsecaRounded',
                fontSize: 20),
        ),
    ),
),
```

### Add some style to the Add Expense section

- Wrap the Column inside container
```dart
Container(
    padding: EdgeInsets.all(10),
    margin: EdgeInsets.all(10),
```

- Add material card to the section just above the Container
```dart
Card(
```

### Align left arrow date field and right arrow in one line

- Add a Row widget to the 3 fields
```dart
Row(
    crossAxisAlignment: CrossAxisAlignment.center,
    children: <Widget>[

    ],
),
```
- move the Buttons and the date field inside the Row widget

### Wrap the date field inside an Expanded widget

```dart
Expanded(
    child: Container(
        padding: EdgeInsets.only(top: 0),
        child: Center(
            child: Text("dd-MM-yyyy", textAlign: TextAlign.center,),
        ),
    ),
),
```

### Extract the whole card to a new function to make the code a bit clean

- Extract the card a new function `getAddExpenseSection`

### Add listing section below

- Wrap the add expense section with column
- Add a container with height 30
- Now add the below code to show a dummy listing
```dart
Expanded(
    child: SizedBox(
        height: 1.0,
        child: Card(
        child: Container(
            color: Colors.grey[100],
            padding: EdgeInsets.all(10),
            child: ListView(
            children: <Widget>[
                Container(
                padding: EdgeInsets.only(top: 10),
                child: Card(
                    child: Container(
                        padding: EdgeInsets.all(20),
                        child: Row(
                        mainAxisAlignment:MainAxisAlignment.spaceBetween,
                        children: <Widget>[
                            Column(
                            crossAxisAlignment:
                                CrossAxisAlignment.start,
                            children: <Widget>[
                                Text("dd-MM-yyyy",style: Theme.of(context).primaryTextTheme.subtitle,textAlign: TextAlign.left,),
                                Text("10",style: TextStyle(fontSize: 25,),textAlign: TextAlign.left,),
                            ],
                            ),
                            Container(
                                padding: EdgeInsets.only(right: 25),
                                child: Transform.scale(
                                scale: 1.6,
                                child: Transform.rotate(
                                    angle: -10 * 3.14 / 180,
                                    child: Icon(
                                    Icons.shopping_cart,
                                    size: 45,
                                    ),
                                ),
                                )),
                        ],
                        )),
                    color: Colors.grey[400],
                    elevation: 10.0,
                ),
                )
            ],
            ),
        ),
        ),
    ),
),
```

### Extract the list area to new function

- Extract to the new function `getListingSection`

### Add bottom navigation bar

- Add a property to hold the page index
```dart
int _currentIndex = 0;
```

- Add bottomNavigationBar
```dart
bottomNavigationBar: BottomNavigationBar(
    currentIndex: _currentIndex, // new
    items: [
        BottomNavigationBarItem(
        icon: new Icon(Icons.home),
        title: new Text('Home'),
        ),
        BottomNavigationBarItem(
        icon: new Icon(Icons.pie_chart),
        title: new Text('Chart'),
        )
    ],
),
```


### Time to add new functionality

#### Add Expense -> Date

- Add internationalization package, take care of the tabing and spacing
```json
intl: ^0.16.1
```
- Reference the package in the main.dart
```dart
import 'package:intl/intl.dart';
```
- Add a date variable and show it in UI
```dart
DateTime date = new DateTime.now();
```
- Change the `dd-MM-yyyy` to
```dart
DateFormat("dd-MM-yyyy").format(date)
```
- Add functionality to the left and right arrow buttons inside `setState`

```dart
date = date.subtract(new Duration(days: 1));

date = date.add(new Duration(days: 1));
```

#### Add Expense -> Capture shopping category data
- Set the state in dropdown change
```dart
category = newValue;
```

#### Add Expense -> Saving the data

- Add a Class to represent the Expense
```dart
class Expense {
  String category;
  DateTime date;
  double amount;

  Expense({
    this.category,
    this.date,
    this.amount,
  });
}
```
- Add a list of Expense to hold each expense
```dart
List<Expense> expenseList = [];
```

- Clicking the Add button construct an Expense object and add to list
```dart
expenseList.add(Expense(
amount: double.parse(amountController.text),
category: category,
date: date));
```

- After saving the data claer the state and change the focus 
```dart
category = "Grocery";
date = DateTime.now();
amountController.text = "";
FocusScope.of(context).requestFocus(new FocusNode());
```

### Update the `getListingSection` to show data based on the stored state

```dart

  Widget getListingSection() {
    var expenses = List<Widget>();
    var icons = new Map();
    icons.putIfAbsent('Grocery', () => Icons.shopping_cart);
    icons.putIfAbsent('Electronics', () => Icons.laptop);
    icons.putIfAbsent('Fashion', () => Icons.shopping_basket);
    icons.putIfAbsent('Travel', () => Icons.beach_access);
    for (var value in expenseList) {
      expenses.add(
        Container(
          padding: EdgeInsets.only(top: 10),
          child: Card(
            child: Container(
                padding: EdgeInsets.all(20),
                child: Row(
                  mainAxisAlignment: MainAxisAlignment.spaceBetween,
                  children: <Widget>[
                    Column(
                      crossAxisAlignment: CrossAxisAlignment.start,
                      children: <Widget>[
                        Text(
                          DateFormat("dd-MM-yyyy").format(value.date),
                          style: Theme.of(context).primaryTextTheme.subtitle,
                          textAlign: TextAlign.left,
                        ),
                        Text(
                          value.amount.toString(),
                          style: TextStyle(
                            fontSize: 25,
                          ),
                          textAlign: TextAlign.left,
                        ),
                        Text(
                          value.category,
                          style: TextStyle(
                            fontSize: 15,
                          ),
                          textAlign: TextAlign.left,
                        ),
                      ],
                    ),
                    Container(
                        padding: EdgeInsets.only(right: 25),
                        child: Transform.scale(
                          scale: 1.6,
                          child: Transform.rotate(
                            angle: -10 * 3.14 / 180,
                            child: Icon(
                              icons[value.category],
                              size: 45,
                            ),
                          ),
                        )),
                  ],
                )),
            color: Colors.grey[400],
            elevation: 10.0,
          ),
        ),
      );
    }

    return Expanded(
      child: SizedBox(
        height: 1.0,
        child: Card(
          child: Container(
            color: Colors.grey[100],
            padding: EdgeInsets.all(10),
            child: ListView(
              children: expenses,
            ),
          ),
        ),
      ),
    );
  }
```

### Add some more little styling to the home page 

- On the outer Column widget add a Contanier and give some padding and color

```dart
Container(
    padding: EdgeInsets.all(20),
    color: Colors.grey[200],
)
```
- Extract this to a function called `getHome`

```dart
Widget getHome(){
    
}
```

### Add page to add Chart

- Update the index of selected tab

```dart
  void onTabTapped(int index) {
    setState(() {
      _currentIndex = index;
    });
  }
```
```dart
onTap: onTabTapped, 
```

### Add a list to hold pages

```dart
List<Widget> _pages = [
      getHome(),
      getHome(),
    ];
```
- Replace the body with the page from the _pages list
```dart
body: _pages[_currentIndex]
```

### Add a chart page

- Add a function to get data for Chart
```dart
  Map<String, double> getDataForChart() {
    Map<String, double> expenseSummary = new Map();
    expenseList.forEach((Expense expense) {
      if (!expenseSummary.containsKey(expense.category))
        expenseSummary.putIfAbsent(expense.category, () => expense.amount);
      else
        expenseSummary[expense.category] += expense.amount;
    });
    return expenseSummary;
  }
```

- Add PieChart package
```json
pie_chart: ^3.1.1
```

- Add reference in the main.dart file

```dart
import 'package:pie_chart/pie_chart.dart';
```

- Add a function to get chart

```dart
  Widget getChart() {
    List<Color> colorList = [
        Colors.yellow,
        Colors.green,
        Colors.blue,
        Colors.brown[100],
    ];
    return PieChart(
      legendStyle: TextStyle(color: Colors.black),
      dataMap: getDataForChart(),
      animationDuration: Duration(milliseconds: 800),
      chartLegendSpacing: 10.0,
      chartRadius: MediaQuery.of(context).size.width / 2.7,
      showChartValuesInPercentage: true,
      showChartValues: true,
      showChartValuesOutside: false,
      chartValueBackgroundColor: Colors.grey[200],
      colorList: colorList,
      showLegends: true,
      legendPosition: LegendPosition.right,
      decimalPlaces: 1,
      showChartValueLabel: true,
      initialAngle: 0,
      chartValueStyle: defaultChartValueStyle.copyWith(
        color: Colors.blueGrey[900].withOpacity(0.9),
      ),
      chartType: ChartType.disc,
    );
  }
```

- Now make this function as the 2nd child page by adding to `_pages` list

# Testing

## 3 types of Testing

- Unit
- Widget
- Integration

___

### Unit Test

- The `test` package provides the core framework for writing unit tests
- `Mockito` could be used to mock the dependencies

#### Issue

- We can add a new expense with invalid amount

#### Add logic to validate the amount before saving

- create a class `amount_validator.dart` under the lib folder
- Add a function `isValidAmount` 
``` dart
class AmountValidator { bool isValidAmount(String s) {} }
```
- Add the test dependency in ymal file
``` dart
test: ^1.14.3
```
- create a subfolder `unit` under the test
- Add `amount_validator_test.dart` file
- import the packages
``` dart
import 'package:expense_tracker/amount_validator.dart';
import 'package:test/test.dart';
```
- Add the test code
``` dart
void main() {
  group('NumberValidatorTests', () {
    test('isNumeric should return false when ' ' is passed', () {
      expect(AmountValidator().isValidAmount(""), false);
    });
    test('isNumeric should return false when any string is passed', () {
      expect(AmountValidator().isValidAmount("test"), false);
    });
    test('isNumeric should return true when integer is passed', () {
      expect(AmountValidator().isValidAmount("10"), true);
    });
    test('isNumeric should return true when decimal is passed', () {
      expect(AmountValidator().isValidAmount("10.50"), true);
    });
    test('isNumeric should return false when 0 is passed', () {
      expect(AmountValidator().isValidAmount("0"), false);
    });
    test('isNumeric should return false when -ve is passed', () {
      expect(AmountValidator().isValidAmount("-1"), false);
    });
    test('isNumeric should return false when -ve 0 is passed', () {
      expect(AmountValidator().isValidAmount("-0"), false);
    });
  });
}
```

``` dart
class AmountValidator {
  bool isValidAmount(String s) {
    if (s == null || double.tryParse(s) == null) {
      return false;
    }
    var value = double.tryParse(s);
    if (value <= 0) return false;
    return true;
  }
}
```

- Now we can use this validation logic in Add Expense
- import `import 'amount_validator.dart';` and then add the below code to button
``` dart
onPressed: () => {
  setState(() {
    if (!AmountValidator().isValidAmount(amountController.text)) {
      
    } else {
      expenseList.add(Expense(
          amount: double.parse(amountController.text),
          category: category,
          date: date));
      category = "Grocery";
      date = DateTime.now();
      amountController.text = "";
      FocusScope.of(context).requestFocus(new FocusNode());
    }
  }),
},
```
- Show an alert to user
``` dart
  Future<void> _showMyDialog() async {
    return showDialog<void>(
      context: context,
      barrierDismissible: false, // user must tap button!
      builder: (BuildContext context) {
        return AlertDialog(
          title: Text('Attention'),
          content: Text('Please corrent the invalid amount'),
          actions: <Widget>[
            FlatButton(
              child: Text('Ok'),
              onPressed: () {
                Navigator.of(context).pop();
              },
            ),
          ],
        );
      },
    );
  }
```
- call `_showMyDialog()` when validation fails
___

### Widget Test

- The `flutter_test` package provides the following tools for testing widgets:
  * The `WidgetTester` allows building and interacting with widgets in a test environment.
  * The `testWidgets()` function automatically creates a new `WidgetTester` for each test case, and is used in place of the normal test() function.
  * The `Finder` classes allow searching for widgets in the test environment.
  * Widget-specific `Matcher` constants help verify whether a Finder locates a widget or multiple widgets in the test environment.

#### Adding the widget test

-Add the `flutter_test` dependency
``` dart
  flutter_test:
    sdk: flutter
```
- We will be finding the widgets by Key, so we can add the keys first
  * In the list showing the expense, for the container just above row widget
  * In the amount field
  * In the add expense button
``` dart
key: Key("item_$i"),

key: Key("amountField"),

key: Key('addExpenseButton'),
```
![alt text](https://github.com/inianantony/expense_tracker/blob/master/readme_images/add_key_in_expense_list.PNG)
- Add a sub folder `widget` under test
- create a new file `add_expene_test.dart`
- import the packages
``` dart
import 'package:flutter/material.dart';
import 'package:flutter_test/flutter_test.dart';
import 'package:expense_tracker/main.dart';
```
- add the test using the `main` method
``` dart
void main() {
  testWidgets('Can Add a New Expense', (WidgetTester tester) async {

    await tester.pumpWidget(MyApp());

    final amountTextField = find.byKey(Key('amountField'));
    final firstEntryInList = find.byKey(Key("item_1"));
    final addExpenseButton = find.byKey(Key('addExpenseButton'));

    expect(firstEntryInList, findsNothing);

    await tester.enterText(amountTextField, '10');

    await tester.tap(addExpenseButton);

    await tester.pump();

    expect(find.byKey(Key("item_1")), findsOneWidget);

  });
}
```
___

### Integration Test

- integration tests, test how individual pieces work together as a whole, or capture the performance of an application running on a real device or emulator
- `flutter_driver` package provides tools to create instrumented apps and drive those apps from a test suite
- Steps
  * deploy an instrumented application to a real device or emulator
  * “drive” the application from a separate test suite & checking to make sure everything is correct along the way.
- Unlike unit and widget tests, integration test suites do not run in the same process as the app being tested
- One test file contains an “instrumented” version of the app. The instrumentation allows you to “drive” the app and record performance profiles from a test suite
- The second file contains the test suite, which drives the app and verifies that it works as expected

#### Adding the integration test

- Add the `flutter_driver` dependency
``` dart
  flutter_driver:
    sdk: flutter
```
- By convention, the integration test run under the directory is named `test_driver` , so lets create it
- create a file `app.dart` to instrument the app
- Add the below code to it
``` dart
import 'package:flutter_driver/driver_extension.dart';
import 'package:expense_tracker/main.dart' as app;

void main() {
  // This line enables the extension.
  enableFlutterDriverExtension();

  // Call the `main()` function of the app, or call `runApp` with
  // any widget you are interested in testing.
  app.main();
}
```
- Add the next file `app_test.dart` to drive the testing
- import the packages and the boilerplate code
``` dart
import 'package:flutter_driver/flutter_driver.dart';
import 'package:test/test.dart';

void main() {
  group('Expense Tracker App', () {
    FlutterDriver driver;

    // Connect to the Flutter driver before running any tests.
    setUpAll(() async {
      driver = await FlutterDriver.connect();
    });

    // Close the connection to the driver after the tests have completed.
    tearDownAll(() async {
      if (driver != null) {
        driver.close();
      }
    });
    
  });
}
```
- Add the first scenario to verify the list is empty in first load
``` dart
final amountTextField = find.byValueKey('amountField');
final buttonFinder = find.byValueKey('addExpenseButton');
final firstEntryInList = find.byValueKey('item_1');
```
``` dart
    isPresent(SerializableFinder byValueKey, FlutterDriver driver,
        {Duration timeout = const Duration(seconds: 1)}) async {
      try {
        await driver.waitFor(byValueKey, timeout: timeout);
        return true;
      } catch (exception) {
        return false;
      }
    }

    test('List is empty', () async {
      // Use the `driver.getText` method to verify the counter starts at 0.
      final isExists = await isPresent(firstEntryInList, driver);
      if (isExists) {
        print('widget is present');
      } else {
        print('widget is not present');
      }
      expect(isExists, false);
    });
```
- Run the command `flutter drive --target=test_driver/app.dart` in terminal
- Add the scenario to verify if expense can be added
``` dart
    test('Add new expense', () async {
      // First, tap the button.
      await driver.tap(amountTextField); // acquire focus
      await driver.enterText('10'); // enter text

      await driver.tap(buttonFinder);

      // Then, verify the counter text is incremented by 1.
      final isExists = await isPresent(firstEntryInList, driver);
      if (isExists) {
        print('widget is present');
      } else {
        print('widget is not present');
      }
      expect(isExists, true);
    });
```

___

