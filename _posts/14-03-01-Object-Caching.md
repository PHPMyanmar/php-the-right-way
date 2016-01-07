---
isChild: true
anchor:  object_caching
---

## Object Caching {#object_caching_title}

သင့်ရဲ့ code ထဲမှာ တစ်ချို့သော object  တွေ ဥပမာ ... ရဖို့ခက်ခဲတဲ့ data တွေ၊ ပြောင်းလဲနိုင်ခြေ နည်းတဲ့ database calls တွေကို  cache လုပ်မယ်ဆိုရင် အကျိုးရှိပါတယ်။ နောက်တစ်ခါသုံးဖို့ လိုအပ်တဲ့ အခါ အရမ်းမြန်ဆန်အောင် memory မှာ အဲ့ဒီ data တွေကို သိမ်းထားဖို့ object caching software  ကို အသုံးပြုနိုင်ပါတယ်။ အဲ့ဒီ item  တွေကို ပထမတစ်ကြိမ်ရယူပြီးရင် data store ထဲ ထည့်ထား၊ နောက်ထပ် ဒါမျိုး request တွေဆိုရင် cache ထဲက နေတိုက်ရိုက်ယူဆိုပြီး ပြုလုပ်ထားမယ်ဆိုရင် performance အရေ မြန်ဆန်ခြင်းရော database server ကို load လုပ် ခြင်းကို လည်း လျော့ချနိုင်မှာပါ။

နာမည်ကြီး bytecode caching solutions တွေဟာ custom data တွေကို ပါ cache လုပ်နိုင်ပြီး သူတို့တွေကနေ ရနိုင်တဲ့ တခြား အကျိုးကျေးဇူး အများအပြားလည်းရှိပါသေးတယ်။  APCu, XCache, နဲ့ WinCache တို့ အကုန်လုံးဟာ သင့်ရဲ့ PHP code တွေကို သူတို့ရဲ့ memory cache တွေမှာ save ဖို့အတွက် APIs တွေပေးထားပါတယ်။

လူသုံးအများဆုံး memory object caching systems တွေကတော့ APCu and memcached တို့ပဲဖြစ်ပါတယ်။ APCu က object caching အတွက် အကောင်းဆုံး ရွေးချယ်မှုဖြစ်ပြီး သင့်ရဲ့ data တွေကို သူ့ရဲ့ memory cache ထဲထည့်ဖို့ setup လုပ်ရန်လွယ်ကူပြီး ရိုးရှင်တဲ့ API ပါဝင်ပါတယ်။ APCu ရဲ့ တစ်ခုတည်းသော ကန့်သတ်ချက်က သူ့ကို installed  လုပ်ထားတဲ့ server နဲ့ တွဲနေခြင်းပဲ ဖြစ်ပါတယ်။ Memcached ကတော့ သီးသန့် service အဖြစ် installed လုပ် သုံးနိုင်ပြီး network မှ တစ်ဆင့် access လုပ်နိုင်ပါတယ်။ ဆိုလိုတာက object တွေကို အရမ်းမြန်ဆန်တဲ့ နေရာတစ်ခုမှာ သိမ်းထားပြီး system အမျိုးမျိုးကနေ ရယူအသုံးပြုနိုင်ပါတယ်။

တစ်ခု သတိထားရမှာက PHP ကို သင့် ရဲ့ webserver မှာ (Fast-)CGI application အဖြစ် run ထားမယ်ဆိုရင်တော့ PHP process တစ်ခုစီမှာ သူ့ကိုယ်ပိုင် cache ရှိပြီးသားပါ။ ဥပမာ။ ။APCu data တွေဟာ worker process တစ်ခုနဲ့ တစ်ခု ကြား share မလုပ်ပါဘူး။ အဲ့ဒါမျိုးဆိုရင်တော့ PHP process တွေနဲ့ တွဲစပ်မထားတဲ့ memcached ကို သုံးဖို့ စဉ်းစားသင့်ပါတယ်။

network configuration တစ်ခုတည်းမှာဆိုရင် APCu က memcached နဲ့ ယှဉ်ရင် access speed ပိုသာပြီး memcached က scale up လုပ်မယ်ဆို ပိုမြန်ပါတယ်။ သင့်ရဲ့ application က server များများ ရှိဖို့ မလိုအပ်ဘူးဆိုရင် ဒါမှမဟုတ် memcached မှ ရနိုင်တဲ့ feature တွေထက် ပိုမလိုအပ်ဘူးဆိုရင် APCu က object caching လုပ်ဖို့ အကောင်းဆုံးရွေးချယ်မှု ဖြစ်ကောင်းဖြစ်နိုင်ပါတယ်။

APCu သုံးထားတဲ့ logic ဥပမာ

{% highlight php %}
<?php
// check if there is data saved as 'expensive_data' in cache
$data = apc_fetch('expensive_data');
if ($data === false) {
    // data is not in cache; save result of expensive call for later use
    apc_add('expensive_data', $data = get_expensive_data());
}

print_r($data);
{% endhighlight %}


PHP 5.5 အရှေ့ပိုင်း မှာဆိုရင် APC က object cache ရော  bytecode cache ရော အထောက်အပံ့ပေးထားပါတယ်။ APCu က PHP 5.5 နောက်ပိုင်း version တွေအတွက်  APC object cache တွေကို သုံးနိုင်အောင်လုပ်ပေးထားတဲ့ project တစ်ခုဖြစ်ပါတယ်။ အခု PHP version က built-in bytecode cache (OPcache) ပါဝင်လို့ပါပဲ။

### Learn more about popular object caching systems:

* [APCu](https://github.com/krakjoe/apcu)
* [APC Functions](http://php.net/ref.apc)
* [Memcached](http://memcached.org/)
* [Redis](http://redis.io/)
* [XCache APIs](http://xcache.lighttpd.net/wiki/XcacheApi)
* [WinCache Functions](http://php.net/ref.wincache)
