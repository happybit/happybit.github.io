---
layout: post
title: "Learn Vim The Hard Way IV"
date: 2015-02-25 10:46
comments: true
categories: Productivity
---

接下来就是不停的练习，以加强肌肉记忆了。其实，不光可以在Vim中练，在其他很多软件中，也可以练习类Vim的快捷键。

<!--more-->

### Emacs & Evil

如果觊觎Vim的各种commands，又离不开Emacs。[Evil](https://gitorious.org/evil/pages/Home)插件就是你的不二选择。它不仅支持大部分的Vim命令。更妙的是，在insert mode，原有的Emacs快捷键也可以继续使用。

唯一有一点不遍的是，Evil在org-mode的Org Agenda界面不起作用，也就是说`jkhl`在Org Agenda里无法进行方向操作。不过网上已有解决办法，从[Steve Purcell](http://www.sanityinc.com/)大神的[配置文件](https://github.com/purcell/emacs.d)中抄的。在Emacs配置文件中加入下面这几行，重定义快捷键即可。

```lisp
; org - minimum for agenda
(add-hook 'org-agenda-mode-hook
  (lambda ()
    (define-key org-agenda-mode-map "\C-n" 'evil-next-buffer)
    (define-key org-agenda-mode-map "\C-p" 'evil-prev-buffer)
    (define-key org-agenda-mode-map "b" 'evil-backward-word-begin)
    (define-key org-agenda-mode-map "h" 'evil-backward-char)
    (define-key org-agenda-mode-map "j" 'evil-next-line)
    (define-key org-agenda-mode-map "k" 'evil-previous-line)
    (define-key org-agenda-mode-map "l" 'evil-forward-char)
    (define-key org-agenda-mode-map "n" 'evil-forward-word-begin)
    (define-key org-agenda-mode-map "p" 'evil-forward-word-begin)
    (define-key org-agenda-mode-map "w" 'evil-forward-word-begin)))
```

### Total Commander & ViATc

Total Commander有一个插件[ViATc](https://github.com/linxinhong/ViATc)，可以实现，对文件及文件夹的操作，也可以用类Vim的快捷键完成。这个工具是开源的，使用AutoHotKey写的。本来想直接把core部分代码移植到自己的AHK配置文件里，看了一下耦合比较严重。直接移植要花一番功夫，暂时搁置。

### Vimperator & Vimium

Firefox上的[Vimperator](http://www.vimperator.org/vimperator)，和Chrome上的[Vimium](https://chrome.google.com/webstore/detail/vimium/dbepggeogbaibhgnhhndojpepiihcmeb?hl=en)，也属必装。总的来说，Vimperator比Vimium强大，可定制性更高。

### Gmail & Twitter

[Gmail](https://mail.google.com)和[Twitter](http://www.twitter.com)原生支持类Vim的快捷键。

### Outlook

在Outlook中，可以使用[这个AHK的脚本](http://www.ocellated.com/2009/03/18/pimping-microsoft-outlook/)，可实现类似Gmail的快捷键。

### Others

其他有编辑功能的软件，如[Android Studio IDE](http://developer.android.com/sdk/index.html)，[Haroopad](pad.haroopress.com/)等，都可以绑定Vim快捷键。

这样，在大部分情况下，就能统一快捷键了。这样不仅减少了context切换的效率损耗，还可以不停演练Vim操作。唯一有一点不便，就是中文输入法的切换，在Vim中经常打乱击键节奏。所以，我尽量只在英文输入环境中使用这套操作。