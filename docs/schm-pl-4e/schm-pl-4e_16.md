# 形式总结

下表总结了在第[4](binding.html#g88)章至第[11](exceptions.html#g147)章中描述的Scheme语法形式和过程。它显示了形式的类别以及定义该形式的页码。类别说明该形式是描述语法形式还是过程。

所有出现在这里的页码均指向本书的印刷版本，并同时作为本书电子版本中相应位置的超文本链接。

| 形式 | 类别 | 页码 |
| --- | --- | --- |

|

* * *

|

| `'*obj*` | 语法 | [141](objects.html#./objects:s2) |
| --- | --- | --- |
| ``*obj*` | 语法 | [142](objects.html#./objects:s5) |
| `,*obj*` | 语法 | [142](objects.html#./objects:s5) |
| `,@*obj*` | 语法 | [142](objects.html#./objects:s5) |
| `=>` | 语法 | [112](control.html#./control:s16) |
| `_` | 语法 | [297](syntax.html#./syntax:s26) |
| `...` | 语法 | [297](syntax.html#./syntax:s26) |
| `#'*template*` | 语法 | [300](syntax.html#./syntax:s33) |
| `#`*template*` | 语法 | [305](syntax.html#./syntax:s40) |
| `#,*template*` | 语法 | [305](syntax.html#./syntax:s40) |
| `#,@*template*` | 语法 | [305](syntax.html#./syntax:s40) |
| `&assertion` | 语法 | [366](exceptions.html#./exceptions:s21) |
| `&condition` | 语法 | [362](exceptions.html#./exceptions:s13) |
| `&error` | 语法 | [367](exceptions.html#./exceptions:s22) |
| `&i/o` | 语法 | [371](exceptions.html#./exceptions:s32) |
| `&i/o-decoding` | 语法 | [375](exceptions.html#./exceptions:s42) |
| `&i/o-encoding` | 语法 | [376](exceptions.html#./exceptions:s43) |
| `&i/o-file-already-exists` | 语法 | [374](exceptions.html#./exceptions:s39) |
| `&i/o-file-does-not-exist` | ��法 | [374](exceptions.html#./exceptions:s40) |
| `&i/o-file-is-read-only` | 语法 | [374](exceptions.html#./exceptions:s38) |
| `&i/o-file-protection` | 语法 | [373](exceptions.html#./exceptions:s37) |
| `&i/o-filename` | 语法 | [373](exceptions.html#./exceptions:s36) |
| `&i/o-invalid-position` | 语法 | [372](exceptions.html#./exceptions:s35) |
| `&i/o-port` | 语法 | [375](exceptions.html#./exceptions:s41) |
| `&i/o-read` | 语法 | [372](exceptions.html#./exceptions:s33) |
| `&i/o-write` | 语法 | [372](exceptions.html#./exceptions:s34) |
| `&implementation-restriction` | 语法 | [369](exceptions.html#./exceptions:s28) |
| `&irritants` | 语法 | [368](exceptions.html#./exceptions:s25) |
| `&lexical` | 语法 | [370](exceptions.html#./exceptions:s29) |
| `&message` | 语法 | [368](exceptions.html#./exceptions:s24) |
| `&no-infinities` | 语法 | [376](exceptions.html#./exceptions:s44) |
| `&no-nans` | 语法 | [377](exceptions.html#./exceptions:s45) |
| `&non-continuable` | 语法 | [369](exceptions.html#./exceptions:s27) |
| `&serious` | 语法 | [366](exceptions.html#./exceptions:s19) |
| `&syntax` | 语法 | [370](exceptions.html#./exceptions:s30) |
| `&undefined` | 语法 | [371](exceptions.html#./exceptions:s31) |
| `&violation` | 语法 | [366](exceptions.html#./exceptions:s20) |
| `&warning` | 语法 | [367](exceptions.html#./exceptions:s23) |
| `&who` | 语法 | [369](exceptions.html#./exceptions:s26) |
| `(* *num* ...)` | 过程 | [172](objects.html#./objects:s91) |
| `(+ *num* ...)` | 过程 | [171](objects.html#./objects:s89) |
| `(- *num*)` | 过程 | [172](objects.html#./objects:s90) |
| `(- *num[1]* *num[2]* *num[3]* ...)` | 过程 | [172](objects.html#./objects:s90) |
| `(/ *num*)` | 过程 | [172](objects.html#./objects:s92) |
| `(/ *num[1]* *num[2]* *num[3]* ...)` | 过程 | [172](objects.html#./objects:s92) |
| `(< *real[1]* *real[2]* *real[3]* ...)` | 过程 | [170](objects.html#./objects:s88) |
| `(<= *real[1]* *real[2]* *real[3]* ...)` | 过程 | [170](objects.html#./objects:s88) |
| `(= *num[1]* *num[2]* *num[3]* ...)` | 过程 | [170](objects.html#./objects:s88) |
| `(> *real[1]* *real[2]* *real[3]* ...)` | 过程 | [170](objects.html#./objects:s88) |
| `(>= *real[1]* *real[2]* *real[3]* ...)` | 过程 | [170](objects.html#./objects:s88) |
| `(abs *real*)` | 过程 | [178](objects.html#./objects:s105) |
| `(acos *num*)` | 过程 | [185](objects.html#./objects:s132) |
| `(and *expr* ...)` | 语法 | [110](control.html#./control:s11) |
| `(angle *num*)` | 过程 | [183](objects.html#./objects:s124) |
| `(append)` | 过程 | [160](objects.html#./objects:s49) |
| `(append *list* ... *obj*)` | 过程 | [160](objects.html#./objects:s49) |
| `(apply *procedure* *obj* ... *list*)` | 过程 | [107](control.html#./control:s3) |
| `(asin *num*)` | 过程 | [185](objects.html#./objects:s132) |
| `(assert *expression*)` | 语法 | [359](exceptions.html#./exceptions:s5) |
| `(assertion-violation *who* *msg* *irritant* ...)` | 过程 | [358](exceptions.html#./exceptions:s4) |
| `(assertion-violation? *obj*)` | 过程 | [366](exceptions.html#./exceptions:s21) |
| `(assoc *obj* *alist*)` | 过程 | [165](objects.html#./objects:s58) |
| `(assp *procedure* *alist*)` | 过程 | [166](objects.html#./objects:s60) |
| `(assq *obj* *alist*)` | 过程 | [165](objects.html#./objects:s58) |
| `(assv *obj* *alist*)` | 过程 | [165](objects.html#./objects:s58) |
| `(atan *num*)` | 过程 | [185](objects.html#./objects:s133) |
| `(atan *real[1]* *real[2]*)` | 过程 | [185](objects.html#./objects:s133) |
| `(begin *expr[1]* *expr[2]* ...)` | 语法 | [108](control.html#./control:s4) |
| `(binary-port? *obj*)` | 过程 | [270](io.html#./io:s45) |
| `(bitwise-and *exint* ...)` | 过程 | [186](objects.html#./objects:s134) |
| `(bitwise-arithmetic-shift *exint[1]* *exint[2]*)` | 过程 | [190](objects.html#./objects:s144) |
| `(bitwise-arithmetic-shift-left *exint[1]* *exint[2]*)` | 过程 | [189](objects.html#./objects:s143) |
| `(bitwise-arithmetic-shift-right *exint[1]* *exint[2]*)` | 过程 | [189](objects.html#./objects:s143) |
| `(按位位计数 *exint*)` | 过程 | [187](objects.html#./objects:s136) |
| `(按位位字段 *exint[1]* *exint[2]* *exint[3]*)` | 过程 | [189](objects.html#./objects:s141) |
| `(按位位设置? *exint[1]* *exint[2]*)` | 过程 | [188](objects.html#./objects:s139) |
| `(按位复制位 *exint[1]* *exint[2]* *exint[3]*)` | 过程 | [188](objects.html#./objects:s140) |
| `(按位复制位字段 *exint[1]* *exint[2]* *exint[3]* *exint[4]*)` | 过程 | [189](objects.html#./objects:s142) |
| `(按位第一个位设置 *exint*)` | 过程 | [187](objects.html#./objects:s138) |
| `(按位条件 *exint[1]* *exint[2]* *exint[3]*)` | 过程 | [186](objects.html#./objects:s135) |
| `(按位或 *exint* ...)` | 过程 | [186](objects.html#./objects:s134) |
| `(按位长度 *exint*)` | 过程 | [187](objects.html#./objects:s137) |
| `(按位非 *exint*)` | 过程 | [186](objects.html#./objects:s134) |
| `(按位反转位字段 *exint[1]* *exint[2]* *exint[3]*)` | 过程 | [191](objects.html#./objects:s146) |
| `(按位旋转位字段 *exint[1]* *exint[2]* *exint[3]* *exint[4]*)` | 过程 | [190](objects.html#./objects:s145) |
| `(按位异或 *exint* ...)` | 过程 | [186](objects.html#./objects:s134) |
| `(布尔=? *boolean[1]* *boolean[2]*)` | 过程 | [243](objects.html#./objects:s271) |
| `(布尔? *obj*)` | 过程 | [150](objects.html#./objects:s14) |
| `(绑定标识符=? *identifier[1]* *identifier[2]*)` | 过程 | [302](syntax.html#./syntax:s37) |
| `(缓冲区模式 *symbol*)` | 语法 | [261](io.html#./io:s27) |
| `(缓冲区模式? *obj*)` | 语法 | [262](io.html#./io:s28) |
| `(字节向量->有符号整数列表 *bytevector* *eness* *size*)` | 过程 | [238](objects.html#./objects:s260) |
| `(字节向量->字符串 *bytevector* *transcoder*)` | 过程 | [286](io.html#./io:s91) |
| `(字节向量->u8列表 *bytevector*)` | 过程 | [232](objects.html#./objects:s252) |
| `(字节向量->无符号整数列表 *bytevector* *eness* *size*)` | 过程 | [238](objects.html#./objects:s260) |
| `(字节向量复制 *bytevector*)` | 过程 | [229](objects.html#./objects:s246) |
| `(字节向量复制! *src* *src-start* *dst* *dst-start* *n*)` | 过程 | [230](objects.html#./objects:s247) |
| `(字节向量填充! *bytevector* *fill*)` | 过程 | [229](objects.html#./objects:s245) |
| `(字节向量IEEE双精度本机引用 *bytevector* *n*)` | 过程 | [239](objects.html#./objects:s262) |
| `(字节向量IEEE双精度本机设置! *bytevector* *n* *x*)` | 过程 | [239](objects.html#./objects:s263) |
| `(字节向量IEEE双精度引用 *bytevector* *n* *eness*)` | 过程 | [240](objects.html#./objects:s264) |
| `(字节向量IEEE双精度设置! *bytevector* *n* *x* *eness*)` | 过程 | [240](objects.html#./objects:s265) |
| `(字节向量IEEE单精度本机引用 *bytevector* *n*)` | 过程 | [239](objects.html#./objects:s262) |
| `(bytevector-ieee-single-native-set! *bytevector* *n* *x*)` | 过程 | [239](objects.html#./objects:s263) |
| `(bytevector-ieee-single-ref *bytevector* *n* *eness*)` | 过程 | [240](objects.html#./objects:s264) |
| `(bytevector-ieee-single-set! *bytevector* *n* *x* *eness*)` | 过程 | [240](objects.html#./objects:s265) |
| `(bytevector-length *bytevector*)` | 过程 | [229](objects.html#./objects:s243) |
| `(bytevector-s16-native-ref *bytevector* *n*)` | 过程 | [232](objects.html#./objects:s254) |
| `(bytevector-s16-native-set! *bytevector* *n* *s16*)` | 过程 | [233](objects.html#./objects:s255) |
| `(bytevector-s16-ref *bytevector* *n* *eness*)` | 过程 | [235](objects.html#./objects:s256) |
| `(bytevector-s16-set! *bytevector* *n* *s16* *eness*)` | 过程 | [236](objects.html#./objects:s257) |
| `(bytevector-s32-native-ref *bytevector* *n*)` | 过程 | [232](objects.html#./objects:s254) |
| `(bytevector-s32-native-set! *bytevector* *n* *s32*)` | 过程 | [233](objects.html#./objects:s255) |
| `(bytevector-s32-ref *bytevector* *n* *eness*)` | 过程 | [235](objects.html#./objects:s256) |
| `(bytevector-s32-set! *bytevector* *n* *s32* *eness*)` | 过程 | [236](objects.html#./objects:s257) |
| `(bytevector-s64-native-ref *bytevector* *n*)` | 过程 | [232](objects.html#./objects:s254) |
| `(bytevector-s64-native-set! *bytevector* *n* *s64*)` | 过程 | [233](objects.html#./objects:s255) |
| `(bytevector-s64-ref *bytevector* *n* *eness*)` | 过程 | [235](objects.html#./objects:s256) |
| `(bytevector-s64-set! *bytevector* *n* *s64* *eness*)` | 过程 | [236](objects.html#./objects:s257) |
| `(bytevector-s8-ref *bytevector* *n*)` | 过程 | [231](objects.html#./objects:s249) |
| `(bytevector-s8-set! *bytevector* *n* *s8*)` | 过程 | [231](objects.html#./objects:s251) |
| `(bytevector-sint-ref *bytevector* *n* *eness* *size*)` | 过程 | [237](objects.html#./objects:s258) |
| `(bytevector-sint-set! *bytevector* *n* *sint* *eness* *size*)` | 过程 | [238](objects.html#./objects:s259) |
| `(bytevector-u16-native-ref *bytevector* *n*)` | 过程 | [232](objects.html#./objects:s254) |
| `(bytevector-u16-native-set! *bytevector* *n* *u16*)` | 过程 | [233](objects.html#./objects:s255) |
| `(bytevector-u16-ref *bytevector* *n* *eness*)` | 过程 | [235](objects.html#./objects:s256) |
| `(bytevector-u16-set! *bytevector* *n* *u16* *eness*)` | 过程 | [236](objects.html#./objects:s257) |
| `(bytevector-u32-native-ref *bytevector* *n*)` | 过程 | [232](objects.html#./objects:s254) |
| `(bytevector-u32-native-set! *bytevector* *n* *u32*)` | 过程 | [233](objects.html#./objects:s255) |
| `(bytevector-u32-ref *bytevector* *n* *eness*)` | 过程 | [235](objects.html#./objects:s256) |
| `(bytevector-u32-set! *bytevector* *n* *u32* *eness*)` | 过程 | [236](objects.html#./objects:s257) |
| `(bytevector-u64-native-ref *bytevector* *n*)` | 过程 | [232](objects.html#./objects:s254) |
| `(bytevector-u64-native-set! *bytevector* *n* *u64*)` | 过程 | [233](objects.html#./objects:s255) |
| `(bytevector-u64-ref *bytevector* *n* *eness*)` | 过程 | [235](objects.html#./objects:s256) |
| `(bytevector-u64-set! *bytevector* *n* *u64* *eness*)` | 过程 | [236](objects.html#./objects:s257) |
| `(bytevector-u8-ref *bytevector* *n*)` | 过程 | [230](objects.html#./objects:s248) |
| `(bytevector-u8-set! *bytevector* *n* *u8*)` | 过程 | [231](objects.html#./objects:s250) |
| `(bytevector-uint-ref *bytevector* *n* *eness* *size*)` | 过程 | [237](objects.html#./objects:s258) |
| `(bytevector-uint-set! *bytevector* *n* *uint* *eness* *size*)` | 过程 | [238](objects.html#./objects:s259) |
| `(bytevector=? *bytevector[1]* *bytevector[2]*)` | 过程 | [229](objects.html#./objects:s244) |
| `(bytevector? *obj*)` | 过程 | [155](objects.html#./objects:s24) |
| `(caaaar *pair*)` | 过程 | [157](objects.html#./objects:s42) |
| `(caaadr *pair*)` | 过程 | [157](objects.html#./objects:s42) |
| `(caaar *pair*)` | 过程 | [157](objects.html#./objects:s42) |
| `(caadar *pair*)` | 过程 | [157](objects.html#./objects:s42) |
| `(caaddr *pair*)` | 过程 | [157](objects.html#./objects:s42) |
| `(caadr *pair*)` | 过程 | [157](objects.html#./objects:s42) |
| `(caar *pair*)` | 过程 | [157](objects.html#./objects:s42) |
| `(cadaar *pair*)` | 过程 | [157](objects.html#./objects:s42) |
| `(cadadr *pair*)` | 过程 | [157](objects.html#./objects:s42) |
| `(cadar *pair*)` | 过程 | [157](objects.html#./objects:s42) |
| `(caddar *pair*)` | 过程 | [157](objects.html#./objects:s42) |
| `(cadddr *pair*)` | 过程 | [157](objects.html#./objects:s42) |
| `(caddr *pair*)` | 过程 | [157](objects.html#./objects:s42) |
| `(cadr *pair*)` | 过程 | [157](objects.html#./objects:s42) |
| `(call-with-bytevector-output-port *procedure*)` | 过程 | [266](io.html#./io:s38) |
| `(call-with-bytevector-output-port *procedure* *?transcoder*)` | 过程 | [266](io.html#./io:s38) |
| `(call-with-current-continuation *procedure*)` | 过程 | [123](control.html#./control:s54) |
| `(call-with-input-file *path* *procedure*)` | 过程 | [281](io.html#./io:s77) |
| `(call-with-output-file *path* *procedure*)` | 过程 | [282](io.html#./io:s78) |
| `(call-with-port *port* *procedure*)` | 过程 | [272](io.html#./io:s51) |
| `(call-with-string-output-port *procedure*)` | 过程 | [267](io.html#./io:s39) |
| `(call-with-values *producer* *consumer*)` | 过程 | [131](control.html#./control:s71) |
| `(call/cc *procedure*)` | 过程 | [123](control.html#./control:s54) |
| `(car *pair*)` | 过程 | [156](objects.html#./objects:s38) |
| `(case *expr[0]* *clause[1]* *clause[2]* ...)` | 语法 | [113](control.html#./control:s18) |
| `(case-lambda *clause* ...)` | 语法 | [94](binding.html#./binding:s13) |
| `(cdaaar *pair*)` | 过程 | [157](objects.html#./objects:s42) |
| `(cdaadr *pair*)` | 过程 | [157](objects.html#./objects:s42) |
| `(cdaar *pair*)` | 过程 | [157](objects.html#./objects:s42) |
| `(cdadar *pair*)` | 过程 | [157](objects.html#./objects:s42) |
| `(cdaddr *pair*)` | 过程 | [157](objects.html#./objects:s42) |
| `(cdadr *pair*)` | 过程 | [157](objects.html#./objects:s42) |
| `(cdar *pair*)` | 过程 | [157](objects.html#./objects:s42) |
| `(cddaar *pair*)` | 过程 | [157](objects.html#./objects:s42) |
| `(cddadr *pair*)` | 过程 | [157](objects.html#./objects:s42) |
| `(cddar *pair*)` | 过程 | [157](objects.html#./objects:s42) |
| `(cdddar *pair*)` | 过程 | [157](objects.html#./objects:s42) |
| `(cddddr *pair*)` | 过程 | [157](objects.html#./objects:s42) |
| `(cdddr *pair*)` | 过程 | [157](objects.html#./objects:s42) |
| `(cddr *pair*)` | 过程 | [157](objects.html#./objects:s42) |
| `(cdr *pair*)` | 过程 | [156](objects.html#./objects:s39) |
| `(ceiling *real*)` | 过程 | [177](objects.html#./objects:s103) |
| `(char->integer *char*)` | 过程 | [215](objects.html#./objects:s210) |
| `(char-alphabetic? *char*)` | 过程 | [213](objects.html#./objects:s203) |
| `(char-ci<=? *char[1]* *char[2]* *char[3]* ...)` | 过程 | [212](objects.html#./objects:s202) |
| `(char-ci<? *char[1]* *char[2]* *char[3]* ...)` | 过程 | [212](objects.html#./objects:s202) |
| `(char-ci=? *char[1]* *char[2]* *char[3]* ...)` | 过程 | [212](objects.html#./objects:s202) |
| `(char-ci>=? *char[1]* *char[2]* *char[3]* ...)` | 过程 | [212](objects.html#./objects:s202) |
| `(char-ci>? *char[1]* *char[2]* *char[3]* ...)` | 过程 | [212](objects.html#./objects:s202) |
| `(char-downcase *char*)` | 过程 | [214](objects.html#./objects:s207) |
| `(char-foldcase *char*)` | 过程 | [215](objects.html#./objects:s209) |
| `(char-general-category *char*)` | 过程 | [214](objects.html#./objects:s205) |
| `(char-lower-case? *char*)` | 过程 | [213](objects.html#./objects:s204) |
| `(char-numeric? *char*)` | 过程 | [213](objects.html#./objects:s203) |
| `(char-title-case? *char*)` | 过程 | [213](objects.html#./objects:s204) |
| `(char-titlecase *char*)` | 过程 | [214](objects.html#./objects:s208) |
| `(char-upcase *char*)` | 过程 | [214](objects.html#./objects:s206) |
| `(char-upper-case? *char*)` | 过程 | [213](objects.html#./objects:s204) |
| `(char-whitespace? *char*)` | 过程 | [213](objects.html#./objects:s203) |
| `(char<=? *char[1]* *char[2]* *char[3]* ...)` | 过程 | [212](objects.html#./objects:s201) |
| `(char<? *char[1]* *char[2]* *char[3]* ...)` | 过程 | [212](objects.html#./objects:s201) |
| `(char=? *char[1]* *char[2]* *char[3]* ...)` | 过程 | [212](objects.html#./objects:s201) |
| `(char>=? *char[1]* *char[2]* *char[3]* ...)` | 过程 | [212](objects.html#./objects:s201) |
| `(char>? *char[1]* *char[2]* *char[3]* ...)` | 过程 | [212](objects.html#./objects:s201) |
| `(char? *obj*)` | 过程 | [154](objects.html#./objects:s19) |
| `(close-input-port *input-port*)` | 过程 | [285](io.html#./io:s88) |
| `(close-output-port *output-port*)` | 过程 | [285](io.html#./io:s88) |
| `(close-port *port*)` | 过程 | [270](io.html#./io:s46) |
| `(command-line)` | 过程 | [350](libraries.html#./libraries:s17) |
| `(complex? *obj*)` | 过程 | [151](objects.html#./objects:s17) |
| `(cond *clause[1]* *clause[2]* ...)` | 语法 | [111](control.html#./control:s13) |
| `(condition *condition* ...)` | 过程 | [362](exceptions.html#./exceptions:s15) |
| `(condition-accessor *rtd* *procedure*)` | 过程 | [365](exceptions.html#./exceptions:s18) |
| `(condition-irritants *condition*)` | 过程 | [368](exceptions.html#./exceptions:s25) |
| `(condition-message *condition*)` | 过程 | [368](exceptions.html#./exceptions:s24) |
| `(condition-predicate *rtd*)` | 过程 | [365](exceptions.html#./exceptions:s18) |
| `(condition-who *condition*)` | 过程 | [369](exceptions.html#./exceptions:s26) |
| `(condition? *obj*)` | 过程 | [362](exceptions.html#./exceptions:s14) |
| `(cons *obj[1]* *obj[2]*)` | 过程 | [156](objects.html#./objects:s37) |
| `(cons* *obj* ... *final-obj*)` | 过程 | [158](objects.html#./objects:s44) |
| `*constant*` | 语法 | [141](objects.html#./objects:s1) |
| `(cos *num*)` | 过程 | [185](objects.html#./objects:s131) |
| `(current-error-port)` | 过程 | [263](io.html#./io:s32) |
| `(current-input-port)` | 过程 | [263](io.html#./io:s32) |
| `(current-output-port)` | 过程 | [263](io.html#./io:s32) |
| `(datum->syntax *template-identifier* *obj*)` | 过程 | [308](syntax.html#./syntax:s45) |
| `(define *var* *expr*)` | 语法 | [100](binding.html#./binding:s24) |
| `(define *var*)` | 语法 | [100](binding.html#./binding:s24) |
| `(define (*var[0]* *var[1]* ...) *body[1]* *body[2]* ...)` | 语法 | [100](binding.html#./binding:s24) |
| `(define (*var[0]* . *var[r]*) *body[1]* *body[2]* ...)` | 语法 | [100](binding.html#./binding:s24) |
| `(define (*var[0]* *var[1]* *var[2]* ... . *var[r]*) *body[1]* *body[2]* ...)` | 语法 | [100](binding.html#./binding:s24) |
| `(define-condition-type *name* *parent* *constructor* *pred* *field* ...)` | 语法 | [364](exceptions.html#./exceptions:s17) |
| `(define-enumeration *name* (*symbol* ...) *constructor*)` | 语法 | [250](objects.html#./objects:s290) |
| `(define-record-type *record-name* *clause* ...)` | 语法 | [328](records.html#./records:s13) |
| `(define-record-type (*record-name* *constructor* *pred*) *clause* ...)` | 语法 | [328](records.html#./records:s13) |
| `(define-syntax *keyword* *expr*)` | 语法 | [292](syntax.html#./syntax:s12) |
| `(delay *expr*)` | 语法 | [128](control.html#./control:s65) |
| `(delete-file *path*)` | 过程 | [286](io.html#./io:s90) |
| `(denominator *rat*)` | 过程 | [181](objects.html#./objects:s119) |
| `(display *obj*)` | 过程 | [285](io.html#./io:s85) |
| `(display *obj* *textual-output-port*)` | 过程 | [285](io.html#./io:s85) |
| `(div *x[1]* *x[2]*)` | 过程 | [175](objects.html#./objects:s99) |
| `(div-and-mod *x[1]* *x[2]*)` | 过程 | [175](objects.html#./objects:s99) |
| `(div0 *x[1]* *x[2]*)` | 过程 | [176](objects.html#./objects:s100) |
| `(div0-and-mod0 *x[1]* *x[2]*)` | 过程 | [176](objects.html#./objects:s100) |
| `(do ((*var* *init* *update*) ...) (*test* *result* ...) *expr* ...)` | 语法 | [115](control.html#./control:s25) |
| `(dynamic-wind *in* *body* *out*)` | 过程 | [124](control.html#./control:s56) |
| `else` | 语法 | [112](control.html#./control:s16) |
| `(endianness *symbol*)` | 语法 | [228](objects.html#./objects:s240) |
| `(enum-set->list *enum-set*)` | 过程 | [252](objects.html#./objects:s294) |
| `(enum-set-complement *enum-set*)` | 过程 | [254](objects.html#./objects:s299) |
| `(enum-set-constructor *enum-set*)` | 过程 | [251](objects.html#./objects:s292) |
| `(enum-set-difference *enum-set[1]* *enum-set[2]*)` | 过程 | [253](objects.html#./objects:s298) |
| `(enum-set-indexer *enum-set*)` | 过程 | [254](objects.html#./objects:s301) |
| `(enum-set-intersection *enum-set[1]* *enum-set[2]*)` | 过程 | [253](objects.html#./objects:s298) |
| `(enum-set-member? *symbol* *enum-set*)` | 过程 | [253](objects.html#./objects:s297) |
| `(enum-set-projection *enum-set[1]* *enum-set[2]*)` | 过程 | [254](objects.html#./objects:s300) |
| `(enum-set-subset? *enum-set[1]* *enum-set[2]*)` | 过程 | [252](objects.html#./objects:s295) |
| `(enum-set-union *enum-set[1]* *enum-set[2]*)` | 过程 | [253](objects.html#./objects:s298) |
| `(enum-set-universe *enum-set*)` | 过程 | [252](objects.html#./objects:s293) |
| `(enum-set=? *enum-set[1]* *enum-set[2]*)` | 过程 | [252](objects.html#./objects:s296) |
| `(environment *import-spec* ...)` | 过程 | [137](control.html#./control:s81) |
| `(eof-object)` | 过程 | [273](io.html#./io:s54) |
| `(eof-object? *obj*)` | 过程 | [273](io.html#./io:s53) |
| `(eol-style *symbol*)` | 语法 | [259](io.html#./io:s23) |
| `(eq? *obj[1]* *obj[2]*)` | 过程 | [143](objects.html#./objects:s10) |
| `(equal-hash *obj*)` | 过程 | [245](objects.html#./objects:s279) |
| `(equal? *obj[1]* *obj[2]*)` | 过程 | [148](objects.html#./objects:s13) |
| `(eqv? *obj[1]* *obj[2]*)` | 过程 | [146](objects.html#./objects:s12) |
| `(error *who* *msg* *irritant* ...)` | 过程 | [358](exceptions.html#./exceptions:s4) |
| `(error-handling-mode *symbol*)` | 语法 | [260](io.html#./io:s25) |
| `(error? *obj*)` | 过程 | [367](exceptions.html#./exceptions:s22) |
| `(eval *obj* *environment*)` | 过程 | [136](control.html#./control:s80) |
| `(even? *int*)` | 过程 | [174](objects.html#./objects:s96) |
| `(exact *num*)` | 过程 | [180](objects.html#./objects:s114) |
| `(exact->inexact *num*)` | 过程 | [181](objects.html#./objects:s116) |
| `(exact-integer-sqrt *n*)` | 过程 | [184](objects.html#./objects:s128) |
| `(exact? *num*)` | 过程 | [170](objects.html#./objects:s86) |
| `(exists *procedure* *list[1]* *list[2]* ...)` | 过程 | [119](control.html#./control:s36) |
| `(exit)` | 过程 | [350](libraries.html#./libraries:s18) |
| `(exit *obj*)` | 过程 | [350](libraries.html#./libraries:s18) |
| `(exp *num*)` | 过程 | [184](objects.html#./objects:s129) |
| `(expt *num[1]* *num[2]*)` | 过程 | [179](objects.html#./objects:s111) |
| `fields` | 语法 | [331](records.html#./records:s16) |
| `(file-exists? *path*)` | 过程 | [286](io.html#./io:s89) |
| `(file-options *symbol* ...)` | 语法 | [261](io.html#./io:s26) |
| `(filter *procedure* *list*)` | 过程 | [164](objects.html#./objects:s55) |
| `(find *procedure* *list*)` | 过程 | [165](objects.html#./objects:s57) |
| `(finite? *real*)` | 过程 | [174](objects.html#./objects:s97) |
| `(fixnum->flonum *fx*)` | 过程 | [211](objects.html#./objects:s198) |
| `(fixnum-width)` | 过程 | [193](objects.html#./objects:s152) |
| `(fixnum? *obj*)` | 过程 | [193](objects.html#./objects:s150) |
| `(fl* *fl* ...)` | 过程 | [207](objects.html#./objects:s186) |
| `(fl+ *fl* ...)` | 过程 | [206](objects.html#./objects:s184) |
| `(fl- *fl*)` | 过程 | [206](objects.html#./objects:s185) |
| `(fl- *fl[1]* *fl[2]* *fl[3]* ...)` | 过程 | [206](objects.html#./objects:s185) |
| `(fl/ *fl*)` | 过程 | [207](objects.html#./objects:s187) |
| `(fl/ *fl[1]* *fl[2]* *fl[3]* ...)` | 过程 | [207](objects.html#./objects:s187) |
| `(fl<=? *fl[1]* *fl[2]* *fl[3]* ...)` | 过程 | [203](objects.html#./objects:s178) |
| `(fl<? *fl[1]* *fl[2]* *fl[3]* ...)` | 过程 | [203](objects.html#./objects:s178) |
| `(fl=? *fl[1]* *fl[2]* *fl[3]* ...)` | 过程 | [203](objects.html#./objects:s178) |
| `(fl>=? *fl[1]* *fl[2]* *fl[3]* ...)` | 过程 | [203](objects.html#./objects:s178) |
| `(fl>? *fl[1]* *fl[2]* *fl[3]* ...)` | 过程 | [203](objects.html#./objects:s178) |
| `(flabs *fl*)` | 过程 | [209](objects.html#./objects:s192) |
| `(flacos *fl*)` | 过程 | [210](objects.html#./objects:s195) |
| `(flasin *fl*)` | 过程 | [210](objects.html#./objects:s195) |
| `(flatan *fl*)` | 过程 | [210](objects.html#./objects:s195) |
| `(flatan *fl[1]* *fl[2]*)` | 过程 | [210](objects.html#./objects:s195) |
| `(flceiling *fl*)` | 过程 | [208](objects.html#./objects:s190) |
| `(flcos *fl*)` | 过程 | [210](objects.html#./objects:s194) |
| `(fldenominator *fl*)` | 过程 | [209](objects.html#./objects:s191) |
| `(fldiv *fl[1]* *fl[2]*)` | 过程 | [207](objects.html#./objects:s188) |
| `(fldiv-and-mod *fl[1]* *fl[2]*)` | 过程 | [207](objects.html#./objects:s188) |
| `(fldiv0 *fl[1]* *fl[2]*)` | 过程 | [208](objects.html#./objects:s189) |
| `(fldiv0-and-mod0 *fl[1]* *fl[2]*)` | 过程 | [208](objects.html#./objects:s189) |
| `(fleven? *fl-int*)` | 过程 | [205](objects.html#./objects:s182) |
| `(flexp *fl*)` | 过程 | [209](objects.html#./objects:s193) |
| `(flexpt *fl[1]* *fl[2]*)` | 过程 | [210](objects.html#./objects:s197) |
| `(flfinite? *fl*)` | 过程 | [205](objects.html#./objects:s181) |
| `(flfloor *fl*)` | 过程 | [208](objects.html#./objects:s190) |
| `(flinfinite? *fl*)` | 过程 | [205](objects.html#./objects:s181) |
| `(flinteger? *fl*)` | 过程 | [204](objects.html#./objects:s180) |
| `(fllog *fl*)` | 过程 | [209](objects.html#./objects:s193) |
| `(fllog *fl[1]* *fl[2]*)` | 过程 | [209](objects.html#./objects:s193) |
| `(flmax *fl[1]* *fl[2]* ...)` | 过程 | [205](objects.html#./objects:s183) |
| `(flmin *fl[1]* *fl[2]* ...)` | 过程 | [205](objects.html#./objects:s183) |
| `(flmod *fl[1]* *fl[2]*)` | 过程 | [207](objects.html#./objects:s188) |
| `(flmod0 *fl[1]* *fl[2]*)` | 过程 | [208](objects.html#./objects:s189) |
| `(flnan? *fl*)` | 过程 | [205](objects.html#./objects:s181) |
| `(flnegative? *fl*)` | 过程 | [204](objects.html#./objects:s179) |
| `(flnumerator *fl*)` | 过程 | [209](objects.html#./objects:s191) |
| `(flodd? *fl-int*)` | 过程 | [205](objects.html#./objects:s182) |
| `(flonum? *obj*)` | 过程 | [203](objects.html#./objects:s177) |
| `(floor *real*)` | 过程 | [177](objects.html#./objects:s102) |
| `(flpositive? *fl*)` | 过程 | [204](objects.html#./objects:s179) |
| `(flround *fl*)` | 过程 | [208](objects.html#./objects:s190) |
| `(flsin *fl*)` | 过程 | [210](objects.html#./objects:s194) |
| `(flsqrt *fl*)` | 过程 | [210](objects.html#./objects:s196) |
| `(fltan *fl*)` | 过程 | [210](objects.html#./objects:s194) |
| `(fltruncate *fl*)` | 过程 | [208](objects.html#./objects:s190) |
| `(flush-output-port *output-port*)` | 过程 | [280](io.html#./io:s74) |
| `(flzero? *fl*)` | 过程 | [204](objects.html#./objects:s179) |
| `(fold-left *procedure* *obj* *list[1]* *list[2]* ...)` | 过程 | [120](control.html#./control:s38) |
| `(fold-right *procedure* *obj* *list[1]* *list[2]* ...)` | 过程 | [121](control.html#./control:s41) |
| `(for-all *procedure* *list[1]* *list[2]* ...)` | 过程 | [119](control.html#./control:s37) |
| `(for-each *procedure* *list[1]* *list[2]* ...)` | 过程 | [118](control.html#./control:s33) |
| `(force *promise*)` | 过程 | [128](control.html#./control:s65) |
| `(free-identifier=? *identifier[1]* *identifier[2]*)` | 过程 | [302](syntax.html#./syntax:s37) |
| `(fx* *fx[1]* *fx[2]*)` | 过程 | [195](objects.html#./objects:s159) |
| `(fx*/carry *fx[1]* *fx[2]* *fx[3]*)` | 过程 | [197](https://objects.html#./objects:s162) |
| `(fx+ *fx[1]* *fx[2]*)` | 过程 | [195](https://objects.html#./objects:s157) |
| `(fx+/carry *fx[1]* *fx[2]* *fx[3]*)` | 过程 | [197](https://objects.html#./objects:s162) |
| `(fx- *fx*)` | 过程 | [195](https://objects.html#./objects:s158) |
| `(fx- *fx[1]* *fx[2]*)` | 过程 | [195](https://objects.html#./objects:s158) |
| `(fx-/carry *fx[1]* *fx[2]* *fx[3]*)` | 过程 | [197](https://objects.html#./objects:s162) |
| `(fx<=? *fx[1]* *fx[2]* *fx[3]* ...)` | 过程 | [193](https://objects.html#./objects:s153) |
| `(fx<? *fx[1]* *fx[2]* *fx[3]* ...)` | 过程 | [193](https://objects.html#./objects:s153) |
| `(fx=? *fx[1]* *fx[2]* *fx[3]* ...)` | 过程 | [193](https://objects.html#./objects:s153) |
| `(fx>=? *fx[1]* *fx[2]* *fx[3]* ...)` | 过程 | [193](https://objects.html#./objects:s153) |
| `(fx>? *fx[1]* *fx[2]* *fx[3]* ...)` | 过程 | [193](https://objects.html#./objects:s153) |
| `(fxand *fx* ...)` | 过程 | [197](https://objects.html#./objects:s163) |
| `(fxarithmetic-shift *fx[1]* *fx[2]*)` | 过程 | [201](https://objects.html#./objects:s173) |
| `(fxarithmetic-shift-left *fx[1]* *fx[2]*)` | 过程 | [201](https://objects.html#./objects:s172) |
| `(fxarithmetic-shift-right *fx[1]* *fx[2]*)` | 过程 | [201](https://objects.html#./objects:s172) |
| `(fxbit-count *fx*)` | 过程 | [198](https://objects.html#./objects:s165) |
| `(fxbit-field *fx[1]* *fx[2]* *fx[3]*)` | 过程 | [200](https://objects.html#./objects:s170) |
| `(fxbit-set? *fx[1]* *fx[2]*)` | 过程 | [199](https://objects.html#./objects:s168) |
| `(fxcopy-bit *fx[1]* *fx[2]* *fx[3]*)` | 过程 | [200](https://objects.html#./objects:s169) |
| `(fxcopy-bit-field *fx[1]* *fx[2]* *fx[3]* *fx[4]*)` | 过程 | [200](https://objects.html#./objects:s171) |
| `(fxdiv *fx[1]* *fx[2]*)` | 过程 | [196](https://objects.html#./objects:s160) |
| `(fxdiv-and-mod *fx[1]* *fx[2]*)` | 过程 | [196](https://objects.html#./objects:s160) |
| `(fxdiv0 *fx[1]* *fx[2]*)` | 过程 | [196](https://objects.html#./objects:s161) |
| `(fxdiv0-and-mod0 *fx[1]* *fx[2]*)` | 过程 | [196](https://objects.html#./objects:s161) |
| `(fxeven? *fx*)` | 过程 | [194](https://objects.html#./objects:s155) |
| `(fxfirst-bit-set *fx*)` | 过程 | [199](https://objects.html#./objects:s167) |
| `(fxif *fx[1]* *fx[2]* *fx[3]*)` | 过程 | [198](https://objects.html#./objects:s164) |
| `(fxior *fx* ...)` | 过程 | [197](https://objects.html#./objects:s163) |
| `(fxlength *fx*)` | 过程 | [198](https://objects.html#./objects:s166) |
| `(fxmax *fx[1]* *fx[2]* ...)` | 过程 | [195](https://objects.html#./objects:s156) |
| `(fxmin *fx[1]* *fx[2]* ...)` | 过程 | [195](https://objects.html#./objects:s156) |
| `(fxmod *fx[1]* *fx[2]*)` | 过程 | [196](https://objects.html#./objects:s160) |
| `(fxmod0 *fx[1]* *fx[2]*)` | 过程 | [196](https://objects.html#./objects:s161) |
| `(fxnegative? *fx*)` | 过程 | [194](https://objects.html#./objects:s154) |
| `(fxnot *fx*)` | 过程 | [197](https://objects.html#./objects:s163) |
| `(fxodd? *fx*)` | 过程 | [194](https://objects.html#./objects:s155) |
| `(fxpositive? *fx*)` | 过程 | [194](objects.html#./objects:s154) |
| `(fxreverse-bit-field *fx[1]* *fx[2]* *fx[3]*)` | 过程 | [202](objects.html#./objects:s175) |
| `(fxrotate-bit-field *fx[1]* *fx[2]* *fx[3]* *fx[4]*)` | 过程 | [201](objects.html#./objects:s174) |
| `(fxxor *fx* ...)` | 过程 | [197](objects.html#./objects:s163) |
| `(fxzero? *fx*)` | 过程 | [194](objects.html#./objects:s154) |
| `(gcd *int* ...)` | 过程 | [179](objects.html#./objects:s109) |
| `(generate-temporaries *list*)` | 过程 | [310](syntax.html#./syntax:s49) |
| `(get-bytevector-all *binary-input-port*)` | 过程 | [275](io.html#./io:s60) |
| `(get-bytevector-n *binary-input-port* *n*)` | 过程 | [274](io.html#./io:s57) |
| `(get-bytevector-n! *binary-input-port* *bytevector* *start* *n*)` | 过程 | [274](io.html#./io:s58) |
| `(get-bytevector-some *binary-input-port*)` | 过程 | [275](io.html#./io:s59) |
| `(get-char *textual-input-port*)` | 过程 | [275](io.html#./io:s61) |
| `(get-datum *textual-input-port*)` | 过程 | [278](io.html#./io:s67) |
| `(get-line *textual-input-port*)` | 过程 | [277](io.html#./io:s66) |
| `(get-string-all *textual-input-port*)` | 过程 | [277](io.html#./io:s65) |
| `(get-string-n *textual-input-port* *n*)` | 过程 | [276](io.html#./io:s63) |
| `(get-string-n! *textual-input-port* *string* *start* *n*)` | 过程 | [276](io.html#./io:s64) |
| `(get-u8 *binary-input-port*)` | 过程 | [274](io.html#./io:s55) |
| `(greatest-fixnum)` | 过程 | [193](objects.html#./objects:s151) |
| `(guard (*var* *clause[1]* *clause[2]* ...) *b1* *b2* ...)` | 语法 | [361](exceptions.html#./exceptions:s8) |
| `(hashtable-clear! *hashtable*)` | 过程 | [249](objects.html#./objects:s287) |
| `(hashtable-clear! *hashtable* *size*)` | 过程 | [249](objects.html#./objects:s287) |
| `(hashtable-contains? *hashtable* *key*)` | 过程 | [246](objects.html#./objects:s282) |
| `(hashtable-copy *hashtable*)` | 过程 | [248](objects.html#./objects:s286) |
| `(hashtable-copy *hashtable* *mutable?*)` | 过程 | [248](objects.html#./objects:s286) |
| `(hashtable-delete! *hashtable* *key*)` | 过程 | [248](objects.html#./objects:s284) |
| `(hashtable-entries *hashtable*)` | 过程 | [250](objects.html#./objects:s289) |
| `(hashtable-equivalence-function *hashtable*)` | 过程 | [245](objects.html#./objects:s278) |
| `(hashtable-hash-function *hashtable*)` | 过程 | [245](objects.html#./objects:s278) |
| `(hashtable-keys *hashtable*)` | 过程 | [249](objects.html#./objects:s288) |
| `(hashtable-mutable? *hashtable*)` | 过程 | [245](objects.html#./objects:s277) |
| `(hashtable-ref *hashtable* *key* *default*)` | 过程 | [246](objects.html#./objects:s281) |
| `(hashtable-set! *hashtable* *key* *obj*)` | 过程 | [246](objects.html#./objects:s280) |
| `(hashtable-size *hashtable*)` | 过程 | [248](objects.html#./objects:s285) |
| `(hashtable-update! *hashtable* *key* *procedure* *default*)` | 过程 | [247](objects.html#./objects:s283) |
| `(hashtable? *obj*)` | 过程 | [155](objects.html#./objects:s25) |
| `(i/o-decoding-error? *obj*)` | 过程 | [375](exceptions.html#./exceptions:s42) |
| `(i/o-encoding-error-char *condition*)` | 过程 | [376](exceptions.html#./exceptions:s43) |
| `(i/o-encoding-error? *obj*)` | 过程 | [376](exceptions.html#./exceptions:s43) |
| `(i/o-error-filename *condition*)` | 过程 | [373](exceptions.html#./exceptions:s36) |
| `(i/o-error-port *condition*)` | 过程 | [375](exceptions.html#./exceptions:s41) |
| `(i/o-error-position *condition*)` | 过程 | [372](exceptions.html#./exceptions:s35) |
| `(i/o-error? *obj*)` | 过程 | [371](exceptions.html#./exceptions:s32) |
| `(i/o-file-already-exists-error? *obj*)` | 过程 | [374](exceptions.html#./exceptions:s39) |
| `(i/o-file-does-not-exist-error? *obj*)` | 过程 | [374](exceptions.html#./exceptions:s40) |
| `(i/o-file-is-read-only-error? *obj*)` | 过程 | [374](exceptions.html#./exceptions:s38) |
| `(i/o-file-protection-error? *obj*)` | 过程 | [373](exceptions.html#./exceptions:s37) |
| `(i/o-filename-error? *obj*)` | 过程 | [373](exceptions.html#./exceptions:s36) |
| `(i/o-invalid-position-error? *obj*)` | 过程 | [372](exceptions.html#./exceptions:s35) |
| `(i/o-port-error? *obj*)` | 过程 | [375](exceptions.html#./exceptions:s41) |
| `(i/o-read-error? *obj*)` | 过程 | [372](exceptions.html#./exceptions:s33) |
| `(i/o-write-error? *obj*)` | 过程 | [372](exceptions.html#./exceptions:s34) |
| `(identifier-syntax *tmpl*)` | 语法 | [297](syntax.html#./syntax:s27) |
| `(identifier-syntax (*id[1]* *tmpl[1]*) ((set! *id[2]* *e[2]*) *tmpl[2]*))` | 语法 | [297](syntax.html#./syntax:s27) |
| `(identifier? *obj*)` | 过程 | [301](syntax.html#./syntax:s35) |
| `(if *test* *consequent* *alternative*)` | 语法 | [109](control.html#./control:s8) |
| `(if *test* *consequent*)` | 语法 | [109](control.html#./control:s8) |
| `(imag-part *num*)` | 过程 | [182](objects.html#./objects:s121) |
| `immutable` | 语法 | [331](records.html#./records:s16) |
| `(implementation-restriction-violation? *obj*)` | 过程 | [369](exceptions.html#./exceptions:s28) |
| `(inexact *num*)` | 过程 | [180](objects.html#./objects:s112) |
| `(inexact->exact *num*)` | 过程 | [181](objects.html#./objects:s116) |
| `(inexact? *num*)` | 过程 | [170](objects.html#./objects:s87) |
| `(infinite? *real*)` | 过程 | [174](objects.html#./objects:s97) |
| `(input-port? *obj*)` | 过程 | [270](io.html#./io:s44) |
| `(integer->char *n*)` | 过程 | [215](objects.html#./objects:s211) |
| `(integer-valued? *obj*)` | 过程 | [153](objects.html#./objects:s18) |
| `(integer? *obj*)` | 过程 | [151](objects.html#./objects:s17) |
| `(irritants-condition? *obj*)` | 过程 | [368](exceptions.html#./exceptions:s25) |
| `(lambda *formals* *body[1]* *body[2]* ...)` | 语法 | [92](binding.html#./binding:s3) |
| `(latin-1-codec)` | 过程 | [259](io.html#./io:s22) |
| `(lcm *int* ...)` | 过程 | [179](objects.html#./objects:s110) |
| `(least-fixnum)` | 过程 | [193](objects.html#./objects:s151) |
| `(length *list*)` | 过程 | [159](objects.html#./objects:s46) |
| `(let ((*var* *expr*) ...) *body[1]* *body[2]* ...)` | 语法 | [95](binding.html#./binding:s16) |
| `(let *name* ((*var* *expr*) ...) *body[1]* *body[2]* ...)` | 语法 | [114](control.html#./control:s20) |
| `(let* ((*var* *expr*) ...) *body[1]* *body[2]* ...)` | 语法 | [96](binding.html#./binding:s18) |
| `(let*-values ((*formals* *expr*) ...) *body[1]* *body[2]* ...)` | 语法 | [99](binding.html#./binding:s23) |
| `(let-syntax ((*keyword* *expr*) ...) *form[1]* *form[2]* ...)` | 语法 | [293](syntax.html#./syntax:s13) |
| `(let-values ((*formals* *expr*) ...) *body[1]* *body[2]* ...)` | 语法 | [99](binding.html#./binding:s23) |
| `(letrec ((*var* *expr*) ...) *body[1]* *body[2]* ...)` | 语法 | [97](binding.html#./binding:s20) |
| `(letrec* ((*var* *expr*) ...) *body[1]* *body[2]* ...)` | 语法 | [98](binding.html#./binding:s22) |
| `(letrec-syntax ((*keyword* *expr*) ...) *form[1]* *form[2]* ...)` | 语法 | [293](syntax.html#./syntax:s13) |
| `(lexical-violation? *obj*)` | 过程 | [370](exceptions.html#./exceptions:s29) |
| `(list *obj* ...)` | 过程 | [158](objects.html#./objects:s43) |
| `(list->string *list*)` | 过程 | [223](objects.html#./objects:s229) |
| `(list->vector *list*)` | 过程 | [226](objects.html#./objects:s238) |
| `(list-ref *list* *n*)` | 过程 | [159](objects.html#./objects:s47) |
| `(list-sort *predicate* *list*)` | 过程 | [167](objects.html#./objects:s62) |
| `(list-tail *list* *n*)` | 过程 | [160](objects.html#./objects:s48) |
| `(list? *obj*)` | 过程 | [158](objects.html#./objects:s45) |
| `(log *num*)` | 过程 | [184](objects.html#./objects:s130) |
| `(log *num[1]* *num[2]*)` | 过程 | [184](objects.html#./objects:s130) |
| `(lookahead-char *textual-input-port*)` | 过程 | [275](io.html#./io:s62) |
| `(lookahead-u8 *binary-input-port*)` | 过程 | [274](io.html#./io:s56) |
| `(magnitude *num*)` | 过程 | [183](objects.html#./objects:s125) |
| `(make-assertion-violation)` | 过程 | [366](exceptions.html#./exceptions:s21) |
| `(make-bytevector *n*)` | 过程 | [228](objects.html#./objects:s242) |
| `(make-bytevector *n* *fill*)` | 过程 | [228](objects.html#./objects:s242) |
| `(make-custom-binary-input-port *id* *r!* *gp* *sp!* *close*)` | 过程 | [267](io.html#./io:s41) |
| `(make-custom-binary-input/output-port *id* *r!* *w!* *gp* *sp!* *close*)` | 过程 | [267](io.html#./io:s41) |
| `(make-custom-binary-output-port *id* *w!* *gp* *sp!* *close*)` | 过程 | [267](io.html#./io:s41) |
| `(make-custom-textual-input-port *id* *r!* *gp* *sp!* *close*)` | 过程 | [268](io.html#./io:s42) |
| `(make-custom-textual-input/output-port *id* *r!* *w!* *gp* *sp!* *close*)` | 过程 | [268](io.html#./io:s42) |
| `(make-custom-textual-output-port *id* *w!* *gp* *sp!* *close*)` | 过程 | [268](io.html#./io:s42) |
| `(make-enumeration *symbol-list*)` | 过程 | [251](objects.html#./objects:s291) |
| `(make-eq-hashtable)` | 过程 | [243](objects.html#./objects:s274) |
| `(make-eq-hashtable *size*)` | 过程 | [243](objects.html#./objects:s274) |
| `(make-eqv-hashtable)` | 过程 | [244](objects.html#./objects:s275) |
| `(make-eqv-hashtable *size*)` | 过程 | [244](objects.html#./objects:s275) |
| `(make-error)` | 过程 | [367](exceptions.html#./exceptions:s22) |
| `(make-hashtable *hash* *equiv?*)` | 过程 | [244](objects.html#./objects:s276) |
| `(make-hashtable *hash* *equiv?* *size*)` | 过程 | [244](objects.html#./objects:s276) |
| `(make-i/o-decoding-error *pobj*)` | 过程 | [375](exceptions.html#./exceptions:s42) |
| `(make-i/o-encoding-error *pobj* *cobj*)` | 过程 | [376](exceptions.html#./exceptions:s43) |
| `(make-i/o-error)` | 过程 | [371](exceptions.html#./exceptions:s32) |
| `(make-i/o-file-already-exists-error *filename*)` | 过程 | [374](exceptions.html#./exceptions:s39) |
| `(make-i/o-file-does-not-exist-error *filename*)` | 过程 | [374](exceptions.html#./exceptions:s40) |
| `(make-i/o-file-is-read-only-error *filename*)` | 过程 | [374](exceptions.html#./exceptions:s38) |
| `(make-i/o-file-protection-error *filename*)` | 过程 | [373](exceptions.html#./exceptions:s37) |
| `(make-i/o-filename-error *filename*)` | 过程 | [373](exceptions.html#./exceptions:s36) |
| `(make-i/o-invalid-position-error *position*)` | 过程 | [372](exceptions.html#./exceptions:s35) |
| `(make-i/o-port-error *pobj*)` | 过程 | [375](exceptions.html#./exceptions:s41) |
| `(make-i/o-read-error)` | 过程 | [372](exceptions.html#./exceptions:s33) |
| `(make-i/o-write-error)` | 过程 | [372](exceptions.html#./exceptions:s34) |
| `(make-implementation-restriction-violation)` | 过程 | [369](exceptions.html#./exceptions:s28) |
| `(make-irritants-condition *irritants*)` | 过程 | [368](exceptions.html#./exceptions:s25) |
| `(make-lexical-violation)` | 过程 | [370](exceptions.html#./exceptions:s29) |
| `(make-message-condition *message*)` | 过程 | [368](exceptions.html#./exceptions:s24) |
| `(make-no-infinities-violation)` | 过程 | [376](exceptions.html#./exceptions:s44) |
| `(make-no-nans-violation)` | 过程 | [377](exceptions.html#./exceptions:s45) |
| `(make-non-continuable-violation)` | 过程 | [369](exceptions.html#./exceptions:s27) |
| `(make-polar *real[1]* *real[2]*)` | 过程 | [183](objects.html#./objects:s123) |
| `(make-record-constructor-descriptor *rtd* *parent-rcd* *protocol*)` | 过程 | [332](records.html#./records:s24) |
| `(make-record-type-descriptor *name* *parent* *uid* *s?* *o?* *fields*)` | 过程 | [331](records.html#./records:s20) |
| `(make-rectangular *real[1]* *real[2]*)` | 过程 | [182](objects.html#./objects:s122) |
| `(make-serious-condition)` | 过程 | [366](exceptions.html#./exceptions:s19) |
| `(make-string *n*)` | 过程 | [218](objects.html#./objects:s218) |
| `(make-string *n* *char*)` | 过程 | [218](objects.html#./objects:s218) |
| `(make-syntax-violation *form* *subform*)` | 过程 | [370](exceptions.html#./exceptions:s30) |
| `(make-transcoder *codec*)` | 过程 | [259](io.html#./io:s19) |
| `(make-transcoder *codec* *eol-style*)` | 过程 | [259](io.html#./io:s19) |
| `(make-transcoder *codec* *eol-style* *error-handling-mode*)` | 过程 | [259](io.html#./io:s19) |
| `(make-undefined-violation)` | 过程 | [371](exceptions.html#./exceptions:s31) |
| `(make-variable-transformer *procedure*)` | 过程 | [306](syntax.html#./syntax:s42) |
| `(make-vector *n*)` | 过程 | [224](objects.html#./objects:s232) |
| `(make-vector *n* *obj*)` | 过程 | [224](objects.html#./objects:s232) |
| `(make-violation)` | 过程 | [366](exceptions.html#./exceptions:s20) |
| `(make-warning)` | 过程 | [367](exceptions.html#./exceptions:s23) |
| `(make-who-condition *who*)` | 过程 | [369](exceptions.html#./exceptions:s26) |
| `(map *procedure* *list[1]* *list[2]* ...)` | 过程 | [117](control.html#./control:s30) |
| `(max *real[1]* *real[2]* ...)` | 过程 | [178](objects.html#./objects:s107) |
| `(member *obj* *list*)` | 过程 | [161](objects.html#./objects:s51) |
| `(memp *procedure* *list*)` | 过程 | [163](objects.html#./objects:s52) |
| `(memq *obj* *list*)` | 过程 | [161](objects.html#./objects:s51) |
| `(memv *obj* *list*)` | 过程 | [161](objects.html#./objects:s51) |
| `(message-condition? *obj*)` | 过程 | [368](exceptions.html#./exceptions:s24) |
| `(min *real[1]* *real[2]* ...)` | 过程 | [178](objects.html#./objects:s108) |
| `(mod *x[1]* *x[2]*)` | 过程 | [175](objects.html#./objects:s99) |
| `(mod0 *x[1]* *x[2]*)` | 过程 | [176](objects.html#./objects:s100) |
| `(modulo *int[1]* *int[2]*)` | 过程 | [175](objects.html#./objects:s98) |
| `mutable` | 语法 | [331](records.html#./records:s16) |
| `(nan? *real*)` | 过程 | [174](objects.html#./objects:s97) |
| `(本地字节顺序)` | 过程 | [228](objects.html#./objects:s241) |
| `(本地换行风格)` | 过程 | [260](io.html#./io:s24) |
| `(本地转码器)` | 过程 | [259](io.html#./io:s21) |
| `(negative? *real*)` | 过程 | [173](objects.html#./objects:s95) |
| `(newline)` | 过程 | [285](io.html#./io:s87) |
| `(newline *textual-output-port*)` | 过程 | [285](io.html#./io:s87) |
| `(no-infinities-violation? *obj*)` | 过程 | [376](exceptions.html#./exceptions:s44) |
| `(no-nans-violation? *obj*)` | 过程 | [377](exceptions.html#./exceptions:s45) |
| `(non-continuable-violation? *obj*)` | 过程 | [369](exceptions.html#./exceptions:s27) |
| `nongenerative` | 语法 | [331](records.html#./records:s16) |
| `(not *obj*)` | 过程 | [110](control.html#./control:s10) |
| `(null-environment *version*)` | 过程 | [137](control.html#./control:s82) |
| `(null? *obj*)` | 过程 | [151](objects.html#./objects:s15) |
| `(number->string *num*)` | 过程 | [191](objects.html#./objects:s148) |
| `(number->string *num* *radix*)` | 过程 | [191](objects.html#./objects:s148) |
| `(number->string *num* *radix* *precision*)` | 过程 | [191](objects.html#./objects:s148) |
| `(number? *obj*)` | 过程 | [151](objects.html#./objects:s17) |
| `(numerator *rat*)` | 过程 | [181](objects.html#./objects:s118) |
| `(odd? *int*)` | 过程 | [174](objects.html#./objects:s96) |
| `opaque` | 语法 | [331](records.html#./records:s16) |
| `(open-bytevector-input-port *bytevector*)` | 过程 | [264](io.html#./io:s34) |
| `(open-bytevector-input-port *bytevector* *?transcoder*)` | 过程 | [264](io.html#./io:s34) |
| `(open-bytevector-output-port)` | 过程 | [265](io.html#./io:s36) |
| `(open-bytevector-output-port *?transcoder*)` | 过程 | [265](io.html#./io:s36) |
| `(open-file-input-port *path*)` | 过程 | [262](io.html#./io:s29) |
| `(open-file-input-port *path* *options*)` | 过程 | [262](io.html#./io:s29) |
| `(open-file-input-port *path* *options* *b-mode*)` | 过程 | [262](io.html#./io:s29) |
| `(open-file-input-port *path* *options* *b-mode* *?transcoder*)` | 过程 | [262](io.html#./io:s29) |
| `(open-file-input/output-port *path*)` | 过程 | [263](io.html#./io:s31) |
| `(open-file-input/output-port *path* *options*)` | 过程 | [263](io.html#./io:s31) |
| `(open-file-input/output-port *path* *options* *b-mode*)` | 过程 | [263](io.html#./io:s31) |
| `(open-file-input/output-port *path* *options* *b-mode* *?transcoder*)` | 过程 | [263](io.html#./io:s31) |
| `(open-file-output-port *path*)` | 过程 | [262](io.html#./io:s30) |
| `(open-file-output-port *path* *options*)` | 过程 | [262](io.html#./io:s30) |
| `(open-file-output-port *path* *options* *b-mode*)` | 过程 | [262](io.html#./io:s30) |
| `(open-file-output-port *path* *options* *b-mode* *?transcoder*)` | 过程 | [262](io.html#./io:s30) |
| `(open-input-file *path*)` | 过程 | [280](io.html#./io:s75) |
| `(open-output-file *path*)` | 过程 | [281](io.html#./io:s76) |
| `(open-string-input-port *string*)` | 过程 | [265](io.html#./io:s35) |
| `(open-string-output-port)` | 过程 | [266](io.html#./io:s37) |
| `(or *expr* ...)` | 语法 | [110](control.html#./control:s12) |
| `(output-port-buffer-mode *port*)` | 过��� | [273](io.html#./io:s52) |
| `(output-port? *obj*)` | 过程 | [270](io.html#./io:s44) |
| `(pair? *obj*)` | 过程 | [151](objects.html#./objects:s16) |
| `parent` | 语法 | [331](records.html#./records:s16) |
| `parent-rtd` | 语法 | [331](records.html#./records:s16) |
| `(partition *procedure* *list*)` | 过程 | [164](objects.html#./objects:s56) |
| `(peek-char)` | 过程 | [284](io.html#./io:s83) |
| `(peek-char *textual-input-port*)` | 过程 | [284](io.html#./io:s83) |
| `(port-eof? *input-port*)` | 过程 | [278](io.html#./io:s68) |
| `(port-has-port-position? *port*)` | 过程 | [271](io.html#./io:s49) |
| `(port-has-set-port-position!? *port*)` | 过程 | [272](io.html#./io:s50) |
| `(port-position *port*)` | 过程 | [271](io.html#./io:s49) |
| `(port-transcoder *port*)` | 过程 | [271](io.html#./io:s48) |
| `(port? *obj*)` | 过程 | [270](io.html#./io:s43) |
| `(positive? *real*)` | 过程 | [173](objects.html#./objects:s94) |
| `(*expr[0]* *expr[1]* ...)` | 语法 | [107](control.html#./control:s1) |
| `(procedure? *obj*)` | 过程 | [155](objects.html#./objects:s23) |
| `protocol` | 语法 | [331](records.html#./records:s16) |
| `(put-bytevector *binary-output-port* *bytevector*)` | 过程 | [279](io.html#./io:s70) |
| `(put-bytevector *binary-output-port* *bytevector* *start*)` | 过程 | [279](io.html#./io:s70) |
| `(put-bytevector *binary-output-port* *bytevector* *start* *n*)` | 过程 | [279](io.html#./io:s70) |
| `(put-char *textual-output-port* *char*)` | 过程 | [279](io.html#./io:s71) |
| `(put-datum *textual-output-port* *obj*)` | 过程 | [279](io.html#./io:s73) |
| `(put-string *textual-output-port* *string*)` | 过程 | [279](io.html#./io:s72) |
| `(put-string *textual-output-port* *string* *start*)` | 过程 | [279](io.html#./io:s72) |
| `(put-string *textual-output-port* *string* *start* *n*)` | 过程 | [279](io.html#./io:s72) |
| `(put-u8 *binary-output-port* *octet*)` | 过程 | [278](io.html#./io:s69) |
| `(quasiquote *obj* ...)` | 语法 | [142](objects.html#./objects:s5) |
| `(quasisyntax *template* ...)` | 语法 | [305](syntax.html#./syntax:s40) |
| `(quote *obj*)` | 语法 | [141](objects.html#./objects:s2) |
| `(quotient *int[1]* *int[2]*)` | 过程 | [175](objects.html#./objects:s98) |
| `(raise *obj*)` | 过程 | [357](exceptions.html#./exceptions:s3) |
| `(raise-continuable *obj*)` | 过程 | [357](exceptions.html#./exceptions:s3) |
| `(rational-valued? *obj*)` | 过程 | [153](objects.html#./objects:s18) |
| `(rational? *obj*)` | 过程 | [151](objects.html#./objects:s17) |
| `(rationalize *real[1]* *real[2]*)` | 过程 | [181](objects.html#./objects:s117) |
| `(read)` | 过程 | [284](io.html#./io:s81) |
| `(read *textual-input-port*)` | 过程 | [284](io.html#./io:s81) |
| `(read-char)` | 过程 | [284](io.html#./io:s82) |
| `(read-char *textual-input-port*)` | 过程 | [284](io.html#./io:s82) |
| `(real->flonum *real*)` | 过程 | [211](objects.html#./objects:s198) |
| `(real-part *num*)` | 过程 | [182](objects.html#./objects:s120) |
| `(real-valued? *obj*)` | 过程 | [153](objects.html#./objects:s18) |
| `(real? *obj*)` | 过程 | [151](objects.html#./objects:s17) |
| `(record-accessor *rtd* *idx*)` | 过程 | [334](records.html#./records:s31) |
| `(record-constructor *rcd*)` | 过程 | [333](records.html#./records:s29) |
| `(record-constructor-descriptor *record-name*)` | 语法 | [333](records.html#./records:s28) |
| `(record-field-mutable? *rtd* *idx*)` | 过程 | [338](records.html#./records:s39) |
| `(record-mutator *rtd* *idx*)` | 过程 | [334](records.html#./records:s32) |
| `(record-predicate *rtd*)` | 过程 | [333](records.html#./records:s30) |
| `(record-rtd *record*)` | 过程 | [338](records.html#./records:s41) |
| `(record-type-descriptor *record-name*)` | 语法 | [333](records.html#./records:s28) |
| `(record-type-descriptor? *obj*)` | 过程 | [332](records.html#./records:s23) |
| `(record-type-field-names *rtd*)` | 过程 | [337](records.html#./records:s38) |
| `(record-type-generative? *rtd*)` | 过程 | [337](records.html#./records:s37) |
| `(record-type-name *rtd*)` | 过程 | [336](records.html#./records:s34) |
| `(record-type-opaque? *rtd*)` | 过程 | [337](records.html#./records:s37) |
| `(record-type-parent *rtd*)` | 过程 | [336](records.html#./records:s35) |
| `(record-type-sealed? *rtd*)` | 过程 | [337](records.html#./records:s37) |
| `(record-type-uid *rtd*)` | 过程 | [336](records.html#./records:s36) |
| `(record? *obj*)` | 过程 | [338](records.html#./records:s40) |
| `(remainder *int[1]* *int[2]*)` | 过程 | [175](objects.html#./objects:s98) |
| `(remove *obj* *list*)` | 过程 | [163](objects.html#./objects:s53) |
| `(remp *procedure* *list*)` | 过程 | [163](objects.html#./objects:s54) |
| `(remq *obj* *list*)` | 过程 | [163](objects.html#./objects:s53) |
| `(remv *obj* *list*)` | 过程 | [163](objects.html#./objects:s53) |
| `(reverse *list*)` | 过程 | [161](objects.html#./objects:s50) |
| `(round *real*)` | 过程 | [178](objects.html#./objects:s104) |
| `(scheme-report-environment *version*)` | 过程 | [137](control.html#./control:s82) |
| `sealed` | 语法 | [331](records.html#./records:s16) |
| `(serious-condition? *obj*)` | 过程 | [366](exceptions.html#./exceptions:s19) |
| `(set! *var* *expr*)` | 语法 | [102](binding.html#./binding:s28) |
| `(set-car! *pair* *obj*)` | 过程 | [157](objects.html#./objects:s40) |
| `(set-cdr! *pair* *obj*)` | 过程 | [157](objects.html#./objects:s41) |
| `(set-port-position! *port* *pos*)` | 过程 | [272](io.html#./io:s50) |
| `(simple-conditions *condition*)` | 过程 | [363](exceptions.html#./exceptions:s16) |
| `(sin *num*)` | 过程 | [185](objects.html#./objects:s131) |
| `(sint-list->bytevector *list* *eness* *size*)` | 过程 | [239](objects.html#./objects:s261) |
| `(sqrt *num*)` | 过程 | [183](objects.html#./objects:s127) |
| `(standard-error-port)` | 过程 | [264](io.html#./io:s33) |
| `(standard-input-port)` | 过程 | [264](io.html#./io:s33) |
| `(standard-output-port)` | 过程 | [264](io.html#./io:s33) |
| `(string *char* ...)` | 过程 | [218](objects.html#./objects:s217) |
| `(string->bytevector *string* *transcoder*)` | 过程 | [287](io.html#./io:s92) |
| `(string->list *string*)` | 过程 | [222](objects.html#./objects:s228) |
| `(string->number *string*)` | 过程 | [191](objects.html#./objects:s147) |
| `(string->number *string* *radix*)` | 过程 | [191](objects.html#./objects:s147) |
| `(string->symbol *string*)` | 过程 | [242](objects.html#./objects:s269) |
| `(string->utf16 *string*)` | 过程 | [287](io.html#./io:s94) |
| `(string->utf16 *string* *endianness*)` | 过程 | [287](io.html#./io:s94) |
| `(string->utf32 *string*)` | 过程 | [287](io.html#./io:s94) |
| `(string->utf32 *string* *endianness*)` | 过程 | [287](io.html#./io:s94) |
| `(string->utf8 *string*)` | 过程 | [287](io.html#./io:s93) |
| `(string-append *string* ...)` | 过程 | [219](objects.html#./objects:s223) |
| `(string-ci-hash *string*)` | 过程 | [245](objects.html#./objects:s279) |
| `(string-ci<=? *string[1]* *string[2]* *string[3]* ...)` | 过程 | [217](objects.html#./objects:s216) |
| `(string-ci<? *string[1]* *string[2]* *string[3]* ...)` | 过程 | [217](objects.html#./objects:s216) |
| `(string-ci=? *string[1]* *string[2]* *string[3]* ...)` | 过程 | [217](objects.html#./objects:s216) |
| `(string-ci>=? *string[1]* *string[2]* *string[3]* ...)` | 过程 | [217](objects.html#./objects:s216) |
| `(string-ci>? *string[1]* *string[2]* *string[3]* ...)` | 过程 | [217](objects.html#./objects:s216) |
| `(string-copy *string*)` | 过程 | [219](objects.html#./objects:s222) |
| `(string-downcase *string*)` | 过程 | [221](objects.html#./objects:s226) |
| `(string-fill! *string* *char*)` | 过程 | [220](objects.html#./objects:s225) |
| `(string-foldcase *string*)` | 过程 | [221](objects.html#./objects:s226) |
| `(string-for-each *procedure* *string[1]* *string[2]* ...)` | 过程 | [122](control.html#./control:s50) |
| `(string-hash *string*)` | 过程 | [245](objects.html#./objects:s279) |
| `(string-length *string*)` | 过程 | [218](objects.html#./objects:s219) |
| `(string-normalize-nfc *string*)` | 过程 | [222](objects.html#./objects:s227) |
| `(string-normalize-nfd *string*)` | 过程 | [222](objects.html#./objects:s227) |
| `(string-normalize-nfkc *string*)` | 过程 | [222](objects.html#./objects:s227) |
| `(string-normalize-nfkd *string*)` | 过程 | [222](objects.html#./objects:s227) |
| `(string-ref *string* *n*)` | 过程 | [218](objects.html#./objects:s220) |
| `(string-set! *string* *n* *char*)` | 过程 | [219](objects.html#./objects:s221) |
| `(string-titlecase *string*)` | 过程 | [221](objects.html#./objects:s226) |
| `(string-upcase *string*)` | 过程 | [221](objects.html#./objects:s226) |
| `(string<=? *string[1]* *string[2]* *string[3]* ...)` | 过程 | [216](objects.html#./objects:s215) |
| `(string<? *string[1]* *string[2]* *string[3]* ...)` | 过程 | [216](objects.html#./objects:s215) |
| `(string=? *string[1]* *string[2]* *string[3]* ...)` | 过程 | [216](objects.html#./objects:s215) |
| `(string>=? *string[1]* *string[2]* *string[3]* ...)` | 过程 | [216](objects.html#./objects:s215) |
| `(string>? *string[1]* *string[2]* *string[3]* ...)` | 过程 | [216](objects.html#./objects:s215) |
| `(string? *obj*)` | 过程 | [154](objects.html#./objects:s20) |
| `(substring *string* *start* *end*)` | 过程 | [220](objects.html#./objects:s224) |
| `(symbol->string *symbol*)` | 过程 | [242](objects.html#./objects:s270) |
| `(symbol-hash *symbol*)` | 过程 | [245](objects.html#./objects:s279) |
| `(symbol=? *symbol[1]* *symbol[2]*)` | 过程 | [242](objects.html#./objects:s268) |
| `(symbol? *obj*)` | 过程 | [154](objects.html#./objects:s22) |
| `(syntax *template*)` | 语法 | [300](syntax.html#./syntax:s33) |
| `(syntax->datum *obj*)` | 过程 | [308](syntax.html#./syntax:s44) |
| `(syntax-case *expr* (*literal* ...) *clause* ...)` | 语法 | [299](syntax.html#./syntax:s30) |
| `(syntax-rules (*literal* ...) *clause* ...)` | 语法 | [294](syntax.html#./syntax:s14) |
| `(syntax-violation *who* *msg* *form*)` | 过程 | [359](exceptions.html#./exceptions:s6) |
| `(syntax-violation *who* *msg* *form* *subform*)` | 过程 | [359](exceptions.html#./exceptions:s6) |
| `(syntax-violation-form *condition*)` | 过程 | [370](exceptions.html#./exceptions:s30) |
| `(syntax-violation-subform *condition*)` | 过程 | [370](exceptions.html#./exceptions:s30) |
| `(syntax-violation? *obj*)` | 过程 | [370](exceptions.html#./exceptions:s30) |
| `(tan *num*)` | 过程 | [185](objects.html#./objects:s131) |
| `(textual-port? *obj*)` | 过程 | [270](io.html#./io:s45) |
| `(transcoded-port *binary-port* *transcoder*)` | 过程 | [271](io.html#./io:s47) |
| `(transcoder-codec *transcoder*)` | 过程 | [259](io.html#./io:s20) |
| `(transcoder-eol-style *transcoder*)` | 过程 | [259](io.html#./io:s20) |
| `(transcoder-error-handling-mode *transcoder*)` | 过程 | [259](io.html#./io:s20) |
| `(truncate *real*)` | 过程 | [177](objects.html#./objects:s101) |
| `(u8-list->bytevector *list*)` | 过程 | [232](objects.html#./objects:s253) |
| `(uint-list->bytevector *list* *eness* *size*)` | 过程 | [239](objects.html#./objects:s261) |
| `(undefined-violation? *obj*)` | 过程 | [371](exceptions.html#./exceptions:s31) |
| `(unless *test-expr* *expr[1]* *expr[2]* ...)` | 语法 | [112](control.html#./control:s17) |
| `(unquote *obj* ...)` | 语法 | [142](objects.html#./objects:s5) |
| `(unquote-splicing *obj* ...)` | 语法 | [142](objects.html#./objects:s5) |
| `(unsyntax *template* ...)` | 语法 | [305](syntax.html#./syntax:s40) |
| `(unsyntax-splicing *template* ...)` | 语法 | [305](syntax.html#./syntax:s40) |
| `(utf-16-codec)` | 过程 | [259](io.html#./io:s22) |
| `(utf-8-codec)` | 过程 | [259](io.html#./io:s22) |
| `(utf16->string *bytevector* *endianness*)` | 过程 | [288](io.html#./io:s96) |
| `(utf16->string *bytevector* *endianness* *endianness-mandatory?*)` | 过程 | [288](io.html#./io:s96) |
| `(utf32->string *bytevector* *endianness*)` | 过程 | [288](io.html#./io:s96) |
| `(utf32->string *bytevector* *endianness* *endianness-mandatory?*)` | 过程 | [288](io.html#./io:s96) |
| `(utf8->string *bytevector*)` | 过程 | [287](io.html#./io:s95) |
| `(values *obj* ...)` | 过程 | [131](control.html#./control:s70) |
| `*variable*` | 语法 | [91](binding.html#./binding:s2) |
| `(vector *obj* ...)` | 过程 | [224](objects.html#./objects:s231) |
| `(vector->list *vector*)` | 过程 | [225](objects.html#./objects:s237) |
| `(vector-fill! *vector* *obj*)` | 过程 | [225](objects.html#./objects:s236) |
| `(vector-for-each *procedure* *vector[1]* *vector[2]* ...)` | 过程 | [122](control.html#./control:s47) |
| `(vector-length *vector*)` | 过程 | [224](objects.html#./objects:s233) |
| `(vector-map *procedure* *vector[1]* *vector[1]* ...)` | 过程 | [121](control.html#./control:s44) |
| `(vector-ref *vector* *n*)` | 过程 | [224](objects.html#./objects:s234) |
| `(vector-set! *vector* *n* *obj*)` | 过程 | [225](objects.html#./objects:s235) |
| `(vector-sort *predicate* *vector*)` | 过程 | [226](objects.html#./objects:s239) |
| `(vector-sort! *predicate* *vector*)` | 过程 | [226](objects.html#./objects:s239) |
| `(vector? *obj*)` | 过程 | [154](objects.html#./objects:s21) |
| `(violation? *obj*)` | 过程 | [366](exceptions.html#./exceptions:s20) |
| `(warning? *obj*)` | 过程 | [367](exceptions.html#./exceptions:s23) |
| `(when *test-expr* *expr[1]* *expr[2]* ...)` | 语法 | [112](control.html#./control:s17) |
| `(who-condition? *obj*)` | 过程 | [369](exceptions.html#./exceptions:s26) |
| `(with-exception-handler *procedure* *thunk*)` | 过程 | [360](exceptions.html#./exceptions:s7) |
| `(with-input-from-file *path* *thunk*)` | 过程 | [283](io.html#./io:s79) |
| `(with-output-to-file *path* *thunk*)` | 过程 | [283](io.html#./io:s80) |
| `(with-syntax ((*pattern* *expr*) ...) *body[1]* *body[2]* ...)` | 语法 | [304](syntax.html#./syntax:s38) |
| `(write *obj*)` | 过程 | [284](io.html#./io:s84) |
| `(write *obj* *textual-output-port*)` | 过程 | [284](io.html#./io:s84) |
| `(write-char *char*)` | 过程 | [285](io.html#./io:s86) |
| `(write-char *char* *textual-output-port*)` | 过程 | [285](io.html#./io:s86) |
| `(zero? *num*)` | 过程 | [173](objects.html#./objects:s93) |
