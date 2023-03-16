# Flutter ShowCaseView

A Flutter package allows you to Showcase/Highlight your widgets step by step.

## Installing

1. Add dependency to pubspec.yaml

Get the latest version in the 'Installing' tab on pub.dev

   `dependencies:
   showcaseview: <latest-version>`

2. Import the package

   `import 'package:showcaseview/showcaseview.dart';`

3. Adding a ShowCaseWidget widget.

   `ShowCaseWidget(
   builder: Builder(
   builder : (context)=> Somewidget()
   ),
   ),`

4. Adding a Showcase widget.

   `GlobalKey _one = GlobalKey();
   GlobalKey _two = GlobalKey();
   GlobalKey _three = GlobalKey(); 
   ...
   Showcase(
   key: _one,
   title: 'Menu',
   description: 'Click here to see menu options',
   child: Icon(
   Icons.menu, 
   color: Colors.black45,
   ),
   ),
   Showcase.withWidget(
   key: _three,
   height: 80,
   width: 140,
   targetShapeBorder: CircleBorder(),
   container: Column(
   crossAxisAlignment: CrossAxisAlignment.start,
   children: <Widget>[
   ...
   ],
   ),
   child: ...,
   ),`

5. Starting the ShowCase

   `someEvent(){
   ShowCaseWidget.of(context).startShowCase([_one, _two, _three]);
   }`

If you want to start the ShowCaseView as soon as your UI built up then use below code.

   `WidgetsBinding.instance.addPostFrameCallback((_) =>
   ShowCaseWidget.of(context).startShowCase([_one, _two, _three])
   );`

## How to use

Check out the example app in the example directory or the 'Example' tab on pub.dartlang.org for a more complete example.

### Scrolling to active showcase

Auto Scrolling to active showcase feature will not work properly in scroll views that renders widgets on demand(ex, ListView, GridView).

In order to scroll to a widget it needs to be attached with widget tree. So, If you are using a scrollview that renders widgets on demand, it is possible that the widget on which showcase is applied is not attached in widget tree. So, flutter won't be able to scroll to that widget.

So, If you want to make a scroll view that contains less number of children widget then prefer to use SingleChildScrollView.

If using SingleChildScrollView is not an option, then you can assign a ScrollController to that scrollview and manually scroll to the position where showcase widget gets rendered. You can add that code in onStart method of ShowCaseWidget.

Example,

   `// This controller will be assigned to respected sctollview.
   final _controller = ScrollController();
   ShowCaseWidget(
   onStart: (index, key) { 
   if(index == 0) { 
   WidgetsBinding.instance.addPostFrameCallback((_) { 
   // If showcase widget is at offset 1000 in the listview. 
   // If you don't know the exact position of the showcase widget, 
   // You can provide nearest possible location. 
   // 
   // In this case providing 990 instead of 1000 will work as well.
   _controller.jumpTo(1000); 
   });
   }
   },
   );`
