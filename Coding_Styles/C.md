# C

## Artistic Style

```
astyle --style=kr --pad-oper --pad-header --add-brackets --break-closing-brackets --convert-tabs --max-code-length=85 --break-after-logical
```

## Spacing

* A single space between a control statement and opening parenthesis.

    `if (` not `if(`, `for (` not `for(`

* A single space between the closing parenthesis and opening bracket for non-function control statements

    `if (something) {` not `if (something){`

* Spaces on either side of comparison and assignment operators

    `a = b`, not `a=b`, `if (a == b)` not `if (a==b)`

* Passing and defining arguments should be spaced properly. At least one space must exist between a comma and the next argument.

    ```
    some_function(arg1, arg2, arg3)
    int function_definition(int arg1, int arg2, int arg3)
    ```

    not

    ```
    some_function(arg1,arg2,arg3)
    int function_definition(int arg1,int arg2,int arg3)
    ```

* When using bitwise operators, appropriate spacing is appreciated.

    ```
    int var = FLAG1 | FLAG2 | FLAG3;
    ```

    not

    ```
    int var = FLAG1|FLAG2|FLAG3;
    ```

## Brackets

* Opening bracket for function definitions is on it's own line, with no indentation

    ```
    void somefunction()
    {
    ```

    not

    ```
    void somefunction() {
    ```


* Always wrap control statements in brackets, even if there is only one operation and brackets are unnecessary

    ```
    if (something) {
        printf("hi\n");
    }
    ```

    not

    ```
    if (something)
        printf("hi\n");
    ```


* Opening bracket for all control statements followed by a newline - **EXCEPT** in a macro definition

    `if (something) {\n` not `if (something) { do_stuff; }`


* Closing bracket is at the same indentation as the control statement of the opening bracket

    ```
    if (something) {
        dosomething();
    }
    ```

    not

    ```
    if (something) {
        dosomething();
            }
    ```


## Indentation

* Use spaces instead of tabs. Each indentation is 4 spaces. When introducing some control structure, the code inside of it becomes indented 1 indentation, recursively

    ```
    if (something) {
        if (somethingelse) {
            do {
                this_is_indented = true;
            } while (somethinghappened)
        }
    }
    ```

    not

    ```
    if (something) {
        if (somethingelse) {
                do {
                        this_is_indented = true;
                } while (somethinghappened)
        }
    }
    ```

## Comments

* Comments are ***A Good Thing*** when used appropriately. Comments are useful for explaining 
  what a block of code does. I don't need to be told "increment variable x and then print modulus 7". 
  That would likely be obvious, but explaining the reason for doing it might be okay.

    ```
    /* printed output is part of a larger expression
       this is only a part. see function start_print() */
    x++;
    printf("%d", x % 7);
    ```

    not

    ```
    /* increment x and print modulus 7 */
    x++;
    printf("%d", x % 7);
    ```

    See the difference? Also, let's take a look at the following *actual* code:

    ```
    for (i = 0; i < nfds; i++) {
        int         fd;
        iobroker_fd *s = NULL;

        fd = iobs->ep_events[i].data.fd;
        if (fd < 0 || fd > iobs->max_fds) {
            continue;
        }
        s = iobs->iobroker_fds[fd];

        if (s) {
            s->handler(fd, iobs->ep_events[i].events, s->arg);
            ret++;
        }
    }
    ```

    What the heck is happening here? Let's see the difference some comments make:

    ```
    /* loop through each possible file descriptor */
    for (i = 0; i < nfds; i++) {
        int         fd;
        iobroker_fd *s = NULL;

        /* grab a file descriptor from our
           iobroker set and do some sanity checking */
        fd = iobs->ep_events[i].data.fd;
        if (fd < 0 || fd > iobs->max_fds) {
            continue;
        }

        /* grab our file descriptor set */
        s = iobs->iobroker_fds[fd];

        if (s) {

            /* handler is the callback that was registered
               when this iobroker fd set was created. we
               pass the event data and argument (set at creation) */
            s->handler(fd, iobs->ep_events[i].events, s->arg);
            ret++;
        }
    }
    ```

* Comments never happen on the same line as code, always before - **EXCEPT** in a macro definition

    ```
    /* this starts a block */
    if (something) {
    ```

    not

    `if (something) { /* this starts a block */`

## Control statements

