# PHP

For the most part, this is very similar to the C coding style. The main differences are:

* Our PHP style tends to use parentheses around all language constructs, except `echo` (e.g.: `require()`, `include()`, `exit()`)

* Coding in PHP allows for use of function calls inside of conditional statements more freely. An example: `if (isset($var))` or `if (!empty($var))`

* In PHP, using the implicit types of conditional expressions are okay - things like `if ($something)` or `if (!$something)` where we frown on those in C

## Spacing

* A single space between a control statement and opening parentheses.

    `if (` not `if(`, `for (` not `for(`

* A single space between the closing parentheses and opening bracket for non-function control statements

    `if ($something) {` not `if ($something){`

* Spaces on either side of comparison and assignment operators

    `$a = $b`, not `$a=$b`, `if ($a == $b)` not `if ($a==$b)`

* Passing and defining arguments should be spaced properly. At least one space must exist between a comma and the next argument.

    ```
    some_function($arg1, $arg2, $arg3)
    function function_definition($arg1, $arg2, $arg3)
    ```

    not

    ```
    some_function($arg1,$arg2,$arg3)
    function function_definition($arg1,$arg2,$arg3)
    ```

* When using bitwise operators, appropriate spacing is appreciated.

    ```
    $var = FLAG1 | FLAG2 | FLAG3;
    ```

    not

    ```
    $var = FLAG1|FLAG2|FLAG3;
    ```

## Language Constructs

* All language constructs should look as if they are functions. Call their arguments with parentheses, except in the case of `echo`.

    ```
    require_once($somefile);
    ```

    not

    ```
    require_once $somefile;
    ```

## Brackets

* Opening bracket for function definitions is on it's own line, with no indentation

    ```
    function somefunction()
    {
    ```

    not

    ```
    function somefunction() {
    ```

* Always wrap control statements in brackets, even if there is only one operation and brackets are unnecessary

    ```
    if ($something) {
        printf("hi\n");
    }
    ```

    not

    ```
    if ($something)
        printf("hi\n");
    ```

* Opening bracket for all control statements followed by a newline

    `if ($something) {\n` not `if ($something) { do_stuff(); }`

* Closing bracket is at the same indentation as the control statement of the opening bracket

    ```
    if ($something) {
        dosomething();
    }
    ```

    not

    ```
    if ($something) {
        dosomething();
            }
    ```

## Indentation

* Use spaces instead of tabs. Each indentation is 4 spaces. When introducing some control structure, the code inside of it becomes indented 1 indentation, recursively

    ```
    if ($something) {
        if ($somethingelse) {
            do {
                $this_is_indented = true;
            } while ($somethinghappened)
        }
    }
    ```

    not

    ```
    if ($something) {
        if ($somethingelse) {
                do {
                        $this_is_indented = true;
                } while ($somethinghappened)
        }
    }
    ```

## Comments

* Comments are ***A Good Thing*** when used appropriately. Comments are useful for explaining 
  what a block of code does. I don't need to be told "increment variable x and then print modulus 7". 
  That would likely be obvious, but explaining the reason for doing it might be okay.

    ```
    // printed output is part of a larger expression
    // this is only a part. see function start_print()
    $x++;
    printf("%d", $x % 7);
    ```

    not

    ```
    // increment x and print modulus 7
    $x++;
    printf("%d", $x % 7);
    ```

    See the difference? Also, let's take a look at the following *actual* code:

    ```
    for ($i = 0; $i < $nfds; $i++) {
        $fd = 0;
        $s = null;

        $fd = $iobs->ep_events[$i]->data->fd;
        if ($fd < 0 || $fd > $iobs->max_fds) {
            continue;
        }
        $s = $iobs->iobroker_fds[$fd];

        if ($s) {
            $s->handler($fd, $iobs->ep_events[$i].events, $s->arg);
            $ret++;
        }
    }
    ```

    What the heck is happening here? Let's see the difference some comments make:

    ```
    // loop through each possible file descriptor
    for ($i = 0; $i < $nfds; $i++) {
        $fd = 0;
        $s = null;

        // grab a file descriptor from our
        // iobroker set and do some sanity checking
        $fd = $iobs->ep_events[$i]->data->fd;
        if ($fd < 0 || $fd > $iobs->max_fds) {
            continue;
        }

        // grab our file descriptor set
        $s = $iobs->iobroker_fds[$fd];

        if ($s) {

            // handler is the callback that was registered
            // when this iobroker fd set was created. we
            // pass the event data and argument (set at creation)
            $s->handler($fd, $iobs->ep_events[$i].events, $s->arg);
            $ret++;
        }
    }
    ```

* Comments never happen on the same line as code, always before

    ```
    // this starts a block
    if ($something) {
    ```

    not

    ```
    if ($something) { // this starts a block
    ```

