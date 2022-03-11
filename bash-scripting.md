# Bash Scripting

## Task 2 Our first simple bash scripts

#### What piece of code can we insert at the start of a line to comment out our code?

{% hint style="success" %}
`#`
{% endhint %}

#### What will the following script output to the screen, echo “BishBashBosh”

{% hint style="success" %}
`BishBashBosh`
{% endhint %}

## Task 3 Variables

#### What would this code return?

{% hint style="success" %}
`Jammy is 21 years old`
{% endhint %}

#### How would you print out the city to the screen?

{% hint style="success" %}
`echo $city`
{% endhint %}

#### How would you print out the country to the screen?

{% hint style="success" %}
`echo $country`
{% endhint %}

## Task 4 Parameters

#### How can we get the number of arguments supplied to a script?

{% hint style="success" %}
`$#`
{% endhint %}

#### How can we get the filename of our current script?

{% hint style="success" %}
`$0`
{% endhint %}

#### How can we get the 4th argument supplied to the script?

{% hint style="success" %}
`$4`
{% endhint %}

#### If a script asks us for input how can we direct our input into a variable called ‘test’ using “read”

{% hint style="success" %}
`read input`
{% endhint %}

#### What will the output of “echo $1 $3” if the script was ran with “./script.sh hello hola aloha”

{% hint style="success" %}
`hello aloha`
{% endhint %}

## Task 5 Arrays

#### What would be the command to print audi to the screen using indexing.

{% hint style="success" %}
`echo "${cars[1]}"`
{% endhint %}

#### If we wanted to remove tesla from the array how would we do so?

{% hint style="success" %}
`unset cars[3]`
{% endhint %}

#### How could we insert a new value called toyota to replace tesla

{% hint style="success" %}
`cars[3]='toyota'`
{% endhint %}

## Task 6 Conditionals

#### What is the flag to check if we have read access to a file?

{% hint style="success" %}
`-r`
{% endhint %}

#### What is the flag to check to see if it's a directory?

{% hint style="success" %}
`-d`
{% endhint %}
