**How to Search an asset :**

The "quick search" of Razuna searches within the following fields; **filename, keywords, description, file contents (e.g. all words in a PDF or word document), ID, labels and custom fields (user created)**. If you want to search in other fields, then use the advanced search or create your own field search that you can use in quick search.
___
**Case - Sensitive**
The search is not case sensitive.
___
**Terms**

There are two types of terms: Single Terms and Phrases.

A Single Term is a single word such as test or hello.

A Phrase is a group of words surrounded by double quotes such as "hello dolly".

Searching for hello dolly without quotes will search for terms matching hello AND terms matching dolly in the index i.e. hello my name is dolly would be a match but hello my name is amanda or my name is dolly would not be a match. To force them to be searched together as a phrase double quotes are required. By default Razuna uses an AND operator between keywords. So searching for hello dolly is equivalent to searching for hello AND dolly. You can override this be adding your own operator e.g. hello OR dolly which will search for terms matching either hello OR dolly i.e. hello my name is amanda or . Note that the operator must be capital case.
___
**Field Search**

Razuna supports fielded data search. When performing a search you can either specify a field, or Razuna searches in the default fields (see above).

You can search any field by typing the field name followed by a colon ":" and then the term you are looking for.

Here are some fields that the Razuna index contains that you can search within:

* id : Unique id of asset
* filename : The current filename of the asset
* filenameorg : The original filename the asset was uploaded with
* keywords : Keywords associated with asset
* description : Description associated with asset
* rawmetadata : The metadata for the asset
* extension : Filename extension of asset
* labels : Labels associated with asset
* customfieldvalue : Values in user created custom fields

If you want to find assets that have "razuna" in the "filename", you can enter:
```
filename:(razuna)
```
If you want to to search in many fields you can either use AND or OR to combine the fields, like:
```
keywords:(hello AND dolly)
```
___

**Wild Card Search**

Razuna supports single and multiple character wildcard searches within single terms (not within phrase queries).

To perform a single character wildcard search use the "?" symbol.

To perform a multiple character wildcard search use the "*" symbol.

The single character wildcard search looks for terms that match that with the single character replaced. For example, to search for "text" or "test" you can use the search:

```
te?t
```
Multiple character wildcard searches looks for 0 or more characters. For example, to search for test, tests or tester, you can use the search:
```
test*
```
___

**Fuzzy Searches**

Razuna supports fuzzy searches based on the Levenshtein Distance, or Edit Distance algorithm. To do a fuzzy search use the tilde, "~", symbol at the end of a Single word Term. For example to search for a term similar in spelling to "roam" use the fuzzy search:
```
roam~
```
This search will find terms like foam and roams.

A optional parameter can specify the required similarity. The value is between 0 and 1, with a value closer to 1 only terms with a higher similarity will be matched. For example:

```
roam~0.8
```

The default that is used if the parameter is not given is 0.5.
___

**Boosting a Term**

Razuna provides the relevance level of matching documents based on the terms found. To boost a term use the caret, "^", symbol with a boost factor (a number) at the end of the term you are searching. The higher the boost factor, the more relevant the term will be.

Boosting allows you to control the relevance of a document by boosting its term. For example, if you are searching for "dam razuna" and you want the term "dam" to be more relevant boost it using the ^ symbol along with the boost factor next to the term. You would type:

```
dam^4 razuna
```

This will make documents with the term "dam" appear more relevant. You can also boost Phrase Terms as in the example:

```
"dam razuna"^4 "dam Razuna"
```

By default, the boost factor is 1. Although the boost factor must be positive, it can be less than 1 (e.g. 0.2)
___

**Boolean Operators**

Boolean operators allow terms to be combined through logic operators. Razuna supports AND, "+", OR, NOT and "-" as Boolean operators(Note: Boolean operators must be ALL CAPS).

The OR operator is the default conjunction operator. This means that if there is no Boolean operator between two terms, the OR operator is used. The OR operator links two terms and finds a matching document if either of the terms exist in a document. This is equivalent to a union using sets. The symbol || can be used in place of the word OR.

To search for documents that contain either "dam razuna" or just "dam" use the query:

```
"dam razuna" dam
```

or

```
"dam razuna" OR dam
```
___

**AND**

The AND operator matches documents where both terms exist anywhere in the text of a single document. This is equivalent to an intersection using sets. The symbol && can be used in place of the word AND.

To search for documents that contain "dam razuna" and "DAM" use the query:

```
"dam razuna" AND "DAM"
```
___

**+**

The "" or required operator requires that the term after the "" symbol exist somewhere in a the field of a single document.

To search for documents that must contain "dam" and may contain "razuna" use the query:

```
+dam razuna
```
___

**NOT**

The NOT operator excludes documents that contain the term after NOT. This is equivalent to a difference using sets. The symbol ! can be used in place of the word NOT.

To search for documents that contain "dam razuna" but not "DAM" use the query:

```
"dam razuna" NOT "DAM"
```

Note: The NOT operator cannot be used with just one term. For example, the following search will return no results:

```
NOT "dam razuna"
```
___
**Grouping**

Razuna supports using parentheses to group clauses to form sub queries. This can be very useful if you want to control the boolean logic for a query.

To search for either "dam" or "razuna" and "DAM" use the query:

```
(dam OR razuna) AND DAM
```

This eliminates any confusion and makes sure you that website must exist and either term dam or razuna may exist.
___

**Escaping Special Characters**

Razuna supports escaping special characters that are part of the query syntax. The current list special characters are

```
+ - && || ! ( ) { } [ ] ^ " ~ * ? : \
```

To escape these character use the \ before the character. For example to search for (1+1):2 use the query:

```
\(1\+1\)\:2
```
___