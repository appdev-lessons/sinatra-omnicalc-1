# Sinatra: Omnicalc 1

In this project, we'll learn how to get input from our users through HTML forms.

Here is our target: [omnicalc-1.matchthetarget.com](https://omnicalc-1.matchthetarget.com/)

Load the assignment and set up a codespace:

LTI{Load Sinatra Omnicalc-1 assignment}(https://grades.firstdraft.com/launch)[S9ymPy6WCsn18gLbByVbZQ7k]{vfdtzJb5bLYqYwuqgeRKpc5d}(10)[Sinatra Omnicalc-1 Project]

---

[Here is a video for this lesson](https://share.descript.com/view/krwGaIMQ2mQ). You should not rely entirely on the video. PLEASE READ the below lesson (and [the _Query Strings and Forms_ lesson](https://learn.firstdraft.com/lessons/102-query-strings-and-forms)) as you are going through the steps, since there are additional details in the text.

## Objectives

Here is how the app should work. As a user:

 - If I visit the path **/square/new**, I should see a form with a label and an input to enter a number.
    - If I submit that form, I should see the square of the number that I entered.
 - If I visit the path **/square_root/new**, I should see a form with a label and an input to enter a number.
    - If I submit that form, I should see the square root of the number that I entered.
 - If I visit the path **/payment/new**, I should see a form with labels and inputs to enter three values:
    - The APR (annual percentage rate).
    - The number of _years_ remaining.
    - The present value.
    - If I submit that form, I should see the **monthly** payment due given the values that I entered.
    - Mind your units! Use this formula:

        <!-- ![Payment formula](assets/omnical-1/payment_formula.gif) -->
        ![](https://res.cloudinary.com/dmxgp9oq2/image/upload/v1688541702/payment_formula_zpumvd.gif)

    - Hint 1: The number of periods, `n`, that we receive from the user is in years. Since we're calculating monthly payment we multiply it by 12.
    - Hint 2: `apr` comes in as a string. We should turn it into a float and divide the number by 100 to get the percentage.
    - Hint 3: `r` in the formula is a percentage per period.  One period is equal to one month.  The `apr` we receive from the user is yearly.
    - Hint 4: Create a variable for the numerator and another one for the denominator.  If they are instance variables, you can view them within your view page. If your output does not match the target, having done this  will make debugging much more manageable.

 - If I visit the path **/random/new**, I should see a form with labels and inputs to enter two numbers, a minimum and a maximum.
    - If I submit that form, I should see a random number that falls between the numbers that I entered.

You can compare your app against the [target](http://omnicalc-1.matchthetarget.com/){:target="_blank"}, including doing "View Source" to look at some of the static HTML.


### Valid, Accessible Forms

**In order for your tests to pass**, you must build _valid_ forms (your Chrome browser _may_ tolerate invalid forms while you are manually testing, but automated test suites reject invalid forms):

 - Each `<input>` in the form must have a unique `id=""` attribute.
 - The `<label>` associated with the `<input>` should have a `for=""` attribute that matches the value of the `<input>`'s `id`.
 - The copy within the `<label>` must exactly match the target — spelling, capitalization, and punctuation matter for labels.
 - The same goes for the copy on the button to submit the form.
 - Any invalid HTML within a form will cause the test to fail, e.g. an orphaned closing `</div>` tag. Keep your code neatly indented to help avoid this.

An example of a valid form; in particular, notice the `id=""` and `for=""` attributes:

```erb
<form action="/random/results">
  <div>
    <label for="min_input">
      Minimum
    </label>

    <input id="min_input" type="text" name="user_min" placeholder="E.g. 1.5">
  </div>

  <div>
    <label for="max_input">
      Maximum
    </label>

    <input id="max_input" type="text" name="user_max" placeholder="E.g. 4.5">
  </div>

  <button>
    Pick random number
  </button>
</form>
```

### Additional Hints

The `to_fs` (as in "format string") method can format `Floats` [in more specific ways](https://learn.firstdraft.com/lessons/33-the-one-ruby-reference#to_fs) that help us easily display data in a variety of ways. (**Note:** We already included the `require "active_support/all"` in the `config/environment.rb` file, so you can use these methods.)

In particular these two:

- [`.to_fs(:currency)`](https://learn.firstdraft.com/lessons/33-the-one-ruby-reference#currency)
- [`.to_fs(:percentage)`](https://learn.firstdraft.com/lessons/33-the-one-ruby-reference#percentage)

could be useful when formatting the output of the payment form.

---

- Approximately how long (in minutes) did this lesson take you to complete?
{: .free_text_number #time_taken title="Time taken" points="1" answer="any" }
