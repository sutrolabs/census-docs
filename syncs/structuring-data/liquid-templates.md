# Liquid Templates

Census uses the [Liquid](https://shopify.github.io/liquid/basics/introduction/) template language to give you extra control over the data you send.

These are tiny programs that let you change the format of data using a simple snippet of code. For example, you can use Liquid to...

* Add prefixes or suffixes
* Change to upper or lower case
* Format dates
* Combine columns together
* Conditionally use alternate values
* Build JSON objects or arrays

Liquid is easy to learn and also very powerful. We look forward to seeing the templates you build!

{% hint style="info" %}
Census supports the full standard set of Liquid 5.4 template features, filters, and tags (with the minor exception of the `include` and `render` tags for external files).
{% endhint %}

{% hint style="warning" %}
Census does not support any Shopify- or Jekyll-specific extensions to Liquid templates, so be sure you're referencing the standard docs at [shopify.github.io/liquid](https://shopify.github.io/liquid).
{% endhint %}

## Getting started

Your most basic operation in Liquid is to reference a record column, like this:

```liquid
{{ record['NAME'] }}
```

<details>

<summary>View result</summary>

{% code title="Data" %}
```yaml
NAME: Boris Jabes
```
{% endcode %}

{% code title="Result" %}
```
Boris Jabes
```
{% endcode %}

</details>

You can add text before or after a variable reference by putting it outside the `{{` and `}}` markers:

```liquid
Customer #{{ record['ID'] }} (new)
```

<details>

<summary>View result</summary>

{% code title="Data" %}
```yaml
ID: 1234
```
{% endcode %}

{% code title="Result" %}
```
Customer #1234 (new)
```
{% endcode %}

</details>

By using two variable references in one template, you can combine columns together:

```liquid
{{ record['LNAME'] }}, {{ record['FNAME'] }}
```

<details>

<summary>View result</summary>

{% code title="Data" %}
```yaml
FNAME: Jane
LNAME: Smith
```
{% endcode %}

{% code title="Result" %}
```
Smith, Jane
```
{% endcode %}

</details>

Another very common job for Liquid is transforming text. Liquid filters are activated with the `|` (pipe) symbol:

```liquid
{{ record['EMAIL'] | downcase }}
```

<details>

<summary>View result</summary>

{% code title="Data" %}
```yaml
EMAIL: USER@EXAMPLE.ORG
```
{% endcode %}

{% code title="Result" %}
```
user@example.org
```
{% endcode %}

</details>

### Column references

All of the columns on your source record are available using the `record['COLUMN_NAME']` syntax. When Census sees this syntax, it knows this column is required from the source.

{% hint style="warning" %}
The exact column name must be used in the `record` property accessor.

For example, if your source column name is `COMPANY_ID`, then you must use `record['COMPANY_ID']` in your Liquid template. Any other variations such as `company_id`, `companyid`, or `companyID` will be raised as [validation](liquid-templates.md#validation) errors.
{% endhint %}

{% hint style="info" %}
Any columns not explicitly referenced are not retrieved from the source, which ensures that syncs using Liquid templates run just as fast as all your other syncs on Census.
{% endhint %}

### Standard Filters

There are over 40 standard Liquid filters to be found in the left sidebar in the [official documenation](https://shopify.github.io/liquid/basics/introduction/#filters). Here are a few common ones...

#### [downcase](https://shopify.github.io/liquid/filters/downcase/)

Convert text to lowercase:

```liquid
{{ record['CUSTOMER_ID'] | downcase }}
```

<details>

<summary>View result</summary>

{% code title="Data" %}
```yaml
CUSTOMER_ID: ABc123
```
{% endcode %}

{% code title="Result" %}
```
abc123
```
{% endcode %}

</details>

#### [upcase](https://shopify.github.io/liquid/filters/upcase/)

Convert text to uppercase:

```liquid
{{ record['STATE_CODE'] | upcase }}
```

<details>

<summary>View result</summary>

{% code title="Data" %}
```yaml
STATE_CODE: hi
```
{% endcode %}

{% code title="Result" %}
```
HI
```
{% endcode %}

</details>

#### [replace](https://shopify.github.io/liquid/filters/replace/)

Substitute all example text with the provided result text:

```liquid
{{ record['PRODUCT_ID'] | replace: "_", "-" }}
```

<details>

<summary>View result</summary>

{% code title="Data" %}
```yaml
PRODUCT_ID: abc_xyz
```
{% endcode %}

{% code title="Result" %}
```
abc-xyz
```
{% endcode %}

</details>

#### [strip](https://shopify.github.io/liquid/filters/strip/)

Remove space characters from the start and end of the text:

```liquid
{{ record['COMPANY_NAME'] | strip }}
```

<details>

<summary>View result</summary>

{% code title="Data" %}
```yaml
COMPANY_NAME: "  Acme Inc.    "
```
{% endcode %}

{% code title="Result" %}
```
Acme Inc.
```
{% endcode %}

</details>

#### [date](https://shopify.github.io/liquid/filters/date/)

Format a timestamp as a text date:

```liquid
{{ record['PURCHASED_AT'] | date: "%Y-%m-%d %H:%M" }}
```

<details>

<summary>View result</summary>

{% code title="Data" %}
```yaml
PURCHASED_AT: 1698166115
```
{% endcode %}

{% code title="Result" %}
```
2023-10-24 16:48
```
{% endcode %}

</details>

### Census Filters

Census also includes a number of custom filters specifically designed to help you with data transforms...

#### json

Encode a value into JSON syntax:

```liquid
{{ record["EXTRA_DATA"] | json }}
```

<details>

<summary>View result</summary>

{% code title="Data" %}
```yaml
EXTRA_DATA:
  a: 1
  b: true
  c: "text"
```
{% endcode %}

{% code title="Result" %}
```json
{"a":1,"b":true,"c":"text"}
```
{% endcode %}

</details>

{% hint style="info" %}
This can be useful when working with APIs or structured data.
{% endhint %}

#### except

Get a subset of an object with some keys removed:

```liquid
{{ record["EXTRA_DATA"] | except: "b", "c" | json }}
```

<details>

<summary>View result</summary>

{% code title="Data" %}
```yaml
EXTRA_DATA:
  a: 1
  b: 2
  c: 3
  d: 4
```
{% endcode %}

{% code title="Result" %}
```json
{"a":1,"d":4}
```
{% endcode %}

</details>

{% hint style="info" %}
Often used together with [json](liquid-templates.md#json). Also accepts an array or an object as a single argument.
{% endhint %}

#### only

Get a subset of an object containing just some keys:

```liquid
{{ record["EXTRA_DATA"] | only: "b", "c" | json }}
```

<details>

<summary>View result</summary>

{% code title="Data" %}
```yaml
EXTRA_DATA:
  a: 1
  b: 2
  c: 3
  d: 4
```
{% endcode %}

{% code title="Result" %}
```
{"b":2,"c":3}
```
{% endcode %}

</details>

{% hint style="info" %}
Often used together with [json](liquid-templates.md#json). Also accepts an array or an object as a single argument.
{% endhint %}

#### keys

Get all of the keys of an object:

<pre class="language-liquid"><code class="lang-liquid"><strong>{{ record["EXTRA_DATA"] | keys | json }}
</strong></code></pre>

<details>

<summary>View result</summary>

{% code title="Data" %}
```yaml
EXTRA_DATA:
  a: 1
  b: 2
  c: 3
  d: 4
```
{% endcode %}

{% code title="Result" %}
```json
["a","b","c","d"]
```
{% endcode %}

</details>

#### sha256

Get the SHA-256 hash of a value and return the hex representation:

```liquid
{{ record['EMAIL'] | sha256 }}
```

<details>

<summary>View result</summary>

{% code title="Data" %}
```yaml
EMAIL: test@example.org
```
{% endcode %}

{% code title="Result" %}
```
388c735eec8225c4ad7a507944dd0a975296baea383198aa87177f29af2c6f69
```
{% endcode %}

</details>

{% hint style="info" %}
Can be helpful for generating hashed identifiers for advertising destinations like [Google Ads](../../destinations/google-ads/) or [LinkedIn](../../destinations/linkedin.md).
{% endhint %}

#### base64

Encode a value using Base64:

```liquid
{{ record['VALUE'] | base64 }}
```

<details>

<summary>View result</summary>

{% code title="Data" %}
```yaml
VALUE: "<b>hello\nworld</b>"
```
{% endcode %}

{% code title="Result" %}
```
PGI+aGVsbG8Kd29ybGQ8L2I+
```
{% endcode %}

</details>

{% hint style="info" %}
May be useful to work around fields that don't allow some special characters.
{% endhint %}

## Validation

As you write your Liquid templates, it's possible that you may make a typo or don't quite have the right syntax. Census will catch all these errors as you type, and you'll know about them well before your sync starts running.

Here are some invalid template examples that will be caught by Census:

* `{{ record['ID' }}` → _Liquid syntax error: Expected close\_square but found end\_of\_string in "\{{ record\['ID' \}}"_
* `{{ record['NAMEE'] }}` → _Column being referenced in template can't be found in data source \[NAMEE]_
* `{% assign category = record['CAT'] %}{{ categoryy.ratio | times: 100 }}` → _\[categoryy.ratio | times: 100] unknown variable \`categoryy\`_

{% hint style="info" %}
Compared to some other implementations of Liquid, Census runs using strict parsing and rendering. This means that invalid templates won't run, and any errors encountered when running a valid template won't cause bad data to be sent to your destination.
{% endhint %}

## Advanced

The examples above just scratch the surface of what can be done with Liquid templates. The language exposes enough capabilities to define complex conditions, process structured data, and do some really advanced data manipulation.

### Custom variables

If you're writing advanced expression and want to store an intermediate result, you can create your own Liquid variables to help ([official docs](https://shopify.github.io/liquid/tags/control-flow/)).

#### [assign](https://shopify.github.io/liquid/tags/variable/#assign)

Make a new variable from a value:

```liquid
{% raw %}
{% assign name = record['NAME'] | upcase %}
{% endraw %}
```

#### [capture](https://shopify.github.io/liquid/tags/variable/#capture)

Make a new variable from captured text:

```liquid
{% raw %}
{% capture full_name -%}
  {{ record['FNAME'] }} {{ record['LNAME'] }}
{%- endcapture %}
{% endraw %}
```

{% hint style="info" %}
This is great for text variables that combine multiple columns or make use of multiple Liquid filters or tags.
{% endhint %}

### Conditionals

You can build advanced conditional code with Liquid, for example, to use one variable or another, or to "translate" values for your destination ([official docs](https://shopify.github.io/liquid/tags/control-flow/)).

#### [if](https://shopify.github.io/liquid/tags/control-flow/#if)

Construct a condition using boolean [operators](https://shopify.github.io/liquid/basics/operators/):

```liquid
{% raw %}
{% if record['LTV'] > 1000 -%}
  diamond
{%- elsif record['LTV'] > 100 -%}
  gold
{%- else -%}
  N/A
{%- endif %}
{% endraw %}
```

#### [case/when](https://shopify.github.io/liquid/tags/control-flow/#casewhen)

Construct conditions based on matching values:

```liquid
{% raw %}
{% case record['TYPE'] -%}
  {%- when "customer" -%}
     {{ record['CNAME'] }}
  {%- when "prospect" -%}
     {{ record['PNAME'] }}
  {%- else -%}
     anon
{%- endcase %}
{% endraw %}
```

### Looping

You can also iterate over arrays to build text with repeating elements ([official docs](https://shopify.github.io/liquid/tags/iteration/)).

#### [for](https://shopify.github.io/liquid/tags/iteration/#for)

Generate text for each item:

```liquid
[
  {% raw %}
{% for tag in record %}
  "{{ tag | upcase }}",
  {% endfor %}
{% endraw %}
]
```

{% hint style="info" %}
Commonly used in [JSON mode](liquid-templates.md#json-mode) and with [batched records](liquid-templates.md#batched-records).
{% endhint %}

### Whitespace

If you're using spaces in a complex template and notice your output now includes unwanted spaces, this is a sign that you need to use Liquid whitespace control syntax.

Liquid is basically text building engine. You can think of `{{ ... }}` and `{% ... %}` as "insertion points" into a text file...

* The code inside the brackets will get run by Liquid, and it doesn't make a difference if there's whitespace inside the code, only the code's output will be inserted.
* On the other hand, any whitespace _outside_ of those insertion points will be preserved by Liquid, just like any other text.

Preserved whitespace won't be an issue for text formats like HTML and JSON where whitespace is collapsed or ignored, but for many other use cases, whitespace is significant and causes problems.

To deal with this, Liquid uses the `-` (hyphen) symbol for whitespace control, stripping out whitespace at the insertion point where the symbol is used ([official docs](https://shopify.github.io/liquid/basics/whitespace/)).

Here are a few examples of whitespace inside vs. outside Liquid code blocks (using `{id: 1}` as the record data)...

<table data-full-width="true"><thead><tr><th>Template</th><th width="115">Result</th><th width="100" data-type="number">Note</th></tr></thead><tbody><tr><td><code>"id{{ record['id'] }}"</code></td><td><code>"id1"</code></td><td>1</td></tr><tr><td><code>" {{record['id']}} "</code></td><td><code>" 1 "</code></td><td>2</td></tr><tr><td><code>"{% if true %}{{ record['id'] }}{% endif %}"</code></td><td><code>"1"</code></td><td>3</td></tr><tr><td><code>"{% if true %} {{ record['id'] }} {% endif %}"</code></td><td><code>" 1 "</code></td><td>4</td></tr><tr><td><code>"{% if true %} {{- record['id'] -}} {% endif %}"</code></td><td><code>"1"</code></td><td>5</td></tr><tr><td><code>"{% if true -%} {{ record['id'] }} {%- endif %}"</code></td><td><code>"1"</code></td><td>6</td></tr></tbody></table>

Notes:

1. Whitespace inside code has no effect
2. Whitespace outside code is preserved
3. No whitespace between tags gives no result whitespace
4. Whitespace between tags is preserved
5. Whitespace control symbol strips whitespace around variable
6. Whitespace control symbol strips whitespace inside tags

{% hint style="info" %}
[Whitespace](https://en.wikipedia.org/wiki/Whitespace\_character) includes single spaces, line breaks, and tabs—any of the blank spaces you see in your template code.
{% endhint %}

### JSON mode

One special use for Liquid templates is to build JSON documents. This can be great for advanced API usage with [templated fields](./#using-templates-to-tranform-source-data) or even building custom integrations with the [HTTP Request](../../destinations/http-request.md) destination.

Two special features get activated when in JSON mode:

#### Escaped strings

JSON strings are escaped by default, which means that you don't need to worry about source data causing JSON syntax errors.

```liquid
{
  "comment": "{{ record['COMMENT'] }}"
}
```

<details>

<summary>View result</summary>

{% code title="Data" %}
```yaml
COMMENT: 'They said "hello"'
```
{% endcode %}

{% code title="Result" %}
```json
{
  "comment": "They said \"hello\""
}
```
{% endcode %}

</details>

This behavior can be overridden using either the `json` filter (to encode a value into valid JSON) or the `raw` filter (when your source data is already valid JSON).

```liquid
{
  "json_data": {{ record['OBJECT'] | json }},
  "raw_data": {{ record['RAW] | raw }}
}
```

<details>

<summary>View result</summary>

{% code title="Data" %}
```yaml
OBJECT:
  x: 1
  y: 2
RAW: '{"a":3,"b":4}'
```
{% endcode %}

{% code title="Result" %}
```json
{
  "json_data": {
    "x": 1,
    "y": 2
  },
  "raw_data": {
    "a": 3,
    "b": 4
  }
}
```
{% endcode %}

</details>

#### Flexible syntax

When generating JSON data using for [loops](liquid-templates.md#looping), this process will often leave a `,` after the last item in an array or object, which is invalid JSON.

```liquid
{
  "products": [
    {% raw %}
{% for product in record["PRODUCTS"] %}
    {
      "id": {{ product.id }},
      "name": "{{ product.name }}"
    },
    {% endfor %}
{% endraw %}
  ]
}
```

<details>

<summary>View result</summary>

{% code title="Data" %}
```yaml
PRODUCTS:
  - id: 1
    name: a
  - id: 2
    name: b
```
{% endcode %}

{% code title="Intermediate YAML" %}
```yaml
{
  "products": [
    {
      "id": 1,
      "name": "a"
    },
    {
      "id": 1,
      "name": "b"
    },
  ]
}
```
{% endcode %}

{% code title="Final JSON" %}
```json
{
  "products": [
    {
      "id": 1,
      "name": "a"
    },
    {
      "id": 1,
      "name": "b"
    }
  ]
}
```
{% endcode %}

</details>

Instead of triggering an error, Census allows this syntax and converts it into valid JSON. It does this by parsing the template output as YAML, which is a strict superset of JSON (allows all valid JSON) that accepts these "trailing commas".

If you want, you're free to use any other YAML features, like block-style collections, and the result will still be converted to valid JSON:

```liquid
products:
  {% raw %}
{% for product in record["PRODUCTS"] %}
  - id: {{ product.id }}
    name: "{{ product.name }}"
  {% endfor %}
{% endraw %}
```

<details>

<summary>View result</summary>

{% code title="Data" %}
```yaml
PRODUCTS:
  - id: 1
    name: a
  - id: 2
    name: b
```
{% endcode %}

{% code title="Intermediate YAML" %}
```yaml
products:
  - id: 1
    name: "a"
  - id: 2
    name: "b"
```
{% endcode %}

{% code title="Final JSON" %}
```json
{
  "products": [
    {
      "id": 1,
      "name": "a"
    },
    {
      "id": 1,
      "name": "b"
    }
  ]
}
```
{% endcode %}

</details>
