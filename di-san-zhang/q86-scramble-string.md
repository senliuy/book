# 87. Scramble String

Given a strings1, we may represent it as a binary tree by partitioning it to two non-empty substrings recursively.

Below is one possible representation ofs1=`"great"`:

```
    great
   /    \
  gr    eat
 / \    /  \
g   r  e   at
           / \
          a   t

```

To scramble the string, we may choose any non-leaf node and swap its two children.

For example, if we choose the node`"gr"`and swap its two children, it produces a scrambled string`"rgeat"`.

```
    rgeat
   /    \
  rg    eat
 / \    /  \
r   g  e   at
           / \
          a   t

```

We say that`"rgeat"`is a scrambled string of`"great"`.

Similarly, if we continue to swap the children of nodes`"eat"`and`"at"`, it produces a scrambled string`"rgtae"`.

```
    rgtae
   /    \
  rg    tae
 / \    /  \
r   g  ta  e
       / \
      t   a

```

We say that`"rgtae"`is a scrambled string of`"great"`.

Given two stringss1ands2of the same length, determine ifs2is a scrambled string ofs1.