* Multiline comments are at the discretion of the coder, there is no preference of which style to use - as long as
  the comment itself is readable. Try and keep the starting column of the text aligned.

    ```
    /*
        This is fine
        just like this
    */
    ```

    or

    ```
    /* This is fine
       just like this */
    ```

    or

    ```
    /*
     * This is fine
     * just like this
     */
    ```

    or

    ```
    //
    // this is fine
    // just like this
    //
    ```

## Control statements

* No unecessarily advanced control statements. Try not to mix assignment and comparison.

    ```
    $my_string = "some text";
    if ($my_string == NULL) {
        return ERROR;
    }
    ```

    not

    ```
    if (($my_string = "some text") == NULL) {
        return ERROR;
    }
    ```

* During a comparison, the variable should be on the left hand side

    ```
    if ($var == NULL)
    ```

    not

    ```
    if (NULL == $var)
    ```

* Unlike the C style guide, we allow (and encourage) the use of functions in a control statement - if that
  functions primary purpose is to be tested (e.g.: a helper function)

    ```
    if (!isset($var)) {
        return false;
    }
    ```

    or

    ```
    if (some_helper_function($var)) {
        return true;
    }
    ```

    *still not*

    ```
    if (($ret = isset($var)) == false) {
        return false;
    }
    ```

* When you need to break up conditional statements over a series of lines, make sure the logical operator is at the beginning
  of the line (not the end). When this happens, ensure there is an additional newline after the end of the opening bracket.
  Use your common sense. It may even be advantageous to put the opening bracket on its own to help with spacing and
  orientation.

    ```
    if ($something
        && $somethingelse) {

        do_something();
    }
    ```

    not

    ```
    if ($something &&
        $somethingelse) {

        do_something();
    }
    ```

    or

    ```
    if ($something
        && $somethingelse) {
        do_something();
    }
    ```

* Be defensive by default: try and always return in a negative sense, and only positive when a condition has been met (whitelist instead of blacklist)

    ```
    function is_good_string($str)
    {
        if (!$str) {
            return FALSE;
        }

        if ($str === "good") {
            return TRUE;
        }

        return FALSE;
    }
    ```

    not

    ```
    function is_good_string($str)
    {
        if (!$str) {
            return FALSE;
        }

        if ($str !== "good") {
            return FALSE;
        }

        return TRUE;
    }
    ```

  They may be functionally the exact same, but in the future you may need to add to it, and it is much easier to add to
  a function that EXPECTS to fail than vice versa in many cases.

## Line Length and Breaking

* Line length isn't generally an issue. But try to keep it around 80. Debugging long lines from the console isn't
  much fun. One tactic to keep line length down is to minimize your indentations. Try to break/return/etc. before you
  get to your main logic instead of wrapping it in conditionals.

    ```
    function some_function($arg1, $arg2)
    {
        if ($arg1 != 3) {
            return false;
        }

        if ($arg2 != 4) {
            return false;
        }

        some_really_long_function_call();
    }
    ```

    instead of

    ```
    function some_function($arg1, $arg2)
    {
        if ($arg1 == 3) {
            if ($arg2 == 4) {
                some_really_long_function_call();
            }
        }
    }
    ```

* When breaking a long function call:

    1. The line ends with a comma, and then the following line contains whatever
        the argument was. The line MUST NOT end with an argument and the next line with a comma.
    2. The subsequent lines must be indented one indentation.
    3. The closing parentheses and semicolon MAY either follow the last argument, or
        be present on its own line, sharing the same indentation with the opening function call.

    ```
    some_long_function_call($arg1, $arg2, $arg3, $arg4,
        $arg5,
        $arg6,
        $arg7);
    ```

    or

    ```
    some_long_function_call($arg1, $arg2, $arg3, $arg4,
        $arg5,
        $arg6,
        $arg7
    );
    ```

    not

    ```
    some_long_function_call($arg1, $arg2, $arg3, $arg4
        ,$arg5
        ,$arg6
        ,$arg7);

    ```

    or

    ```
    some_long_function_call($arg1, $arg2, $arg3, $arg4,
        $arg5,
        $arg6,
        $arg7
        );
    ```

* Following the trend set in Donald Knuth's *Computers and Typesetting* series: "Although formulas within 
    a paragraph always break after binary operations and relations, displayed formulas always break before
    binary operators". So when breaking large formulas, start new lines with the operators.

    ```
    $i = (($some_large_number * $some_other_large_number)
          + ($a_small_number * $a_negative_number)
          - ($the_integer_representation_of_pi_is_3))
    ```

    not

    ```
    $i = (($some_large_number * $some_other_large_number) +
          ($a_small_number * $a_negative_number) -
          ($the_integer_representation_of_pi_is_3))
    ```
