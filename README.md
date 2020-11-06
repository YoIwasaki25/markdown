# Neovim導入手順

1. ~/.config/nvim にinit.nvimというセッティングファイルを置く
2. ~/.config/nvim/rc のなかに、dein.toml, dein_lazy.tomlというファイルを置く  
	- dein.toml は常時使うプラグインの名前を書く
	- dein_lazy.toml は、言語や使う用途が限られているときその拡張子のファイルを開いたときに読み込まれるファイル。特定の言語の補完のプラグインなどはこっちに書きます。

3. init.nvimに以下のコードを記載する
~~~
if &compatible
	set nocompatible			   " Be iMproved
endif

" Required:
set runtimepath+=/home/yoiwasaki/.cache/dein/repos/github.com/Shougo/dein.vim

" Required:
if dein#load_state('/home/yoiwasaki/.cache/dein')
	call dein#begin('/home/yoiwasaki/.cache/dein')

	" Let dein manage dein
	" Required:
	call dein#add('/home/yoiwasaki/.cache/dein/repos/github.com/Shougo/dein.vim')

	" Add or remove your plugins here like this:
	let s:toml_dir = expand('/home/yoiwasaki/.config/nvim/rc/')  
	call dein#load_toml(s:toml_dir . '/dein.toml',{'lazy':0})
	call dein#load_toml(s:toml_dir . '/dein_lazy.toml',{'lazy':1})
	call dein#end()
	call dein#save_state()
endif

" Required:
filetype plugin indent on
filetype plugin on
syntax enable

" If you want to install not installed plugins on startup.
if dein#check_install()
	call dein#install()
endif
~~~
- これのやってる処理は、deinがなかったら自動インストールするよ。場所は~/.cacheの中に配置するよ。dein.tomlとdein_lazy.tomlの場所はここだよ。vimを起動したときに、dein.toml, dein_lazy.tomlの中に新しいプラグインがあったら、自動的に~/.cache/dein/repos/github.comの中にcloneするよってこと。


# おすすめのプラグイン

