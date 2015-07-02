# Enums Exercises

## Setup

[Fork](https://github.com/JumpstartLab/enums-exercises/fork) and clone the `enums-exercises` repository.

```bash
$ cd ~/turing/1module/
$ git clone git@github.com:USERNAME/enums-exercises.git
$ cd enums-exercises
```

Create a branch so that you're not changing `master`:

```bash
$ git checkout -b make-tests-pass
```

## Instructions

After cloning the repository down, and checking out a new branch, we are ready
to get started on these enumerables exercises.

The goal of these exercises is to help you understand enumerables, both how
they work and how they can be replicated through the use of the #each, the
basis of all enumerables.

You should perform the exercises in the order below:

* `map`
* `select`
* `reject`
* `any?`
* `all?`
* `none?`
* `one?`
* `group_by`
* `find`
* `count`
* `sort_by`
* `reduce`
* `zip`

You should perform the pattern test first, and then the test.

For example, you should work on `map_pattern_test.rb` followed by `map_test.rb`
Upon completing that, you should do `select_pattern_test.rb` and then
`select_test.rb` and so forth.

## Contributing Patches

### Fixing Errors in Exercises

If you find an error in one of the exercises, then it needs to be fixed upstream in the generators or templates.

For example, someone discovered that there were two tests with the same name in the `all_pattern_test.rb` exercise:

```ruby
def test_all_gone
  skip
  words = ["gone", "gone", "gone", "gone", "gone", "gone", "gone"]
  all_gone = true
  # Your code goes here
  assert all_gone
end

def test_all_gone
  skip
  words = ["gone", "gone", "gone", "gone", "gone", "there", "gone", "gone"]
  # Your code goes here
  refute all_gone
end
```

The second test should have been named `test_not_all_gone`.

In order to fix this, we need to locate the problem generator: `lib/generator/all_problem.rb`.

```ruby
exercise << Problem.new(
  "all_gone",
  {"words" => %w(gone gone gone gone gone gone gone)},
  {"all_gone" => "assert"},
  "word == 'gone'"
).assignment!

exercise << Problem.new(
  "all_gone",
  {"words" => %w(gone gone gone gone gone there gone gone)},
  {"all_gone" => "refute"},
  "word == 'gone'"
)
```

The name of the second problem can be changed.

Then regenerate the exercises with:

```bash
rake generate
```

Finally, run the tests:

```bash
rake test
```

### Creating New Exercises

Check out master:

```bash
$ git checkout master
```

Create a new branch:

```bash
$ git checkout -b new-exercises
```

Make up one extra test for each test suite. Remember to delete the implementation once it's passing, and add a `skip` to it.

```bash
$ git diff
$ git add -A
$ git commit -m "Add more exercises"
```

Push your branch up to GitHub:

```bash
$ git push -u origin new-exercises
```

Submit a pull request (go to the front page of your own `enums-exercises` repository, there should be a button to compare/create a pull request for the branch that you just pushed up).

### Keeping in sync with the upstream repository

`origin` is your fork of the project. We'll need to connect to the upstream repository.

To do this, add a new remote named upstream that points to the Turing School repository:

```bash
$ git remote add upstream git@github.com:turingschool/enums-exercises.git
```

Then pull down the updated version of upstream:

```bash
$ git fetch upstream
```

And now make sure you're on master:

```bash
$ git checkout master
$ git branch # should say *master
```

Make master point to the exact commit that upstream/master is pointing at:

```bash
$ git reset --hard upstream/master
```

## Solving Exercises

For each method of interest there are two files of interest. Let's look at `map` as an example:

1. `exercises/map_pattern_test.rb`
2. `exercises/map_test.rb`

In the `map_pattern_test.rb` you'll find a collection of exercises which do what `map` is good at,
but they do it just with `each`. Then in `map_test.rb` you'll find the same examples using `map`.

We recommend you...

* Open your text editor with two panes (left and right)
* In the left pane, open the pattern file like `map_pattern_test.rb`
* In the right pane, open the matching file like `map_test.rb`
* Run the `map_pattern_test.rb` and solve the first exercise
* Run the `map_test.rb` and solve the same exercise
* Repeat for each matching pair of exercises
* Commit your solutions after finishing each file

## Work Order

You'll find the exercises in `exercises/` and we recommend working in this order:

* `map`
* `select`
* `reject`
* `any?`
* `all?`
* `none?`
* `one?`
* `group_by`
* `find`
* `count`
* `sort_by`
* `reduce`
* `zip`

## License

The MIT License (MIT)

Copyright (c) 2014 Jumpstart Lab
