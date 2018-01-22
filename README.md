
## Terminal and vim

### Keep ssh connection alive (on client side)
``` Bash
sudo vi /etc/ssh/ssh_config
```
Insert
```
ServerAliveInterval 100
```

### _Terminal and vim debug info_
#### Test terminal speed in bash
``` Bash
time seq -f 'blah blah %g' 100000
```
#### Print out colors used in vim
``` vim
:so $VIMRUNTIME/syntax/hitest.vim
```
#### Print used colorscheme in vim
``` vim
:color
```
#### Print colorgroups used in vim
``` vim
:hi
```
#### Print terminal  colortheme colors
``` Bash
#!/bin/bash

#Terminal color table printout

T='gYw'   # The test text

echo -e "\n                 40m     41m     42m     43m\
     44m     45m     46m     47m";

for FGs in '    m' '   1m' '  30m' '1;30m' '  31m' '1;31m' '  32m' '1;32m' '  33m' '1;33m' '  34m' '1;34m' '  35m' '1;35m'  '  36m' '1;36m' '  37m' '1;37m';
  do FG=${FGs// /}
  echo -en " $FGs \033[$FG  $T  "
  for BG in 40m 41m 42m 43m 44m 45m 46m 47m;
    do echo -en "$EINS \033[$FG\033[$BG  $T  \033[0m";
  done
  echo;
done
echo
```
### Install colortheme for windows WSL
Download colortool to c:\utils\colortool
https://github.com/Microsoft/console/

Download and copy c:\utils\colortool\schemes
https://github.com/mbadolato/iTerm2-Color-Schemes/raw/master/schemes/Builtin%20Dark.itermcolors
Execute in cmd.exe:
```colortool.exe -b Builtin_dark```

### Set up neovim and colortheme
Choose colortheme base16 here:
http://chriskempson.com/projects/base16/
#### Install neovim and  “plug” plugin manager
``` Bash
sudo apt install neovim
curl -fLo ~/.local/share/nvim/site/autoload/plug.vim --create-dirs https://raw.githubusercontent.com/junegunn/vim-plug/master/plug.vim
```
#### Set up nvim init file

```Bash
vi .config/nvim/init.vim
```
Insert:
``` vim
" Nvim ini file with themes install

call plug#begin('~/.local/share/nvim/plugged')
  Plug 'sheerun/vim-polyglot'
  Plug 'chriskempson/base16-vim'
  Plug 'itchyny/lightline.vim'
" Plug 'tyrannicaltoucan/vim-quantum'
" Plug 'ayu-theme/ayu-vim'
" Plug 'KeitaNakamura/neodark.vim'
" Plug 'jacoborus/tender.vim'
" Plug 'joshdick/onedark.vim'
" Plug 'nanotech/jellybeans.vim'
" Plug 'tomasr/molokai'
" Plug 'morhetz/gruvbox'
  Plug 'felixjung/vim-base16-lightline'
call plug#end()

let g:lightline = {'colorscheme': 'base16_default',}
" let g:gruvbox_contrast_dark='hard'
" let ayucolor="dark"

set background=dark

if (has("termguicolors"))
  set termguicolors
endif

syntax on
colorscheme base16-irblack

" This is needed to Lightline to work
set laststatus=2

set nowrap

" This is needed for non-black backgounds.
" let &t_ut=''
```
#### Make nvim the default editor
``` Bash
sudo update-alternatives --install /usr/bin/vi vi /usr/bin/nvim 60
sudo update-alternatives --config vi
sudo update-alternatives --install /usr/bin/vim vim /usr/bin/nvim 60
sudo update-alternatives --config vim
sudo update-alternatives --install /usr/bin/editor editor /usr/bin/nvim 60
sudo update-alternatives --config editor
```
## Vitrual machine with KVM
### Install basic KVM, libvirt virtualization packages
``` Bash
sudo apt install libvirt-daemon libvirt-bin libosinfo-bin virt-top
sudo apt install --no-install-recommends virtinst # recommend install xorg and other unneeded packages
sudo apt install --no-install-recommends  libguestfs-tools  # for mounting guests filesystem into hosts
groups
id   # if user atti is not member of libvirt group add it
sudo adduser atti libvirt
sudo adduser atti kvm
```
### Install Ubuntu virtual machine
``` Bash
mkdir Letöltések
cd Letöltések
wget http://de.releases.ubuntu.com/17.10/ubuntu-17.10-server-amd64.iso
Create qcow2 filsystem thin provisioned image to use later
sudo chown root:libvirt /var/lib/libvirt/images/
sudo chmod 771 /var/lib/libvirt/images/
sudo qemu-img create -f qcow2 /var/lib/libvirt/images/ubuntu-test.qcow2 8G
```
Get a list of available OS types
``` Bash
osinfo-query os
```
Install ubuntu with virsh
``` Bash
virt-install \
 --name=ubuntu-test \
 --ram=2048 \
 --vcpus=2 \
 --disk path=/var/lib/libvirt/images/ubuntu-test.qcow2,format=qcow2,bus=virtio,cache=writeback,discard=unmap \
 --disk ./ubuntu-17.10-server-amd64.iso,device=cdrom,bus=ide \
 --os-type=linux \
 --os-variant=ubuntu17.04 \
 --network bridge=virbr0 \
 --graphics spice,listen=0.0.0.0 \
 --console pty,target_type=serial \
 --noautoconsole
```
Get IP address of VMs
``` Bash
virsh net-list
virsh net-dhcp-leases default # default is the name of the network
```
### virsh snapshot-create-as --domain ubuntu-test --name "clean install"

virsh snapshot-list ubuntu-test
virsh snapshot-info ubuntu-test 'clean install'
virsh pool-list
virsh pool-list images
virsh snapshot-delete ubuntu-test 'clean install'
qemu-img info /var/lib/libvirt/images/ubuntu-test.qcow2
virsh dumpxml ubuntu-test

Get back lost space after deletion
sudo virt-sparsify  /var/lib/libvirt/images/ubuntu-test.qcow2 /var/lib/libvirt/images/ubuntu-test2.qcow2
sudo mv /var/lib/libvirt/images/ubuntu-test2.qcow2 /var/lib/libvirt/images/ubuntu-test.qcow2

<!--stackedit_data:
eyJoaXN0b3J5IjpbLTExODg2NTIyNjAsLTY1Mzc3NjI2Nl19
-->