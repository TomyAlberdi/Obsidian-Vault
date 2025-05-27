Created: 2025-05-27 16:58
## Family Tree:
1. Clean Code
2. [[Comments]]
-- -
Some comments are necessary or beneficial. Keep in mind, however, that the only truly good comment is the one you found a way not to write.
#### Legal Comments
Sometimes our corporate coding standards force us to write certain comments for legal reasons. For example, copyright and authorship statements are necessary and reasonable things to put into a comment at the start of each source file.
```java
// Copyright (C) 2003, 2004, 2005 by Object Mentor, Inc. All rights reserved.
// Released under the terms of the GNU General Public License version 2 or later.
```
Comments like this should not be contracts or legal tomes. Where possible, refer to a standard license or other external document rather than putting all the terms and conditions into the comment.
#### Informative Comments
It is sometimes useful to provide basic information with a comment.
```java
// format matched kk:mm:ss EEE, MMM dd, yyyy
Pattern timeMatcher = Pattern.compile("\\d*:\\d*:\\d* \\w*, \\w* \\d*, \\d*");
```
In this case the comment lets us know that the regular expression is intended to match a time and date that were formatted with the `SimpleDateFormat.format` function using the specified format string.
#### Explanation of Intent
Sometimes a comment goes beyond just useful information about the implementation and provides the intent behind a decision. In the following case we see an interesting decision documented by a comment:
```java
public void testConcurrentAddWidgets() throws Exception {
	WidgetBuilder widgetBuilder = new WidgetBuilder(new Class[]{BoldWidget.class});
	String text = "'''bold text'''"
	ParentWidget patent = new BoldWidget(new MockWidgetRoot(),"'''bold text'''");
	AtomicBoolean failFlag = new AtomicBoolean();
	failFlag.set(false)
	// this is our best attempt to get a race condition
	// by creating large number of threads
	for (int i = 0; i < 25000; i++) {
		WidgetBuilderThread widgetBuilderThread = new WidgetBuilderThread(widgetBuilder, text, parent, failFlag);
		Thread thread = new Thread(widgetBuilderThread);
		thread.start();
	}
	assertEquals(false, failFlag.get())
}
```