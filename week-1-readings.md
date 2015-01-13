#WEEK ONE READINGS

# Writing Readable Code
Written by [Torey Hickman](https://github.com/toreyhickman).


## Introduction
When you write code, you have two audiences:  the computer and people.

The computer will parse and execute your code, and so your code needs to follow certain guidelines.  For example, when you define a method, you begin with `def` and close with `end`.  If you don't follow that pattern, the computer won't be able to execute the code.  If you try to run code with improper syntax, you get an error:

```
example.rb:4: syntax error, unexpected end-of-input, expecting keyword_end
```

As long as the syntax is correct, your code will run.  The computer doesn't care what you name variables or methods, how many methods you chain together, or anything else.

However, people do care.  The "Ruby way" is to write code that is easily understandable for programmers who might encounter your code:  your pair, a teammate, a programmer who picks up your code base in the future, even your future self.

## Readable Code Best Practices

### Style
There is a [Ruby Style Guide](https://github.com/styleguide/ruby) on GitHub that describes how your code should be written.  It includes guidelines on indentation and white space, delimiting blocks with `{...}` or `do ... end`, naming, etc.  Familiarize yourself with these guidelies and apply them to your code.

Pay particular attention to indentation.  Indentation will make your code much easier to read:  what lines belong to which methods, when does an `if` statement end, which lines are with a block, etc.  If code is not indented properly, it's much more difficult for a human to parse (i.e., read).

### Variable and Method Naming
Names should be descriptive.  A variable name should inform readers of the value assigned to the variable.  Methods should be named the same way:  inform readers what the method does ... or at least what it returns.

Variables with names like `x` might make sense in the moment you're writing code, but a few days later, you might have to ask yourself, "Now, what was 'x'?"  And, someone unfamiliar with your code would have no clue.  In addition, variable names like `string` or `array` pass on information about the type of object assigned to the variable, but not what the object represents.

```ruby
# poor naming choices
require 'prime'

def p_factors(x)
  return [x] if x.prime?

  pf = p_factor(x)
  n = x / pf

  [pf] + p_factors(n)
end

def p_factor(x)
  pos_factors(x).find { |p| p.prime? && number % p == 0 }
end

def pos_factors(x)
  (2..(x / 2))
end


# better naming choices
require 'prime'

def prime_factors(number)
  return [number] if number.prime?

  prime_factor = find_prime_factor_of(number)
  next_number_to_check = number / prime_factor

  [prime_factor] + prime_factors(next_number_to_check)
end

def find_prime_factor_of(number)
  possible_factors_of(number).find do |possibility|
    possibility.prime? && possibility % x == 0
  end
end

def possible_factors_of(number)
  (2..(number / 2))
end
```

### Method Chaining
Chaining method calls together can make code more concise and readable:

```ruby
def doubled_evens(numbers)
  numbers.select(&:even?).map { |number| number * 2 }
end

my_numbers = [1, 2, 3, 4]

doubled_events(my_numbers)
# => [4, 8]
```

In the code above, the body of the `doubled_evens` method shows an example of method chaining.  Notice that the data type does not change.  The method accepts an array argument and calls `#select` on that array, returning another array.  `#map` is called on this returned array, returning yet another array.

Be wary of hiding a change of data type (e.g., array to string) within a chain of method calls.

Also, remember that you are attempting to write readable code.  Less lines of code is generally a good thing, but not if it makes the code harder to understand. The computer will chain a dozen method calls without a problem, but it will be difficult for a person to read.

# Prelude

> Role models are important. <br/>
> -- Officer Alex J. Murphy / RoboCop

One thing has always bothered me as a Ruby developer - Python developers have a
great programming style reference
([PEP-8][]) and we never got an official
guide, documenting Ruby coding style and best practices. And I do believe that
style matters. I also believe that a great hacker community, such as Ruby has,
should be quite capable of producing this coveted document.

This guide started its life as our internal company Ruby coding guidelines
(written by yours truly). At some point I decided that the work I was doing
might be interesting to members of the Ruby community in general and that the
world had little need for another internal company guideline. But the world
could certainly benefit from a community-driven and community-sanctioned set of
practices, idioms and style prescriptions for Ruby programming.

Since the inception of the guide I've received a lot of feedback from members of
the exceptional Ruby community around the world. Thanks for all the suggestions
and the support! Together we can make a resource beneficial to each and every
Ruby developer out there.

By the way, if you're into Rails you might want to check out the complementary
[Ruby on Rails Style Guide][rails-style-guide].

# The Ruby Style Guide

This Ruby style guide recommends best practices so that real-world Ruby
programmers can write code that can be maintained by other real-world Ruby
programmers. A style guide that reflects real-world usage gets used, and a style
guide that holds to an ideal that has been rejected by the people it is supposed
to help risks not getting used at all &ndash; no matter how good it is.

The guide is separated into several sections of related rules. I've tried to add
the rationale behind the rules (if it's omitted I've assumed it's pretty
obvious).

I didn't come up with all the rules out of nowhere - they are mostly
based on my extensive career as a professional software engineer,
feedback and suggestions from members of the Ruby community and
various highly regarded Ruby programming resources, such as
["Programming Ruby 1.9"][pickaxe] and
["The Ruby Programming Language"][trpl].

There are some areas in which there is no clear consensus in the Ruby community
regarding a particular style (like string literal quoting, spacing inside hash
literals, dot position in multi-line method chaining, etc.). In such scenarios
all popular styles are acknowledged and it's up to you to pick one and apply it
consistently.

This style guide evolves over time as additional conventions are
identified and past conventions are rendered obsolete by changes in
Ruby itself.

Many projects have their own coding style guidelines (often derived
from this guide). In the event of any conflicts, such
project-specific guides take precedence for that project.

You can generate a PDF or an HTML copy of this guide using
[Transmuter][].

[RuboCop][] is a code analyzer, based on this
style guide.

Translations of the guide are available in the following languages:

* [Chinese Simplified](https://github.com/JuanitoFatas/ruby-style-guide/blob/master/README-zhCN.md)
* [Chinese Traditional](https://github.com/JuanitoFatas/ruby-style-guide/blob/master/README-zhTW.md)
* [French](https://github.com/porecreat/ruby-style-guide/blob/master/README-frFR.md)
* [German](https://github.com/arbox/ruby-style-guide/blob/master/README-deDE.md)
* [Japanese](https://github.com/fortissimo1997/ruby-style-guide/blob/japanese/README.ja.md)
* [Korean](https://github.com/dalzony/ruby-style-guide/blob/master/README-koKR.md)
* [Portuguese](https://github.com/rubensmabueno/ruby-style-guide/blob/master/README-PT-BR.md)
* [Russian](https://github.com/arbox/ruby-style-guide/blob/master/README-ruRU.md)
* [Spanish](https://github.com/alemohamad/ruby-style-guide/blob/master/README-esLA.md)
* [Vietnamese](https://github.com/scrum2b/ruby-style-guide/blob/master/README-viVN.md)

## Table of Contents

* [Source Code Layout](#source-code-layout)
* [Syntax](#syntax)
* [Naming](#naming)
* [Comments](#comments)
  * [Comment Annotations](#comment-annotations)
* [Classes](#classes--modules)
* [Exceptions](#exceptions)
* [Collections](#collections)
* [Strings](#strings)
* [Regular Expressions](#regular-expressions)
* [Percent Literals](#percent-literals)
* [Metaprogramming](#metaprogramming)
* [Misc](#misc)
* [Tools](#tools)

## Source Code Layout

> Nearly everybody is convinced that every style but their own is
> ugly and unreadable. Leave out the "but their own" and they're
> probably right... <br/>
> -- Jerry Coffin (on indentation)

* <a name="utf-8"></a>
  Use `UTF-8` as the source file encoding.
<sup>[[link](#utf-8)]</sup>

* <a name="spaces-indentation"></a>
  Use two **spaces** per indentation level (aka soft tabs). No hard tabs.
<sup>[[link](#spaces-indentation)]</sup>

  ```Ruby
  # bad - four spaces
  def some_method
      do_something
  end

  # good
  def some_method
    do_something
  end
  ```

* <a name="crlf"></a>
  Use Unix-style line endings. (*BSD/Solaris/Linux/OS X users are covered by
  default, Windows users have to be extra careful.)
<sup>[[link](#crlf)]</sup>

  * If you're using Git you might want to add the following
    configuration setting to protect your project from Windows line
    endings creeping in:

    ```bash
    $ git config --global core.autocrlf true
    ```

* <a name="no-semicolon"></a>
  Don't use `;` to separate statements and expressions. As a corollary - use one
  expression per line.
<sup>[[link](#no-semicolon)]</sup>

  ```Ruby
  # bad
  puts 'foobar'; # superfluous semicolon

  puts 'foo'; puts 'bar' # two expressions on the same line

  # good
  puts 'foobar'

  puts 'foo'
  puts 'bar'

  puts 'foo', 'bar' # this applies to puts in particular
  ```

* <a name="single-line-classes"></a>
  Prefer a single-line format for class definitions with no body.
<sup>[[link](#single-line-classes)]</sup>

  ```Ruby
  # bad
  class FooError < StandardError
  end

  # okish
  class FooError < StandardError; end

  # good
  FooError = Class.new(StandardError)
  ```

* <a name="no-single-line-methods"></a>
  Avoid single-line methods. Although they are somewhat popular in the wild,
  there are a few peculiarities about their definition syntax that make their
  use undesirable. At any rate - there should be no more than one expression in
  a single-line method.
<sup>[[link](#no-single-line-methods)]</sup>

  ```Ruby
  # bad
  def too_much; something; something_else; end

  # okish - notice that the first ; is required
  def no_braces_method; body end

  # okish - notice that the second ; is optional
  def no_braces_method; body; end

  # okish - valid syntax, but no ; makes it kind of hard to read
  def some_method() body end

  # good
  def some_method
    body
  end
  ```

  One exception to the rule are empty-body methods.

  ```Ruby
  # good
  def no_op; end
  ```

* <a name="spaces-operators"></a>
  Use spaces around operators, after commas, colons and semicolons, around `{`
  and before `}`. Whitespace might be (mostly) irrelevant to the Ruby
  interpreter, but its proper use is the key to writing easily readable code.
<sup>[[link](#spaces-operators)]</sup>

  ```Ruby
  sum = 1 + 2
  a, b = 1, 2
  [1, 2, 3].each { |e| puts e }
  class FooError < StandardError; end
  ```

  The only exception, regarding operators, is the exponent operator:

  ```Ruby
  # bad
  e = M * c ** 2

  # good
  e = M * c**2
  ```

  `{` and `}` deserve a bit of clarification, since they are used
  for block and hash literals, as well as embedded expressions in
  strings. For hash literals two styles are considered acceptable.

  ```Ruby
  # good - space after { and before }
  { one: 1, two: 2 }

  # good - no space after { and before }
  {one: 1, two: 2}
  ```

  The first variant is slightly more readable (and arguably more
  popular in the Ruby community in general). The second variant has
  the advantage of adding visual difference between block and hash
  literals. Whichever one you pick - apply it consistently.

  As far as embedded expressions go, there are also two acceptable
  options:

  ```Ruby
  # good - no spaces
  "string#{expr}"

  # ok - arguably more readable
  "string#{ expr }"
  ```

  The first style is extremely more popular and you're generally
  advised to stick with it. The second, on the other hand, is
  (arguably) a bit more readable. As with hashes - pick one style
  and apply it consistently.

* <a name="no-spaces-braces"></a>
  No spaces after `(`, `[` or before `]`, `)`.
<sup>[[link](#no-spaces-braces)]</sup>

  ```Ruby
  some(arg).other
  [1, 2, 3].size
  ```

* <a name="no-space-bang"></a>
  No space after `!`.
<sup>[[link](#no-space-bang)]</sup>

  ```Ruby
  # bad
  ! something

  # good
  !something
  ```

* <a name="no-space-inside-range-literals"></a>
  No space inside range literals.
<sup>[[link](#no-space-inside-range-literals)]</sup>

    ```Ruby
    # bad
    1 .. 3
    'a' ... 'z'

    # good
    1..3
    'a'...'z'
    ```

* <a name="indent-when-to-case"></a>
  Indent `when` as deep as `case`. I know that many would disagree
  with this one, but it's the style established in both "The Ruby
  Programming Language" and "Programming Ruby".
<sup>[[link](#indent-when-to-case)]</sup>

  ```Ruby
  # bad
  case
    when song.name == 'Misty'
      puts 'Not again!'
    when song.duration > 120
      puts 'Too long!'
    when Time.now.hour > 21
      puts "It's too late"
    else
      song.play
  end

  # good
  case
  when song.name == 'Misty'
    puts 'Not again!'
  when song.duration > 120
    puts 'Too long!'
  when Time.now.hour > 21
    puts "It's too late"
  else
    song.play
  end
  ```

* <a name="indent-conditional-assignment"></a>
  When assigning the result of a conditional expression to a variable,
  preserve the usual alignment of its branches.
<sup>[[link](#indent-conditional-assignment)]</sup>

  ```Ruby
  # bad - pretty convoluted
  kind = case year
  when 1850..1889 then 'Blues'
  when 1890..1909 then 'Ragtime'
  when 1910..1929 then 'New Orleans Jazz'
  when 1930..1939 then 'Swing'
  when 1940..1950 then 'Bebop'
  else 'Jazz'
  end

  result = if some_cond
    calc_something
  else
    calc_something_else
  end

  # good - it's apparent what's going on
  kind = case year
         when 1850..1889 then 'Blues'
         when 1890..1909 then 'Ragtime'
         when 1910..1929 then 'New Orleans Jazz'
         when 1930..1939 then 'Swing'
         when 1940..1950 then 'Bebop'
         else 'Jazz'
         end

  result = if some_cond
             calc_something
           else
             calc_something_else
           end

  # good (and a bit more width efficient)
  kind =
    case year
    when 1850..1889 then 'Blues'
    when 1890..1909 then 'Ragtime'
    when 1910..1929 then 'New Orleans Jazz'
    when 1930..1939 then 'Swing'
    when 1940..1950 then 'Bebop'
    else 'Jazz'
    end

  result =
    if some_cond
      calc_something
    else
      calc_something_else
    end
  ```

* <a name="empty-lines-between-methods"></a>
  Use empty lines between method definitions and also to break up a method
  into logical paragraphs internally.
<sup>[[link](#empty-lines-between-methods)]</sup>

  ```Ruby
  def some_method
    data = initialize(options)

    data.manipulate!

    data.result
  end

  def some_method
    result
  end
  ```

* <a name="no-trailing-params-comma"></a>
  Avoid comma after the last parameter in a method call, especially when the
  parameters are not on separate lines.
<sup>[[link](#no-trailing-params-comma)]</sup>

  ```Ruby
  # bad - easier to move/add/remove parameters, but still not preferred
  some_method(
               size,
               count,
               color,
             )

  # bad
  some_method(size, count, color, )

  # good
  some_method(size, count, color)
  ```

* <a name="spaces-around-equals"></a>
  Use spaces around the `=` operator when assigning default values to method
  parameters:
<sup>[[link](#spaces-around-equals)]</sup>

  ```Ruby
  # bad
  def some_method(arg1=:default, arg2=nil, arg3=[])
    # do something...
  end

  # good
  def some_method(arg1 = :default, arg2 = nil, arg3 = [])
    # do something...
  end
  ```

  While several Ruby books suggest the first style, the second is much more
  prominent in practice (and arguably a bit more readable).

* <a name="no-trailing-backslash"></a>
  Avoid line continuation `\` where not required. In practice, avoid using
  line continuations for anything but string concatenation.
<sup>[[link](#no-trailing-backslash)]</sup>

  ```Ruby
  # bad
  result = 1 - \
           2

  # good (but still ugly as hell)
  result = 1 \
           - 2

  long_string = 'First part of the long string' \
                ' and second part of the long string'
  ```

* <a name="consistent-multi-line-chains"></a>
    Adopt a consistent multi-line method chaining style. There are two
    popular styles in the Ruby community, both of which are considered
    good - leading `.` (Option A) and trailing `.` (Option B).
<sup>[[link](#consistent-multi-line-chains)]</sup>

  * **(Option A)** When continuing a chained method invocation on
    another line keep the `.` on the second line.

    ```Ruby
    # bad - need to consult first line to understand second line
    one.two.three.
      four

    # good - it's immediately clear what's going on the second line
    one.two.three
      .four
    ```

  * **(Option B)** When continuing a chained method invocation on another line,
    include the `.` on the first line to indicate that the
    expression continues.

    ```Ruby
    # bad - need to read ahead to the second line to know that the chain continues
    one.two.three
      .four

    # good - it's immediately clear that the expression continues beyond the first line
    one.two.three.
      four
    ```

  A discussion on the merits of both alternative styles can be found
  [here](https://github.com/bbatsov/ruby-style-guide/pull/176).

* <a name="no-double-indent"></a>
    Align the parameters of a method call if they span more than one
    line. When aligning parameters is not appropriate due to line-length
    constraints, single indent for the lines after the first is also
    acceptable.
<sup>[[link](#no-double-indent)]</sup>

  ```Ruby
  # starting point (line is too long)
  def send_mail(source)
    Mailer.deliver(to: 'bob@example.com', from: 'us@example.com', subject: 'Important message', body: source.text)
  end

  # bad (double indent)
  def send_mail(source)
    Mailer.deliver(
        to: 'bob@example.com',
        from: 'us@example.com',
        subject: 'Important message',
        body: source.text)
  end

  # good
  def send_mail(source)
    Mailer.deliver(to: 'bob@example.com',
                   from: 'us@example.com',
                   subject: 'Important message',
                   body: source.text)
  end

  # good (normal indent)
  def send_mail(source)
    Mailer.deliver(
      to: 'bob@example.com',
      from: 'us@example.com',
      subject: 'Important message',
      body: source.text
    )
  end
  ```

* <a name="align-multiline-arrays"></a>
  Align the elements of array literals spanning multiple lines.
<sup>[[link](#align-multiline-arrays)]</sup>

  ```Ruby
  # bad - single indent
  menu_item = ['Spam', 'Spam', 'Spam', 'Spam', 'Spam', 'Spam', 'Spam', 'Spam',
    'Baked beans', 'Spam', 'Spam', 'Spam', 'Spam', 'Spam']

  # good
  menu_item = [
    'Spam', 'Spam', 'Spam', 'Spam', 'Spam', 'Spam', 'Spam', 'Spam',
    'Baked beans', 'Spam', 'Spam', 'Spam', 'Spam', 'Spam'
  ]

  # good
  menu_item =
    ['Spam', 'Spam', 'Spam', 'Spam', 'Spam', 'Spam', 'Spam', 'Spam',
     'Baked beans', 'Spam', 'Spam', 'Spam', 'Spam', 'Spam']
  ```

* <a name="underscores-in-numerics"></a>
  Add underscores to large numeric literals to improve their readability.
<sup>[[link](#underscores-in-numerics)]</sup>

  ```Ruby
  # bad - how many 0s are there?
  num = 1000000

  # good - much easier to parse for the human brain
  num = 1_000_000
  ```

* <a name="rdoc-conventions"></a>
    Use RDoc and its conventions for API documentation.  Don't put an
    empty line between the comment block and the `def`.
<sup>[[link](#rdoc-conventions)]</sup>

* <a name="80-character-limits"></a>
  Limit lines to 80 characters.
<sup>[[link](#80-character-limits)]</sup>

* <a name="no-trailing-whitespace"></a>
  Avoid trailing whitespace.
<sup>[[link](#no-trailing-whitespace)]</sup>

* <a name="newline-eof"></a>
  End each file with a newline.
<sup>[[link](#newline-eof)]</sup>

* <a name="no-block-comments"></a>
    Don't use block comments. They cannot be preceded by whitespace and are not
    as easy to spot as regular comments.
<sup>[[link](#no-block-comments)]</sup>

  ```Ruby
  # bad
  =begin
  comment line
  another comment line
  =end

  # good
  # comment line
  # another comment line
  ```

## Syntax

* <a name="double-colons"></a>
    Use `::` only to reference constants(this includes classes and
    modules) and constructors (like `Array()` or `Nokogiri::HTML()`).
    Do not use `::` for regular method invocation.
<sup>[[link](#double-colons)]</sup>

  ```Ruby
  # bad
  SomeClass::some_method
  some_object::some_method

  # good
  SomeClass.some_method
  some_object.some_method
  SomeModule::SomeClass::SOME_CONST
  SomeModule::SomeClass()
  ```

* <a name="method-parens"></a>
    Use `def` with parentheses when there are parameters. Omit the
    parentheses when the method doesn't accept any parameters.
<sup>[[link](#method-parens)]</sup>

   ```Ruby
   # bad
   def some_method()
     # body omitted
   end

   # good
   def some_method
     # body omitted
   end

   # bad
   def some_method_with_parameters param1, param2
     # body omitted
   end

   # good
   def some_method_with_parameters(param1, param2)
     # body omitted
   end
   ```

* <a name="no-for-loops"></a>
    Do not use `for`, unless you know exactly why. Most of the time iterators
    should be used instead. `for` is implemented in terms of `each` (so
    you're adding a level of indirection), but with a twist - `for`
    doesn't introduce a new scope (unlike `each`) and variables defined
    in its block will be visible outside it.
<sup>[[link](#no-for-loops)]</sup>

  ```Ruby
  arr = [1, 2, 3]

  # bad
  for elem in arr do
    puts elem
  end

  # note that elem is accessible outside of the for loop
  elem # => 3

  # good
  arr.each { |elem| puts elem }

  # elem is not accessible outside each's block
  elem # => NameError: undefined local variable or method `elem'
  ```

* <a name="no-then"></a>
  Do not use `then` for multi-line `if/unless`.
<sup>[[link](#no-then)]</sup>

  ```Ruby
  # bad
  if some_condition then
    # body omitted
  end

  # good
  if some_condition
    # body omitted
  end
  ```

* <a name="same-line-condition"></a>
  Always put the condition on the same line as the `if`/`unless` in a
  multi-line conditional.
<sup>[[link](#same-line-condition)]</sup>

  ```Ruby
  # bad
  if
    some_condition
    do_something
    do_something_else
  end

  # good
  if some_condition
    do_something
    do_something_else
  end
  ```

* <a name="ternary-operator"></a>
  Favor the ternary operator(`?:`) over `if/then/else/end` constructs.
  It's more common and obviously more concise.
<sup>[[link](#ternary-operator)]</sup>

  ```Ruby
  # bad
  result = if some_condition then something else something_else end

  # good
  result = some_condition ? something : something_else
  ```

* <a name="no-nested-ternary"></a>
  Use one expression per branch in a ternary operator. This
  also means that ternary operators must not be nested. Prefer
  `if/else` constructs in these cases.
<sup>[[link](#no-nested-ternary)]</sup>

  ```Ruby
  # bad
  some_condition ? (nested_condition ? nested_something : nested_something_else) : something_else

  # good
  if some_condition
    nested_condition ? nested_something : nested_something_else
  else
    something_else
  end
  ```

* <a name="no-semicolon-ifs"></a>
  Do not use `if x; ...`. Use the ternary
  operator instead.
<sup>[[link](#no-semicolon-ifs)]</sup>

  ```Ruby
  # bad
  result = if some_condition; something else something_else end

  # good
  result = some_condition ? something : something_else
  ```

* <a name="use-if-case-returns"></a>
  Leverage the fact that `if` and `case` are expressions which return a
  result.
<sup>[[link](#use-if-case-returns)]</sup>

  ```Ruby
  # bad
  if condition
    result = x
  else
    result = y
  end

  # good
  result =
    if condition
      x
    else
      y
    end
  ```

* <a name="one-line-cases"></a>
  Use `when x then ...` for one-line cases. The alternative syntax `when x:
  ...` has been removed as of Ruby 1.9.
<sup>[[link](#one-line-cases)]</sup>

* <a name="no-when-semicolons"></a>
  Do not use `when x; ...`. See the previous rule.
<sup>[[link](#no-when-semicolons)]</sup>

* <a name="bang-not-not"></a>
  Use `!` instead of `not`.
<sup>[[link](#bang-not-not)]</sup>

  ```Ruby
  # bad - braces are required because of op precedence
  x = (not something)

  # good
  x = !something
  ```

* <a name="no-bang-bang"></a>
  Avoid the use of `!!`.
<sup>[[link](#no-bang-bang)]</sup>

  ```Ruby
  # bad
  x = 'test'
  # obscure nil check
  if !!x
    # body omitted
  end

  x = false
  # double negation is useless on booleans
  !!x # => false

  # good
  x = 'test'
  unless x.nil?
    # body omitted
  end
  ```

* <a name="no-and-or-or"></a>
  The `and` and `or` keywords are banned. It's just not worth it. Always use
  `&&` and `||` instead.
<sup>[[link](#no-and-or-or)]</sup>

  ```Ruby
  # bad
  # boolean expression
  if some_condition and some_other_condition
    do_something
  end

  # control flow
  document.saved? or document.save!

  # good
  # boolean expression
  if some_condition && some_other_condition
    do_something
  end

  # control flow
  document.saved? || document.save!
  ```

* <a name="no-multiline-ternary"></a>
  Avoid multi-line `?:` (the ternary operator); use `if/unless` instead.
<sup>[[link](#no-multiline-ternary)]</sup>

* <a name="if-as-a-modifier"></a>
  Favor modifier `if/unless` usage when you have a single-line body. Another
  good alternative is the usage of control flow `&&/||`.
<sup>[[link](#if-as-a-modifier)]</sup>

  ```Ruby
  # bad
  if some_condition
    do_something
  end

  # good
  do_something if some_condition

  # another good option
  some_condition && do_something
  ```

* <a name="no-multiline-if-modifiers"></a>
  Avoid modifier `if/unless` usage at the end of a non-trivial multi-line
  block.
<sup>[[link](#no-multiline-if-modifiers)]</sup>

  ```Ruby
  # bad
  10.times do
    # multi-line body omitted
  end if some_condition

  # good
  if some_condition
    10.times do
      # multi-line body omitted
    end
  end
  ```

* <a name="unless-for-negatives"></a>
  Favor `unless` over `if` for negative conditions (or control flow `||`).
<sup>[[link](#unless-for-negatives)]</sup>

  ```Ruby
  # bad
  do_something if !some_condition

  # bad
  do_something if not some_condition

  # good
  do_something unless some_condition

  # another good option
  some_condition || do_something
  ```

* <a name="no-else-with-unless"></a>
  Do not use `unless` with `else`. Rewrite these with the positive case first.
<sup>[[link](#no-else-with-unless)]</sup>

  ```Ruby
  # bad
  unless success?
    puts 'failure'
  else
    puts 'success'
  end

  # good
  if success?
    puts 'success'
  else
    puts 'failure'
  end
  ```

* <a name="no-parens-if"></a>
  Don't use parentheses around the condition of an `if/unless/while/until`.
<sup>[[link](#no-parens-if)]</sup>

  ```Ruby
  # bad
  if (x > 10)
    # body omitted
  end

  # good
  if x > 10
    # body omitted
  end
  ```

Note that there is an exception to this rule, namely [safe assignment in
condition](#safe-assignment-in-condition).

* <a name="no-multiline-while-do"></a>
  Do not use `while/until condition do` for multi-line `while/until`.
<sup>[[link](#no-multiline-while-do)]</sup>

  ```Ruby
  # bad
  while x > 5 do
    # body omitted
  end

  until x > 5 do
    # body omitted
  end

  # good
  while x > 5
    # body omitted
  end

  until x > 5
    # body omitted
  end
  ```

* <a name="while-as-a-modifier"></a>
  Favor modifier `while/until` usage when you have a single-line body.
<sup>[[link](#while-as-a-modifier)]</sup>

  ```Ruby
  # bad
  while some_condition
    do_something
  end

  # good
  do_something while some_condition
  ```

* <a name="until-for-negatives"></a>
  Favor `until` over `while` for negative conditions.
<sup>[[link](#until-for-negatives)]</sup>

  ```Ruby
  # bad
  do_something while !some_condition

  # good
  do_something until some_condition
  ```

* <a name="infinite-loop"></a>
  Use `Kernel#loop` instead of `while/until` when you need an infinite loop.
<sup>[[link](#infinite-loop)]</sup>

    ```ruby
    # bad
    while true
      do_something
    end

    until false
      do_something
    end

    # good
    loop do
      do_something
    end
    ```

* <a name="loop-with-break"></a>
  Use `Kernel#loop` with `break` rather than `begin/end/until` or
  `begin/end/while` for post-loop tests.
<sup>[[link](#loop-with-break)]</sup>

  ```Ruby
  # bad
  begin
    puts val
    val += 1
  end while val < 0

  # good
  loop do
    puts val
    val += 1
    break unless val < 0
  end
  ```

* <a name="no-dsl-parens"></a>
  Omit parentheses around parameters for methods that are part of an internal
  DSL (e.g. Rake, Rails, RSpec), methods that have "keyword" status in Ruby
  (e.g. `attr_reader`, `puts`) and attribute access methods. Use parentheses
  around the arguments of all other method invocations.
<sup>[[link](#no-dsl-parens)]</sup>

  ```Ruby
  class Person
    attr_reader :name, :age

    # omitted
  end

  temperance = Person.new('Temperance', 30)
  temperance.name

  puts temperance.age

  x = Math.sin(y)
  array.delete(e)

  bowling.score.should == 0
  ```

* <a name="no-braces-opts-hash"></a>
  Omit the outer braces around an implicit options hash.
<sup>[[link](#no-braces-opts-hash)]</sup>

  ```Ruby
  # bad
  user.set({ name: 'John', age: 45, permissions: { read: true } })

  # good
  user.set(name: 'John', age: 45, permissions: { read: true })
  ```

* <a name="no-dsl-decorating"></a>
  Omit both the outer braces and parentheses for methods that are part of an
  internal DSL.
<sup>[[link](#no-dsl-decorating)]</sup>

  ```Ruby
  class Person < ActiveRecord::Base
    # bad
    validates(:name, { presence: true, length: { within: 1..10 } })

    # good
    validates :name, presence: true, length: { within: 1..10 }
  end
  ```

* <a name="no-args-no-parens"></a>
  Omit parentheses for method calls with no arguments.
<sup>[[link](#no-args-no-parens)]</sup>

  ```Ruby
  # bad
  Kernel.exit!()
  2.even?()
  fork()
  'test'.upcase()

  # good
  Kernel.exit!
  2.even?
  fork
  'test'.upcase
  ```

* <a name="single-line-blocks"></a>
  Prefer `{...}` over `do...end` for single-line blocks.  Avoid using `{...}`
  for multi-line blocks (multiline chaining is always ugly). Always use
  `do...end` for "control flow" and "method definitions" (e.g. in Rakefiles and
  certain DSLs).  Avoid `do...end` when chaining.
<sup>[[link](#single-line-blocks)]</sup>

  ```Ruby
  names = ['Bozhidar', 'Steve', 'Sarah']

  # bad
  names.each do |name|
    puts name
  end

  # good
  names.each { |name| puts name }

  # bad
  names.select do |name|
    name.start_with?('S')
  end.map { |name| name.upcase }

  # good
  names.select { |name| name.start_with?('S') }.map { |name| name.upcase }
  ```

  Some will argue that multiline chaining would look OK with the use of {...},
  but they should ask themselves - is this code really readable and can the
  blocks' contents be extracted into nifty methods?

* <a name="block-argument"></a>
  Consider using explicit block argument to avoid writing block literal that
  just passes its arguments to another block. Beware of the performance impact,
  though, as the block gets converted to a Proc.
<sup>[[link](#block-argument)]</sup>

  ```Ruby
  require 'tempfile'

  # bad
  def with_tmp_dir
    Dir.mktmpdir do |tmp_dir|
      Dir.chdir(tmp_dir) { |dir| yield dir }  # block just passes arguments
    end
  end

  # good
  def with_tmp_dir(&block)
    Dir.mktmpdir do |tmp_dir|
      Dir.chdir(tmp_dir, &block)
    end
  end

  with_tmp_dir do |dir|
    puts "dir is accessible as a parameter and pwd is set: #{dir}"
  end
  ```

* <a name="no-explicit-return"></a>
  Avoid `return` where not required for flow of control.
<sup>[[link](#no-explicit-return)]</sup>

  ```Ruby
  # bad
  def some_method(some_arr)
    return some_arr.size
  end

  # good
  def some_method(some_arr)
    some_arr.size
  end
  ```

* <a name="no-self-unless-required"></a>
  Avoid `self` where not required. (It is only required when calling a self
  write accessor.)
<sup>[[link](#no-self-unless-required)]</sup>

  ```Ruby
  # bad
  def ready?
    if self.last_reviewed_at > self.last_updated_at
      self.worker.update(self.content, self.options)
      self.status = :in_progress
    end
    self.status == :verified
  end

  # good
  def ready?
    if last_reviewed_at > last_updated_at
      worker.update(content, options)
      self.status = :in_progress
    end
    status == :verified
  end
  ```

* <a name="no-shadowing"></a>
  As a corollary, avoid shadowing methods with local variables unless they are
  both equivalent.
<sup>[[link](#no-shadowing)]</sup>

  ```Ruby
  class Foo
    attr_accessor :options

    # ok
    def initialize(options)
      self.options = options
      # both options and self.options are equivalent here
    end

    # bad
    def do_something(options = {})
      unless options[:when] == :later
        output(self.options[:message])
      end
    end

    # good
    def do_something(params = {})
      unless params[:when] == :later
        output(options[:message])
      end
    end
  end
  ```

* <a name="safe-assignment-in-condition"></a>
  Don't use the return value of `=` (an assignment) in conditional expressions
  unless the assignment is wrapped in parentheses. This is a fairly popular
  idiom among Rubyists that's sometimes referred to as *safe assignment in
  condition*.
<sup>[[link](#safe-assignment-in-condition)]</sup>

  ```Ruby
  # bad (+ a warning)
  if v = array.grep(/foo/)
    do_something(v)
    ...
  end

  # good (MRI would still complain, but RuboCop won't)
  if (v = array.grep(/foo/))
    do_something(v)
    ...
  end

  # good
  v = array.grep(/foo/)
  if v
    do_something(v)
    ...
  end
  ```

* <a name="self-assignment"></a>
  Use shorthand self assignment operators whenever applicable.
<sup>[[link](#self-assignment)]</sup>

  ```Ruby
  # bad
  x = x + y
  x = x * y
  x = x**y
  x = x / y
  x = x || y
  x = x && y

  # good
  x += y
  x *= y
  x **= y
  x /= y
  x ||= y
  x &&= y
  ```

* <a name="double-pipe-for-uninit"></a>
  Use `||=` to initialize variables only if they're not already initialized.
<sup>[[link](#double-pipe-for-uninit)]</sup>

  ```Ruby
  # bad
  name = name ? name : 'Bozhidar'

  # bad
  name = 'Bozhidar' unless name

  # good - set name to Bozhidar, only if it's nil or false
  name ||= 'Bozhidar'
  ```

* <a name="no-double-pipes-for-bools"></a>
  Don't use `||=` to initialize boolean variables. (Consider what would happen
  if the current value happened to be `false`.)
<sup>[[link](#no-double-pipes-for-bools)]</sup>

  ```Ruby
  # bad - would set enabled to true even if it was false
  enabled ||= true

  # good
  enabled = true if enabled.nil?
  ```

* <a name="double-amper-preprocess"></a>
  Use `&&=` to preprocess variables that may or may not exist. Using `&&=`
  will change the value only if it exists, removing the need to check its
  existence with `if`.
<sup>[[link](#double-amper-preprocess)]</sup>

  ```Ruby
  # bad
  if something
    something = something.downcase
  end

  # bad
  something = something ? something.downcase : nil

  # ok
  something = something.downcase if something

  # good
  something = something && something.downcase

  # better
  something &&= something.downcase
  ```

* <a name="no-case-equality"></a>
  Avoid explicit use of the case equality operator `===`. As its name implies
  it is meant to be used implicitly by `case` expressions and outside of them it
  yields some pretty confusing code.
<sup>[[link](#no-case-equality)]</sup>

  ```Ruby
  # bad
  Array === something
  (1..100) === 7
  /something/ === some_string

  # good
  something.is_a?(Array)
  (1..100).include?(7)
  some_string =~ /something/
  ```

* <a name="eql"></a>
  Do not use `eql?` when using `==` will do. The stricter comparison semantics
  provided by `eql?` are rarely needed in practice.
<sup>[[link](#eql)]</sup>

  ```Ruby
  # bad - eql? is the same as == for strings
  "ruby".eql? some_str

  # good
  "ruby" == some_str
  1.0.eql? x # eql? makes sense here if want to differentiate between Fixnum and Float 1
  ```

* <a name="no-cryptic-perlisms"></a>
  Avoid using Perl-style special variables (like `$:`, `$;`, etc. ). They are
  quite cryptic and their use in anything but one-liner scripts is discouraged.
  Use the human-friendly aliases provided by the `English` library.
<sup>[[link](#no-cryptic-perlisms)]</sup>

  ```Ruby
  # bad
  $:.unshift File.dirname(__FILE__)

  # good
  require 'English'
  $LOAD_PATH.unshift File.dirname(__FILE__)
  ```

* <a name="parens-no-spaces"></a>
  Do not put a space between a method name and the opening parenthesis.
<sup>[[link](#parens-no-spaces)]</sup>

  ```Ruby
  # bad
  f (3 + 2) + 1

  # good
  f(3 + 2) + 1
  ```

* <a name="parens-as-args"></a>
  If the first argument to a method begins with an open parenthesis, always
  use parentheses in the method invocation. For example, write `f((3 + 2) + 1)`.
<sup>[[link](#parens-as-args)]</sup>

* <a name="always-warn-at-runtime"></a>
  Always run the Ruby interpreter with the `-w` option so it will warn you if
  you forget either of the rules above!
<sup>[[link](#always-warn-at-runtime)]</sup>

* <a name="lambda-multi-line"></a>
  Use the new lambda literal syntax for single line body blocks. Use the
  `lambda` method for multi-line blocks.
<sup>[[link](#lambda-multi-line)]</sup>

  ```Ruby
  # bad
  l = lambda { |a, b| a + b }
  l.call(1, 2)

  # correct, but looks extremely awkward
  l = ->(a, b) do
    tmp = a * 7
    tmp * b / 50
  end

  # good
  l = ->(a, b) { a + b }
  l.call(1, 2)

  l = lambda do |a, b|
    tmp = a * 7
    tmp * b / 50
  end
  ```

* <a name="proc"></a>
  Prefer `proc` over `Proc.new`.
<sup>[[link](#proc)]</sup>

  ```Ruby
  # bad
  p = Proc.new { |n| puts n }

  # good
  p = proc { |n| puts n }
  ```

* <a name="proc-call"></a>
  Prefer `proc.call()` over `proc[]` or `proc.()` for both lambdas and procs.
<sup>[[link](#proc-call)]</sup>

  ```Ruby
  # bad - looks similar to Enumeration access
  l = ->(v) { puts v }
  l[1]

  # also bad - uncommon syntax
  l = ->(v) { puts v }
  l.(1)

  # good
  l = ->(v) { puts v }
  l.call(1)
  ```

* <a name="underscore-unused-vars"></a>
  Prefix with `_` unused block parameters and local variables. It's also
  acceptable to use just `_` (although it's a bit less descriptive). This
  convention is recognized by the Ruby interpreter and tools like RuboCop and
  will suppress their unused variable warnings.
<sup>[[link](#underscore-unused-vars)]</sup>

  ```Ruby
  # bad
  result = hash.map { |k, v| v + 1 }

  def something(x)
    unused_var, used_var = something_else(x)
    # ...
  end

  # good
  result = hash.map { |_k, v| v + 1 }

  def something(x)
    _unused_var, used_var = something_else(x)
    # ...
  end

  # good
  result = hash.map { |_, v| v + 1 }

  def something(x)
    _, used_var = something_else(x)
    # ...
  end
  ```

* <a name="global-stdout"></a>
  Use `$stdout/$stderr/$stdin` instead of `STDOUT/STDERR/STDIN`.
  `STDOUT/STDERR/STDIN` are constants, and while you can actually reassign
  (possibly to redirect some stream) constants in Ruby, you'll get an
  interpreter warning if you do so.
<sup>[[link](#global-stdout)]</sup>

* <a name="warn"></a>
  Use `warn` instead of `$stderr.puts`. Apart from being more concise and
  clear, `warn` allows you to suppress warnings if you need to (by setting the
  warn level to 0 via `-W0`).
<sup>[[link](#warn)]</sup>

* <a name="sprintf"></a>
  Favor the use of `sprintf` and its alias `format` over the fairly cryptic
  `String#%` method.
<sup>[[link](#sprintf)]</sup>

  ```Ruby
  # bad
  '%d %d' % [20, 10]
  # => '20 10'

  # good
  sprintf('%d %d', 20, 10)
  # => '20 10'

  # good
  sprintf('%{first} %{second}', first: 20, second: 10)
  # => '20 10'

  format('%d %d', 20, 10)
  # => '20 10'

  # good
  format('%{first} %{second}', first: 20, second: 10)
  # => '20 10'
  ```

* <a name="array-join"></a>
  Favor the use of `Array#join` over the fairly cryptic `Array#*` with
<sup>[[link](#array-join)]</sup>
  a string argument.

  ```Ruby
  # bad
  %w(one two three) * ', '
  # => 'one, two, three'

  # good
  %w(one two three).join(', ')
  # => 'one, two, three'
  ```

* <a name="splat-arrays"></a>
  Use `[*var]` or `Array()` instead of explicit `Array` check, when dealing
  with a variable you want to treat as an Array, but you're not certain it's an
  array.
<sup>[[link](#splat-arrays)]</sup>

  ```Ruby
  # bad
  paths = [paths] unless paths.is_a? Array
  paths.each { |path| do_something(path) }

  # good
  [*paths].each { |path| do_something(path) }

  # good (and a bit more readable)
  Array(paths).each { |path| do_something(path) }
  ```

* <a name="ranges-or-between"></a>
  Use ranges or `Comparable#between?` instead of complex comparison logic when
  possible.
<sup>[[link](#ranges-or-between)]</sup>

  ```Ruby
  # bad
  do_something if x >= 1000 && x <= 2000

  # good
  do_something if (1000..2000).include?(x)

  # good
  do_something if x.between?(1000, 2000)
  ```

* <a name="predicate-methods"></a>
  Favor the use of predicate methods to explicit comparisons with `==`.
  Numeric comparisons are OK.
<sup>[[link](#predicate-methods)]</sup>

  ```Ruby
  # bad
  if x % 2 == 0
  end

  if x % 2 == 1
  end

  if x == nil
  end

  # good
  if x.even?
  end

  if x.odd?
  end

  if x.nil?
  end

  if x.zero?
  end

  if x == 0
  end
  ```

* <a name="no-non-nil-checks"></a>
  Don't do explicit non-`nil` checks unless you're dealing with boolean
  values.
<sup>[[link](#no-non-nil-checks)]</sup>

    ```ruby
    # bad
    do_something if !something.nil?
    do_something if something != nil

    # good
    do_something if something

    # good - dealing with a boolean
    def value_set?
      !@some_boolean.nil?
    end
    ```

* <a name="no-BEGIN-blocks"></a>
  Avoid the use of `BEGIN` blocks.
<sup>[[link](#no-BEGIN-blocks)]</sup>

* <a name="no-END-blocks"></a>
  Do not use `END` blocks. Use `Kernel#at_exit` instead.
<sup>[[link](#no-END-blocks)]</sup>

  ```ruby
  # bad
  END { puts 'Goodbye!' }

  # good
  at_exit { puts 'Goodbye!' }
  ```

* <a name="no-flip-flops"></a>
  Avoid the use of flip-flops.
<sup>[[link](#no-flip-flops)]</sup>

* <a name="no-nested-conditionals"></a>
  Avoid use of nested conditionals for flow of control.
<sup>[[link](#no-nested-conditionals)]</sup>

  Prefer a guard clause when you can assert invalid data. A guard clause
  is a conditional statement at the top of a function that bails out as
  soon as it can.

  ```Ruby
  # bad
  def compute_thing(thing)
    if thing[:foo]
      update_with_bar(thing)
      if thing[:foo][:bar]
        partial_compute(thing)
      else
        re_compute(thing)
      end
    end
  end

  # good
  def compute_thing(thing)
    return unless thing[:foo]
    update_with_bar(thing[:foo])
    return re_compute(thing) unless thing[:foo][:bar]
    partial_compute(thing)
  end
  ```

  Prefer `next` in loops instead of conditional blocks.

  ```Ruby
  # bad
  [0, 1, 2, 3].each do |item|
    if item > 1
      puts item
    end
  end

  # good
  [0, 1, 2, 3].each do |item|
    next unless item > 1
    puts item
  end
  ```

* <a name="map-find-select-reduce-size"></a>
  Prefer `map` over `collect`, `find` over `detect`, `select` over `find_all`,
  `reduce` over `inject` and `size` over `length`. This is not a hard
  requirement; if the use of the alias enhances readability, it's ok to use it.
  The rhyming methods are inherited from Smalltalk and are not common in other
  programming languages. The reason the use of `select` is encouraged over
  `find_all` is that it goes together nicely with `reject` and its name is
  pretty self-explanatory.
<sup>[[link](#map-find-select-reduce-size)]</sup>

* <a name="count-vs-size"></a>
  Don't use `count` as a substitute for `size`. For `Enumerable` objects other
  than `Array` it will iterate the entire collection in order to determine its
  size.
<sup>[[link](#count-vs-size)]</sup>

  ```Ruby
  # bad
  some_hash.count

  # good
  some_hash.size
  ```

* <a name="flat-map"></a>
  Use `flat_map` instead of `map` + `flatten`.  This does not apply for arrays
  with a depth greater than 2, i.e.  if `users.first.songs == ['a', ['b','c']]`,
  then use `map + flatten` rather than `flat_map`.  `flat_map` flattens the
  array by 1, whereas `flatten` flattens it all the way.
<sup>[[link](#flat-map)]</sup>

  ```Ruby
  # bad
  all_songs = users.map(&:songs).flatten.uniq

  # good
  all_songs = users.flat_map(&:songs).uniq
  ```

* <a name="reverse-each"></a>
  Use `reverse_each` instead of `reverse.each`. `reverse_each` doesn't do a
  new array allocation and that's a good thing.
<sup>[[link](#reverse-each)]</sup>

  ```Ruby
  # bad
  array.reverse.each { ... }

  # good
  array.reverse_each { ... }
  ```

## Naming

> The only real difficulties in programming are cache invalidation and
> naming things. <br/>
> -- Phil Karlton

* <a name="english-identifiers"></a>
  Name identifiers in English.
<sup>[[link](#english-identifiers)]</sup>

  ```Ruby
  # bad - identifier using non-ascii characters
  заплата = 1_000

  # bad - identifier is a Bulgarian word, written with Latin letters (instead of Cyrillic)
  zaplata = 1_000

  # good
  salary = 1_000
  ```

* <a name="snake-case-symbols-methods-vars"></a>
  Use `snake_case` for symbols, methods and variables.
<sup>[[link](#snake-case-symbols-methods-vars)]</sup>

  ```Ruby
  # bad
  :'some symbol'
  :SomeSymbol
  :someSymbol

  someVar = 5

  def someMethod
    ...
  end

  def SomeMethod
   ...
  end

  # good
  :some_symbol

  def some_method
    ...
  end
  ```

* <a name="camelcase-classes"></a>
  Use `CamelCase` for classes and modules.  (Keep acronyms like HTTP, RFC, XML
  uppercase.)
<sup>[[link](#camelcase-classes)]</sup>

  ```Ruby
  # bad
  class Someclass
    ...
  end

  class Some_Class
    ...
  end

  class SomeXml
    ...
  end

  # good
  class SomeClass
    ...
  end

  class SomeXML
    ...
  end
  ```

* <a name="snake-case-files"></a>
  Use `snake_case` for naming files, e.g. `hello_world.rb`.
<sup>[[link](#snake-case-files)]</sup>

* <a name="snake-case-dirs"></a>
  Use `snake_case` for naming directories, e.g.
  `lib/hello_world/hello_world.rb`.
<sup>[[link](#snake-case-dirs)]</sup>

* <a name="one-class-per-file"></a>
  Aim to have just a single class/module per source file. Name the file name
  as the class/module, but replacing CamelCase with snake_case.
<sup>[[link](#one-class-per-file)]</sup>

* <a name="screaming-snake-case"></a>
  Use `SCREAMING_SNAKE_CASE` for other constants.
<sup>[[link](#screaming-snake-case)]</sup>

  ```Ruby
  # bad
  SomeConst = 5

  # good
  SOME_CONST = 5
  ```

* <a name="bool-methods-qmark"></a>
  The names of predicate methods (methods that return a boolean value) should
  end in a question mark.  (i.e. `Array#empty?`). Methods that don't return a
  boolean, shouldn't end in a question mark.
<sup>[[link](#bool-methods-qmark)]</sup>

* <a name="dangerous-method-bang"></a>
  The names of potentially *dangerous* methods (i.e. methods that modify
  `self` or the arguments, `exit!` (doesn't run the finalizers like `exit`
  does), etc.) should end with an exclamation mark if there exists a safe
  version of that *dangerous* method.
<sup>[[link](#dangerous-method-bang)]</sup>

  ```Ruby
  # bad - there is no matching 'safe' method
  class Person
    def update!
    end
  end

  # good
  class Person
    def update
    end
  end

  # good
  class Person
    def update!
    end

    def update
    end
  end
  ```

* <a name="safe-because-unsafe"></a>
  Define the non-bang (safe) method in terms of the bang (dangerous) one if
  possible.
<sup>[[link](#safe-because-unsafe)]</sup>

  ```Ruby
  class Array
    def flatten_once!
      res = []

      each do |e|
        [*e].each { |f| res << f }
      end

      replace(res)
    end

    def flatten_once
      dup.flatten_once!
    end
  end
  ```

* <a name="reduce-blocks"></a>
  When using `reduce` with short blocks, name the arguments `|a, e|`
  (accumulator, element).
<sup>[[link](#reduce-blocks)]</sup>

* <a name="other-arg"></a>
  When defining binary operators, name the parameter `other`(`<<` and `[]` are
  exceptions to the rule, since their semantics are different).
<sup>[[link](#other-arg)]</sup>

  ```Ruby
  def +(other)
    # body omitted
  end
  ```

## Comments

> Good code is its own best documentation. As you're about to add a
> comment, ask yourself, "How can I improve the code so that this
> comment isn't needed?" Improve the code and then document it to make
> it even clearer. <br/>
> -- Steve McConnell

* <a name="no-comments"></a>
  Write self-documenting code and ignore the rest of this section. Seriously!
<sup>[[link](#no-comments)]</sup>

* <a name="english-comments"></a>
  Write comments in English.
<sup>[[link](#english-comments)]</sup>

* <a name="hash-space"></a>
  Use one space between the leading `#` character of the comment and the text
  of the comment.
<sup>[[link](#hash-space)]</sup>

* <a name="english-syntax"></a>
  Comments longer than a word are capitalized and use punctuation. Use [one
  space](http://en.wikipedia.org/wiki/Sentence_spacing) after periods.
<sup>[[link](#english-syntax)]</sup>

* <a name="no-superfluous-comments"></a>
  Avoid superfluous comments.
<sup>[[link](#no-superfluous-comments)]</sup>

  ```Ruby
  # bad
  counter += 1 # Increments counter by one.
  ```

* <a name="comment-upkeep"></a>
  Keep existing comments up-to-date. An outdated comment is worse than no
  comment at all.
<sup>[[link](#comment-upkeep)]</sup>

> Good code is like a good joke - it needs no explanation. <br/>
> -- Russ Olsen

* <a name="refactor-dont-comment"></a>
  Avoid writing comments to explain bad code. Refactor the code to make it
  self-explanatory. (Do or do not - there is no try. --Yoda)
<sup>[[link](#refactor-dont-comment)]</sup>

### Comment Annotations

* <a name="annotate-above"></a>
  Annotations should usually be written on the line immediately above the
  relevant code.
<sup>[[link](#annotate-above)]</sup>

* <a name="annotate-keywords"></a>
  The annotation keyword is followed by a colon and a space, then a note
  describing the problem.
<sup>[[link](#annotate-keywords)]</sup>

* <a name="indent-annotations"></a>
  If multiple lines are required to describe the problem, subsequent lines
  should be indented two spaces after the `#`.
<sup>[[link](#indent-annotations)]</sup>

  ```Ruby
  def bar
    # FIXME: This has crashed occasionally since v3.2.1. It may
    #   be related to the BarBazUtil upgrade.
    baz(:quux)
  end
  ```

* <a name="rare-eol-annotations"></a>
  In cases where the problem is so obvious that any documentation would be
  redundant, annotations may be left at the end of the offending line with no
  note. This usage should be the exception and not the rule.
<sup>[[link](#rare-eol-annotations)]</sup>

  ```Ruby
  def bar
    sleep 100 # OPTIMIZE
  end
  ```

* <a name="todo"></a>
  Use `TODO` to note missing features or functionality that should be added at
  a later date.
<sup>[[link](#todo)]</sup>

* <a name="fixme"></a>
  Use `FIXME` to note broken code that needs to be fixed.
<sup>[[link](#fixme)]</sup>

* <a name="optimize"></a>
  Use `OPTIMIZE` to note slow or inefficient code that may cause performance
  problems.
<sup>[[link](#optimize)]</sup>

* <a name="hack"></a>
  Use `HACK` to note code smells where questionable coding practices were used
  and should be refactored away.
<sup>[[link](#hack)]</sup>

* <a name="review"></a>
  Use `REVIEW` to note anything that should be looked at to confirm it is
  working as intended. For example: `REVIEW: Are we sure this is how the client
  does X currently?`
<sup>[[link](#review)]</sup>

* <a name="document-annotations"></a>
  Use other custom annotation keywords if it feels appropriate, but be sure to
  document them in your project's `README` or similar.
<sup>[[link](#document-annotations)]</sup>

## Classes & Modules

* <a name="consistent-classes"></a>
  Use a consistent structure in your class definitions.
<sup>[[link](#consistent-classes)]</sup>

  ```Ruby
  class Person
    # extend and include go first
    extend SomeModule
    include AnotherModule

    # inner classes
    CustomErrorKlass = Class.new(StandardError)

    # constants are next
    SOME_CONSTANT = 20

    # afterwards we have attribute macros
    attr_reader :name

    # followed by other macros (if any)
    validates :name

    # public class methods are next in line
    def self.some_method
    end

    # followed by public instance methods
    def some_method
    end

    # protected and private methods are grouped near the end
    protected

    def some_protected_method
    end

    private

    def some_private_method
    end
  end
  ```

* <a name="file-classes"></a>
  Don't nest multi line classes within classes. Try to have such nested
  classes each in their own file in a folder named like the containing class.
<sup>[[link](#file-classes)]</sup>

  ```Ruby
  # bad

  # foo.rb
  class Foo
    class Bar
      # 30 methods inside
    end

    class Car
      # 20 methods inside
    end

    # 30 methods inside
  end

  # good

  # foo.rb
  class Foo
    # 30 methods inside
  end

  # foo/bar.rb
  class Foo
    class Bar
      # 30 methods inside
    end
  end

  # foo/car.rb
  class Foo
    class Car
      # 20 methods inside
    end
  end
  ```

* <a name="modules-vs-classes"></a>
  Prefer modules to classes with only class methods. Classes should be used
  only when it makes sense to create instances out of them.
<sup>[[link](#modules-vs-classes)]</sup>

  ```Ruby
  # bad
  class SomeClass
    def self.some_method
      # body omitted
    end

    def self.some_other_method
    end
  end

  # good
  module SomeModule
    module_function

    def some_method
      # body omitted
    end

    def some_other_method
    end
  end
  ```

* <a name="module-function"></a>
  Favor the use of `module_function` over `extend self` when you want to turn
  a module's instance methods into class methods.
<sup>[[link](#module-function)]</sup>

  ```Ruby
  # bad
  module Utilities
    extend self

    def parse_something(string)
      # do stuff here
    end

    def other_utility_method(number, string)
      # do some more stuff
    end
  end

  # good
  module Utilities
    module_function

    def parse_something(string)
      # do stuff here
    end

    def other_utility_method(number, string)
      # do some more stuff
    end
  end
  ```

* <a name="liskov"></a>
  When designing class hierarchies make sure that they conform to the [Liskov
  Substitution
  Principle](http://en.wikipedia.org/wiki/Liskov_substitution_principle).
<sup>[[link](#liskov)]</sup>

* <a name="solid-design"></a>
  Try to make your classes as
  [SOLID](http://en.wikipedia.org/wiki/SOLID_\(object-oriented_design\)) as
  possible.
<sup>[[link](#solid-design)]</sup>

* <a name="define-to-s"></a>
  Always supply a proper `to_s` method for classes that represent domain
  objects.
<sup>[[link](#define-to-s)]</sup>

  ```Ruby
  class Person
    attr_reader :first_name, :last_name

    def initialize(first_name, last_name)
      @first_name = first_name
      @last_name = last_name
    end

    def to_s
      "#{@first_name} #{@last_name}"
    end
  end
  ```

* <a name="attr_family"></a>
  Use the `attr` family of functions to define trivial accessors or mutators.
<sup>[[link](#attr_family)]</sup>

  ```Ruby
  # bad
  class Person
    def initialize(first_name, last_name)
      @first_name = first_name
      @last_name = last_name
    end

    def first_name
      @first_name
    end

    def last_name
      @last_name
    end
  end

  # good
  class Person
    attr_reader :first_name, :last_name

    def initialize(first_name, last_name)
      @first_name = first_name
      @last_name = last_name
    end
  end
  ```

* <a name="attr"></a>
  Avoid the use of `attr`. Use `attr_reader` and `attr_accessor` instead.
<sup>[[link](#attr)]</sup>

  ```Ruby
  # bad - creates a single attribute accessor (deprecated in 1.9)
  attr :something, true
  attr :one, :two, :three # behaves as attr_reader

  # good
  attr_accessor :something
  attr_reader :one, :two, :three
  ```

* <a name="struct-new"></a>
  Consider using `Struct.new`, which defines the trivial accessors,
  constructor and comparison operators for you.
<sup>[[link](#struct-new)]</sup>

  ```Ruby
  # good
  class Person
    attr_accessor :first_name, :last_name

    def initialize(first_name, last_name)
      @first_name = first_name
      @last_name = last_name
    end
  end

  # better
  Person = Struct.new(:first_name, :last_name) do
  end
  ````

* <a name="no-extend-struct-new"></a>
  Don't extend a `Struct.new` - it already is a new class. Extending it
  introduces a superfluous class level and may also introduce weird errors if
  the file is required multiple times.
<sup>[[link](#no-extend-struct-new)]</sup>

* <a name="factory-methods"></a>
  Consider adding factory methods to provide additional sensible ways to
  create instances of a particular class.
<sup>[[link](#factory-methods)]</sup>

  ```Ruby
  class Person
    def self.create(options_hash)
      # body omitted
    end
  end
  ```

* <a name="duck-typing"></a>
  Prefer [duck-typing](http://en.wikipedia.org/wiki/Duck_typing) over
  inheritance.
<sup>[[link](#duck-typing)]</sup>

  ```Ruby
  # bad
  class Animal
    # abstract method
    def speak
    end
  end

  # extend superclass
  class Duck < Animal
    def speak
      puts 'Quack! Quack'
    end
  end

  # extend superclass
  class Dog < Animal
    def speak
      puts 'Bau! Bau!'
    end
  end

  # good
  class Duck
    def speak
      puts 'Quack! Quack'
    end
  end

  class Dog
    def speak
      puts 'Bau! Bau!'
    end
  end
  ```

* <a name="no-class-vars"></a>
  Avoid the usage of class (`@@`) variables due to their "nasty" behavior in
  inheritance.
<sup>[[link](#no-class-vars)]</sup>

  ```Ruby
  class Parent
    @@class_var = 'parent'

    def self.print_class_var
      puts @@class_var
    end
  end

  class Child < Parent
    @@class_var = 'child'
  end

  Parent.print_class_var # => will print "child"
  ```

  As you can see all the classes in a class hierarchy actually share one
  class variable. Class instance variables should usually be preferred
  over class variables.

* <a name="visibility"></a>
  Assign proper visibility levels to methods (`private`, `protected`) in
  accordance with their intended usage. Don't go off leaving everything `public`
  (which is the default). After all we're coding in *Ruby* now, not in *Python*.
<sup>[[link](#visibility)]</sup>

* <a name="indent-public-private-protected"></a>
  Indent the `public`, `protected`, and `private` methods as much the method
  definitions they apply to. Leave one blank line above the visibility modifier
  and one blank line below in order to emphasize that it applies to all methods
  below it.
<sup>[[link](#indent-public-private-protected)]</sup>

  ```Ruby
  class SomeClass
    def public_method
      # ...
    end

    private

    def private_method
      # ...
    end

    def another_private_method
      # ...
    end
  end
  ```

* <a name="def-self-singletons"></a>
  Use `def self.method` to define singleton methods. This makes the code
  easier to refactor since the class name is not repeated.
<sup>[[link](#def-self-singletons)]</sup>

  ```Ruby
  class TestClass
    # bad
    def TestClass.some_method
      # body omitted
    end

    # good
    def self.some_other_method
      # body omitted
    end

    # Also possible and convenient when you
    # have to define many singleton methods.
    class << self
      def first_method
        # body omitted
      end

      def second_method_etc
        # body omitted
      end
    end
  end
  ```

* <a name="alias-method-lexically"></a>
  Prefer `alias` when aliasing methods in lexical class scope as the
  resolution of `self` in this context is also lexical, and it communicates
  clearly to the user that the indirection of your alias will not be altered
  at runtime or by any subclass unless made explicit.
<sup>[[link](#alias-method-lexically)]</sup>

  ```Ruby
  class Westerner
    def first_name
      @names.first
    end

    alias given_name first_name
  end
  ```

  Since `alias`, like `def`, is a keyword, prefer bareword arguments over
  symbols or strings. In other words, do `alias foo bar`, not
  `alias :foo :bar`.

  Also be aware of how Ruby handles aliases and inheritance: an alias
  references the method that was resolved at the time the alias was defined;
  it is not dispatched dynamically.

  ```Ruby
  class Fugitive < Westerner
    def first_name
      'Nobody'
    end
  end
  ```

  In this example, `Fugitive#given_name` would still call the original
  `Westerner#first_name` method, not `Fugitive#first_name`. To override the
  behavior of `Fugitive#given_name` as well, you'd have to redefine it in the
  derived class.

  ```Ruby
  class Fugitive < Westerner
    def first_name
      'Nobody'
    end

    alias given_name first_name
  end
  ```

* <a name="alias-method"></a>
  Always use `alias_method` when aliasing methods of modules, classes, or
  singleton classes at runtime, as the lexical scope of `alias` leads to
  unpredictability in these cases.
<sup>[[link](#alias-method)]</sup>

  ```Ruby
  module Mononymous
    def self.included(other)
      other.class_eval { alias_method :full_name, :given_name }
    end
  end

  class Sting < Westerner
    include Mononymous
  end
  ```

## Exceptions

* <a name="fail-method"></a>
  Signal exceptions using the `fail` method. Use `raise` only when catching an
  exception and re-raising it (because here you're not failing, but explicitly
  and purposefully raising an exception).
<sup>[[link](#fail-method)]</sup>

  ```Ruby
  begin
    fail 'Oops'
  rescue => error
    raise if error.message != 'Oops'
  end
  ```

* <a name="no-explicit-runtimeerror"></a>
  Don't specify `RuntimeError` explicitly in the two argument version of
  `fail/raise`.
<sup>[[link](#no-explicit-runtimeerror)]</sup>

  ```Ruby
  # bad
  fail RuntimeError, 'message'

  # good - signals a RuntimeError by default
  fail 'message'
  ```

* <a name="exception-class-messages"></a>
  Prefer supplying an exception class and a message as two separate arguments
  to `fail/raise`, instead of an exception instance.
<sup>[[link](#exception-class-messages)]</sup>

  ```Ruby
  # bad
  fail SomeException.new('message')
  # Note that there is no way to do `fail SomeException.new('message'), backtrace`.

  # good
  fail SomeException, 'message'
  # Consistent with `fail SomeException, 'message', backtrace`.
  ```

* <a name="no-return-ensure"></a>
  Do not return from an `ensure` block. If you explicitly return from a method
  inside an `ensure` block, the return will take precedence over any exception
  being raised, and the method will return as if no exception had been raised at
  all. In effect, the exception will be silently thrown away.
<sup>[[link](#no-return-ensure)]</sup>

  ```Ruby
  def foo
    fail
  ensure
    return 'very bad idea'
  end
  ```

* <a name="begin-implicit"></a>
  Use *implicit begin blocks* where possible.
<sup>[[link](#begin-implicit)]</sup>

  ```Ruby
  # bad
  def foo
    begin
      # main logic goes here
    rescue
      # failure handling goes here
    end
  end

  # good
  def foo
    # main logic goes here
  rescue
    # failure handling goes here
  end
  ```

* <a name="contingency-methods"></a>
  Mitigate the proliferation of `begin` blocks by using *contingency methods*
  (a term coined by Avdi Grimm).
<sup>[[link](#contingency-methods)]</sup>

  ```Ruby
  # bad
  begin
    something_that_might_fail
  rescue IOError
    # handle IOError
  end

  begin
    something_else_that_might_fail
  rescue IOError
    # handle IOError
  end

  # good
  def with_io_error_handling
     yield
  rescue IOError
    # handle IOError
  end

  with_io_error_handling { something_that_might_fail }

  with_io_error_handling { something_else_that_might_fail }
  ```

* <a name="dont-hide-exceptions"></a>
  Don't suppress exceptions.
<sup>[[link](#dont-hide-exceptions)]</sup>

  ```Ruby
  # bad
  begin
    # an exception occurs here
  rescue SomeError
    # the rescue clause does absolutely nothing
  end

  # bad
  do_something rescue nil
  ```

* <a name="no-rescue-modifiers"></a>
  Avoid using `rescue` in its modifier form.
<sup>[[link](#no-rescue-modifiers)]</sup>

  ```Ruby
  # bad - this catches exceptions of StandardError class and its descendant classes
  read_file rescue handle_error($!)

  # good - this catches only the exceptions of Errno::ENOENT class and its descendant classes
  def foo
    read_file
  rescue Errno::ENOENT => ex
    handle_error(ex)
  end
  ```

* <a name="no-exceptional-flows"></a>
  Don't use exceptions for flow of control.
<sup>[[link](#no-exceptional-flows)]</sup>

  ```Ruby
  # bad
  begin
    n / d
  rescue ZeroDivisionError
    puts 'Cannot divide by 0!'
  end

  # good
  if d.zero?
    puts 'Cannot divide by 0!'
  else
    n / d
  end
  ```

* <a name="no-blind-rescues"></a>
  Avoid rescuing the `Exception` class.  This will trap signals and calls to
  `exit`, requiring you to `kill -9` the process.
<sup>[[link](#no-blind-rescues)]</sup>

  ```Ruby
  # bad
  begin
    # calls to exit and kill signals will be caught (except kill -9)
    exit
  rescue Exception
    puts "you didn't really want to exit, right?"
    # exception handling
  end

  # good
  begin
    # a blind rescue rescues from StandardError, not Exception as many
    # programmers assume.
  rescue => e
    # exception handling
  end

  # also good
  begin
    # an exception occurs here

  rescue StandardError => e
    # exception handling
  end
  ```

* <a name="exception-ordering"></a>
  Put more specific exceptions higher up the rescue chain, otherwise they'll
  never be rescued from.
<sup>[[link](#exception-ordering)]</sup>

  ```Ruby
  # bad
  begin
    # some code
  rescue Exception => e
    # some handling
  rescue StandardError => e
    # some handling that will never be executed
  end

  # good
  begin
    # some code
  rescue StandardError => e
    # some handling
  rescue Exception => e
    # some handling
  end
  ```

* <a name="file-close"></a>
  Release external resources obtained by your program in an ensure block.
<sup>[[link](#file-close)]</sup>

  ```Ruby
  f = File.open('testfile')
  begin
    # .. process
  rescue
    # .. handle error
  ensure
    f.close if f
  end
  ```

* <a name="standard-exceptions"></a>
  Favor the use of exceptions for the standard library over introducing new
  exception classes.
<sup>[[link](#standard-exceptions)]</sup>

## Collections

* <a name="literal-array-hash"></a>
  Prefer literal array and hash creation notation (unless you need to pass
  parameters to their constructors, that is).
<sup>[[link](#literal-array-hash)]</sup>

  ```Ruby
  # bad
  arr = Array.new
  hash = Hash.new

  # good
  arr = []
  hash = {}
  ```

* <a name="percent-w"></a>
  Prefer `%w` to the literal array syntax when you need an array of words
  (non-empty strings without spaces and special characters in them).  Apply this
  rule only to arrays with two or more elements.
<sup>[[link](#percent-w)]</sup>

  ```Ruby
  # bad
  STATES = ['draft', 'open', 'closed']

  # good
  STATES = %w(draft open closed)
  ```

* <a name="percent-i"></a>
  Prefer `%i` to the literal array syntax when you need an array of symbols
  (and you don't need to maintain Ruby 1.9 compatibility). Apply this rule only
  to arrays with two or more elements.
<sup>[[link](#percent-i)]</sup>

  ```Ruby
  # bad
  STATES = [:draft, :open, :closed]

  # good
  STATES = %i(draft open closed)
  ```

* <a name="no-trailing-array-commas"></a>
  Avoid comma after the last item of an `Array` or `Hash` literal, especially
  when the items are not on separate lines.
<sup>[[link](#no-trailing-array-commas)]</sup>

  ```Ruby
  # bad - easier to move/add/remove items, but still not preferred
  VALUES = [
             1001,
             2020,
             3333,
           ]

  # bad
  VALUES = [1001, 2020, 3333, ]

  # good
  VALUES = [1001, 2020, 3333]
  ```

* <a name="no-gappy-arrays"></a>
  Avoid the creation of huge gaps in arrays.
<sup>[[link](#no-gappy-arrays)]</sup>

  ```Ruby
  arr = []
  arr[100] = 1 # now you have an array with lots of nils
  ```

* <a name="first-and-last"></a>
  When accessing the first or last element from an array, prefer `first` or
  `last` over `[0]` or `[-1]`.
<sup>[[link](#first-and-last)]</sup>

* <a name="set-vs-array"></a>
  Use `Set` instead of `Array` when dealing with unique elements. `Set`
  implements a collection of unordered values with no duplicates. This is a
  hybrid of `Array`'s intuitive inter-operation facilities and `Hash`'s fast
  lookup.
<sup>[[link](#set-vs-array)]</sup>

* <a name="symbols-as-keys"></a>
  Prefer symbols instead of strings as hash keys.
<sup>[[link](#symbols-as-keys)]</sup>

  ```Ruby
  # bad
  hash = { 'one' => 1, 'two' => 2, 'three' => 3 }

  # good
  hash = { one: 1, two: 2, three: 3 }
  ```

* <a name="no-mutable-keys"></a>
  Avoid the use of mutable objects as hash keys.
<sup>[[link](#no-mutable-keys)]</sup>

* <a name="hash-literals"></a>
  Use the Ruby 1.9 hash literal syntax when your hash keys are symbols.
<sup>[[link](#hash-literals)]</sup>

  ```Ruby
  # bad
  hash = { :one => 1, :two => 2, :three => 3 }

  # good
  hash = { one: 1, two: 2, three: 3 }
  ```

* <a name="no-mixed-hash-syntaces"></a>
  Don't mix the Ruby 1.9 hash syntax with hash rockets in the same hash
  literal. When you've got keys that are not symbols stick to the hash rockets
  syntax.
<sup>[[link](#no-mixed-hash-syntaces)]</sup>

  ```Ruby
  # bad
  { a: 1, 'b' => 2 }

  # good
  { :a => 1, 'b' => 2 }
  ```

* <a name="hash-key"></a>
  Use `Hash#key?` instead of `Hash#has_key?` and `Hash#value?` instead of
  `Hash#has_value?`. As noted
  [here](http://blade.nagaokaut.ac.jp/cgi-bin/scat.rb/ruby/ruby-core/43765) by
  Matz, the longer forms are considered deprecated.
<sup>[[link](#hash-key)]</sup>

  ```Ruby
  # bad
  hash.has_key?(:test)
  hash.has_value?(value)

  # good
  hash.key?(:test)
  hash.value?(value)
  ```

* <a name="hash-fetch"></a>
  Use `Hash#fetch` when dealing with hash keys that should be present.
<sup>[[link](#hash-fetch)]</sup>

  ```Ruby
  heroes = { batman: 'Bruce Wayne', superman: 'Clark Kent' }
  # bad - if we make a mistake we might not spot it right away
  heroes[:batman] # => "Bruce Wayne"
  heroes[:supermann] # => nil

  # good - fetch raises a KeyError making the problem obvious
  heroes.fetch(:supermann)
  ```

* <a name="hash-fetch-defaults"></a>
  Introduce default values for hash keys via `Hash#fetch` as opposed to using
  custom logic.
<sup>[[link](#hash-fetch-defaults)]</sup>

  ```Ruby
  batman = { name: 'Bruce Wayne', is_evil: false }

  # bad - if we just use || operator with falsy value we won't get the expected result
  batman[:is_evil] || true # => true

  # good - fetch work correctly with falsy values
  batman.fetch(:is_evil, true) # => false
  ```

* <a name="use-hash-blocks"></a>
  Prefer the use of the block instead of the default value in `Hash#fetch`.
<sup>[[link](#use-hash-blocks)]</sup>

  ```Ruby
  batman = { name: 'Bruce Wayne' }

  # bad - if we use the default value, we eager evaluate it
  # so it can slow the program down if done multiple times
  batman.fetch(:powers, get_batman_powers) # get_batman_powers is an expensive call

  # good - blocks are lazy evaluated, so only triggered in case of KeyError exception
  batman.fetch(:powers) { get_batman_powers }
  ```

* <a name="hash-values-at"></a>
  Use `Hash#values_at` when you need to retrieve several values consecutively
  from a hash.
<sup>[[link](#hash-values-at)]</sup>

  ```Ruby
  # bad
  email = data['email']
  username = data['nickname']

  # good
  email, username = data.values_at('email', 'nickname')
  ```

* <a name="ordered-hashes"></a>
  Rely on the fact that as of Ruby 1.9 hashes are ordered.
<sup>[[link](#ordered-hashes)]</sup>

* <a name="no-modifying-collections"></a>
  Do not modify a collection while traversing it.
<sup>[[link](#no-modifying-collections)]</sup>

## Strings

* <a name="string-interpolation"></a>
  Prefer string interpolation and string formatting instead of string
  concatenation:
<sup>[[link](#string-interpolation)]</sup>

  ```Ruby
  # bad
  email_with_name = user.name + ' <' + user.email + '>'

  # good
  email_with_name = "#{user.name} <#{user.email}>"

  # good
  email_with_name = format('%s <%s>', user.name, user.email)
  ```

* <a name="pad-string-interpolation"></a>
  Consider padding string interpolation code with space. It more clearly sets
  the code apart from the string.
<sup>[[link](#pad-string-interpolation)]</sup>

  ```Ruby
  "#{ user.last_name }, #{ user.first_name }"
  ```

* <a name="consistent-string-literals"></a>
  Adopt a consistent string literal quoting style. There are two popular
  styles in the Ruby community, both of which are considered good - single
  quotes by default (Option A) and double quotes by default (Option B).
<sup>[[link](#consistent-string-literals)]</sup>

  * **(Option A)** Prefer single-quoted strings when you don't need
    string interpolation or special symbols such as `\t`, `\n`, `'`,
    etc.

    ```Ruby
    # bad
    name = "Bozhidar"

    # good
    name = 'Bozhidar'
    ```

  * **(Option B)** Prefer double-quotes unless your string literal
    contains `"` or escape characters you want to suppress.

    ```Ruby
    # bad
    name = 'Bozhidar'

    # good
    name = "Bozhidar"
    ```

  The second style is arguably a bit more popular in the Ruby
  community. The string literals in this guide, however, are
  aligned with the first style.

* <a name="no-character-literals"></a>
  Don't use the character literal syntax `?x`. Since Ruby 1.9 it's basically
  redundant - `?x` would interpreted as `'x'` (a string with a single character
  in it).
<sup>[[link](#no-character-literals)]</sup>

  ```Ruby
  # bad
  char = ?c

  # good
  char = 'c'
  ```

* <a name="curlies-interpolate"></a>
  Don't leave out `{}` around instance and global variables being interpolated
  into a string.
<sup>[[link](#curlies-interpolate)]</sup>

  ```Ruby
  class Person
    attr_reader :first_name, :last_name

    def initialize(first_name, last_name)
      @first_name = first_name
      @last_name = last_name
    end

    # bad - valid, but awkward
    def to_s
      "#@first_name #@last_name"
    end

    # good
    def to_s
      "#{@first_name} #{@last_name}"
    end
  end

  $global = 0
  # bad
  puts "$global = #$global"

  # good
  puts "$global = #{$global}"
  ```

* <a name="no-to-s"></a>
  Don't use `Object#to_s` on interpolated objects. It's invoked on them
  automatically.
<sup>[[link](#no-to-s)]</sup>

  ```Ruby
  # bad
  message = "This is the #{result.to_s}."

  # good
  message = "This is the #{result}."
  ```

* <a name="concat-strings"></a>
  Avoid using `String#+` when you need to construct large data chunks.
  Instead, use `String#<<`. Concatenation mutates the string instance in-place
  and is always faster than `String#+`, which creates a bunch of new string
  objects.
<sup>[[link](#concat-strings)]</sup>

  ```Ruby
  # good and also fast
  html = ''
  html << '<h1>Page title</h1>'

  paragraphs.each do |paragraph|
    html << "<p>#{paragraph}</p>"
  end
  ```

* <a name="dont-abuse-gsub"></a>
  Don't use `String#gsub` in scenarios in which you can use a faster more specialized alternative.
<sup>[[link](#dont-abuse-gsub)]</sup>

    ```Ruby
    url = 'http://example.com'
    str = 'lisp-case-rules'

    # bad
    url.gsub("http://", "https://")
    str.gsub("-", "_")

    # good
    url.sub("http://", "https://")
    str.tr("-", "_")
    ```

* <a name="heredocs"></a>
  When using heredocs for multi-line strings keep in mind the fact that they
  preserve leading whitespace. It's a good practice to employ some margin based
  on which to trim the excessive whitespace.
<sup>[[link](#heredocs)]</sup>

  ```Ruby
  code = <<-END.gsub(/^\s+\|/, '')
    |def test
    |  some_method
    |  other_method
    |end
  END
  # => "def test\n  some_method\n  other_method\nend\n"
  ```

## Regular Expressions

> Some people, when confronted with a problem, think
> "I know, I'll use regular expressions." Now they have two problems.<br/>
> -- Jamie Zawinski

* <a name="no-regexp-for-plaintext"></a>
  Don't use regular expressions if you just need plain text search in string:
  `string['text']`
<sup>[[link](#no-regexp-for-plaintext)]</sup>

* <a name="regexp-string-index"></a>
  For simple constructions you can use regexp directly through string index.
<sup>[[link](#regexp-string-index)]</sup>

  ```Ruby
  match = string[/regexp/]             # get content of matched regexp
  first_group = string[/text(grp)/, 1] # get content of captured group
  string[/text (grp)/, 1] = 'replace'  # string => 'text replace'
  ```

* <a name="non-capturing-regexp"></a>
  Use non-capturing groups when you don't use captured result of parentheses.
<sup>[[link](#non-capturing-regexp)]</sup>

  ```Ruby
  /(first|second)/   # bad
  /(?:first|second)/ # good
  ```

* <a name="no-perl-regexp-last-matchers"></a>
  Don't use the cryptic Perl-legacy variables denoting last regexp group
  matches (`$1`, `$2`, etc). Use `Regexp.last_match[n]` instead.
<sup>[[link](#no-perl-regexp-last-matchers)]</sup>

  ```Ruby
  /(regexp)/ =~ string
  ...

  # bad
  process $1

  # good
  process Regexp.last_match[1]
  ```

* <a name="no-numbered-regexes"></a>
  Avoid using numbered groups as it can be hard to track what they contain.
  Named groups can be used instead.
<sup>[[link](#no-numbered-regexes)]</sup>

  ```Ruby
  # bad
  /(regexp)/ =~ string
  ...
  process Regexp.last_match[1]

  # good
  /(?<meaningful_var>regexp)/ =~ string
  ...
  process meaningful_var
  ```

* <a name="limit-escapes"></a>
  Character classes have only a few special characters you should care about:
  `^`, `-`, `\`, `]`, so don't escape `.` or brackets in `[]`.
<sup>[[link](#limit-escapes)]</sup>

* <a name="caret-and-dollar-regexp"></a>
  Be careful with `^` and `$` as they match start/end of line, not string
  endings.  If you want to match the whole string use: `\A` and `\z` (not to be
  confused with `\Z` which is the equivalent of `/\n?\z/`).
<sup>[[link](#caret-and-dollar-regexp)]</sup>

  ```Ruby
  string = "some injection\nusername"
  string[/^username$/]   # matches
  string[/\Ausername\z/] # doesn't match
  ```

* <a name="comment-regexes"></a>
  Use `x` modifier for complex regexps. This makes them more readable and you
  can add some useful comments. Just be careful as spaces are ignored.
<sup>[[link](#comment-regexes)]</sup>

  ```Ruby
  regexp = /
    start         # some text
    \s            # white space char
    (group)       # first group
    (?:alt1|alt2) # some alternation
    end
  /x
  ```

* <a name="gsub-blocks"></a>
  For complex replacements `sub`/`gsub` can be used with block or hash.
<sup>[[link](#gsub-blocks)]</sup>

## Percent Literals

* <a name="percent-q-shorthand"></a>
  Use `%()`(it's a shorthand for `%Q`) for single-line strings which require
  both interpolation and embedded double-quotes. For multi-line strings, prefer
  heredocs.
<sup>[[link](#percent-q-shorthand)]</sup>

  ```Ruby
  # bad (no interpolation needed)
  %(<div class="text">Some text</div>)
  # should be '<div class="text">Some text</div>'

  # bad (no double-quotes)
  %(This is #{quality} style)
  # should be "This is #{quality} style"

  # bad (multiple lines)
  %(<div>\n<span class="big">#{exclamation}</span>\n</div>)
  # should be a heredoc.

  # good (requires interpolation, has quotes, single line)
  %(<tr><td class="name">#{name}</td>)
  ```

* <a name="percent-q"></a>
  Avoid `%q` unless you have a string with both `'` and `"` in it. Regular
  string literals are more readable and should be preferred unless a lot of
  characters would have to be escaped in them.
<sup>[[link](#percent-q)]</sup>

  ```Ruby
  # bad
  name = %q(Bruce Wayne)
  time = %q(8 o'clock)
  question = %q("What did you say?")

  # good
  name = 'Bruce Wayne'
  time = "8 o'clock"
  question = '"What did you say?"'
  ```

* <a name="percent-r"></a>
  Use `%r` only for regular expressions matching *more than* one '/'
  character.
<sup>[[link](#percent-r)]</sup>

  ```Ruby
  # bad
  %r(\s+)

  # still bad
  %r(^/(.*)$)
  # should be /^\/(.*)$/

  # good
  %r(^/blog/2011/(.*)$)
  ```

* <a name="percent-x"></a>
  Avoid the use of `%x` unless you're going to invoke a command with
  backquotes in it(which is rather unlikely).
<sup>[[link](#percent-x)]</sup>

  ```Ruby
  # bad
  date = %x(date)

  # good
  date = `date`
  echo = %x(echo `date`)
  ```

* <a name="percent-s"></a>
  Avoid the use of `%s`. It seems that the community has decided `:"some
  string"` is the preferred way to create a symbol with spaces in it.
<sup>[[link](#percent-s)]</sup>

* <a name="percent-literal-braces"></a>
  Prefer `()` as delimiters for all `%` literals, except `%r`. Since parentheses
  often appear inside regular expressions in many scenarios a less common
  character like `{` might be a better choice for a delimiter, depending on the
  regexp's content.
<sup>[[link](#percent-literal-braces)]</sup>

  ```Ruby
  # bad
  %w[one two three]
  %q{"Test's king!", John said.}

  # good
  %w(one two three)
  %q("Test's king!", John said.)
  ```

## Metaprogramming

* <a name="no-metaprogramming-masturbation"></a>
  Avoid needless metaprogramming.
<sup>[[link](#no-metaprogramming-masturbation)]</sup>

* <a name="no-monkey-patching"></a>
  Do not mess around in core classes when writing libraries.  (Do not
  monkey-patch them.)
<sup>[[link](#no-monkey-patching)]</sup>

* <a name="block-class-eval"></a>
  The block form of `class_eval` is preferable to the string-interpolated
  form.  - when you use the string-interpolated form, always supply `__FILE__`
  and `__LINE__`, so that your backtraces make sense:
<sup>[[link](#block-class-eval)]</sup>

  ```ruby
  class_eval 'def use_relative_model_naming?; true; end', __FILE__, __LINE__
  ```

  - `define_method` is preferable to `class_eval{ def ... }`

* <a name="eval-comment-docs"></a>
  When using `class_eval` (or other `eval`) with string interpolation, add a
  comment block showing its appearance if interpolated (a practice used in Rails
  code):
<sup>[[link](#eval-comment-docs)]</sup>

  ```ruby
  # from activesupport/lib/active_support/core_ext/string/output_safety.rb
  UNSAFE_STRING_METHODS.each do |unsafe_method|
    if 'String'.respond_to?(unsafe_method)
      class_eval <<-EOT, __FILE__, __LINE__ + 1
        def #{unsafe_method}(*params, &block)       # def capitalize(*params, &block)
          to_str.#{unsafe_method}(*params, &block)  #   to_str.capitalize(*params, &block)
        end                                       # end

        def #{unsafe_method}!(*params)              # def capitalize!(*params)
          @dirty = true                           #   @dirty = true
          super                                   #   super
        end                                       # end
      EOT
    end
  end
  ```

* <a name="no-method-missing"></a>
  Avoid using `method_missing` for metaprogramming because backtraces become
  messy, the behavior is not listed in `#methods`, and misspelled method calls
  might silently work, e.g. `nukes.launch_state = false`. Consider using
  delegation, proxy, or `define_method` instead. If you must use
  `method_missing`:
<sup>[[link](#no-method-missing)]</sup>

  - Be sure to [also define `respond_to_missing?`](http://blog.marc-andre.ca/2010/11/methodmissing-politely.html)
  - Only catch methods with a well-defined prefix, such as `find_by_*` -- make your code as assertive as possible.
  - Call `super` at the end of your statement
  - Delegate to assertive, non-magical methods:

    ```ruby
    # bad
    def method_missing?(meth, *params, &block)
      if /^find_by_(?<prop>.*)/ =~ meth
        # ... lots of code to do a find_by
      else
        super
      end
    end

    # good
    def method_missing?(meth, *params, &block)
      if /^find_by_(?<prop>.*)/ =~ meth
        find_by(prop, *params, &block)
      else
        super
      end
    end

    # best of all, though, would to define_method as each findable attribute is declared
    ```

* <a name="prefer-public-send"></a>
  Prefer `public_send` over `send` so as not to circumvent `private`/`protected` visibility.
<sup>[[link](#prefer-public-send)]</sup>

## Misc

* <a name="always-warn"></a>
  Write `ruby -w` safe code.
<sup>[[link](#always-warn)]</sup>

* <a name="no-optional-hash-params"></a>
  Avoid hashes as optional parameters. Does the method do too much? (Object
  initializers are exceptions for this rule).
<sup>[[link](#no-optional-hash-params)]</sup>

* <a name="short-methods"></a>
  Avoid methods longer than 10 LOC (lines of code). Ideally, most methods will
  be shorter than 5 LOC. Empty lines do not contribute to the relevant LOC.
<sup>[[link](#short-methods)]</sup>

* <a name="too-many-params"></a>
  Avoid parameter lists longer than three or four parameters.
<sup>[[link](#too-many-params)]</sup>

* <a name="private-global-methods"></a>
  If you really need "global" methods, add them to Kernel and make them
  private.
<sup>[[link](#private-global-methods)]</sup>

* <a name="instance-vars"></a>
  Use module instance variables instead of global variables.
<sup>[[link](#instance-vars)]</sup>

  ```Ruby
  # bad
  $foo_bar = 1

  # good
  module Foo
    class << self
      attr_accessor :bar
    end
  end

  Foo.bar = 1
  ```

* <a name="optionparser"></a>
  Use `OptionParser` for parsing complex command line options and `ruby -s`
  for trivial command line options.
<sup>[[link](#optionparser)]</sup>

* <a name="time-now"></a>
  Prefer `Time.now` over `Time.new` when retrieving the current system time.
<sup>[[link](#time-now)]</sup>

* <a name="functional-code"></a>
  Code in a functional way, avoiding mutation when that makes sense.
<sup>[[link](#functional-code)]</sup>

* <a name="no-param-mutations"></a>
  Do not mutate parameters unless that is the purpose of the method.
<sup>[[link](#no-param-mutations)]</sup>

* <a name="three-is-the-number-thou-shalt-count"></a>
  Avoid more than three levels of block nesting.
<sup>[[link](#three-is-the-number-thou-shalt-count)]</sup>

* <a name="be-consistent"></a>
  Be consistent. In an ideal world, be consistent with these guidelines.
<sup>[[link](#be-consistent)]</sup>

* <a name="common-sense"></a>
  Use common sense.
<sup>[[link](#common-sense)]</sup>

## Tools

Here's some tools to help you automatically check Ruby code against
this guide.

### RuboCop

[RuboCop][] is a Ruby code style
checker based on this style guide. RuboCop already covers a
significant portion of the Guide, supports both MRI 1.9 and MRI 2.0
and has good Emacs integration.

### RubyMine

[RubyMine](http://www.jetbrains.com/ruby/)'s code inspections are
[partially based](http://confluence.jetbrains.com/display/RUBYDEV/RubyMine+Inspections)
on this guide.

# Contributing

The guide is still a work in progress - some rules are lacking examples, some
rules don't have examples that illustrate them clearly enough. Improving such rules
is a great (and simple way) to help the Ruby community!

In due time these issues will (hopefully) be addressed - just keep them in mind
for now.

Nothing written in this guide is set in stone. It's my desire to work
together with everyone interested in Ruby coding style, so that we could
ultimately create a resource that will be beneficial to the entire Ruby
community.

Feel free to open tickets or send pull requests with improvements. Thanks in
advance for your help!

You can also support the project (and RuboCop) with financial
contributions via [gittip](https://www.gittip.com/bbatsov).

[![Support via Gittip](https://rawgithub.com/twolfson/gittip-badge/0.2.0/dist/gittip.png)](https://www.gittip.com/bbatsov)

## How to Contribute?

It's easy, just follow the [contribution guidelines](https://github.com/bbatsov/ruby-style-guide/blob/master/CONTRIBUTING.md).

# License

![Creative Commons License](http://i.creativecommons.org/l/by/3.0/88x31.png)
This work is licensed under a [Creative Commons Attribution 3.0 Unported License](http://creativecommons.org/licenses/by/3.0/deed.en_US)

# Spread the Word

A community-driven style guide is of little use to a community that
doesn't know about its existence. Tweet about the guide, share it with
your friends and colleagues. Every comment, suggestion or opinion we
get makes the guide just a little bit better. And we want to have the
best possible guide, don't we?

Cheers,<br/>
[Bozhidar](https://twitter.com/bbatsov)

[PEP-8]: http://www.python.org/dev/peps/pep-0008/
[rails-style-guide]: https://github.com/bbatsov/rails-style-guide
[pickaxe]: http://pragprog.com/book/ruby4/programming-ruby-1-9-2-0
[trpl]: http://www.amazon.com/Ruby-Programming-Language-David-Flanagan/dp/0596516177
[transmuter]: https://github.com/TechnoGate/transmuter
[RuboCop]: https://github.com/bbatsov/rubocop


# Ruby Scope
Written by [Nate Delage](https://github.com/ndelage).

## Introduction
Scope describes where a variable is accessible. For example, given the following
function:

```ruby
def nickname_generator(name)
  adjective = ["dizzy", "jazzy", "little", "big", "fresh", "junior", "cheezy"].sample
  "#{adjective} #{name}"
end
```

The function `nickname_generator` assigns a local variable `adjective`, which is
only accessible inside the `nickname_generator` function.

```text
irb> nickname_generator("mike")
=> "cheezy mike"
irb> adjective
NameError: undefined local variable or method `adjective' for main:Object
  from (irb):30
  from /opt/boxen/rbenv/versions/2.1.1/bin/irb:11:in `<main>'
```

## Types of Scope
In Ruby, the scope of any variable is determined by its name.

| Scope     | variable name begins with |
|-----------|---------------------------|
| global    | $                         |
| constant  | [A-Z]                     |
| class     | @@                        |
| instance  | @                         |
| local     | [a-z] or _                |

For example, just by changing the name of our variable `adjective` in the
previous example, we can access it outside the function. Here we'll switch it to
the global scope:

```ruby
def nickname_generator(name)
  $adjective = ["dizzy", "jazzy", "little", "big", "fresh", "junior", "cheezy"].sample
  "#{$adjective} #{name}"
end
```

```text
irb> nickname_generator("jill")
=> "fresh mike"
irb> $adjective
=> "fresh"
```

## Why Scope?
You might ask, why even have scope? Why not make all variables available
everywhere? It'd be much easier than having to keep track of these different
scope rules, right?

For one, scope narrows our working space. Imagine you're working on a program
to register students. It has with thousands of functions. Without fail, some
common variable names are going to be repeated. For example `index`, `name`,
`element`, `students`, `schedule`, etc.

Without variable scoping you'd probably pull your hair out trying to
figure out who last changed the value of some commonly used variable name like
`students`. **Scope insulates one part of code from another.**

## Types of Variable Scope in Ruby

### Globals
Globals, like the name suggests are visible everywhere. Quite convenient, but
consider globals a sharp knife that you should use with care. Aim to never
create new global variables if possible. Sometimes they're necessary, but treat
global scope as a last resort.

Global variables in Ruby can be defined anywhere and are prefixed with a `$`
character. Ruby provides a number of useful global variables. For example `$0`
holds the name of the Ruby file you're running:

```ruby
puts "This filename is: #{$0}"
```

```text
$ ruby example.rb
This filename is: example.rb
```

There are a number of other globals available in all your Ruby programs, most of
them with cryptic names like: `$!`, `$@`, `$_`. Quite often there are more
readable ways to access the same data. For example the file's name is also
available as a variable named `__FILE__` (which incidently is a local variable
that has been defined in the top-level `main` scope).

## Constants

Constants are variables that begin with a capital letter. Classes and modules
are examples of constants:

```ruby
class Person
end

module Enumerable
end
```

Tradtionally in Ruby we'll capitalize only the first letter of things like
classes and modules, but capitalize the entire variable name for constants that
aren't classes or modules.

In some languages, constants are a type of variable that once set to a value
cannot be changed. In Ruby, it's possible to change a constant's value:

```ruby
DEFAULT_NAME="Jane Doe"

DEFAULT_NAME="John Doe"
```

But Ruby does *warn* you when you change a constant's value:

```text
example.rb:3: warning: already initialized constant DEFAULT_NAME
example.rb:1: warning: previous definition of DEFAULT_NAME was here
```

Heed these warnings and either reconsider whether the variable in question
should be a constant. You might decide to modify your program so that you don't
redefine the constant's value.

Configuration values, defaults or lookup keys are often good fits for constants.
Here are some examples:

```ruby
class Car
  DEFAULT_CYLINDER_COUNT = 4
  HORSEPOWER_PER_CYLINDER = 30

  def initialize(cylinder_count=DEFAULT_CYLINDER_COUNT)
    @cylinder_count = cylinder_count
  end

  def horsepower
    @cylinder_count * HORSEPOWER_PER_CYLINDER
  end
end
```

The visibility of constants is limited to the class or module in which the
constant is defined. If a constant is not defined inside a class or module, it's
treated as a global.

```ruby
APP_NAME = "Person Tracker"

class Person
  DEFAULT_NAME = "Pat"
end
```

```text
irb> puts DEFAULT_NAME
NameError: uninitialized constant DEFAULT_NAME
irb> puts APP_NAME
Person Tracker
```

Constants are available from outside a class or module if you include the class
or module name:

```text
irb> puts Person::DEFAULT_NAME
Pat
```

## Class

Class variables visible only from inside the class. They are prefixed with `@@`:

```ruby
class Person
  @@person_count = 0

  def initialize(name)
    @name = name
    @@person_count += 1
  end

  def self.count
    "There are #{@@person_count} people."
  end
end
```

In the above example the **class** `Person` has a variable `@@person_count` that is
incremented by one each time the class' `initialize` method is called:

```text
irb> Person.new("Bob")
irb> puts Person.stats
There are 1 people.

irb> Person.new("Jill")
irb> Person.new("Meghan")
irb> puts Person.stats
There are 3 people.
```

Class variables, like instance variables aren't available to outsiders. For
example you can't access the Person class' variable `@@person_count` from
outside the class:

```text
irb> Person.person_count
NoMethodError: undefined method `person_count' for Person:Class
```

You could expose the variable with a getter method similar to our `Person.stats`
method:

```ruby
class Person
  @@person_count = 0 # class variable, there's only one variable and value for
                     # @@person_count

  def initialize(name)
    @name = name # instance variable, different for each Person instance
    @@person_count += 1
  end

  def self.person_count
    @@person_count
  end
end
```

```text
irb> Person.person_count
=> 0
```

## Instance Variables

Instance variables are scoped to a particular instance of an object. Much like
class variables, without a getter or setter method instance variable aren't accessible
outside the instance.

Typically you'll use a class to define (and store) common *behavior* (methods that all
instances will have available) and instance variables to store unique *state*.

```ruby
class Person
  # class constant
  NICKNAME_ADJECTIVES = ["dizzy", "jazzy", "little", "big", "fresh", "junior", "cheezy"]

  def initialize(name, age, favorite_color)
    # below: three pieces of state, stored per instance of the Person class.
    # saved as instance variables
    @name = name.capitalize
    @age = age
    @favorite_color = favorite_color
  end

  # below: two behaviors (methods), shared across all instances
  def nickname
    NICKNAME_ADJECTIVES.sample.upcase + " " + @name
  end

  def birth_year
    Time.now.year - @age
  end
end
```

```text
irb> p = Person.new("nate", 32, "red")
=> #<Person:0x007fb36c355940 @name="Nate", @age=32, @favorite_color="red">
irb> p.nickname
=> "FRESH Nate"
irb> p.birth_year
=> 1982
irb> p.name
=> NoMethodError: undefined method `name' for #<Person:0x007fb36c355940>
```

Note at the end of the above irb session we aren't able to access instance
variables from outside the instance. Instance variables are scoped only to the
instance. Use a getter to expose an instance variable to the outside:

```ruby
class Person

  def initialize(name, age, favorite_color)
    @name = name.capitalize
    @age = age
    @favorite_color = favorite_color
  end

  def name
    @name
  end

  def age
    @age
  end

  def favorite_color
    @favorite_color
  end
end
```

Now, with getter instance methods available for all our instance variables, we
can access a `Person` instance's properties from outside the instance:

```text
irb> p = Person.new("Mike", 17, "orange")
=> #<Person:0x007fb36c2b7358 @name="Mike", @age=17, @favorite_color="orange">
irb> p.name
=> "Mike"
irb> p.age
=> 17
irb> p.favorite_color
=> "orange"
```

Typing all these getter methods is pretty tedious though, so Ruby has some
class methods to create getters and setters for you:

```ruby
class Person
  attr_reader :name, :age, :favorite_color # creates getters for all instance
                                           # variables

  def initialize(name, age, favorite_color)
    @name = name.capitalize
    @age = age
    @favorite_color = favorite_color
  end
end
```

```text
irb> p = Person.new("Mike", 17, "orange")
=> #<Person:0x007fb36c2b7358 @name="Mike", @age=17, @favorite_color="orange">
irb> p.name
=> "Mike"
irb> p.age
=> 17
irb> p.favorite_color
=> "orange"
```

There are a few helper methods available:

| class method    | creates                  |
|-----------------|--------------------------|
| attr_reader     | getter                   |
| attr_writer     | setter                   |
| attr_accessor   | getter & setter          |

It's tempting to think these helper methods perform magic, but the work they do
is actually quite simple:

`attr_reader :name, age` creates simple getter methods:

```ruby
def name
  @name
end

def age
  @age
end
```

`attr_writer :name, :age` creates simple setter methods:

```ruby
def name=(name)
  @name = name
end

def age=(age)
  @age = age
end
```

Note the distinctive name of the setter methods, they include an `=` as part of
the variable name. Ruby looks for methods with this naming convention when you
set an instance variable:

```ruby
p = Person.new
p.age = 18 # calls the setter method age=(age) with 18 as the only argument
```

In fact you could adjust your syntax to look a bit more like a traditional
method call:

```ruby
p = Person.new
p.age=(18)
```

Of course the former style of calling a setter is preferred.


### Custom getters & setters

Sometimes you'll want to do more than just set or return an instance variable
from a getter or setter method. Feel free to write your own methods instead of
having Ruby generate them via the `attr_` helper methods.

```ruby
class Person
  def initialize(name, age)
    @name = name.strip
    @age = age
  end

  def name
    # always return an uppercase version of the person's name
    @name.upcase
  end

  def name=(name)
    # remove any leading & trailing whitespace
    @name = name.strip
  end
end
```

```text
irb> p = Person.new("Torey", 23)
irb> puts p.name
TOREY
irb> p.name = "    mr. pink    "
irb> puts p.name
MR. PINK
```

## Local

Local variables are visible only during the scope in which they were created.
Local variables begin with a lower case letter or an underscore:

```ruby
# local variables
age = 17
_age = 17
```

In order to understand local variable scope it's important to understand when
new local scopes are created. Here are some examples of when a new scope is
created:

**Methods** define their own local scope. A local variable defined in  one method is
invisible to another:

```ruby
def random_roll
  # roll is a local variable
  roll = 1 + rand(5)
end

def jackpot?
  random_roll

  # since roll is a local variable defined in random_roll
  # we won't be able to access it here
  if roll == 6
    puts "You won the jackpot!"
  else
    puts "Unlucky! Try again."
  end
end
```

Method scope is one of the easiest to understand. In the above example, since
`roll` is a local variable defined inside the method `random_roll`, we won't be
able to access it in the other method `jackpot?`.

**Blocks** also generate new method scope in Ruby:

```ruby
[1,2,3].each do |item|
  item = item * item
end

puts item # NameError: undefined local variable or method `item' for main:Object
```

You'll use local variables more than any other type in Ruby. They're perfect for
data that you won't need to retain access to for any considerable time. Also,
local variables prevent data from leaking across your codebase, since they're
only available for the scope in which they were defined.


# Debugging

Written by [Torey Hickman](https://github.com/toreyhickman).  Based on resources written by [Tanner Welsh](https://github.com/openspectrum) and [Alyssa Diaz](https://github.com/alycit).

## Introduction
Debugging is a technique for finding and fixing errors. All programs have bugs. Therefore, the better you get at debugging, the better you will be at programming.

Debugging is great for fixing problems in your code. It will not necessarily lead you to fixing problems in your thinking.  Furthermore, debugging will not be very useful unless you first understand the problem the code is supposed to solve.

## Debugging Steps
An example debugging process is described in the following steps; this approach will be effective for some people while others will develop their own.


1.  **Isolate the error**  
  Where is the source of the error?
  
2.  **Visualize state**  
  What are the values of variables when the error occurs?
  
3.  **Compare expected to actual state**  
  How does the state differ from my conception of what it should be?
  
4.  **Generate a hypothesis**  
  Why does this dissonance exist?
  
5.  **Modify with purpose**  
  Make changes to the code which directly solve for the conditions in your hypothesis.
  
6.  **Test and iterate**  
  Ensure that the code works as intended; repeat steps above until success is reached.


### Isolate the Error
In isolating the error, we want to identify, as best as possible, where the error is occuring.  A great first step when confronted with an error is to **read the error message**.  Often, the error message will identify the file and line number where the error occured and provide some context about what went wrong.

Consider the following bit of code.

```ruby
def show_me_errors
  (0..4).each do |num|
    something << num
  end

  something
end

puts show_me_errors
```

If we ran this code, we would receive the following error message.

```
show_me_errors.rb:3:in `block in show_me_errors': undefined local variable or method 'something' for main:Object (NameError)
  from show_me_errors.rb:2:in `each'
  from show_me_errors.rb:2:in `show_me_errors'
  from show_me_errors.rb:9:in `<main>'
```

There's a lot of information that we can gather.  First, I can see that in the file `show_me_errors.rb`, the error occured on Line 3.  I also know that there is an `undefined local variable or method 'something'`; in others words, Ruby hit a reference to `something` and didn't know what it was.  Furthermore, by looking at the stack trace—beginning at the bottom of the error message—I can see how the program reached the error point:  the `show_me_errors` method was called on Line 9, the method is run, and the error occurs during the call to `#each`.  Looking at the block passed to the `#each` method, I see that the code is attempting to call the `#<<` method on `something`.  At this point, I have isolated the error to there being no `something` in the scope of the block.

### Visualize State
Often, we run into errors where we think a variable is referencing an object with a specific value, but it's actual value is something different.  Sometimes our expectations are close, and sometime they're not.  It can be helpful to visualize the value of our variables at specific points in our program—isolating the error, as described above, gives us a clue as to where we should look to visualize the state of our program (e.g., variables).

Consider the following code sample.

```ruby
def see_into_code(number)
  x = 0
  result = []

  until x == number
    result << x
  end

  result
end

puts see_into_code(10)
```

Running the preceeding code results in an infinite loop.  We think that our code should break out of the `until` loop when `x == number` but it never happens.

There are a couple approaches that you can take to visualize your variables.  One simple, common approach is to insert `puts` statements.  In the code above, I know that I'm not breaking out of the `until` loop.  Breaking out of the loop depends on the values of `x` and `number`.  By inserting a couple of `puts` statements within the loop, I will be able to see how the values of `x` and `number` change for each iteration of the loop ... or if they change.  

```ruby
def see_into_code(number)
  x = 0
  result = []

  until x == number
    puts "The value of varaible 'x' is #{x}."
    puts "The value of varaible 'number' is #{number}."
  
    result << x
  end

  result
end

puts see_into_code(10)
```

`puts` statements can be an effective tool for debugging, but they don't belong in your production code.  Remove them once you've debugged your code.

An alternative is to use a debugger.  Debuggers are used somewhat similarly to `puts` statements, but they are more robust, allowing you to explore the state of your program as it's running, rather than declaring before runtime which variables you want to see.  There are a few gems to choose from. Examples include ... 

- [debugger](https://rubygems.org/gems/debugger)
- [byebug](https://rubygems.org/gems/byebug)
- [pry](https://rubygems.org/gems/pry)

Each of these are gems that would need to be required in your program (e.g., `require 'debugger'`).  Then, similarly to placing `puts` statements where we've isolated the error, we call for the debugger.

```ruby
require 'debugger'

def see_into_code(number)
  x = 0
  result = []

  until x == number
  debugger
    
    result << x
  end

  result
end

puts see_into_code(10)
```

When the code is run and the call to the debugger is made, an interactive irb-like session will begin, showing the line number where execution was halted and the surrounding lines of code:

```
see_into_code.rb:10
result << x

[5, 14] in show_me_errors.rb
   5    result = []
   6  
   7    until x == number
   8    debugger
   9  
=> 10      result << x
   11    end
   12  
   13    result
   14  end
(rdb:1) x
0
(rdb:1) number
10
(rdb:1) result
[]
```

We can then interact with the program.  In the example above, I've retrieved the values of the variables `x`, `number`, and `result`.  The values are `0`, `10`, and `[]`, as I would expect, so all looks good.  

When I'm done exploring, I can run the `continue` command to resume execution, which will halt again when the next call to the debugger is reached—in this case, the next iteration of the `until` loop.

```
(rdb:1) continue
show_me_errors.rb:10
result << x

[5, 14] in show_me_errors.rb
   5    result = []
   6  
   7    until x == number
   8    debugger
   9  
=> 10      result << x
   11    end
   12  
   13    result
   14  end
(rdb:1) x
0
(rdb:1) number
10
(rdb:1) result
[0]  
```

In this next iteration of the `until` loop, I've again retrieved the values of the variables `x`, `number`, and `result`.  I can see that `number` is still `10` and the array `result` now contains the previous value of `x`, `0`, as expected.  However, `x` has not changed; it was `0` in the last iteration and `0` in this iteration.  That's not what I expected; I expected it to be `1`.  `x` should increment until it equals `number`, so I now know that I forgot to increment `x`.  I can enter the `exit` command to stop running the program and then fix the code:

```ruby
def see_into_code(number)
  x = 0
  result = []

  until x == number
    result << x
    x += 1
  end

  result
end

puts see_into_code(10)
```

###Compare Expected to Actual
In debugging it's important to know what you expect to happen when your code runs.  For example given `name = "John"`, I expect `name.upcase` to return the string `"JOHN"`.  In the earlier example, where I was iterating `until` a condition was met, I expected `x` to be `0` during the first iteration of the loop and then be `1` during the next iteration.  Only by having an expectation was I able to see that the actual value was not what I wanted.

Writing tests is a great way to compare expected values to actual values.

```ruby
describe "#convert_to_pig_latin" do
  context "when a word begins with a vowel" do
    it "returns the word" do
      word = "ahoy"
      expect(convert_to_pig_latin word).to eq word
    end
  end
  context "when the word begins with a consonant" do
    it "moves opening consonants to the end and then appends 'ay'" do
      word = "boy"
      expect(convert_to_pig_latin word).to eq "oybay"
    end
  end
end
```

Given the following `convert_to_pig_latin` method ...

```ruby
def convert_to_pig_latin(word)
  return word
end
```

... the second test example will fail, and the rspec output will let us know what we *expected* and also what we *got* when running the method.


```
Failures:

  1) #convert_to_pig_latin when the word begins with a consonant moves opening consonants  
     to the end and then appends 'ay'
     
     Failure/Error: expect(convert_to_pig_latin word).to eq "oybay"
       
       expected: "oybay"
            got: "boy"
       
       (compared using ==)
```

I know that when my method receives an argument beginning with a consonant (e.g., "boy"), it just returns the same word rather than converting it as I would expect.  I can now focus my efforts on making a fix targeted to making this test pass.

### Generate a Hypothesis
When we encounter a situation where our code is not operating as we think it should, we obviosly need to fix the code.  We can use the previous steps (i.e., isolating the error, visualizing state, and comparing expected values to actual values) to gether information about our program, but we still need to determine what is causing the bug.

Sometimes the error will be clear.  At other times, it won't.  If you encounter a situation where you aren't sure what is causing an error, resist the urge to just start making changes.  Generate the best hypothesis possible:  "changing Line X to ... will ...".  

### Modify with Purpose

Make the change identified in your hypothesis ...

### Test and Iterate
... and run the code to see what happens.  Did it work?  Great.  If not, decide the best course of action.  Do you need to go back to the previous code?  Was this one change necessary but not sufficient to fix the bug?  You'll have to use your best judgement, but don't guess.

# Developing an Intuition for Regex

## Overview

Here's everything you need to know about regular expressions in one pithy quote:

> Some people, when confronted with a problem, think “I know, I’ll use regular expressions.” Now they have two problems.
> - Jamie Zawinski

The goal of this investigation is to expose you to regular expressions from many sides.

Here's the funny side, a [diversion](http://xkcd.com/208/)

By the end you should have an intuitive sense of what regular expressions are, when (and when not) to use them and how to read and write them like a pro.

*Give yourself at least 1 hour for this work and be patient with yourself.  You can spend a whole day or more here if you want to but the fact is regular expressions are most often used for specialized cases so don't over do it.  When you really need to dig in, all this content, these tools, these ideas ... they're publicly available for you to come back to.*

Move around the content like an explorer. You do NOT need to work in order from top to bottom.  You *could* work from most interesting to least interesting, or, if you can swing it, try to work in whatever order you find that keeps you most focused and engaged on the learning, creating and resolving feelings of confusion, switching up as needed to keep yourself fresh and alert, wondering, at the edge of your seat, what's around the next corner -- with some bathroom breaks in between, of course.

Ok, enough chatter, here's the goods.

## Learning Competencies

- read and write regular expressions fluently
- recognize common regex patterns
- estimate regex complexity intuitively
- gain exposure to various tools and techniques for learning
- develop an intuitive understanding for a new topic through deep and varied exposure
- learn to recognize "good" learning resources from "bad" through massive, directed exposure
- gain an appreciation for multiple representations of a single concept
- develop a deeper self-awareness for maintaining your high performance learning edge
- become aware of various thought leaders and forums where thought leaders congregate

## Activities

- Step 1: scan this entire list
- Step 2: pick somewhere to start
- Step 3: you win!


### Read a few (!) books

Read [this chapter](http://regex.learncodethehardway.org/book/introduction.html) of a book you'll revisit in another activity.  This is a quick intro to regex.

Read [this chapter](http://eloquentjavascript.net/2nd_edition/preview/09_regexp.html) of a [great book](http://eloquentjavascript.net) that you WILL NOT be distracted by until you are asked to focus on Javascript because you know what's good for you.

Now, this will be a bit tricky because you should *ignore* the syntax that isn't related to regex.  how do you recognize a regex?  most systems use the forward slash (/) to start and end a regex.  here's one: /./  amazing huh?  it matches a single character.  any printable character actually.

Ok, now go read.  and look for those slashes!   pay attention to what's inside them.

### Watch a video

Did you read the last chapter?  If you didn't then make sure you don't forget to go back to at some point.  It's worth it!

Ok, here's a [video](http://www.youtube.com/watch?v=EkluES9Rvak) from [Fluent 2012](http://fluentconf.com/fluent2014) by [Lea Verou](http://lea.verou.me/about/).  She has a charming Greek accent which I'm sure you'll find distracting at first but -- check this out -- you'll probably start thinking about regex in a Greek accent!  Won't that be fun?!

Oh, there were 3 links in the previous paragraph -- go take a peek at the Fluent conference, you might want to attend this year or next.  And have a glance at Lea's web page.  What kind of work does she do?  What makes her qualified to give this talk?

Getting to know the people in **your** new community (yes! pinch yourself) is an important part of becoming a software developer.

### Identify the best tools

Check these out:

- http://rubular.com
- http://www.regexper.com


### Focus on the concept, not the syntax

Something that often happens with learning a new representation is we get all hung up on the details of the dits and dots and forget to practice a new way of thinking.

What you should be thinking about regex now, if your brain isn't fried, is this:

- there's no flow in regex, no movement of code.  they're basically a pattern (like an [apple corer](http://www.webstaurantstore.com/clean-cut-apple-corer/32711508.html?utm_source=Shopzilla&utm_medium=cse&utm_campaign=Shopzilla+Campaign)) that gets pressed up against some text (like an [apple](http://www.cricketbread.com/images/apple_cored.jpg)) and out comes the matches!

- with only a few bits of syntax i can do a lot -- i should probably keep it simple.  complex regex are hard to read, no?  imagine how hard that would be to debug.  consider this bit of wisdom:

> “Debugging is twice as hard as writing the code in the first place. Therefore, if you write the code as cleverly as possible, you are, by definition, not smart enough to debug it.”
> - Brian Kernighan

If you liked that, go read [a few of these](http://www.hackification.com/2008/12/23/a-double-handful-of-programming-quotes/) and make sure to lookup all the accredited folks too, this is your new community after all.

- regex seems to require a parser of some kind, like an engine that knows how to interpret the syntax.  nice catch!  here's the [regex engine: Onigurama](http://www.geocities.jp/kosako3/oniguruma/) behind Ruby's regex implementation that I first read about [here](http://patshaughnessy.net/2012/4/3/exploring-rubys-regular-expression-algorithm).  Apparently Ruby 2.0 is using a fork of Onigurama called [Onigmo](https://github.com/k-takata/Onigmo).  Go figure.


### Get massive amounts of exposure

Read the following articles

- http://www.codinghorror.com/blog/2008/06/regular-expressions-now-you-have-two-problems.html
- http://net.tutsplus.com/tutorials/other/8-regular-expressions-you-should-know/

Read a book!  Yes, another.  Well, same one as above, but now there's more.

Well, you don't actually have to "read" it cover to cover, just scan the entire thing -- yes, all the content from end to end -- and, when you find something unfamiliar, stop and look closer.  If this is the first activity you do, you'll end up spending a lot of time on this book.  That may be a good thing or a bad thing, but I prefer to go for a couple quick hits like the links above or a video to get my bearings before I start scanning books.  Anyway, read the headers, look for new stuff, stop and read what catches your interest.  Keep up the pace!  Your goal is to expose yourself to a massive volume of content and, in this case, examples of regular expressions.

- http://regex.learncodethehardway.org/book/


### Play a game

Grab a pair (or two) and play this game against each other.  You can make up the rules but you've basically got all the ingredients you need for some serious competition -- points!

- http://regex.alf.nu/

Here's another one if you're feeling frisky

- http://regexcrossword.com/

### Stretch yourself into a painful new pose

Have you heard of Peter Norvig?

Check out this high brow geekery: http://nbviewer.ipython.org/url/norvig.com/ipython/xkcd1313.ipynb


### Consider a new representation

Have you heard of [Regexper](http://www.regexper.com/)? It's pretty sweet AND (bonus!) it's [written in Ruby](https://github.com/javallone/regexper)

Here's what it does: you give it a regex and it generates a bunch of SVG elements that make a [railroad diagram](http://en.wikipedia.org/wiki/Syntax_diagram) to help you interpret the regex.

Check it out: (these regex's are all taken from the Nettuts tutorial above)

---

**match a username:** `/^[a-z0-9_-]{3,16}$/`

![image of regex](http://f.cl.ly/items/2G290h0l0Y1i3j3k3U2r/Screen%20shot%202014-01-14%20at%2010.00.26%20PM.png "match a username")

---

**match a password:** `/^[a-z0-9_-]{6,18}$/`

![image of regex](http://f.cl.ly/items/0z031E1W0S3d132o3r35/Screen%20shot%202014-01-14%20at%2010.01.42%20PM.png "match a password")

---

**match a hex value:** `/^#?([a-f0-9]{6}|[a-f0-9]{3})$/`

![image of regex](http://f.cl.ly/items/043N3G2Z0c14160v1S3C/Screen%20shot%202014-01-14%20at%2010.02.07%20PM.png "match a hex value")

---

**match a slug:** `/^[a-z0-9-]+$/`

![image of regex](http://f.cl.ly/items/161g393v2u3D261Q1x0t/Screen%20shot%202014-01-14%20at%2010.02.28%20PM.png "match a slug")

---

**match an email:** `/^([a-z0-9_\.-]+)@([\da-z\.-]+)\.([a-z\.]{2,6})$/`

![image of regex](http://f.cl.ly/items/2K2Q3N011R402w2p3o1z/Screen%20shot%202014-01-14%20at%2010.02.49%20PM.png "match an email")

---

**match a url:** `/^(https?:\/\/)?([\da-z\.-]+)\.([a-z\.]{2,6})([\/\w \.-]*)*\/?$/`

![image of regex](http://f.cl.ly/items/411G1m3Q3r3R3M2X2m1V/Screen%20shot%202014-01-14%20at%2010.03.17%20PM.png "match a url")

---

**match an ip address:** `/^(?:(?:25[0-5]|2[0-4][0-9]|[01]?[0-9][0-9]?)\.){3}(?:25[0-5]|2[0-4][0-9]|[01]?[0-9][0-9]?)$/`

![image of regex](http://f.cl.ly/items/411w1M2k2Y2e2P2v1a3p/Screen%20shot%202014-01-14%20at%2010.03.58%20PM.png "match an ip address")

---

**match an html tag:** `/^<([a-z]+)([^<]+)*(?:>(.*)<\/\1>|\s+\/>)$/`

![image of regex](http://f.cl.ly/items/3Q0B3L2E1Y192P2E443A/Screen%20shot%202014-01-14%20at%2010.04.30%20PM.png "match an html tag")


# Single Responsibility Methods

## Introduction
Writing methods with a single responsibility is a practice that is stressed in Phase 1.  The idea is that every method should do just one thing (i.e., have one responsibility).

## Breaking Down a Method
On Monday you were presented with a [design drill challenge dealing with method chaining](../../../../../design-drill-method-chaining-challenge).  Release 1 asked you to refactor a `squared_primes` method.

```ruby
# FIXME: This is convoluted. Refactor for clarity.
def squared_primes(array)
  array.find_all{|x| (2..x-1).select(){|i| x % i == 0 }.count == 0 }.map{|p| p*p}
end
```

Looking at this method, it doesn't look all that complex.  It's hard to read because of the method chaining, the nested blocks within blocks, and unnecessary parentheses, but it can be cleaned up fairly easily:

```ruby
def squared_primes(numbers)
  # find the primes
  primes = numbers.find_all do |x|
    (2..x-1).select { |i| x % i == 0 }.count == 0
  end

  # square the primes
  primes.map{ |p| p * p }
end
```

It's now much more readable.  We find the prime numbers in the `numbers` argument and then square each of those prime numbers.  Just that simple refactor and explanation makes it obvious that this method has multiple bits of logic tucked inside itself.  The clue is that the method does that *and* that.

Ask yourself, "What is the responsibility of this method?"

It receives an array of integers and it returns another array that includes the square of any prime number in the argument array.

In it's current form, it's doing much more than that.  At a minimum, it is ...

1. determining what it means for a number to be prime.  
   `{ |x| (2..x-1).select { |i| x % i == 0 }.count == 0 }`

2. determining how to square a number.  
  `{ |p| p * p }`

Furthermore, in the way the method identifies prime numbers in an array and squares all numbers in an array, it is hiding even more logic, which we'll see later.

For now, a simple refactor would be to extract identifying primes in an array and squaring numbers in an array:

```ruby
def squared_primes(numbers)
  primes = primes_in(numbers)
  square_all(primes)
end

def primes_in(numbers)
  numbers.find_all do |x|
    (2..x-1).select{ |i| x % i == 0 }.count == 0
  end
end

def square_all(numbers)
  numbers.map { |p| p * p }
end
```

And we can then make the code of `#squared_primes` even more concise:

```ruby
def squared_primes(numbers)
  square_all primes_in(numbers)
end

def primes_in(numbers)
  numbers.find_all do |x|
    (2..x-1).select { |i| x % i == 0 }.count == 0
  end
end

def square_all(numbers)
  numbers.map { |p| p * p }
end
```

The purpose of the `#squared_primes` method is now very clear.  With our well named methods, if anyone wonders what the `#squared_primes` method does, all they have to do is read the code:  given an array of numbers, the method will `square_all primes_in(numbers)`.

In addition to a method whose code is readable and whose purpose is clear, we've gained a couple of methods that might prove useful in the future.  There is a method for finding prime numbers in an array and another method that will square all numbers in an array.

However, our new methods are hiding logic of their own.

The `#square_all` method hides how to square a number within the block that it passes to `#map`.  We can extract squaring a number into its own method, giving us the possibility to square any number we want in the future—just pass the number to the `#square` method.

```ruby
def squared_primes(numbers)
  square_all primes_in(numbers)
end

def primes_in(numbers)
  numbers.find_all do |x|
    (2..x-1).select { |i| x % i == 0 }.count == 0
  end
end

def square_all(numbers)
  numbers.map { |p| square(p) }
end

def square(number)
  number * number
end
```

There is even more logic tucked away within the `#primes_in` method.  The block passed to the `#find_all` method identifies whether or not a number is prime.  We can move that to its own method.

```ruby
def squared_primes(numbers)
  square_all primes_in(numbers)
end

def primes_in(numbers)
  numbers.find_all { |number| is_prime?(number) }
end

def is_prime?(number)
  (2..number-1).select { |i| number % i == 0 }.count == 0
end

def square_all(numbers)
  numbers.map { |p| square(p) }
end

def square(number)
  number * number
end
```

Our new `#is_prime?` method can now be used any time we might need to determine whether or not an `Integer` is prime.  What is this method really doing?  If we look at the code, it's determining whether or not a number has factors other than 1 and itself.  Let's extract finding factors other than 1 and self into its own method.

```ruby
def squared_primes(numbers)
  square_all primes_in(numbers)
end

def primes_in(numbers)
  numbers.find_all { |number| is_prime?(number) }
end

def is_prime?(number)
  number > 1 && !has_factors_other_than_one_and_self?(number)
end

def has_factors_other_than_one_and_self?(number)
  (2..number-1).select { |divisor| number % divisor == 0 }.any?
end

def square_all(numbers)
  numbers.map { |p| square(p) }
end

def square(number)
  number * number
end
```

We've now described in the `#is_prime?` method what it means to be prime: (1) a number is greater than 1 and (2) it has no factors other than 1 and itself.  1 is not considered to be prime.  This logic around 1 was not present in the original method, but is being introduced here to be mathematically correct.

And, we have another method that we might reuse later:  `#has_factors_other_than_one_and_self?`.  This method can be broken down itself.  It's purpose is to identify whether the factors of a number includes any value other than 1 and the number itself.  Finding the factors is not its responsibility; that should belong in another method.

```ruby
def squared_primes(numbers)
  square_all primes_in(numbers)
end

def primes_in(numbers)
  numbers.find_all { |number| is_prime?(number) }
end

def is_prime?(number)
  number > 1 && !has_factors_other_than_one_and_self?(number)
end

def has_factors_other_than_one_and_self?(number)
  (factors(number) - [1, number]).any?
end

def factors(number)
  (1..number).select { |divisor| number % divisor == 0 }
end

def square_all(numbers)
  numbers.map { |p| square(p) }
end

def square(number)
  number * number
end
```

We now have a `#factors` method that will return the factors of any number.  As you might have guessed, there's more logic to be extracted from this new method.  There are two things.  First, the method identifies the possible factors of `number`:  `(1..number)`.  Second, in determining whether or not a possible factor is in deed a factor, the block tests whether `number` is evenly divisible by the possible factor.  Both of these can be extracted to their own methods.

```ruby
def squared_primes(numbers)
  square_all primes_in(numbers)
end

def primes_in(numbers)
  numbers.find_all { |number| is_prime?(number) }
end

def is_prime?(number)
  number > 1 && !has_factors_other_than_one_and_self?(number)
end

def has_factors_other_than_one_and_self?(number)
  (factors(number) - [1, number]).any?
end

def factors(number)
  possible_factors(number).select { |divisor| evenly_divisible?(number, divisor) }
end

def possible_factors(number)
  (1..number)
end

def evenly_divisible?(dividend, divisor)
  (dividend % divisor).zero?
end

def square_all(numbers)
  numbers.map { |p| square(p) }
end

def square(number)
  number * number
end
```
## Conclusion
At this point, we've taken a largely illegible method, refactored it to make it more readable, and piece-by-piece extracted out all the tiny bits of logic being done.  It might seem like a lot of extra work to take a working method and make changes that provide no immediate gains.

However, consider Wednesday's [prime factors challenge](../../../../algorithm-drill-prime-factors-challenge).  What does that challenge entail?  Finding a numbers factors?  Determining whether or not a number is prime?  I can complete the prime factors challenge, relying largely on the individual methods extracted from the `#squared_primes` method to do the heavy lifting.

```ruby
def prime_factors(number)
  return Array.new unless number > 1

  first_prime_factor = primes_in(factors(number)).first
  [first_prime_factor] + prime_factors(number / first_prime_factor)
end
```

Code reuse in action.  This would not have been possible if the logic from the `#square_primes` method had been left tucked away inside that method.