# Unicode flag (u)

The unicode (`u`) flag is mandatory when working with Unicode strings, in particular when you might need to handle characters in astral planes, the ones that are not included in the first 1600 Unicode characters.

Like Emojis, for example, but not just those.

If you donβt add that flag, this simple regex that should match one character will not work, because for JavaScript that emoji is represented internally by 2 characters (see [Unicode in JavaScript](https://flaviocopes.com/javascript-unicode/)):

```js
/^.$/.test('a')   // β
/^.$/.test('πΆ')  // β
/^.$/u.test('πΆ') // β
```

So, always use the `u` flag.

Keep in mind that Unicode, just normal characters, handle ranges:

```js
/[a-z]/.test('a') // β
/[1-9]/.test('1') // β

/[πΆ-π¦]/u.test('πΊ') // β
/[πΆ-π¦]/u.test('π') // β
```

JavaScript checks the internal code representation, so `πΆ < πΊ < π¦` because `\u1F436 < \u1F43A < \u1F98A`. Check [emoji-regex](https://github.com/mathiasbynens/emoji-regex) for exploring more about that.