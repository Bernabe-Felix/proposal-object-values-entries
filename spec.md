# Object.keys( O )

When the **keys** function is called with argument *O*, the following steps are taken:
  1. Let *obj* be [?][return-if-abrupt] [ToObject][to-object](*O*).
  1. Let *nameList* be [?][return-if-abrupt] [EnumerableOwnProperties][enumerable-own-properties](*obj*, **"key"**).
  1. Return [CreateArrayFromList][create-array-from-list](*nameList*).

If an implementation defines a specific order of enumeration for the for-in statement, the same order must be used for the elements of the array returned in step 5.

# Object.values( O )

When the *values* function is called with argument *O*, the following steps are taken:
  1. Let *obj* be [?][return-if-abrupt] [ToObject][to-object](*O*).
  1. Let *nameList* be [?][return-if-abrupt] [EnumerableOwnProperties][enumerable-own-properties](*obj*, **"value"**).
  1. Return [CreateArrayFromList][create-array-from-list](*nameList*).

If an implementation defines a specific order of enumeration for the for-in statement, the same order must be used for the elements of the array returned in step 5.

# Object.entries( O )

When the **entries** function is called with argument *O*, the following steps are taken:
  1. Let *obj* be [?][return-if-abrupt] [ToObject][to-object](*O*).
  1. Let *nameList* be [?][return-if-abrupt] [EnumerableOwnProperties][enumerable-own-properties](*obj*, **"key+value"**).
  1. Return [CreateArrayFromList][create-array-from-list](*nameList*).

If an implementation defines a specific order of enumeration for the for-in statement, the same order must be used for the elements of the array returned in step 5.

## EnumerableOwnProperties Abstract Operation

When the abstract operation EnumerableOwnProperties is called with Object *O* and String *kind* the following steps are taken:
  1. Assert: [Type][type](*O*) is Object.
  1. Let *ownKeys* be [?][return-if-abrupt] O.[[OwnPropertyKeys]]().
  1. Let *properties* be a new empty [List][list].
  1. Repeat, for each element *key* of *ownKeys* in [List][list] order
    1. If [Type][type](*key*) is String, then
      1. Let *desc* be [?][return-if-abrupt] O.[[GetOwnProperty]](*key*).
      1. If *desc* is not **undefined** and *desc*.[[Enumerable]] is **true**, then
        1. If *kind* is **"key"**, append *key* to *properties*.
        1. Else,
          1. Let *value* be [?][return-if-abrupt] [Get][get](*O*, *key*).
          1. If *kind* is **"value"**, append *value* to *properties*.
          1. Else,
            1. Assert: *kind* is **"key+value"**.
            1. Let *entry* be [CreateArrayFromList][create-array-from-list](&laquo; *key*, *value* &raquo;).
            1. Append *entry* to *properties*.
  1. Order the elements of *properties* so they are in the same relative order as would be produced by the Iterator that would be returned if the [[Enumerate]] internal method was invoked on *O*.
  1. Return *properties*.

The order of elements in the returned list is the same as the enumeration order that is used by a for-in statement.

Note: The "[EnumerableOwnNames][enumerable-own-names]" section is deleted. Any existing references to [EnumerableOwnNames][enumerable-own-names](*x*) should be changed to [EnumerableOwnProperties][enumerable-own-properties](*x*, **"key"**)

[return-if-abrupt]: http://www.ecma-international.org/ecma-262/6.0/index.html#sec-returnifabrupt
[to-object]: http://www.ecma-international.org/ecma-262/6.0/index.html#sec-toobject
[to-string]: http://www.ecma-international.org/ecma-262/6.0/index.html#sec-tostring
[list]: http://www.ecma-international.org/ecma-262/6.0/#sec-list-and-record-specification-type
[get]: http://www.ecma-international.org/ecma-262/6.0/index.html#sec-get-o-p
[type]: http://www.ecma-international.org/ecma-262/6.0/#sec-ecmascript-data-types-and-values
[enumerable-own-names]: http://www.ecma-international.org/ecma-262/6.0/#sec-enumerableownnames
[enumerable-own-properties]: #enumerableownproperties
[create-array-from-list]: http://www.ecma-international.org/ecma-262/6.0/index.html#sec-createarrayfromlist
