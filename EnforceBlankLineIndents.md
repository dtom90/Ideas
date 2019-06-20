**What rule do you want to change?**
[`indent` (enforce consistent indentation)](https://eslint.org/docs/rules/indent#enforce-consistent-indentation-indent)

**Does this change cause the rule to produce more or fewer warnings?**
If enabled, more warnings. If left as default, equal warnings

**How will the change be implemented? (New option, new default behavior, etc.)?**
New option

**Please provide some example code that this change will affect:**

Often when coding, blank (padding) lines within blocks may have inconsistent indentation:
```js
if (a) {
••••••••
••••b=c;

••••function foo(d) {
••••
••••••••e=f;
••••••••••••
••••}
••••
}
```

**What does the rule currently do for this code?**

By default, eslint will strip away these blank line indentations due to the [`no-trailing-spaces`](https://eslint.org/docs/rules/no-trailing-spaces) rule:
```js
if (a) {

••••b=c;

••••function foo(d) {

••••••••e=f;

••••}

}
```

**What will the rule do after it's changed?**

Style preference may be to keep indents consistent within blocks, even on blank (padding) lines:
```js
if (a) {
••••
••••b=c;
••••
••••function foo(d) {
••••••••
••••••••e=f;
••••••••
••••}
••••
}
```
Currently, we can tell eslint to ignore these blank line indents through the [`no-trailing-spaces: skipBlankLines`](https://eslint.org/docs/rules/no-trailing-spaces#skipblanklines) option. However, this will often lead to the same problem as in the first example, as now there is no indentation enforcement on blank lines.

The proposal is to add an option `enforceBlankLines` to `indent` which will enforce indentation within blocks, even on blank lines:

`"enforceBlankLines"` (default: `false`) can be set to `true` to enforce indentation on blank lines

**Are you willing to submit a pull request to implement this change?**
Yes