---
isChild: true
anchor:  opcode_cache
---

## Opcode Cache {#opcode_cache_title}

PHP file တစ်ခုကို executed လုပ်တဲ့အခါ နောက်ကွယ်မှာ opcodes အဖြစ်သို့ အရင် compiled လုပ်ပြီးတော့မှ အဲ့ဒီ opcodes တွေကို executed လုပ်ပါတယ်။ PHP file တစ်ခုဟာ ပြုပြင် ပြောင်းလဲမှု လုပ်မထားဘူးဆိုရင် opcodes ဟာ အတူတူပဲဖြစ်ပါတယ်။ အဲ့ဒါဆိုရင် compilation လုပ်တာက CPU resources ကို ဖြုန်းတီးခြင်း သက်သက်ပဲဖြစ်ပါတယ်။

အခုလိုနေရာမျိးမှာ opcode caches က အရေးပါလာပါတယ်။ opcodes တွေကို memory မှာ သိမ်းထားပြီး လိုအပ်တဲ့ အခါ ပြန်သုံးခြင်းအားခြင်းအားဖြင့် မလိုအပ်တဲ့ compilation တွေကို မဖြစ်စေပါဘူး။ opcode cache ကို အသုံးပြုဖို့ ပြင်ဆင်ချိန်ဟာ မိနစ် အနည်းငယ်ပဲကြာပြီး သင့်ရဲ့ application ကို သိသိသာသာ မြန်ဆန်စေမှာ ဖြစ်တဲ့ အတွက် မသုံးသင့်ဘူးဆိုတဲ့ အကြောင်းပြချက်တော့ မရှိပါဘူး

PHP 5.5 မှာ [OPcache][opcache-book] လို့ခေါ်တဲ့ built-in opcode cache ပါဝင်လာပါတယ်။ 5.5 အရှေ့ versions တွေ အတွက်လည်း ရရှိနိုင်ပါတယ်။

opcode caches အကြောင်းကို ထပ်မံ ဖတ်ရှုနိုင်ပါတယ်။

* [OPcache][opcache-book] (built-in since PHP 5.5)
* [APC] (PHP 5.4 and earlier)
* [XCache]
* [Zend Optimizer+] (part of Zend Server package)
* [WinCache] (extension for MS Windows Server)
* [list of PHP accelerators on Wikipedia][PHP_accelerators]


[opcache-book]: http://php.net/book.opcache
[APC]: http://php.net/book.apc
[XCache]: http://xcache.lighttpd.net/
[Zend Optimizer+]: http://www.zend.com/en/products/zend_server
[WinCache]: http://www.iis.net/download/wincacheforphp
[PHP_accelerators]: http://en.wikipedia.org/wiki/List_of_PHP_accelerators
