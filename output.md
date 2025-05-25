# Flutter Shadcn UI Documentation

Flutter Shadcn UI is a beautiful, accessible, and customizable UI component library for Flutter applications, inspired by the popular Shadcn UI for web.

![Shadcn UI](/shadcn-banner.png)

> Note: The work is still in progress.

## Table of Contents

- [Installation](#installation)
- [Setup Options](#setup-options)
  - [Shadcn (pure)](#shadcn-pure)
  - [Shadcn + Material](#shadcn--material)
  - [Shadcn + Cupertino](#shadcn--cupertino)
- [Components](#components)
  - [Accordion](#accordion)
  - [Alert](#alert)
  - [Button](#button)
  - [Card](#card)
  - [Checkbox](#checkbox)
  - [Dialog](#dialog)
  - [Input](#input)
  - [Select](#select)
  - [Switch](#switch)
  - [Tabs](#tabs)

## Installation

Run this command in your terminal from your project root directory:

```bash
flutter pub add shadcn_ui
```

Or manually add it to your `pubspec.yaml`:

```yaml
dependencies:
    shadcn_ui: ^0.2.4 # replace with the latest version
```

## Setup Options

### Shadcn (pure)

Use the `ShadApp` widget if you want to use just the ShadcnUI components, without Material or Cupertino.

```dart
import 'package:shadcn_ui/shadcn_ui.dart';

void main() {
  runApp(const MyApp());
}

class MyApp extends StatelessWidget {
  const MyApp({super.key});

  @override
  Widget build(BuildContext context) {
    return ShadApp();
  }
}
```

### Shadcn + Material

Flutter Shadcn UI allows shadcn components to be used simultaneously with Material components. The setup is simple:

```dart
import 'package:shadcn_ui/shadcn_ui.dart';
import 'package:flutter/material.dart';

void main() {
  runApp(const MyApp());
}

class MyApp extends StatelessWidget {
  const MyApp({super.key});

  @override
  Widget build(BuildContext context) {
    return ShadApp.custom(
      themeMode: ThemeMode.dark,
      darkTheme: ShadThemeData(
        brightness: Brightness.dark,
        colorScheme: const ShadSlateColorScheme.dark(),
      ),
      appBuilder: (context) {
        return MaterialApp(
          theme: Theme.of(context),
          builder: (context, child) {
            return ShadAppBuilder(child: child!);
          },
        );
      },
    );
  }
}
```

The default `ThemeData` created by `ShadApp` is:

```dart
ThemeData(
  useMaterial3: true,
  brightness: themeData.brightness,
  colorScheme: ColorScheme(
    brightness: themeData.brightness,
    primary: themeData.colorScheme.primary,
    onPrimary: themeData.colorScheme.primaryForeground,
    secondary: themeData.colorScheme.secondary,
    onSecondary: themeData.colorScheme.secondaryForeground,
    error: themeData.colorScheme.destructive,
    onError: themeData.colorScheme.destructiveForeground,
    background: themeData.colorScheme.background,
    onBackground: themeData.colorScheme.foreground,
    surface: themeData.colorScheme.card,
    onSurface: themeData.colorScheme.cardForeground,
  ),
  scaffoldBackgroundColor: themeData.colorScheme.background,
  dividerColor: themeData.colorScheme.border,
  dividerTheme: DividerThemeData(
    color: themeData.colorScheme.border,
    thickness: 1,
  ),
  textSelectionTheme: TextSelectionThemeData(
    cursorColor: themeData.colorScheme.primary,
    selectionColor: themeData.colorScheme.selection,
    selectionHandleColor: themeData.colorScheme.primary,
  ),
  iconTheme: IconThemeData(
    size: 16,
    color: themeData.colorScheme.foreground,
  ),
  scrollbarTheme: ScrollbarThemeData(
    crossAxisMargin: 1,
    mainAxisMargin: 1,
    thickness: const WidgetStatePropertyAll(8),
    radius: const Radius.circular(999),
    thumbColor: WidgetStatePropertyAll(themeData.colorScheme.border),
  ),
),
```

### Shadcn + Cupertino

If you need to use shadcn components with Cupertino components, use `CupertinoApp` instead of `MaterialApp`:

```dart
import 'package:shadcn_ui/shadcn_ui.dart';
import 'package:flutter/cupertino.dart';
import 'package:flutter_localizations/flutter_localizations.dart';

void main() {
  runApp(const MyApp());
}

class MyApp extends StatelessWidget {
  const MyApp({super.key});

  @override
  Widget build(BuildContext context) {
    return ShadApp.custom(
      themeMode: ThemeMode.dark,
      darkTheme: ShadThemeData(
        brightness: Brightness.dark,
        colorScheme: const ShadSlateColorScheme.dark(),
      ),
      appBuilder: (context) {
        return CupertinoApp(
          theme: CupertinoTheme.of(context),
          localizationsDelegates: const [
            DefaultMaterialLocalizations.delegate,
            DefaultCupertinoLocalizations.delegate,
            DefaultWidgetsLocalizations.delegate,
          ],
          builder: (context, child) {
            return ShadAppBuilder(child: child!);
          },
        );
      },
    );
  }
}
```

The default `CupertinoThemeData` created by `ShadApp` is:

```dart
CupertinoThemeData(
  primaryColor: themeData.colorScheme.primary,
  primaryContrastingColor: themeData.colorScheme.primaryForeground,
  scaffoldBackgroundColor: themeData.colorScheme.background,
  barBackgroundColor: themeData.colorScheme.primary,
  brightness: themeData.brightness,
),
```

## Components

### Accordion

A vertically stacked set of interactive headings that each reveal a section of content.

#### Basic Accordion

```dart
final details = [
  (
    title: 'Is it acceptable?',
    content: 'Yes. It adheres to the WAI-ARIA design pattern.',
  ),
  (
    title: 'Is it styled?',
    content: "Yes. It comes with default styles that matches the other components' aesthetic.",
  ),
  (
    title: 'Is it animated?',
    content: "Yes. It's animated by default, but you can disable it if you prefer.",
  ),
];

@override
Widget build(BuildContext context) {
  return ShadAccordion<({String content, String title})>(
    children: details.map(
      (detail) => ShadAccordionItem(
        value: detail,
        title: Text(detail.title),
        child: Text(detail.content),
      ),
    ),
  );
}
```

#### Multiple Accordion

```dart
final details = [
  (
    title: 'Is it acceptable?',
    content: 'Yes. It adheres to the WAI-ARIA design pattern.',
  ),
  (
    title: 'Is it styled?',
    content: "Yes. It comes with default styles that matches the other components' aesthetic.",
  ),
  (
    title: 'Is it animated?',
    content: "Yes. It's animated by default, but you can disable it if you prefer.",
  ),
];

@override
Widget build(BuildContext context) {
  return ShadAccordion<({String content, String title})>.multiple(
    children: details.map(
      (detail) => ShadAccordionItem(
        value: detail,
        title: Text(detail.title),
        child: Text(detail.content),
      ),
    ),
  );
}
```

### Alert

Displays a callout for user attention.

#### Basic Alert

```dart
ShadAlert(
  iconData: LucideIcons.terminal,
  title: Text('Heads up!'),
  description: Text('You can add components to your app using the cli.'),
),
```

#### Destructive Alert

```dart
ShadAlert.destructive(
  iconData: LucideIcons.circleAlert,
  title: Text('Error'),
  description: Text('Your session has expired. Please log in again.'),
)
```

### Button

Displays a button or a component that looks like a button.

#### Primary Button

```dart
ShadButton(
  child: const Text('Primary'),
  onPressed: () {},
)
```

#### Secondary Button

```dart
ShadButton.secondary(
  child: const Text('Secondary'),
  onPressed: () {},
)
```

#### Destructive Button

```dart
ShadButton.destructive(
  child: const Text('Destructive'),
  onPressed: () {},
)
```

#### Outline Button

```dart
ShadButton.outline(
  child: const Text('Outline'),
  onPressed: () {},
)
```

#### Ghost Button

```dart
ShadButton.ghost(
  child: const Text('Ghost'),
  onPressed: () {},
)
```

#### Link Button

```dart
ShadButton.link(
  child: const Text('Link'),
  onPressed: () {},
)
```

#### Text and Icon Button

```dart
ShadButton(
  onPressed: () {},
  leading: const Icon(LucideIcons.mail),
  child: const Text('Login with Email'),
)
```

#### Loading Button

```dart
ShadButton(
  onPressed: () {},
  leading: const SizedBox.square(
    dimension: 16,
    child: CircularProgressIndicator(
      strokeWidth: 2,
      color: ShadTheme.of(context).colorScheme.primaryForeground,
    ),
  ),
  child: const Text('Please wait'),
)
```

#### Gradient and Shadow Button

```dart
ShadButton(
  onPressed: () {},
  gradient: const LinearGradient(colors: [
    Colors.cyan,
    Colors.indigo,
  ]),
  shadows: [
    BoxShadow(
      color: Colors.blue.withOpacity(.4),
      spreadRadius: 4,
      blurRadius: 10,
      offset: const Offset(0, 2),
    ),
  ],
  child: const Text('Gradient with Shadow'),
)
```

### Card

Displays a card with header, content, and footer.

```dart
const frameworks = {
  'next': 'Next.js',
  'react': 'React',
  'astro': 'Astro',
  'nuxt': 'Nuxt.js',
};

class CardProject extends StatelessWidget {
  const CardProject({super.key});

  @override
  Widget build(BuildContext context) {
    final theme = ShadTheme.of(context);
    return ShadCard(
      width: 350,
      title: Text('Create project', style: theme.textTheme.h4),
      description: const Text('Deploy your new project in one-click.'),
      footer: Row(
        mainAxisAlignment: MainAxisAlignment.spaceBetween,
        children: [
          ShadButton.outline(
            child: const Text('Cancel'),
            onPressed: () {},
          ),
          ShadButton(
            child: const Text('Deploy'),
            onPressed: () {},
          ),
        ],
      ),
      child: Padding(
        padding: const EdgeInsets.symmetric(vertical: 16),
        child: Column(
          mainAxisSize: MainAxisSize.min,
          crossAxisAlignment: CrossAxisAlignment.stretch,
          children: [
            const Text('Name'),
            const ShadInput(placeholder: Text('Name of your project')),
            const SizedBox(height: 6),
            const Text('Framework'),
            ShadSelect<String>(
              placeholder: const Text('Select'),
              options: frameworks.entries
                  .map((e) => ShadOption(value: e.key, child: Text(e.value)))
                  .toList(),
              selectedOptionBuilder: (context, value) {
                return Text(frameworks[value]!);
              },
              onChanged: (value) {},
            ),
          ],
        ),
      ),
    );
  }
}
```

### Checkbox

A control that allows the user to toggle between checked and not checked.

#### Basic Checkbox

```dart
class CheckboxSample extends StatefulWidget {
  const CheckboxSample({super.key});

  @override
  State<CheckboxSample> createState() => _CheckboxSampleState();
}

class _CheckboxSampleState extends State<CheckboxSample> {
  bool value = false;

  @override
  Widget build(BuildContext context) {
    return ShadCheckbox(
      value: value,
      onChanged: (v) => setState(() => value = v),
      label: const Text('Accept terms and conditions'),
      sublabel: const Text(
        'You agree to our Terms of Service and Privacy Policy.',
      ),
    );
  }
}
```

#### Form Checkbox

```dart
ShadCheckboxFormField(
  id: 'terms',
  initialValue: false,
  inputLabel: const Text('I accept the terms and conditions'),
  onChanged: (v) {},
  inputSublabel: const Text('You agree to our Terms and Conditions'),
  validator: (v) {
    if (!v) {
      return 'You must accept the terms and conditions';
    }
    return null;
  },
)
```

### Dialog

A modal dialog that interrupts the user.

#### Basic Dialog

```dart
final profile = [
  (title: 'Name', value: 'Alexandru'),
  (title: 'Username', value: 'nank1ro'),
];

class DialogExample extends StatelessWidget {
  const DialogExample({super.key});

  @override
  Widget build(BuildContext context) {
    final theme = ShadTheme.of(context);
    return ShadButton.outline(
      child: const Text('Edit Profile'),
      onPressed: () {
        showShadDialog(
          context: context,
          builder: (context) => ShadDialog(
            title: const Text('Edit Profile'),
            description: const Text(
                "Make changes to your profile here. Click save when you're done"),
            actions: const [ShadButton(child: Text('Save changes'))],
            child: Container(
              width: 375,
              padding: const EdgeInsets.symmetric(vertical: 20),
              child: Column(
                mainAxisSize: MainAxisSize.min,
                crossAxisAlignment: CrossAxisAlignment.end,
                children: profile
                    .map(
                      (p) => Row(
                        children: [
                          Expanded(
                            child: Text(
                              p.title,
                              textAlign: TextAlign.end,
                              style: theme.textTheme.small,
                            ),
                          ),
                          const SizedBox(width: 16),
                          Expanded(
                            flex: 3,
                            child: ShadInput(initialValue: p.value),
                          ),
                        ],
                      ),
                    )
                    .toList(),
              ),
            ),
          ),
        );
      },
    );
  }
}
```

#### Alert Dialog

```dart
class DialogExample extends StatelessWidget {
  const DialogExample({super.key});

  @override
  Widget build(BuildContext context) {
    return ShadButton.outline(
      child: const Text('Show Dialog'),
      onPressed: () {
        showShadDialog(
          context: context,
          builder: (context) => ShadDialog.alert(
            title: const Text('Are you absolutely sure?'),
            description: const Padding(
              padding: EdgeInsets.only(bottom: 8),
              child: Text(
                'This action cannot be undone. This will permanently delete your account and remove your data from our servers.',
              ),
            ),
            actions: [
              ShadButton.outline(
                child: const Text('Cancel'),
                onPressed: () => Navigator.of(context).pop(false),
              ),
              ShadButton(
                child: const Text('Continue'),
                onPressed: () => Navigator.of(context).pop(true),
              ),
            ],
          ),
        );
      },
    );
  }
}
```

### Input

Displays a form input field or a component that looks like an input field.

#### Basic Input

```dart
ConstrainedBox(
  constraints: const BoxConstraints(maxWidth: 320),
  child: const ShadInput(
    placeholder: Text('Email'),
    keyboardType: TextInputType.emailAddress,
  ),
),
```

#### With Leading and Trailing

```dart
class PasswordInput extends StatefulWidget {
  const PasswordInput({super.key});

  @override
  State<PasswordInput> createState() => _PasswordInputState();
}

class _PasswordInputState extends State<PasswordInput> {
  bool obscure = true;

  @override
  Widget build(BuildContext context) {
    return ShadInput(
      placeholder: const Text('Password'),
      obscureText: obscure,
      leading: const Padding(
        padding: EdgeInsets.all(4.0),
        child: Icon(LucideIcons.lock),
      ),
      trailing: ShadButton(
        width: 24,
        height: 24,
        padding: EdgeInsets.zero,
        decoration: const ShadDecoration(
          secondaryBorder: ShadBorder.none,
          secondaryFocusedBorder: ShadBorder.none,
        ),
        icon: Icon(obscure ? LucideIcons.eyeOff : LucideIcons.eye),
        onPressed: () {
          setState(() => obscure = !obscure);
        },
      ),
    );
  }
}
```

#### Form Input

```dart
ShadInputFormField(
  id: 'username',
  label: const Text('Username'),
  placeholder: const Text('Enter your username'),
  description: const Text('This is your public display name.'),
  validator: (v) {
    if (v.length < 2) {
      return 'Username must be at least 2 characters.';
    }
    return null;
  },
),
```

### Select

Displays a list of options for the user to pick from—triggered by a button.

#### Basic Select

```dart
final fruits = {
  'apple': 'Apple',
  'banana': 'Banana',
  'blueberry': 'Blueberry',
  'grapes': 'Grapes',
  'pineapple': 'Pineapple',
};

class SelectExample extends StatelessWidget {
  const SelectExample({super.key});

  @override
  Widget build(BuildContext context) {
    final theme = ShadTheme.of(context);
    return ConstrainedBox(
      constraints: const BoxConstraints(minWidth: 180),
      child: ShadSelect<String>(
        placeholder: const Text('Select a fruit'),
        options: [
          Padding(
            padding: const EdgeInsets.fromLTRB(32, 6, 6, 6),
            child: Text(
              'Fruits',
              style: theme.textTheme.muted.copyWith(
                fontWeight: FontWeight.w600,
                color: theme.colorScheme.popoverForeground,
              ),
              textAlign: TextAlign.start,
            ),
          ),
          ...fruits.entries
              .map((e) => ShadOption(value: e.key, child: Text(e.value))),
        ],
        selectedOptionBuilder: (context, value) => Text(fruits[value]!),
        onChanged: print,
      ),
    );
  }
}
```

#### Multiple Select

```dart
final fruits = {
  'apple': 'Apple',
  'banana': 'Banana',
  'blueberry': 'Blueberry',
  'grapes': 'Grapes',
  'pineapple': 'Pineapple',
};

class SelectMultiple extends StatelessWidget {
  const SelectMultiple({super.key});

  @override
  Widget build(BuildContext context) {
    final theme = ShadTheme.of(context);
    return ShadSelect<String>.multiple(
      minWidth: 340,
      onChanged: print,
      allowDeselection: true,
      closeOnSelect: false,
      placeholder: const Text('Select multiple fruits'),
      options: [
        Padding(
          padding: const EdgeInsets.fromLTRB(32, 6, 6, 6),
          child: Text(
            'Fruits',
            style: theme.textTheme.large,
            textAlign: TextAlign.start,
          ),
        ),
        ...fruits.entries.map(
          (e) => ShadOption(
            value: e.key,
            child: Text(e.value),
          ),
        ),
      ],
      selectedOptionsBuilder: (context, values) =>
          Text(values.map((v) => v.capitalize()).join(', ')),
    );
  }
}
```

### Switch

A control that allows the user to toggle between checked and not checked.

#### Basic Switch

```dart
class SwitchExample extends StatefulWidget {
  const SwitchExample({super.key});

  @override
  State<SwitchExample> createState() => _SwitchExampleState();
}

class _SwitchExampleState extends State<SwitchExample> {
  bool value = false;

  @override
  Widget build(BuildContext context) {
    return ShadSwitch(
      value: value,
      onChanged: (v) => setState(() => value = v),
      label: const Text('Airplane Mode'),
    );
  }
}
```

#### Form Switch

```dart
ShadSwitchFormField(
  id: 'terms',
  initialValue: false,
  inputLabel: const Text('I accept the terms and conditions'),
  onChanged: (v) {},
  inputSublabel: const Text('You agree to our Terms and Conditions'),
  validator: (v) {
    if (!v) {
      return 'You must accept the terms and conditions';
    }
    return null;
  },
)
```

### Tabs

A set of layered sections of content—known as tab panels—that are displayed one at a time.

```dart
class TabsExample extends StatelessWidget {
  const TabsExample({super.key});

  @override
  Widget build(BuildContext context) {
    return ShadTabs<String>(
      value: 'account',
      tabBarConstraints: const BoxConstraints(maxWidth: 400),
      contentConstraints: const BoxConstraints(maxWidth: 400),
      tabs: [
        ShadTab(
          value: 'account',
          content: ShadCard(
            title: const Text('Account'),
            description: const Text(
                "Make changes to your account here. Click save when you're done."),
            footer: const ShadButton(child: Text('Save changes')),
            child: Column(
              mainAxisSize: MainAxisSize.min,
              children: [
                const SizedBox(height: 16),
                ShadInputFormField(
                  label: const Text('Name'),
                  initialValue: 'Ale',
                ),
                const SizedBox(height: 8),
                ShadInputFormField(
                  label: const Text('Username'),
                  initialValue: 'nank1ro',
                ),
                const SizedBox(height: 16),
              ],
            ),
          ),
          child: const Text('Account'),
        ),
        ShadTab(
          value: 'password',
          content: ShadCard(
            title: const Text('Password'),
            description: const Text(
                "Change your password here. After saving, you'll be logged out."),
            footer: const ShadButton(child: Text('Save password')),
            child: Column(
              children: [
                const SizedBox(height: 16),
                ShadInputFormField(
                  label: const Text('Current password'),
                  obscureText: true,
                ),
                const SizedBox(height: 8),
                ShadInputFormField(
                  label: const Text('New password'),
                  obscureText: true,
                ),
                const SizedBox(height: 16),
              ],
            ),
          ),
          child: const Text('Password'),
        ),
      ],
    );
  }
}
```
