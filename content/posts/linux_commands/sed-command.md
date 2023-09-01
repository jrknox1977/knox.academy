---
title: "The sed Command"
date: 2023-08-27T15:20:35-04:00
draft: false
---
# Sed Command

Sed, which stands for Stream Editor, is a powerful Unix tool used to parse and transform text. It's primarily used for text substitution, and it can also perform more complex tasks like inserting, deleting, or replacing lines of text.

## Use Cases for Sed

1. **Text Substitution:** The most common use of sed is to substitute a string of text with another string.
2. **Text Deletion:** Sed can be used to delete lines of text that match a particular pattern.
3. **Text Insertion:** Sed is capable of inserting new lines of text before or after a line that matches a certain pattern.
4. **Text Appending:** You can append a line of text after a line that matches a certain pattern.
5. **Text Selection:** Sed can select lines of text that match a certain pattern.

## Simple Examples

The simplest form of a sed command looks like this:

```bash
sed 's/old/new/' file
```

This command replaces the first occurrence of the string "old" with "new" on each line of the file.

If you want to replace all the occurrences and not just the first one, you can add the "g" option:

```bash
sed 's/old/new/g' file
```

To directly modify the file instead of just outputting the modified text, use the "-i" option:

```bash
sed -i 's/old/new/g' file
```

## Intermediate Examples

Sed can also delete lines of text. The "d" command in sed is used for this purpose. For example:

```bash
sed '/pattern/d' file
```

This command deletes all lines containing "pattern".

You can also print only the lines that match a certain pattern using the "-n" and "p" options:

```bash
sed -n '/pattern/p' file
```

This command prints only the lines containing "pattern".

## Advanced Examples

Sed can execute multiple commands at once. Here's an example:

```bash
sed -e 's/old/new/g' -e '/pattern/d' file
```

This command replaces "old" with "new" and deletes all lines containing "pattern".

You can also use sed to insert text before or after a line:

```bash
sed '/pattern/i\Text before' file
sed '/pattern/a\Text after' file
```

The first command inserts "Text before" before every line containing "pattern". The second command appends "Text after" after every line containing "pattern".

## Conclusion

As you can see, sed is a powerful tool for manipulating text. While its syntax may seem cryptic at first, with practice it becomes an invaluable tool. From simple substitutions to complex transformations, sed can handle a wide variety of tasks. The key to mastering sed is to understand its syntax and commands, and to practice by using it in real-world applications.