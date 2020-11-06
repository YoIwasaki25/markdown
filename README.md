# init.nvimの設定
~~~vim

" 行番号の表示
set number
set relativenumber
" 現在の列を強調表示
set cursorline
" 入力中のコマンドをステータスに表示する
set showcmd
" 行末の一文字先までカーソルを移動できるように
set virtualedit=onemore
" シンタクスハイライトの有効化
syntax enable
" インクリメンタルサーチ.　1文字入力ごとに検索を行う
set incsearch
" 検索パターンに大文字小文字を区別しない
set ignorecase
" 検索パターンに大文字を含んでいたら大文字小文字を区別する set smartcase 検索結果をハイライト
set hlsearch
" タブ入力を複数の空白入力に置き換える set expandtab 画面上でタブ文字が占める幅
set tabstop=4
" 連続した空白に対してタブキーやバックスペースキーでカーソルが動く幅
set softtabstop=4
" 開業時に前の行のインデントを継続する
set autoindent
" 改行時に前の行の構文をチェックし次の行のインデントを増減する
set smartindent
" smartindent で増減する幅
set shiftwidth=4
" コマンドモードの補完
set wildmenu 
" 保存するコマンド履歴の数
set history=5000
"bro olの設定 :bro o したときに何ファイル表示できるようにするか
set viminfo='20
' 閉じるクォーテーションマークは書かなくてオッケー。

" 補完時の挙動 補完がでたらすぐenterおして補完できるようにする
set completeopt=menuone,noinsert
" Ubuntu のクリップボードとvimのヤンク(コピー)の連携
set clipboard=unnamedplus

" テキストファイルとvim scriptのファイルを見やすくするために折りたたみ表示ができるようにする

au Filetype vim setlocal foldmethod=marker
au Filetype text setlocal foldmethod=marker
~~~
### 折りたたみの使い方  
- [x] (岩崎のinit.vimが折りたたみ表示されてると思う)
- zi : 折りたたみの有効無効の切り替え
- zf : 折りたたみの作成(範囲選択の開始行と終了行の末尾にマーカーを追加する)
- za : 折りたたみの開閉
- zA : 折りたたみの再帰的開閉
- zd : 折りたたみの削除
- zR : バッファ内の全ての折りたたみを開く
- zM : バッファ内の全ての折りたたみを閉じる

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

- 万が一いらないプラグインなどを入れてしまった場合、tomlファイルの中身のいらない箇所を消す(vimを再起動するとまたクローンされてしまう)その次に~/.cache/dein/repos/github.comのなかのいらないプラグインを消す。
- 万が一それでも消したプラグインがまだ動いていた場合、vimを開いてコマンド
``:call dein#recache_runtimepath()``を実行すれば、キャッシュの読み直しをしてくれます。

# おすすめのプラグイン
1. **カラースキーム**
~~~vim
colorscheme iceberg
set background=dark
set termguicolors

highlight Normal ctermbg=NONE guibg=NONE
highlight NonText ctermbg=NONE guibg=NONE
highlight LineNr ctermbg=NONE guibg=NONE
highlight Folded ctermbg=NONE guibg=NONE
highlight EndOfBuffer ctermbg=NONE guibg=NONE
~~~
- neovimに対応しているカラースキームをgitやらサイトから探してdeinでインストール
- highlight以下は、背景を透過させる設定。gnomeエディタの背景も透過させると背景が見えます。

2. **vim-airline**
- vimのステータスバーをおしゃれにするやつ。lightline.vimとこっちの二台巨塔
- 設定は俺の設定ファイル見ていじったら良いと思うコピペでも動くと思います。
- vim-airlineで検索するとthemeの一覧サイトみたいなのがあるから気に入ったのを、dein.tomlに書いてクローン,init.nvimのなかのairline-themeの中をそのthemeの名前にしたら反映されると思います。

3. **luochen/rainbow**
- カッコの対応を色でわかりやすくしてくれるプラグイン

4. **jiangmiao/autopairsi**
- カッコやクォーテーションマークを自動的に閉じてくれる補完をしてくれる有能

5. **reireias/vim-cheatsheet**
- vimのコマンドに``:Cheat``でvimのチートシートが見れる(自分で書いた独自のチートシート,そのファイルまでのPATHの指定をinit.vimに書く必要がある)

6. **tpope/vim-surround**
- visual modeで範囲を選択してS( を押すと、範囲をカッコでくくってくれる。

7. **tpope/vim-commentary**
- visual modeで範囲を選択してgccを押すとコメントアウトしてくれる

8. **neoclide/coc.nvim**
- language server に接続して、様々な言語の補完をしてくれる。超優秀
	これのおかげでIDE使わなくて良くなった。気になったら後日手伝う

# Markdownについて
1. dein.tomlに以下を記載する
~~~
[[plugins]]
repo = 'plasticboy/vim-markdown'
~~~

2. dein_lazy.tomlに以下を記載する
~~~
[[plugins]]
repo = 'tyru/open-browser.vim'
hook_add = '''
let g:openbrowser_browser_commands=[{'name': 'google-chrome-stable', 'args': ['{browser}', '{uri}']}]
'''
[[plugins]]
repo = 'iamcco/markdown-preview.nvim'
on_ft = [ 'markdown', 'pandoc.markdown', 'rmd' ]
build = 'sh -c "cd app & yarn install"'
~~~
を記載する。

3. Yoiwasaki25/markdown.gitの中のcheatsheet.mdをneovimで開いて、コマンド
`:MarkdownPreview`を実行すると,chromeにファイルがレンダリングされるはず！


以上お疲れ様でした。
