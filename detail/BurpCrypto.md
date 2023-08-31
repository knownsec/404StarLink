## BurpCrypto <https://github.com/whwlsfb/BurpCrypto>
<!--auto_detail_badge_begin_0b490ffb61b26b45de3ea5d7dd8a582e-->
![Language](https://img.shields.io/badge/Language-Java-blue)
![Author](https://img.shields.io/badge/Author-whwlsfb-orange)
![GitHub stars](https://img.shields.io/github/stars/whwlsfb/BurpCrypto.svg?style=flat&logo=github)
![Version](https://img.shields.io/badge/Version-V0.0.1-red)
![Time](https://img.shields.io/badge/Join-20211122-green)
<!--auto_detail_badge_end_fef74f2d7ea73fcc43ff78e05b1e7451-->

Burpcrypto is a collection of burpsuite encryption plug-ins, supporting AES/RSA/DES/ExecJs(execute JS encryption code in burpsuite).

# Build
`$ mvn package`
# Usage
[中文使用说明](https://blog.wanghw.cn/burpcrypto)

- Download the precompiled jar package from [Releases](https://github.com/whwlsfb/BurpCrypto/releases).
- Add this jar package to your burpsuite's Extensions.
- Switch to BurpCrypto tab, select you need Cipher tab.
- Set key or some value.
- press "Add processor", and give a name for this processor.
- Switch to Intruder->Payloads->Payload Processing.
- press "Add", select "Invoke Burp extension", and select processor you just created.
- press "Start attack", have fun!

## Key Example

- Aes Key(UTF8String): abcdefgabcdefg12
- Aes IV(UTF8String): abcdefgabcdefg12
- Rsa X509 Key: MIGfMA0GCSqGSIb3DQEBAQUAA4GNADCBiQKBgQCC0hrRIjb3noDWNtbDpANbjt5Iwu2NFeDwU16Ec87ToqeoIm2KI+cOs81JP9aTDk/jkAlU97mN8wZkEMDr5utAZtMVht7GLX33Wx9XjqxUsDfsGkqNL8dXJklWDu9Zh80Ui2Ug+340d5dZtKtd+nv09QZqGjdnSp9PTfFDBY133QIDAQAB
- Rsa Modulus: ca27d90f03753cbbc9958011baf701ac99305b63f68e26ab5617593e01d2fb519127fb87bafbe6e0472ec3a038575fa292adadbc79390a955a61b29431f78f4734773048a45dcf100e23cabf2df11a55aa90cd6b024a44eed1096c3b9e1408d46aae54d7291b82fe4b7867c5eaa45e9cc0ba7f7ae3e5593337c7dcbace2d02ed2fbbff26c6df8a32bb26be80603fcd94c6c8dbd67878d77b37fedcf808e3d8f469aaa7c65d033d547a5c8ea9bdd5c89b836c65852f355a5efd9c7137a186a62b5eb0e052c8be3096d3b51133f8a8c108292a296c99d37bad42bcc3f6c39fa5e583582942b4fc4e7ff4b6779fff5bbaddc65b19c7c57d8cdb39b1a994e08d4a2f50793d8f707d069c380baf0f64bfdce3b35d0b5c5c59348a35a082012aaf4991080abf518b55787969ff24186cb95f7e7218c904cf1dcaeb5bed723e305b83f2e85d6f116d2c7400f9e49d904db8a5a3a0701cdb579fbf3128511acd0f789ece1233ed926d705b3b0dfa34bf33f5ae4bdc611a602aa03aaae13400bc7ad3813ea4474dc62de3d0cb1f5aac277d895a75d38f9b920938fa6b1de35bd6132798c122403c685bdb6e5e24bbd70cfb3e968da0b8affd398e539e7c1e7add09891780bcbd278f3900499ae09cee0dc62e3f92e70001bab6d46261d2801a37f80d84d0e39fce6eaedf106a61b5961960641b9db0e4e23c770e6370ac5d61c6c9eb0f07
- Rsa Exponent: 010001
- DES Key: 12345678
- DESede Key: 123456781234567812345678


## Screenshots

AES Example:

![](https://github.com/whwlsfb/BurpCrypto/raw/master/screenshot/aes.gif)

ExecJs Example (Here is the modified MD5 algorithm):

![](https://github.com/whwlsfb/BurpCrypto/raw/master/screenshot/execjs.gif)

Quick Crypto:

![](https://github.com/whwlsfb/BurpCrypto/raw/master/screenshot/quick_crypto.gif)


<!--auto_detail_active_begin_e1c6fb434b6f0baf6912c7a1934f772b-->
## 项目相关

- 2021-11-25 发布文章[《BurpCrypto : 万能网站密码爆破测试工具》](https://mp.weixin.qq.com/s/-paMF8IepVUue7HyVHiLmw)

## 最近更新

<!--auto_detail_active_end_f9cf7911015e9913b7e691a7a5878527-->
