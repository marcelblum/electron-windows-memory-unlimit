Binaries of Electron using a fork of Chromium that sets the memory usage limit on Windows equal to that on macOS & Linux (16GB) instead of 8GB. Note: 8GB can only be exceeded on Windows if `sandbox` is off in the renderer (or `nodeIntegration` is on which automatically sets `sandbox` off).

Built using **Electron** v21.0.0-nightly.20220801, **Chromium** v105.0.5187.0, **Node** v16.16.0, **v8** v10.5.196-electron.0

```diff
$ git diff partition_alloc_constants.h
diff --git a/base/allocator/partition_allocator/partition_alloc_constants.h b/base/allocator/partition_allocator/partition_alloc_constants.h
index 0d0cab2033c88..345bc6dc3f3a8 100644
--- a/base/allocator/partition_allocator/partition_alloc_constants.h
+++ b/base/allocator/partition_allocator/partition_alloc_constants.h
@@ -247,7 +247,7 @@ constexpr size_t kSuperPageBaseMask = ~kSuperPageOffsetMask;
 #if defined(PA_HAS_64_BITS_POINTERS)
 // The Configurable Pool is only available in 64-bit mode
 constexpr size_t kNumPools = 3;
-#if BUILDFLAG(IS_MAC) || BUILDFLAG(IS_LINUX)
+//#if BUILDFLAG(IS_MAC) || BUILDFLAG(IS_LINUX)
 // Special-case macOS. Contrary to other platforms, there is no sandbox limit
 // there, meaning that a single renderer could "happily" consume >8GiB. So the
 // 8GiB pool size is a regression. Make the limit higher on this platform only
@@ -256,9 +256,9 @@ constexpr size_t kNumPools = 3;
 // On Linux, reserving memory is not costly, and we have cases where heaps can
 // grow to more than 8GiB without being a memory leak.
 constexpr size_t kPoolMaxSize = 16 * kGiB;
-#else
-constexpr size_t kPoolMaxSize = 8 * kGiB;
-#endif
+//#else
+//constexpr size_t kPoolMaxSize = 8 * kGiB;
+//#endif
 #else  // defined(PA_HAS_64_BITS_POINTERS)
 constexpr size_t kNumPools = 2;
 constexpr size_t kPoolMaxSize = 4 * kGiB;
```

re: https://github.com/electron/electron/issues/31330, https://github.com/electron/electron/issues/35032
