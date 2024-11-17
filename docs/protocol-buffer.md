# Protocol Buffers とは

- Google によって 2008 年にオープンソース化されたスキーマ言語
- スキーマ言語は要素や属性などの構造を定義するための言語

## 特徴

- gRPC のデータフォーマットとして採用されている
- プログラミングから独立していてさまざまな言語(Java, GO, Python など)に変換可能
- バイナリ形式にシリアライズされているのでサイズが小さく高速な通信が可能
- 型安全
- JSON に変換できる

## 開発の進め方

1. データスキーマを定義する
2. スキーマから開発言語のオブジェクトを自動生成
3. バイナリ形式へシリアライズ

## Proto ファイル

- 拡張子は.proto

```proto
// 指定しないと自動でproto2が定義される
syntax="proto3";
```

## message

- 複数のフィールドを持つことができる型定義
- それぞれのフィールドはスカラ型もしくはコンポジット型
- 1 つの proto ファイルに複数の message 型を定義することも可能

```proto
message Person {
    string name = 1;
    int32 id = 2;
    string email = 3;
}
```

## スカラー型

- message のフォーマットの一つ
- int32、string などがある
- https://protobuf.dev/programming-guides/proto3/#scalar

## タグ

- フィールドはフィールド名ではなく、タグ番号によって識別される
- 重複は許されず、一意である必要がある
- タグの最小値は 1、最大値は 2 の 29 乗-1
- 19000 から 19999 は Protocol Buffers の予約番号のため使用不可
- 1 から 15 番までは 1byte で表すことができるため、よく使うフィールドには 1 から 15 番を割り当てる
- タグは連番にする必要がないのであまり使わないフィールドはあえて 16 番以降を割り当てることが可能

## 列挙型

```proto
syntax="proto3";

message Person {
    string name = 1;
    int32 id = 2;
    string email = 3;
    Occupation occupation = 4;
}

// 列挙型
// enumのタグ番号は0からはじまる必要がある
enum Occupation {
  OCCUPATION_UNKNOWN = 0;
  ENGINEER = 1;
  DESIGNER = 2;
  MANAGER = 3;
}
```
