# Ubuntu安装Rime一些配置速览

(以默认ibus、自带的朙月输入法为主，没有对应的文件就自建)

## 设置横排

主要是在 `ibus_rime.custom.yaml` 文件，输入：

```yaml
patch:
  "style/horizontal": true
```

## 设置开机默认英文与Ctrl+空格切换中英文

是在 `default.custom.yaml` 文件，输入：

```yaml
patch:
  # 设置默认输入状态为英文 (ascii_mode)
  "switches/@0/reset": 1

  # 禁用所有 Shift 键切换中英文的功能
  "ascii_composer/switch_key":
    Shift_L: noop
    Shift_R: noop

  # 设置仅使用 Control+space 来切换中英文
  "key_binder/bindings":
    - { when: always, accept: Control+space, toggle: ascii_mode }

  # 后续开启用户词典功能
  "translator/enable_user_dict": true
```

对于简化方案，是在 `luna_pinyin_simp.custom.yaml`中，可以补充（顺便设置候词数为9）：

```yaml
patch:
  # 强制设置该方案启动时，中英文开关状态为“英文”
  "switches/@0/reset": 1

  # 设置候选词个数为9
  "menu/page_size": 9

  # encoding: utf-8
  'translator/dictionary': custom_dict.all
```



## 设置字典

前置设置，见前文 `设置开机默认英文` 。

`default.custom.yaml` 文件有

```yaml
  # 后续开启用户词典功能
  "translator/enable_user_dict": true
```

`luna_pinyin_simp.custom.yaml`中

```yaml
  # encoding: utf-8
  'translator/dictionary': custom_dict.all
```



创建文件夹 `dicts` ，丢词典进去。

编辑 `custom_dict.all.dict.yaml` ，字典文件去掉后缀 `.dict.yaml` ，然后按照使用习惯按顺序排列，有

```yaml
name: custom_dict.all ##注意name和文件名一致
version: "2026.x.xx"
use_preset_vocabulary: true
# 此处为 输入法所用到的词库，既补充拓展词库的地方
import_tables:
  - dicts/8105 # 基本单字
  - dicts/41448 # 基本单字
  - dicts/base # 现代汉语词典基本词汇
  - dicts/ext # 基本的一些词汇
  - dicts/rime_mint.base  # 二、三词
  - dicts/rime_mint.correlation # 基本四字词语
  - dicts/rime_mint.ext # 五字词语
  - dicts/other_kaomoji # 颜文字
  # - dicts/other_emoji # emoji
  - dicts/rime_ice.en # 基本英文词汇
  - dicts/rime_ice.en_ext # 基本英文词汇
```




