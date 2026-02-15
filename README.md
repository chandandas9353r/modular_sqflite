# modular_sqflite

![Dart](https://img.shields.io/badge/Dart-3.10.7-blue)
![Platform](https://img.shields.io/badge/Platform-Android%20%7C%20iOS-green)

A modular and structured abstraction layer built on top of `sqflite` to simplify table creation, enforce clean architecture patterns, and provide reusable database utilities for Flutter applications.

---

## 🚀 Why modular_sqflite?

When building multiple Flutter applications, local database handling often involves:

- Rewriting table creation logic
- Repeating SQL type definitions
- Duplicating CRUD methods
- Mixing raw SQL inside UI or business logic
- Poor separation of concerns

`modular_sqflite` solves this by providing:

- Structured table field definitions
- Clean table creation utilities
- Reusable base DAO architecture
- Centralized database service handling
- Fully customizable SQL control
- Lightweight abstraction

---

## 🧠 Philosophy

This package does **not** replace `sqflite`.

Instead, it:

- Preserves raw SQL flexibility
- Reduces repetitive boilerplate
- Encourages clean architecture
- Enforces separation of data layer
- Keeps business logic independent

It is intentionally lightweight and modular.

---

## 📦 Features

- Enum-based SQL type definitions
- Structured table field builder
- Dynamic `CREATE TABLE` generation
- Base DAO class for reusable CRUD logic
- Centralized database initialization
- Version and migration handling
- Clean separation between database and UI

---

## 🏗 Architecture Overview

```
lib/
├── modular_sqflite.dart
└── src/
    ├── database_service.dart
    ├── table_field.dart
    ├── sql_type.dart
    ├── base_dao.dart
    └── query_helper.dart
```

---

## 🔹 Example Usage

### Define SQL Types

```dart
enum SqlType {
  integer("INTEGER"),
  real("REAL"),
  text("TEXT"),
  blob("BLOB");

  final String value;
  const SqlType(this.value);
}
```
### Define Table Fields

```dart
TableField(
  name: "id",
  type: SqlType.text,
  isPrimaryKey: true,
  isNotNull: true,
);
```
### Create Table

```dart
await databaseService.createTable(
  tableName: "messages",
  fields: [
    TableField(name: "id", type: SqlType.text, isPrimaryKey: true),
    TableField(name: "chatId", type: SqlType.text),
    TableField(name: "content", type: SqlType.text),
    TableField(name: "createdAt", type: SqlType.integer),
  ],
);
```
### Extend Base DAO

```dart
class MessageDao extends BaseDao<MessageModel> {
  @override
  String get tableName => "messages";

  @override
  Map<String, dynamic> toMap(MessageModel model) {
    return {
      "id": model.id,
      "chatId": model.chatId,
      "content": model.content,
      "createdAt": model.createdAt,
    };
  }

  @override
  MessageModel fromMap(Map<String, dynamic> map) {
    return MessageModel.fromJson(map);
  }
}
```
### Extend Base DAO

```dart
class MessageDao extends BaseDao<MessageModel> {
  @override
  String get tableName => "messages";

  @override
  Map<String, dynamic> toMap(MessageModel model) {
    return {
      "id": model.id,
      "chatId": model.chatId,
      "content": model.content,
      "createdAt": model.createdAt,
    };
  }

  @override
  MessageModel fromMap(Map<String, dynamic> map) {
    return MessageModel.fromJson(map);
  }
}
```

---

## 🎯 Intended Use Cases

- Offline-first applications
- Chat applications
- Enterprise apps with local caching
- Modular Flutter architecture
- Feature-based project structure

---

## 🛠 Dependencies

- sqflite
- path_provider

No heavy ORM or external abstraction libraries.

---

## 🏁 Goals

- Promote clean architecture
- Encourage modular data layer design
- Reduce repeated database boilerplate
- Maintain full SQL flexibility
- Keep performance optimized

---

## 🔮 Future Improvements

- Migration helpers
- Batch operation utilities
- Conflict resolution helpers
- Query builder enhancements

---

## 👨‍💻 Author

Chandan Das  
Flutter & Cross-Platform Mobile Developer

---
