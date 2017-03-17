---
title:  "Coming Soon"
date:   2017-03-16 16:14:06 -0700
tags:
  - test
---

Test post with some syntax highlighting and stuff.

I just stumbled on a bug in CakePHP that prevents related child records from being returned when only selecting a single field from the parent. It looks something like this:

```php
<?php
$this->Model->find('all', array(
  'contain' => array(
    'Parent' => array(
      'fields' => array('id', 'type'),
      'Child' => array(
        'fields' => array('id', 'type')
      )
    )
  )
);
// Returns as expected
//array(
//  'Model' => array(...),
//  'Parent' => array(
//    'id' => '',
//    'type' => '',
//    'Child' => array(
//      array(
//        'id' => '',
//        'type' => ''
//      ),
//      ...
//    )
//  )
//)
```

Now if we modify the contain for Parent to return only **one field** we lose all Child records:

```php
<?php
$this->Model->find('all', array(
  'contain' => array(
    'Parent' => array(
      'fields' => array('id'),
      'Child' => array(
        'fields' => array('id', 'type')
      )
    )
  )
);
// Returns no Child records
//array(
//  'Model' => array(...),
//  'Parent' => array(
//    'id' => '',
//    'type' => '',
//  )
//)
```

This is due to a bug in `Model/DataSource/DboSource.php`:

```php
<?php
//...
if (count($merge[0][$association]) > 1) {
    foreach ($merge[0] as $assoc => $data2) {
//...
```
Since Parent only has one field, `id`, it does not do the merge. This has been corrected in CakePHP 2.4.2 to `!empty()` instead of `count() > 1`.

This has been fixed in the CakePHP master branch with [this commit](https://github.com/cakephp/cakephp/commit/940a51b5faa0b88fa5334764c19f93fe8364ef30).
