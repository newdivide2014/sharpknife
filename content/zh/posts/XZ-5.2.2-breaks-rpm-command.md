---
title: "/lib64/liblzma.so.5: version `XZ_5.1.2alpha' not found"
date: 2021-08-31T13:48:18+08:00
description: XZ 5.2.2 breaks rpm command
# weight: 1
# aliases: ["/first"]
draft: false
author: "嘟囔"
# author: ["Me", "You"] # multiple authors
tags: ["XZ"]
categories: ["Linux"]
---

执行`yum`和`rpm`都报错了，错误如下：
```sh
[root@localhost lib64]: yum
There was a problem importing one of the Python modules
required to run yum. The error leading to this problem was:

   liblzma.so.5: version `XZ_5.1.2alpha' not found (required by librpmio.so.3)

Please install a package which provides this module, or
verify that the module is installed correctly.

It's possible that the above module doesn't match the
current version of Python, which is:
2.7.5 (default, Oct 31 2018, 18:48:32)
[GCC 4.8.5 20150623 (Red Hat 4.8.5-36)]

If you cannot solve this problem yourself, please go to
the yum faq at:
  http://yum.baseurl.org/wiki/Faq


[root@localhost lib64]# rpm
rpm: liblzma.so.5: version `XZ_5.1.2alpha' not found (required by librpmio.so.3)
```
报错信息说的是在这个`liblzma.so.5`找不到符号`XZ_5.1.2alpha`，但是`librpmio.so.3`又需要使用这个玩意。
```sh
[root@localhost lib64]: strings liblzma.so.5.2.2  | grep XZ_5.1.2alpha
[root@localhost lib64]:
```
查了一下现在系统里的确实没有`XZ_5.1.2alpha`这符号。然后就网上一顿找。  
各种垃圾文章都是让`ln -s -f liblzma.so.5.2.2 liblzma.so.5`一下就好了。但是我的没用，不是这问题。我`/lib64/`下的这个链接和文件都是正常的，就是因为`liblzma.so.5`找不到符号`XZ_5.1.2alpha`。

然后找到`github`上才终于能解决 [人家这才是正确的方法]https://github.com/easybuilders/easybuild-easyconfigs/issues/4036

重新下载了xz-5.2.2.tar.gz的源码 [官网下载地址在此]https://sourceforge.net/projects/lzmautils/files/
然后修改了`src/liblzma/liblzma.map`

```sh
We provided two 5.1.2alpha symbols (lzma_stream_encoder_mt and
lzma_stream_encoder_mt_memusage) before we updated to xz-5.2.2-1 in RHEL7.3.

Those symbols did not change ABI in 5.2.2 so it should be safe to provide
(except for 5.0 and 5.2 symbols) also the two 5.1.2alpha symbols and
use 5.1.2alpha symbol version as parent for 5.2.

For better reasoning look at container.h in 5.1.2alpha -- those two symbols
were for testing purposes only, and thus not considered to be API/ABI.

diff --git a/src/liblzma/liblzma.map b/src/liblzma/liblzma.map
index f53a4ea..9c3002a 100644
--- a/src/liblzma/liblzma.map
+++ b/src/liblzma/liblzma.map
@@ -95,7 +95,13 @@ global:
 	lzma_vli_size;
 };
 
-XZ_5.2 {
+XZ_5.1.2alpha {
+global:
+	lzma_stream_encoder_mt;
+	lzma_stream_encoder_mt_memusage;
+} XZ_5.0;
+
+XZ_5.2.2 {
 global:
 	lzma_block_uncomp_encode;
 	lzma_cputhreads;
@@ -105,4 +111,4 @@ global:
 
 local:
 	*;
-} XZ_5.0;
+} XZ_5.1.2alpha;

```
![🐶](/images/posts/xz-map-diff.png)

修改好之后退到源码根目录，执行`make`
```sh
./configure --prefix=/user/local
make
make install
```

问题解决，可以使用`yum`和`rpm`命令了。

---

以下放上原始文件和修改后的文件。

