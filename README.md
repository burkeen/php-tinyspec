# Tiny TDD for PHP

php-tinyspec is a one-file framework for test-driven development in PHP 5.3+

## A simple spec

    \Spec\describe('Calculator')->add(array(
      'The __constructor' => array(
        'can be called with no arguments' => function() {
          new Calculator();
        }
      ),
      'Operations' => array(
        'topic' => function() { return new Calculator(); },
        'sum works with floats' => function($topic) {
          $topic->sum(1.5, 2.5);
          \Spec\assert::must(4 == $topic->result);
        },
        'sum fails with strings' => function($topic) {
          \Spec\assert::throws('cannot sum strings');
          $topic->sum('left', 'right');
        }
      )
    ))->run();

The result of running the specs:

    % php example.php
    Calculator:
      The __constructor:
        - can be called with no arguments:                              PASS
      Operations:
        - sum works with floats:                                        PASS
        - sum fails with strings:                                       PASS

    Expectations: 3, passed: 3, failed 0; 100.00% successful.

## Assertions

- **throws**($needle)

   Executed after the spec to validate an exception with the given message was
   thrown. Fails when no exception was encountered or the message did not
   contain `$needle`.

- **is_true**($subject, $message)

   Strict `$subject === true`

- **is_not_true**($subject, $message)

   Strict `$subject !== true`

- **is_false**($subject, $message)

   Strict `$subject === false`

- **is_not_false**($subject, $message)

   Strict `$subject !== false`

- **is_null**($subject, $message)

   Strict `$subject === null`

- **is_not_null**($subject, $message)

   Strict `$subject !== null`

- **key_missing**($array, $key, $message = null)

   Validate `$key` exists in `$array` even if its value is `NULL`.

- **key_not_missing**($array, $key, $message = null)

   Validate `$key` is missing in `$array`.

- **is_array**($subject, $message = null)<br \/>
  **is_bool**($subject, $message = null)<br \/>
  **is_callable**($subject, $message = null)<br \/>
  **is_double**($subject, $message = null)<br \/>
  **is_float**($subject, $message = null)<br \/>
  **is_int**($subject, $message = null)<br \/>
  **is_integer**($subject, $message = null)<br \/>
  **is_long**($subject, $message = null)<br \/>
  **is_null**($subject, $message = null)<br \/>
  **is_numeric**($subject, $message = null)<br \/>
  **is_object**($subject, $message = null)<br \/>
  **is_real**($subject, $message = null)<br \/>
  **is_resource**($subject, $message = null)<br \/>
  **is_scalar**($subject, $message = null)<br \/>
  **is_string**($subject, $message = null)

  Validate `$subject` is of the given type.

- **value_empty**($subject, $message)

   Validate no value was present in `$subject`. Uses `empty(..)` internally.

- **value_not_empty**($subject, $message)

   Validate non-falsy value was present in `$subject`.

- **hash_equal**($subject, $reference, $message)

   Serialize `$subject` and `$reference` and compare their hash values. Both
   variables must be exactly the same (incl. ordering of keys) for this
   validation to pass.

- **is_reference**(&$a, &$b, $message = null)

   Works on objects and arrays only. Inserts a temporary key/property and
   unsets it if it exists in both variables.

- **must**($condition, $message)

   Validate `$condition` is non-falsy.

## Contribute

There is plenty of work to be done -- starting from how specs are run to what
assertions are built into the framework. If you find your favourite `assert::?`
method to be missing, fork the project and add it.
