```java

let mapleader = " "
set easymotion
set gdefault

set smartcase


" use system clipboard
set clipboard=unnamedplus,unnamed

set surround

" Allow backspace and cursor keys to cross line boundaries
set whichwrap+=<,>,h,l

" black hole register
vmap <backspace> "_d
vmap <del> "_d



" ============================================================================
" expand and collapse
" ============================================================================
nmap zO :action ExpandAllRegions<CR>
nmap zo :action ExpandRegion<CR>
nmap zc :action CollapseRegion<CR>
nmap zC :action CollapseAllRegions<CR>

" Quit insert mode
inoremap jj <Esc>
inoremap jk <Esc>
inoremap kk <Esc>

" Quit visual mode
vnoremap v <Esc>

" Move to the start of line
nnoremap H ^

" Move to the end of line
nnoremap L $

" Redo
nnoremap U <C-r>

" Yank to the end of line
nnoremap Y y$

nmap <leader>ll      :actionlist<CR>

" ============================================================================
" IDE actions
" ============================================================================

nnoremap gc              :action GotoClass<CR>
nnoremap gf              :action GotoFile<CR>
nnoremap gs              :action GotoSymbol<CR>
nnoremap ga              :action GotoAction<CR>
nnoremap gr              :action RecentFiles<CR>


nnoremap gd              :action GotoDeclaration<CR>
nnoremap gj              :action QuickJavaDoc<CR>
nnoremap gu              :action FindUsages<CR>
nnoremap gi              :action GotoImplementation<CR>
nnoremap gl              :action GotoLine<CR>


nnoremap ha              :action SaveAll<CR>
nnoremap hs              :action $SelectAll<CR>
nnoremap hf              :action ReformatCode<CR>
nnoremap hi              :action ImplementMethods<CR>

nnoremap rc              :action RunClass<CR>
nnoremap rr              :action Run<CR>
nnoremap rs              :action Stop<CR>
nnoremap re              :action DebugClass<CR>
nnoremap rd              :action Debug<CR>

nnoremap ws              :action ActivateStructureToolWindow<CR>
nnoremap wt              :action ActivateTerminalToolWindow<CR>
nnoremap wp              :action ActivateProjectToolWindow<CR>
nnoremap wr              :action ReopenClosedTab<CR>

```