原始liblzma.map文件内容
```sh
XZ_5.0 {
global:
	lzma_alone_decoder;
	lzma_alone_encoder;
	lzma_auto_decoder;
	lzma_block_buffer_bound;
	lzma_block_buffer_decode;
	lzma_block_buffer_encode;
	lzma_block_compressed_size;
	lzma_block_decoder;
	lzma_block_encoder;
	lzma_block_header_decode;
	lzma_block_header_encode;
	lzma_block_header_size;
	lzma_block_total_size;
	lzma_block_unpadded_size;
	lzma_check_is_supported;
	lzma_check_size;
	lzma_code;
	lzma_crc32;
	lzma_crc64;
	lzma_easy_buffer_encode;
	lzma_easy_decoder_memusage;
	lzma_easy_encoder;
	lzma_easy_encoder_memusage;
	lzma_end;
	lzma_filter_decoder_is_supported;
	lzma_filter_encoder_is_supported;
	lzma_filter_flags_decode;
	lzma_filter_flags_encode;
	lzma_filter_flags_size;
	lzma_filters_copy;
	lzma_filters_update;
	lzma_get_check;
	lzma_index_append;
	lzma_index_block_count;
	lzma_index_buffer_decode;
	lzma_index_buffer_encode;
	lzma_index_cat;
	lzma_index_checks;
	lzma_index_decoder;
	lzma_index_dup;
	lzma_index_encoder;
	lzma_index_end;
	lzma_index_file_size;
	lzma_index_hash_append;
	lzma_index_hash_decode;
	lzma_index_hash_end;
	lzma_index_hash_init;
	lzma_index_hash_size;
	lzma_index_init;
	lzma_index_iter_init;
	lzma_index_iter_locate;
	lzma_index_iter_next;
	lzma_index_iter_rewind;
	lzma_index_memusage;
	lzma_index_memused;
	lzma_index_size;
	lzma_index_stream_count;
	lzma_index_stream_flags;
	lzma_index_stream_padding;
	lzma_index_stream_size;
	lzma_index_total_size;
	lzma_index_uncompressed_size;
	lzma_lzma_preset;
	lzma_memlimit_get;
	lzma_memlimit_set;
	lzma_memusage;
	lzma_mf_is_supported;
	lzma_mode_is_supported;
	lzma_physmem;
	lzma_properties_decode;
	lzma_properties_encode;
	lzma_properties_size;
	lzma_raw_buffer_decode;
	lzma_raw_buffer_encode;
	lzma_raw_decoder;
	lzma_raw_decoder_memusage;
	lzma_raw_encoder;
	lzma_raw_encoder_memusage;
	lzma_stream_buffer_bound;
	lzma_stream_buffer_decode;
	lzma_stream_buffer_encode;
	lzma_stream_decoder;
	lzma_stream_encoder;
	lzma_stream_flags_compare;
	lzma_stream_footer_decode;
	lzma_stream_footer_encode;
	lzma_stream_header_decode;
	lzma_stream_header_encode;
	lzma_version_number;
	lzma_version_string;
	lzma_vli_decode;
	lzma_vli_encode;
	lzma_vli_size;
};

XZ_5.2 {
global:
	lzma_block_uncomp_encode;
	lzma_cputhreads;
	lzma_get_progress;
	lzma_stream_encoder_mt;
	lzma_stream_encoder_mt_memusage;

local:
	*;
} XZ_5.0;
```

修改后的liblzma.map
```sh
XZ_5.0 {
global:
	lzma_alone_decoder;
	lzma_alone_encoder;
	lzma_auto_decoder;
	lzma_block_buffer_bound;
	lzma_block_buffer_decode;
	lzma_block_buffer_encode;
	lzma_block_compressed_size;
	lzma_block_decoder;
	lzma_block_encoder;
	lzma_block_header_decode;
	lzma_block_header_encode;
	lzma_block_header_size;
	lzma_block_total_size;
	lzma_block_unpadded_size;
	lzma_check_is_supported;
	lzma_check_size;
	lzma_code;
	lzma_crc32;
	lzma_crc64;
	lzma_easy_buffer_encode;
	lzma_easy_decoder_memusage;
	lzma_easy_encoder;
	lzma_easy_encoder_memusage;
	lzma_end;
	lzma_filter_decoder_is_supported;
	lzma_filter_encoder_is_supported;
	lzma_filter_flags_decode;
	lzma_filter_flags_encode;
	lzma_filter_flags_size;
	lzma_filters_copy;
	lzma_filters_update;
	lzma_get_check;
	lzma_index_append;
	lzma_index_block_count;
	lzma_index_buffer_decode;
	lzma_index_buffer_encode;
	lzma_index_cat;
	lzma_index_checks;
	lzma_index_decoder;
	lzma_index_dup;
	lzma_index_encoder;
	lzma_index_end;
	lzma_index_file_size;
	lzma_index_hash_append;
	lzma_index_hash_decode;
	lzma_index_hash_end;
	lzma_index_hash_init;
	lzma_index_hash_size;
	lzma_index_init;
	lzma_index_iter_init;
	lzma_index_iter_locate;
	lzma_index_iter_next;
	lzma_index_iter_rewind;
	lzma_index_memusage;
	lzma_index_memused;
	lzma_index_size;
	lzma_index_stream_count;
	lzma_index_stream_flags;
	lzma_index_stream_padding;
	lzma_index_stream_size;
	lzma_index_total_size;
	lzma_index_uncompressed_size;
	lzma_lzma_preset;
	lzma_memlimit_get;
	lzma_memlimit_set;
	lzma_memusage;
	lzma_mf_is_supported;
	lzma_mode_is_supported;
	lzma_physmem;
	lzma_properties_decode;
	lzma_properties_encode;
	lzma_properties_size;
	lzma_raw_buffer_decode;
	lzma_raw_buffer_encode;
	lzma_raw_decoder;
	lzma_raw_decoder_memusage;
	lzma_raw_encoder;
	lzma_raw_encoder_memusage;
	lzma_stream_buffer_bound;
	lzma_stream_buffer_decode;
	lzma_stream_buffer_encode;
	lzma_stream_decoder;
	lzma_stream_encoder;
	lzma_stream_flags_compare;
	lzma_stream_footer_decode;
	lzma_stream_footer_encode;
	lzma_stream_header_decode;
	lzma_stream_header_encode;
	lzma_version_number;
	lzma_version_string;
	lzma_vli_decode;
	lzma_vli_encode;
	lzma_vli_size;
};


XZ_5.1.2alpha {
global:
	lzma_stream_encoder_mt;
	lzma_stream_encoder_mt_memusage;
} XZ_5.0;

XZ_5.2.2{
global:
	lzma_block_uncomp_encode;
	lzma_cputhreads;
	lzma_get_progress;
	lzma_stream_encoder_mt;
	lzma_stream_encoder_mt_memusage;

local:
	*;
} XZ_5.1.2alpha;
```

