# Why (objectives)

* This method targets modularity.
* So that it scales;
* maintenability (objective)
* organized
* readability
* easy to mount in brain's memory. have a map of the rules for one component. at a glance.
* reduce specificity in your stylesheets
  * specificity makes it hard to make sure that your override in a
  certain situation will works (and you don't want to have to go with
  `!important`)

# How

* Choose a preprocessor or postprocessor that enables rule nesting
  * sass is a good candidate
* a good name is not necessary a short name. don't be afraid to have
long class names. e.g.: a prefix can have multiple words
* use kebab case

* a component can have only one selector with 2 rules.
  * components do not have to be huge
  * prefer more small components over less large components

## Stylesheets

* __base
* __typography
* __variables
* __forms
* __component-1
* __component-2

## rules

* in one file
all css classes are prefixed by the same words (for that file)
  * the file is actually named after those prefix words; it's the component's name
  * why?
    * 'cause it's easy to know where the class is describe when you see it in your HTML document
* keep nesting at the minimum. the rule is: you can indent only once. (see cleancode)
* the only place a component can be styled is in it's own file
* you don't embed a class selector inside a class selector
  * you want to add a class to the children
  * i.e.
  ```css
    * .breadcrumb-items {
      }

      .breadcrumb-item {
      }
    * NOT
      * .breadcrumb-items {
        li {
        }
      }
    * <ul class="breadcrumb-items">
      * <li class="breadcrumb-item">
  ```

* a media query doesn't encapsulate anything
  * BAD
  ```css
  @media (max-width: 600px) {
    .breadcrumb-items {
    }
  }
  ```
  * GOOD
  ```css
  .breadcrumb-items {
    @media (max-width: 600px) {
    }
  }
  ```

* don't obfuscate your selectors, you want to search through your files and find the class you saw in your HTML document.
  * BAD
    ```css
      .breadcrumb-items {
        &-something {
        }
      }
    ```

# What you can embed inside a selector

* media queries
* pseudo-elements
* pseudo-selector
* state classes
  * .is-open
  * .is-active
  * .has-children
* elements (should be exceptional cases) and only if you precede it with `>`
  * i.e.
  ```css
    .breadcrumb-items {
      > li {
      }
    }
  ```
  * the only reason you could do that is because you couldn't find a name for the element you are targeting
  * so that you don't have the white page syndrome
  * but you should refactor and find a name when you have styled it to the specs.
* sibling combinators `+`, `~`
  * but you want to style the element you have declared, not the sibling
    ```css
      .breadcrumb-items {
        .an-adjacent-element + & {
        }
      }
    ```
  * NOT
    ```css
      .breadcrumb-items {
        * + .an-adjacent-element-that-i-will-style {
        }
      }
    ```

## exceptions

those stylesheets do not absolutely follow the rules

* __base
* __typography
* __variables
* __forms

