---
title: "The 'entity:user' context is required and not present"
date: "2023-11-15"
tags: ["Drupal", "Drupal Error"]
tags: ["Drupal"]
---

## Error Message
```
Drupal\Component\Plugin\Exception\ContextException: The 'entity:user' context is required and not present. in Drupal\Core\Plugin\Context\Context->getContextValue() (line 73 of core/lib/Drupal/Core/Plugin/Context/Context.php).
```

![2023.11.15 - 115721](2023.11.15%20-%20115721.jpg)

## Working Solution for Me

File: `public_html/core/lib/Drupal/Core/ParamConverter/EntityConverter.php b/core/lib/Drupal/Core/ParamConverter/EntityConverter.php`

```diff
-    if (isset($contexts[$context_id])) {
-      $account = $contexts[$context_id]->getContextValue();
-      unset($account->_skipProtectedUserFieldConstraint);
-      unset($contexts[$context_id]);
-    }
+    if (isset($contexts[$context_id]) && $contexts[$context_id]->hasContextValue()) {
+        $account = $contexts[$context_id]->getContextValue();
+        unset($account->_skipProtectedUserFieldConstraint, $contexts[$context_id]);
+    }
```

Reference
- [https://www.drupal.org/project/drupal/issues/3056234](https://www.drupal.org/project/drupal/issues/3056234)
- [https://www.drupal.org/files/issues/2023-09-08/3056234-44.patch](https://www.drupal.org/files/issues/2023-09-08/3056234-44.patch)




## Community Solution 1
File: `public_html/core/lib/Drupal/Core/ParamConverter/EntityConverter.php b/core/lib/Drupal/Core/ParamConverter/EntityConverter.php`

```diff
diff --git a/core/lib/Drupal/Core/ParamConverter/EntityConverter.php b/core/lib/Drupal/Core/ParamConverter/EntityConverter.php
index aa2b00d647..7f87d1c9c8 100644
--- a/core/lib/Drupal/Core/ParamConverter/EntityConverter.php
+++ b/core/lib/Drupal/Core/ParamConverter/EntityConverter.php
@@ -145,10 +145,9 @@ public function convert($value, $definition, $name, array $defaults) {
     //   triggering some test failures. We can remove these lines once
     //   https://www.drupal.org/node/2934192 is fixed.
     $context_id = '@user.current_user_context:current_user';
-    if (isset($contexts[$context_id])) {
+    if (isset($contexts[$context_id]) && $contexts[$context_id]->hasContextValue()) {
       $account = $contexts[$context_id]->getContextValue();
-      unset($account->_skipProtectedUserFieldConstraint);
-      unset($contexts[$context_id]);
+      unset($account->_skipProtectedUserFieldConstraint, $contexts[$context_id]);
     }
     $entity = $this->entityRepository->getCanonical($entity_type_id, $value, $contexts);

diff --git a/core/tests/Drupal/KernelTests/Core/Entity/EntityUrlTest.php b/core/tests/Drupal/KernelTests/Core/Entity/EntityUrlTest.php
new file mode 100644
index 0000000000..70ab99719c
--- /dev/null
+++ b/core/tests/Drupal/KernelTests/Core/Entity/EntityUrlTest.php
@@ -0,0 +1,27 @@
+<?php
+
+namespace Drupal\KernelTests\Core\Entity;
+
+use Drupal\Core\Url;
+use Drupal\entity_test\Entity\EntityTest;
+
+/**
+ * Tests URL method.
+ *
+ * @group Entity
+ */
+class EntityUrlTest extends EntityKernelTestBase {
+
+  public function testUrl() {
+    $this->installEntitySchema('entity_test');
+    $this->installEntitySchema('user');
+
+    $entity = EntityTest::create();
+    $entity->save();
+    $entityId = $entity->id();
+    $url = Url::fromUri('internal:/entity_test/' . $entityId);
+    $this->assertEquals('entity.entity_test.canonical', $url->getRouteName());
+    $this->assertEquals(['entity_test' => $entityId], $url->getRouteParameters());
+  }
+
+}
```

Reference
- [https://www.drupal.org/project/drupal/issues/3056234](https://www.drupal.org/project/drupal/issues/3056234)
- [https://www.drupal.org/files/issues/2023-09-08/3056234-44.patch](https://www.drupal.org/files/issues/2023-09-08/3056234-44.patch)

## Community Solution 2

File: `public_html/core/lib/Drupal/Core/ParamConverter/EntityConverter.php b/core/lib/Drupal/Core/ParamConverter/EntityConverter.php`

```diff
diff --git a/core/lib/Drupal/Core/ParamConverter/EntityConverter.php b/core/lib/Drupal/Core/ParamConverter/EntityConverter.php
index c3820baaca..3f69b2b858 100644
--- a/core/lib/Drupal/Core/ParamConverter/EntityConverter.php
+++ b/core/lib/Drupal/Core/ParamConverter/EntityConverter.php
@@ -2,6 +2,7 @@

 namespace Drupal\Core\ParamConverter;

+use Drupal\Component\Plugin\Exception\ContextException;
 use Drupal\Core\Entity\EntityInterface;
 use Drupal\Core\Entity\EntityRepositoryInterface;
 use Drupal\Core\Entity\EntityTypeManagerInterface;
@@ -146,8 +147,12 @@ public function convert($value, $definition, $name, array $defaults) {
     //   https://www.drupal.org/node/2934192 is fixed.
     $context_id = '@user.current_user_context:current_user';
     if (isset($contexts[$context_id])) {
-      $account = $contexts[$context_id]->getContextValue();
-      unset($account->_skipProtectedUserFieldConstraint);
+      try {
+        $account = $contexts[$context_id]->getContextValue();
+        unset($account->_skipProtectedUserFieldConstraint);
+      }
+      catch (ContextException $e) {
+      }
       unset($contexts[$context_id]);
     }
     $entity = $this->entityRepository->getCanonical($entity_type_id, $value, $contexts);
```

Reference:
- [https://www.drupal.org/project/drupal/issues/3357354](https://www.drupal.org/project/drupal/issues/3357354)
- [https://www.drupal.org/files/issues/2023-06-06/3357354-8.patch](https://www.drupal.org/files/issues/2023-06-06/3357354-8.patch)