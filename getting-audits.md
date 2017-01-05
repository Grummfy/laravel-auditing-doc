# Getting Audits

The `Audit` logs can be fetched very easily, via [Eloquent](https://laravel.com/docs/master/eloquent) relations.

## Retrieving audit logs

Using a `Post` model example, here's how it works:

```php
// Get first available Post
$post = Post::first();

// Get all associated Audits
$all = $post->audits;

// Get first Audit
$first = $post->audits()->first();

// Get last Audit
$last = $post->audits()->last();

// Get Audit by id
$audit = $post->audits()->find(4);
```

## Getting audit logs with the associated User model

```php
// Get all associated Audits
$all = $post->audits()->with('user')->get();
```

> {tip} Remember to properly set the `User` **model** and **resolver** in the `config/audit.php` file.

## Getting the Audit metadata
Retrieve an `array` with the `Audit` metadata.

```php
// Get first available Post
$post = Post::first();

// Get latest Audit
$audit = $post->audits()->last();

var_dump($audit->getMetadata());
```

**Output:**
```php
array(6) {
  ["audit_id"]=>
  string(36) "123b4567-4b94-41f1-9f12-fb1c7d1c9b3d"
  ["audit_event"]=>
  string(7) "updated"
  ["audit_url"]=>
  string(26) "http://example.com/posts/1"
  ["audit_ip_address"]=>
  string(9) "127.0.0.1"
  ["audit_created_at"]=>
  string(19) "2017-01-01 01:02:03"
  ["user_id"]=>
  string(1) "1"
}
```

## Getting the modified properties
Get an `array` with the modified properties of the `Auditable` model.
The data includes the **old** and **new** values for each attribute.

```php
// Get first available Post
$post = Post::first();

// Get latest Audit
$audit = $post->audits()->last();

var_dump($audit->getModified());
```

**Output:**
```php
array(2) {
  ["title"]=>
  array(2) {
    ["new"]=>
    string(28) "How To Audit Eloquent Models"
    ["old"]=>
    string(19) "How to audit models"
  }
  ["content"]=>
  array(2) {
    ["new"]=>
    string(62) "First, let's start by installing the laravel-auditing package."
    ["old"]=>
    string(16) "This is a draft."
  }
}
```
