在用户文件夹下`_vimrc`文件

```powershell
type nul > "_vimrc"
```

然后添加以下代码：

```vim
" 预先检查是否存在这些文件夹
if !isdirectory($TEMP . '/vim/vim_backup')
    call mkdir($TEMP . '/vim/vim_backup', 'p')
endif
if !isdirectory($TEMP . '/vim/vim_swap')
    call mkdir($TEMP . '/vim/vim_swap', 'p')
endif
if !isdirectory($TEMP . '/vim/vim_undo')
    call mkdir($TEMP . '/vim/vim_undo', 'p')
endif

" 设置使用 %TEMP% 环境变量，vim 会自动展开
set backupdir=$TEMP/vim/vim_backup//
set directory=$TEMP/vim/vim_swap//
set undodir=$TEMP/vim/vim_undo//)
endif

" 开启备份和撤销持久化（可选）
" set backup
" set writebackup
" set undofile
```

关机后文件都会被系统自动清除
