[Aria2](https://github.com/aria2/aria2) with some limitations removed:

- max connection per server (-x) set to INF;

- min split size set to 1k and split size default to 1m.

Changes made:

```
diff --git a/src/OptionHandlerFactory.cc b/src/OptionHandlerFactory.cc
index 2cd2c43e..320b2d2c 100644
--- a/src/OptionHandlerFactory.cc
+++ b/src/OptionHandlerFactory.cc
@@ -440,7 +440,7 @@ std::vector<OptionHandler*> OptionHandlerFactory::createOptionHandlers()
   {
     OptionHandler* op(new NumberOptionHandler(PREF_MAX_CONNECTION_PER_SERVER,
                                               TEXT_MAX_CONNECTION_PER_SERVER,
-                                              "1", 1, 16, 'x'));
+                                              "1", 1, -1, 'x'));
     op->addTag(TAG_BASIC);
     op->addTag(TAG_FTP);
     op->addTag(TAG_HTTP);
@@ -501,7 +501,7 @@ std::vector<OptionHandler*> OptionHandlerFactory::createOptionHandlers()
   }
   {
     OptionHandler* op(new UnitNumberOptionHandler(
-        PREF_MIN_SPLIT_SIZE, TEXT_MIN_SPLIT_SIZE, "20M", 1_m, 1_g, 'k'));
+        PREF_MIN_SPLIT_SIZE, TEXT_MIN_SPLIT_SIZE, "1M", 1_k, 1_g, 'k'));
     op->addTag(TAG_BASIC);
     op->addTag(TAG_FTP);
     op->addTag(TAG_HTTP);
@@ -905,7 +905,7 @@ std::vector<OptionHandler*> OptionHandlerFactory::createOptionHandlers()
   }
   {
     OptionHandler* op(new UnitNumberOptionHandler(
-        PREF_PIECE_LENGTH, TEXT_PIECE_LENGTH, "1M", 1_m, 1_g));
+        PREF_PIECE_LENGTH, TEXT_PIECE_LENGTH, "1M", 1_k, 1_g));
     op->addTag(TAG_ADVANCED);
     op->addTag(TAG_FTP);
     op->addTag(TAG_HTTP);
```
