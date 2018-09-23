---
title: A comment about code comments
description: Code comments are one of those things that usually divide programmers. In this post I will comment about this and talk a little about my experiences.
updated: 2016-08-08 23:37
---

<small>
  ![People eating a meal around a table](/assets/2018-09-23-a-comment-about-code-comments/1.jpg "People eating a meal around a table")
  *Photo by [Priscilla Du Preez](https://unsplash.com/@priscilladupreez) on [Unsplash](https://unsplash.com/photos/W3SEyZODn8U?utm_source=unsplash&utm_medium=referral&utm_content=creditCopyText)*
</small>

Code comments were something very confusing for me for a long time. During college, all teachers of all disciplines who approached software programming always said that all of their code should be commented on. The justifications were always about when you, or someone else, needed to go back on that stretch, the comment would help the programmer better understand what the code is doing. I agree with the college, in parts, but I must say that I ended up always making this kind of comment:

```ruby
  # Public: Return the sum of two numbers.
  #
  # number1 - First number to sum.
  # number2 - Second number to sum.
  #
  # Examples
  #
  #   sum(2, 5)
  #   # => 7
  #
  # Returns the duplicated String.
  def sum(number1, number2)
    number1 + number2
  end
```

When I finished college, when I started using languages with more modern proposals, I came across people, books and posts that said that my code needed to be clean, self-explanatory, and any kind of comment should be avoided in favor of a code that was more clean and more self explanatory. A very good memory I have of this is from my good friend [Arthur](https://github.com/arthurfsilva) commenting on a paragraph from [Clean Code](https://www.amazon.com.br/Clean-Code-Handbook-Software-Craftsmanship/dp/0132350882) written by Robert C. Martin, better known as Uncle Bob](https://blog.cleancoder.com/):

> `So when you find yourself in a position where you need to write a comment, think it through and see whether there isn’t some way to turn the tables and express yourself in code. Every time you express yourself in code, you should pat yourself on the back. Every time you write a comment, you should grimace and feel the failure of your ability of expression. `

Robert C. Martin. Clean Code. Page 54, line 7.

## Ok, let's try in the real world now

One day, I find myself writing a function where I wished from the first character that there was a comment so that I would save time when I needed to go back to it.

Instead of explaining what's happening, I'll leave the code with your comment and suggest an exercise: Imagine that there is no comment documenting the code and try to understand what the function does. I think the task will be a bit complicated.

```ruby
# In some worksheet rows, is returned formula errors that are inside
# an extra cell object, at the end of map process, an array is returned
# with an extra element.
#
# As we are treating that values by this position, this extra element
# in the array beginning causes validations errors when the line is
# persisted on the database.
#
# Examples
#
#  clean_formula_errors_from(['item 1', 'item 2', 'item 3'])
#  # => ['item 1', 'item 2', 'item 3']
#
#  clean_formula_errors_from(['#SomeKindOfError!', 'item 1', 'item 2', 'item 3'])
#  # => ['item 1', 'item 2', 'item 3']
#
# Returns an array without error items
def clean_formula_errors_from(row)
  row.map(&:value)
    .reject { |value| value.to_s.match?(/^\#\w*!$/) }
end
```

Much simpler to understand with the comment, right?

Valuable comments for your application are those that, in addition to explaining what your code does, explains why your code is doing that. This does not invalidate the fact that you should always keep your code as clean and self-explanatory as possible, but as we saw in the example, it is not always possible to make a fully self explanatory-code. It is often necessary to understand the context for this clean, self-explanatory piece of code to make sense.

## Quick tips

When you need to do, leave your comments with the language as simple as possible. Do not skimp when writing, but keep this in your mind: If your comment is too large, consider refactoring your code. Always asks for a opinion of a co-worker or some senior developer, either in person or at the time of Code Review.

To write these comments of the text I used the rules of [TomDoc](http://tomdoc.org/). It's worth reading no matter what your level of software development experience. Although TomDoc is focused on Ruby, there are standards for other languages like [JSDoc](http://usejsdoc.org/) for Javascript or [PEP 257 definitions](https://www.python.org/dev/peps/pep-0257/) for Python.

## One (very) short comment about documentation outside of code

About out-of-code documentation for procedures and/or specificities that are not fully tied to the code: Yes, it's worth it because you share knowledge about a certain part of your system with other programmers and make it much easier for new programmers to better understand the code base.

I was brief here because I believe someone might be left with doubts about comments outside the code. And also why I intend to write more about this in other post.


Thanks! 😄
