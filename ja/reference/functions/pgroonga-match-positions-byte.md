---
title: pgroonga_match_positions_byte関数
upper_level: ../
---

# `pgroonga_match_positions_byte`関数

1.0.7で追加。

## 概要

`pgroonga_match_positions_byte`関数は指定したテキスト中にある指定したキーワードの位置を返します。単位はバイトです。HTML出力用にキーワードをハイライトしたいなら[`pgroonga_snippet_html`関数](pgroonga-snippet-html.html)または[`pgroonga_highlight_html`関数](pgroonga-highlight-html.html)の方が適しているでしょう。`pgroonga_match_positions_byte`関数は高度な用途向けです。

文字単位バージョンが欲しい場合は代わりに[`pgroonga_match_positions_character`](pgroonga-match-positions-character.html)を参照してください。

## 構文

この関数の構文は次の通りです。

```text
integer[2][] pgroonga_match_positions_byte(target, ARRAY[keyword1, keyword2, ...])
```

`target`はキーワード検索対象のテキストです。型は`text`です。

`keyword1`、`keyword2`、`...`は見つけたいキーワードです。型は`text`の配列です。1つ以上のキーワードを指定しなければいけません。

`pgroonga_match_positions_byte`は位置の配列を返します。

位置は「オフセット」と「長さ」で表現します。「オフセット」は先頭からキーワードが現れた位置までのバイト数です。「長さ」はマッチしたテキストのバイト数です。「長さ」はキーワードの長さと違うかもしれません。これはキーワードもマッチしたテキストも正規化されるからです。

## 使い方

少なくとも1つキーワードを指定しなければいけません。

{% raw %}
```sql
SELECT pgroonga_match_positions_byte('PGroonga is a PostgreSQL extension.',
                                     ARRAY['PostgreSQL']) AS match_positions_byte;
--  match_positions_byte 
-- ----------------------
--  {{14,10}}
-- (1 row)
```
{% endraw %}

複数のキーワードを指定できます。

{% raw %}
```sql
SELECT pgroonga_match_positions_byte('PGroonga is a PostgreSQL extension.',
                                     ARRAY['Groonga', 'PostgreSQL']) AS match_positions_byte;
--  match_positions_byte 
-- ----------------------
--  {{1,7},{14,10}}
-- (1 row)
```
{% endraw %}

[`pgroonga_query_extract_keywords`関数](pgroonga-query-extract-keywords.html)を使うとクエリーからキーワードを抽出できます。

{% raw %}
```sql
SELECT pgroonga_match_positions_byte('PGroonga is a PostgreSQL extension.',
                                     pgroonga_query_extract_keywords('Groonga PostgreSQL -extension')) AS match_positions_byte;
--  match_positions_byte 
-- ----------------------
--  {{1,7},{14,10}}
-- (1 row)
```
{% endraw %}

文字は正規化されます。

{% raw %}
```sql
SELECT pgroonga_match_positions_byte('PGroonga + pglogical = replicatable!',
                                     ARRAY['Pg']) AS match_positions_byte;
--  match_positions_byte 
-- ----------------------
--  {{0,2},{11,2}}
-- (1 row)
```
{% endraw %}

マルチバイト文字にも対応しています。

{% raw %}
```sql
SELECT pgroonga_match_positions_byte('10㌖先にある100ｷﾛグラムの米',
                                     ARRAY['キロ']) AS match_positions_byte;
--  match_positions_byte 
-- ----------------------
--  {{2,3},{20,6}}
-- (1 row)
```
{% endraw %}

## 参考

  * [`pgroonga_match_positions_character`関数][match-positions-character]

  * [`pgroonga_snippet_html`関数](pgroonga-query-snippet-html.html)

  * [`pgroonga_highlight_html`関数](pgroonga-query-highlight-html.html)

  * [`pgroonga_query_extract_keywords`関数][query-extract-keywords]

[match-positions-character]:pgroonga-match-positions-character.html
[query-snippet-html]:pgroonga-query-snippet-html.html
[query-highlight-html]:pgroonga-query-highlight-html.html
[query-extract-keywords]:pgroonga-query-extract-keywords.html