* Try and be specific in comparison statements. Explicit allows the reader to understand what you truly meant. Compare the following:

    ```
    if (something == NULL) {
        return ERROR;
    }
    ```

    vs.

    ```
    if (!something) {
        return ERROR;
    }
    ```

    While the second was easier to write, and you understand what it's checking for - the first is much more explicit and allows you to both
    know at least some information about the variable.

* No unecessarily advanced control statements. Don't mix assignment and comparison. Sometimes this may be unavoidable in do/while - use with caution.

    ```
    my_string = strdup("some text");
    if (my_string == NULL) {
        return ERROR;
    }
    ```

    not

    ```
    if ((my_string = strdup("some text")) == NULL) {
        return ERROR;
    }
    ```

* During a comparison, the variable should be on the left hand side

    ```
    if (var == NULL)
    ```

    not

    ```
    if (NULL == var)
    ```

* Try to not mix function calls and comparison where possible. Sometimes it is just easy to do it, but it does read better when broken apart.

    ```
    some_variable = do_something(flag1, flag2, flag3);
    if (some_variable == ERROR) {
        handle_the_error();
    }
    ```

    not

    ```
    if (do_something(flag1, flag2, flag3) == ERROR) {
        handle_the_error();
    }
    ```

* For `if` statements, the closing bracket of each control block (e.g.: else) shall be alone its own line

    ```
    if (something) {
        do_something();
    }
    else if (somethingelse) {
        do_something_else();
    }
    else {
        do_the_other_thing();
    }
    ```

    not

    ```
    if (something) {
        do_something();
    } else if (somethingelse) {
        do_something_else();
    } else {
        do_the_other_thing();
    }
    ```

* When you need to break up conditional statements over a series of lines, make sure the logical operator is at the beginning
  of the line (not the end). When this happens, ensure there is an additional newline after the end of the opening bracket.
  Use your common sense. It may even be advantageous to put the opening bracket on its own to help with spacing and
  orientation.

    ```
    if (something
        && somethingelse) {

        do_something();
    }
    ```

    not

    ```
    if (something &&
        somethingelse) {

        do_something();
    }
    ```

    or

    ```
    if (something
        && somethingelse) {
        do_something();
    }
    ```

* Be defensive by default: try and always return in a negative sense, and only positive when a condition has been met (whitelist instead of blacklist)

    ```
    int is_good_string(char * str)
    {
        if (str == NULL) {
            return FALSE;
        }

        if (!strcmp(str, "good")) {
            return TRUE;
        }

        return FALSE;
    }
    ```

    not

    ```
    int is_good_string(char * str)
    {
        if (str == NULL) {
            return FALSE;
        }

        if (strcmp(str, "good")) {
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
    int some_function(int arg1, int arg2)
    {
        if (arg1 != 3) {
            return false;
        }

        if (arg2 != 4) {
            return false;
        }

        some_really_long_function_call();
    }
    ```

    instead of

    ```
    int some_function(int arg1, int arg2)
    {
        if (arg1 == 3) {
            if (arg2 == 4) {
                some_really_long_function_call();
            }
        }
    }
    ```

* When breaking a long function call:

    1. The line ends with a comma, and then the following line contains whatever
        the argument was. The line MUST NOT end with an argument and the next line with a comma.
    2. The subsequent lines must be indented one indentation.
    3. The closing parenthesis and semicolon MAY either follow the last argument, or
        be present on its own line, sharing the same indentation with the opening function call.


    ```
    some_long_function_call(arg1, arg2, arg3, arg4,
        arg5,
        arg6,
        arg7);
    ```

    or

    ```
    some_long_function_call(arg1, arg2, arg3, arg4,
        arg5,
        arg6,
        arg7
    );
    ```

    not

    ```
    some_long_function_call(arg1, arg2, arg3, arg4
        ,arg5
        ,arg6
        ,arg7);

    ```

    or

    ```
    some_long_function_call(arg1, arg2, arg3, arg4,
        arg5,
        arg6,
        arg7
        );
    ```

* Following the trend set in Donald Knuth's *Computers and Typesetting* series: "Although formulas within 
    a paragraph always break after binary operations and relations, displayed formulas always break before
    binary operators". So when breaking large formulas, start new lines with the operators.

    ```
    int i = ((some_large_number * some_other_large_number)
            + (a_small_number * a_negative_number)
            - (the_integer_representation_of_pi_is_3))
    ```

    not

    ```
    int i = ((some_large_number * some_other_large_number) +
            (a_small_number * a_negative_number) -
            (the_integer_representation_of_pi_is_3))
    ```
